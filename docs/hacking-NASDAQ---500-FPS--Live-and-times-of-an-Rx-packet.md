<!--yml

类别：未分类

日期：2024 年 05 月 13 日 00:07:12

-->

# hacking NASDAQ @ 500 FPS：Rx 数据包的实时情况

> 来源：[`hackingnasdaq.blogspot.com/2010/01/live-and-times-of-rx-packet.html#0001-01-01`](http://hackingnasdaq.blogspot.com/2010/01/live-and-times-of-rx-packet.html#0001-01-01)

为了完善图片，我们需要查看 Rx 数据包流的全过程，从 Linux 接收 Rx 中断到用户从 recvfrom() 中获得数据包。首先是高层次的视图，从中断确认 -> recvfrom() 的总时间。

intr ack -> recvfrom()

这个看起来跟我们的其它图表相当相似。禁用 NAPI 并使用单独的 Rx/Tx 处理程序后，有趣的是使用 NAPI 时延迟会更低（18,000ns），高（35,000ns），可能是在 300Hz（softirq）轮询时的变化。

Linux 接收中断后发生了什么？网络驱动程序的 irq 处理程序被调用，确认和清除中断。目前还没有特别有趣的地方，但显然在做某些事情花了很多时间… 是 L1/L2 的未命中更新？还是仅仅是读取寄存器的延迟？不清楚。下图所示，大约在 600ns 左右。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjrjmSjmadMJPsW_LBCxmfOms9Vvrfo29LKQvRaLbvlLoTUV2ZOuBVrHw0kOQKDP3R6So-1OU_ETyvjpPHOKKPywIv6DVMuMkWWwdfcrLgmtbI9TCJKd0eUIpZ-Wm0CIrMCY7EdRHWJEw/s1600-h/recv_irq2clear.png)

irq 矢量 -> 驱动程序 Rx 清除

中断清除后，驱动程序读入了 Rx 描述符，并使用 CPU 将数据包（从设备 DMA 环形缓冲区）复制到通常的套接字 RECV 缓冲区中。这个（RECV）缓冲区是讨论套接字时人们常说的内容。

设备缓冲 -> 套接字缓冲复制

如你所见（如上图所示），这个直方图有些奇怪，一片清晰的区域后面跟着一长串的东西。猜测部分是 DDR 取数据延迟，至少 1000ns 的部分是因为只有 128B + UDP + IP + 以太网，不多。并且目标内存地址可能没有正确对齐以启用写组合，所以它做了读修改写 + 源数据获取未命中，但愿不是，因为这是一块旧的 x86 处理器。2500ns 理所当然是取消数据包的 DMA 区域，一些内核/PCI 功能在工作。顺便说一句，不清楚为什么会取消，然后在 Rx 描述符空闲和准备好时重新映射，应该不是为了安全性吧？

在传输完载荷后，进行 IP 处理 / 容错检查，这部分内存很小，所以不包含图表 - 它缓存上一个数据包的所有 IP/设备/套接字信息。

netfilter PRE_ROUTING

IP 处理完成之后，进入 netfilter。PRE_ROUTING 非常简单（如上图所示），不包含任何规则定义。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjf8PuxUcPd43ZjYw79tAL-aRt7iCJgfSSH90SeDwzj6ffuU3hdxaNWyqCMDnEQWizpP3mvYLA4TtIxJUiUzPEJBmU2BbNm3RI2mHraJHi_Z2ZvUZ8i8Aoi_Ro6ojStnPomKjcIfflREA/s1600-h/recv_netfilter_local.png)

netfiler LOCAL_IN

对于 LOCAL_IN（上文），基本上什么都不做 - 没有定义规则。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi6isItXqvu-KI96_OxwGMj20UgcgLObo-9acSqUEhcTeIvMPrQAIMsm5cKgk0w5JWvo9lqsqIGZzU2sT8eOa-KCwuIiMrGGiuJsAL312OIaKvX7Jd1v-big0wg6KeYSlPtxIxSNuoEfg/s1600-h/recv_udp.png)

UDP 处理

最后 UDP 处理（上文）变得有趣。首先，图表的分布范围非常大，所以肯定有问题。真正有趣的部分是高度 - 可能很难看到，但时间间隔 0 中有一个 100%的列。例如，大部分时间，udp 处理非常低，然后偶尔会做些*事情*。不确定是什么，但绝对值得调查。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgCut-R0ZEapP7Mk3WgFexq_x6lLic54_8Jg4jz2cxPeI3l-PYOunsl4DlJcghG3q_0qhyOA0RBVGCh5B5YmK99kjk6jgf65XXx1KpZZbhYuys7nKvIUJlRYL5zBAjmyzCXDvIaNt56ew/s1600-h/recv_ipudp2user.png)

UDP（内核）-> recvfrom（用户）

最后，数据包到达用户空间（上文），这是我们总延迟中的两个峰值的来源。原因是？不太确定，可能与阻塞/信令行为的阻塞 recvfrom()调用有关。大小和频率的可能理论是 softirq 定时器频率（300Mhz 默认）。快速测试是增加/减少此频率，重建内核，运行测试并检查结果。

Rx 延迟摘要

很难用单个数字总结每个模块，因为每个组件的标准偏差可能会有很大变化，但以上是对非 napi 配置驱动程序和 2.6.30.10 堆栈的粗略指南。准确复现这些数字非常困难，只需启动存档的 arch-linux 发行版内核，这是该 2.6.30.10 内核的源.config 文件，显示了完全不同的配置文件。或者多次重新加载网络驱动程序会导致奇怪的事情发生，这就是当有大量代码运行时的生活。

Linux-2.6.30.10/net 中的 C 文件行数大约为 912K LOC。 net/ipv4 中有 128K LOC……显然 Ethernet+IP/UDP+Intel e1000e 只是其中的一部分，但即使 20k LOC 也是使微秒级调整成为真正艺术的重要逻辑块。
