<!--yml

category: 未分类

date: 2024-05-13 00:07:29

-->

# 在 500 FPS 下黑客攻击纳斯达克：一个 Tx 数据包的生活和时代

> 来源：[`hackingnasdaq.blogspot.com/2010/01/life-and-times-of-tx-packet.html#0001-01-01`](http://hackingnasdaq.blogspot.com/2010/01/life-and-times-of-tx-packet.html#0001-01-01)

最后..有一些时间可以用在这个上面。上次我们对时间消耗的大致高层视图，所以让我们深入挖掘一下软件堆栈，看看到底发生了什么。所以...让我们开始使用一个标准的 2.6.30.10 内核，构建它，安装它，运行它，然后第一个图出现了。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiPuVzSCZitEgZPy9EOC8AGrnx4nlhaWNAW2QbrAciLkscR49PFg7TQhq8rJ7Qa3Tuq9AN9ojhWy6PElbaphir3nYmk3_Pg4ap8A5KiRNSe-hYUZ-mTGYSyN0vDlQZp1EgfAqZVi_bdDg/s1600-h/send_latency_base.png)

A 机 sendto（）-> Tx 描述符

我们的最高层的延迟参考值大约为 1500ns，从用户级函数调用到网卡驱动程序增加 Tx 描述符环的时间。不错，意外地比我们先前的测试（2000-3000ns）要快得多。我不知道为什么，但很可能是由于稍有不同的内核版本和构建参数。另一个奇怪的事情是“阴影图”**，可能是由于增加我们直方图箱尺寸的分辨率（100ns -> 10ns）**，所有时间都是基于一个旧的 2.6Ghz Xeon 处理器。

黑客攻击网络核心真是一件非常讨厌的事情，没有一个容易构建的模块，这意味着每次都要重新构建内核并重新启动...开发周期极其缓慢。但让我们从查看 glibc 代码开始，对于 sendto（）来说，基本上什么都不做-调用一个内核命令，因此第一个图是内核调用开销。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgQnWn2Et2rloBvepk8lE3zh_VkdYu-Jsc6ezJivhK2LVosOUhpyWOxqGY61wdDZsy6fjs2Gc88mgfcGK1oFh_-9AGLWRTjr92qxYqAogtSliQm-XC8KjQ2aP9QhtZwrN5FdW3jPWRDvg/s1600-h/send_latency_kernel.png)

用户区-> 内核开销

平均大约 250ns。双峰很可能是由于该机器上 2 个硬件线程，所以大约 700 个周期。在图中并不明显的一点是，内核开销时间从开始的大约 1200 个周期快速下降到平均 700 个周期左右，约 1000 个调用。

数据包然后到达 ipv4 udp 代码中的 udp_sendmsg（），在这里进行一些杂项数据包头/缓冲区分配和一些检查，找到缓存的路由并在套接字上获取锁。一般维护工作。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhStcK0WHBz6zDqmCXEnetHhS99_BtJHi9hW9e5rQ6jt4ljqvR7GFZIa7hyphenhyphen6lfAlDgr7vncXLgGRPcuqjzVHBNY_IMpVlafX0DIh8Tm6kb4D6nrYLIV6Fqo4QjbgTykQ99mdSN6buy-cg/s1600-h/send_latency_prep.png)

内核套接字/数据包维护

系统清理钟大约与内核切换一样多，大约 6-700 次循环或大约 250 纳秒。在数据包被检查后，它被复制到套接字发送缓冲区中 - 当人们讨论套接字缓冲区时，这是人们通常想到的，它将数据包从用户空间复制到内核空间，并允许/映射网络接口卡的 PCI/DMA 访问。

用户空间 -> 内核空间数据包复制

直方图因某种原因有些棘手，可能是由于 PCI DMA 映射命令，因为我们要复制的数据量很小 - 128B，它应该在 L1 和绝对在 L2 缓存中，所以不确定发生了什么。有可能是旧硬件和非对齐写操作的组合意味着 CPU 在读取修改写入目标内存缓存行，而不是直接写入（无需读取），因此我们要支付未缓存内存提取的延迟成本。或者... 它只是内核 DMA/PCI 映射代码，不确定。

IP/UDP 头部写

在复制有效载荷之后，堆栈添加了适当的 IP/UDP 头部（上文）这里没有什么特别有趣的，但让人惊讶的是这需要很长时间，大约 150 纳秒，这... 太多了。数据包校验和都被卸载到硬件上，所以它在这里做了别的事情。

现在变得越来越有趣，几乎所有标准内核版本都启用了 netfilter，以允许数据包过滤 / 路由 / 防火墙 / VPN 等等 - 这些都是 Linux 的非常核心的用例。有大量关于如何使用 netfilter/ipchains 的书籍和文档，但在我们的案例中，它完全是经过传递的，实际上我们应该禁用 netfilter 以减少延迟。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiEuTCMD0KX-14MwVZvmkdCWUieSBDPM-Tqo3SyPJL7aHoxfGArBs2u39GRDK6myDjWJP8ThJJm6jy_Pe1iJMLSJEO_r2PSVX3JB3K5XUokM6PojI6pv3szKxLIlvaSnTRT48MfNOXjdg/s1600-h/send_latency_nf_local.png) 

netfilter 本地经过

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgEMk-X93c2i01d4F9shAsaj7SwB3deU8OhqVX2r6lD2JBhG7NuYBH8npHvSIV0lLwJcLV1CMvxOpTOBxOemiaNMcmj5t7QHWNTCpzsLLsY6GDaKosWCBXDqG0VCI8d8WkHIyRnzaaG2g/s1600-h/send_latency_nf_post.png)

netfilter 后经过

正如你所看到的（上文），它仍然非常快，整体大约 80 纳秒，但我认为可以肯定交换不会尝试入侵你的机器，这都是多余的。

在 netfilter 批准数据包后，其被发送到网卡驱动程序，使用另一个缓冲系统，即 qdisc - 排队规则。这是 MAC 层级的，通常每个 MAC 只有一个单一的快速优先级 FIFO ，但完全可以使用 "tc" 交通控制命令和可能其他工具进行配置。Qdisc 是一个功能强大的系统，可以应用各种缓冲、调度和过滤，但它们都会增加延迟，对于低延迟系统而言不是特别有帮助。实际上，我打算完全禁用 qdisc 以减少延迟。

qdisc 数据包排队

排队速度相当快（上面）大约为 130ns 左右，直方图中的第二个波峰很有趣。猜测这是等待原子锁的等待时间。现在我们的数据包已经在 eth0 的队列中，唯一剩下的就是网络调度器将其发送到 NIC 驱动程序。然而，有一个很好的优化，就在数据包入队之后，立即尝试发送到驱动程序，而且通常可以成功。它不能立即发送的唯一原因是，如果另一个硬件线程正在运行网络调度程序，因此将数据推送到驱动程序，例如在这里我们有一个小的 fifo 用来避免丢包，但它确实增加了另一个延迟来源。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjv5s23fNho5WhHGVIWeOkxFoRqkFygqeOv67oav_iAlmSVHDbLaumUcQr0tpMA5oofVPYDnvpXj1nY0yIS5v8anY09oKznN2sLTcVb3nsebcerH8Qg1se5hOYFycijxGwRrE1mLRewtw/s1600-h/send_latency_soft.png)

qdisc queue -> driver xmit

正如预期的（上面），从排队队列到发出驱动程序调用的延迟很小，大约为 100ns 左右。有趣的是双重峰值，假设它错过了初始调度传递，并在第二次尝试时碰巧成功。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgnCeUreqhYUu4u2w3eltrdVjR1nW0Sd_Rkil9zJHjg3T14pczX0BU8d-i8k8jAFM1F4S1kbwGS8PlJgRUJ-ptv-4k8yA1ufnlkqneRVHI8vksqYxbY1Adz80gxPtK9N9lK-CmE_Q6jVA/s1600-h/send_latency_driver.png)

NIC 驱动程序 1 Tx 数据包处理时间

最后（上面）我们可靠的 e1000e NIC 驱动程序处理成本，填充了我们的 Tx 描述符并将环形缓冲区向前移动。然后释放数据包，处理速度相当快，大约为 400ns。注意，这是从驱动程序入口点到出口点的时间，这比驱动程序入口-> Tx 更新（下文）/硬件移交的时间长，因为有清理代码。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjyZUtnz_nqpmkRLzT_QdO8OKLS6W5Xve75ARnyi-wOAGUOn1GBi9b32DFCWjUsjcICL8Xh28YTrTnrFL2Hw3Vm17yR513LTwuzlfb0GxRUiQjQUQI71jjW2141U1uEMWAjh8Yel1D-vw/s1600-h/send_latency_qdq_tx.png)

qdisc enqueue -> NIC Tx descriptor write

问题是，如果 NIC 驱动程序只需要 3-400ns 来启动一个 Tx 描述符，那么其余的时间必须花在 Linux 内核的网络堆栈中？

sendto() -> NIC 驱动程序移交的开始

答案-> 是的，大部分时间花费在内核中。上图显示了除 NIC 驱动程序外的整个软件延迟，形状与第一个高级图（绿色的那个）匹配，只是稍微向左偏移。这很好，因为我们有很多选项来减少内核处理时间，从而使数据包在<1,000ns 内到达 MAC！

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEinv_rWdWtW4EZDmmtqD_iRZ8IudjSisRWOgi-idK62xQI5erVZNRvRA_n4Mf4x024pcAe4V9SK2kSkLmETuNZIt2XfjGyCbMdWjdoWxwO1a7NBLkHXK7P14bczf32x5v_vEn5FQCqcOg/s1600-h/tx_send_highlevel.png)

典型的高级 Tx 硬件/软件流程 @ 2.6Ghz 旧款 Xeon 机器

总之，上面的流程图显示了我们当前的延迟估计。由于缺乏工具，我们只能大致估计硬件延迟，但你可以明显看到硬件延迟远远大于软件。因为我们正在使用一个典型的（旧款）消费者/服务器型号的硬件布局，这款硬件设计用于高吞吐量而不是超低延迟。这就是为什么任何严肃对待超低延迟的人……会有一个完全不同的硬件拓扑结构 :)
