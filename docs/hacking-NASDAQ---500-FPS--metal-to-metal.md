<!--yml

category: 未分类

日期：2024-05-13 00:05:49

-->

# NASDAQ 黑客 @ 500 FPS：金属对金属

> 来源：[`hackingnasdaq.blogspot.com/2010/02/metal-to-metal.html#0001-01-01`](http://hackingnasdaq.blogspot.com/2010/02/metal-to-metal.html#0001-01-01)

上周忙于其他事情，现在是时候回到这个问题了。我们上次的调查看了一下，我们看到的网络延迟的相当大一部分是由于 stock linux scheduler 引起的。因此，一个很自然的问题是，如果我们放弃一切直接与底层硬件交互会发生什么呢？

Intel 硬件非常适合这个用途，硬件文档非常出色，参考 sauce/linux 驱动非常易于跟踪。设置是什么？非常简单，编写一个将 BAR0（寄存器空间）和 BAR1（闪存）直接映射到用户空间的 linux 驱动程序，然后为用户空间分配和映射 4 个 DMA 缓冲区，Rx 描述符，Rx 缓冲区，Tx 描述符，Tx 缓冲区。这就是我们编写自己的 PHY/MAC/Ether/IPV4 + ARP/ICMP/UDP/TCP 栈所需的一切。这是一个直截了当的过程，唯一棘手的部分是 TCP 栈。除了 TCP，几天内就把所有东西都运行起来了，因为 NIC 硬件非常简单，无连接协议非常轻松。当然还不完全成熟，但足以获得一些有趣的结果。

我们从往返延迟开始。这两台机器相同，我们使用 ICMP 64 字节负载进行此测试 - 请注意时间刻度不同。

64B ICMP 往返（金属）

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj4i9JAr-1CZa14-b3I57IvbVOQj5AoaPHi8GAgcs1qBed0L8QdM8rCY-8_yS71nAcqnk9KiION7O1thCJ9G6c8LmKlhtIHd6YAwXDi5zB44otDQ9xc9y87UeN9zX9_jijCCgo9JGRnPA/s1600-h/tcp_round_default_poll.png)

128B TCP 往返（轮询）

我们的金属在总体往返时间上平均大约为 19,000ns，因此我们可以平均说每一边是 9,500ns，但实际上并非一半一半，我们会看到。尽管不是苹果和苹果的比较，但与我们迄今为止的最佳结果相比，轮询 TCP，我们比 linux 栈快了大约 15,000ns，几乎是 x2 多！

那么这 19,000ns 去哪了？令人惊讶的是，在 x86 IO 架构上的表现实际上令人相当沮丧。首先是结果。

机器 A - 延迟 1 32 位寄存器读取

机器 B - 延迟 1 32 位寄存器读取

... 如你所见，机器 A 大约需要 800ns 读取 1 个寄存器，而机器 B 需要 2,200ns 读取*一个*。为什么这两台机器如此不同？正如之前所讨论的，机器 B 的 NIC 在 PCIe 总线上，而机器 A 直接连接到南桥。因此，尽管机器 B 是最新款的 nehalem，而机器 A 是 2007 年左右的旧款 Xeon，但旧款 Xeon 知道如何取胜，真正印证了在这个性能水平上物理硬件拓扑是多么重要。

你日常使用的驱动程序将是中断（ish.. NAPI 轮询）驱动，从一个 Rx isr 开始，读取中断状态寄存器以确定发生了什么，然后读取 Rx 描述符头寄存器，查看新数据包的数量和位置. 如果我们使用“花哨的机器 B”来进行总结。

MAC -> CPU isr 延迟：2,200 / 2 = 1,100ns

CPU isr 状态寄存器读取：2,200ns

CPU rx 描述符头寄存器读取：2,200ns

将延迟设定在大约 5,500ns，这是 *协议处理之前*，而我们甚至还没有查看 Rx 描述符或 Rx 缓冲区数据！

机器 A Rx 描述符加载（DDR）

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgYnBCnHQD5X6JRNpETpUx2zyIfs1EMMLNopFfT9b-GnttJfCBu9PDvcpJE8knulKN62M3o2dY17MMfIAwdNPB-FUEkFyPNTMAS4BGjRRSc06JID4W7j9dFA7mxburKngrQqOGFNitb_A/s1600-h/rxdesc_read_b.png)

机器 B Rx 描述符加载（DDR）

Rx 描述符位于 DDR 中，令人欣慰的是可以对其进行缓存，但问题在于当设备写入 DDR 时，我相信（而且数字看起来也是一致的），它会使所有级别的缓存行无效，这有些糟糕。我原本以为尼哈勒姆会只使 l1/l2 无效，并更新 L3，但看起来它没那么聪明。因此在上面的图表中，我们可以看到在机器 A 上缓存未命中的成本约为 100ns/270 个周期，在机器 B 上约为 75ns/200 个周期。由于机器 B 更快，因为内存控制器位于 CPU 上而不是北桥上-少了一个总线要走。

总结：

电线 -> PHY : ?ns

PHY -> MAC : ?ns

MAC -> CPU isr 延迟：2,200 / 2 = 1,100ns

CPU isr 状态寄存器读取：2,200

CPU rx 描述符头读取：2,200

CPU rx 描述符读取：75ns

CPU rx 缓冲区读取：75ns

总计：5,650ns 或 15,000 个周期！显然我们可以对其中一些进行流水线处理，但是你在标准驱动程序中不会找到这些和其他优化。实际上，在 x86 上，不能确定你是否能发出多个非缓存读取，而这些读取没有受到保护/序列化，例如流水线处理。故事的寓意是，利用标准 PC 服务器硬件让单个微秒延迟转变（Rx -> Tx）是一项挑战，从电线上测量，。
