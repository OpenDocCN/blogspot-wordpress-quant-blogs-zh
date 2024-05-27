<!--yml

类别：未分类

日期：2024 年 05 月 13 日 00:06:45

-->

# hacking NASDAQ @ 500 FPS: Life and times of Reliable Tx

> 来源：[`hackingnasdaq.blogspot.com/2010/01/life-and-times-of-reliable-tx.html#0001-01-01`](http://hackingnasdaq.blogspot.com/2010/01/life-and-times-of-reliable-tx.html#0001-01-01)

在我们对网络堆栈的调查中，我们看到 UDP 堆栈的延迟，因此下一个逻辑步骤是 TCP。很多人看不起 TCP 用于低延迟连接，说它的缓冲太多，延迟太高，最好使用 UDP ，它非常适合一定类别的通信，比如丢包网络游戏物理。然而在金融领域，错过几次更新就是灾难，不是个选择。

有两种一般的方法：

1) 在 UDP 之上构建糟糕的 TCP 版本。这是许多开发人员陷入的经典“非自行发明”综合症。

2) 使用 TCP 并针对情况进行优化。

在图形学中，OpenGL / Direct3D 存在一个“快速路径”，用于通常是应用程序瓶颈的操作/状态/驱动程序，驱动程序/堆栈工程师会对其进行积极优化。如果更改状态，使其不再处于快速路径上，则通过慢速通用代码路径进行操作，会产生正确的结果，但速度会慢得多。这种方法是为了兼顾两者，既具有丰富功能的 API，又能在特定用例下拥有闪电般的性能。

如果我们将这种思想应用到网络堆栈上，就没有理由不可以为特定用例获得 UDP 或更好级别的性能，比如短 128B 低延迟的发送，但当它偶尔丢包时，能够回到更通用/更慢的代码路径。从而产生一个快速的、低延迟的协议，可靠、有序，最重要的是事实上的标准。接下来...让我们戴上橡胶手套，深入到 TCP 堆栈中去。

首先，让我们从高层次来比较 UDP 和 TCP 的 128B 消息的往返延迟。请记住，这一切都是在一个未加载的系统上进行的，UDP 的数字并不完全是 128B 的消息，但接近，因此更多的是作为指南而不是绝对的比较。事关这里的诀窍在于假设 0%的数据包丢失，并且已经建立了 TCP 连接，那么每个发送()都将生成自己的 TCP 段，因此我们可以将数据插入负载中。虽然有些粗糙，但易于做，现在做得很好。

往返 UDP A->B->A

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj7o0d1hzX7hglSwggdFH98dcfy-OF2tlyZUdKL2sVjBNoxKky4H6hdstWK95cy2eZy_e0CXQhzeiVG264hKh59pwUeZlmsEaKtAdd8cq0Wnrcyl4RMZ_2AlcuDJN-0O6OjngyNNjsrzA/s1600-h/tcp_round_default.png)

往返 TCP A->B->A

请记住，TCP 的时间范围是 UDP 图的两倍，大约是 35,000ns 对比 50,000ns，TCP 明显慢得多-证明了传统智慧。时间去哪了？第一步是看看来自应用程序 -> NIC 在机器 A 的 Tx 和 Rx 两侧的时间。

UDP sendto() -> Tx 描述符

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg5hyGFl4s31Tascn7w5QhT1uf6243XLXjVEu1OJgf6nA5fgC5FOOPc-dZxCcdDqOjSPfpDguHAxHKR4uKvIEpHM893-LyvkWyz9OwasjGQgWRUQTq0cVOuBfaYwYKh57e2FpYdcc86kA/s1600-h/tcp_a_user2tx.png)

TCP send() -> Tx 描述符

上面的图表是等式的 Tx 一方，这是相当不错的，考虑到往返的 UDP 与 TCP 之间的差异并不是很大。所以问题可能出在了 Rx 的逻辑，TCP 出了问题？

UDP Rx Intr -> recvfrom()

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiCnqXvQnCvGL_lgYofCl2wCLLPr_ll1ZTaX_KP-CHopdoYOVGeV_9TeWkjUFesS_g_gBH6iBZzTcGF_JZeOb6gXlWx9Otm8X_vaWeWDNMTxppzYSFash2Y27Lj9Bh7cTLD7VzQdgRh0A/s1600-h/tcp_a_rx2user.png)

TCP Rx Intr -> recv()

...我们看到 TCP 的 Rx 速度比 UDP 慢了大约两倍，大约是 2,500ns 对 1,200ns。不太清楚这里发生了什么，显然与收到的每个 TCP 分段的 ACK 相关，但慢了两倍？我们应该对这种情况做出改善。

比较往返延迟，我们差约 15,000ns。机器 A 大约 3,000ns，那剩下的 12,000ns 去哪了呢？是机器 B。请记住，机器 A 的 NIC 直接连线到南桥，而机器 B 必须通过 PCIexpress 传输，因此机器之间的延迟差异。

UDP 机器 B Rx Intr -> recvfrom()

机器 B 的 TCP Rx Intr -> recv()

在 Rx 的一边是挺有趣的，几乎在 5,000ns 附近的一瞥有些可疑，但比 UDP 略快 - 这有点奇怪。然后有个大块，超过一半的传输是在 8,000ns 附近，所以再说 3,000ns 左右是机器 B 的 Rx。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjhrJm1iviPf-dk0MoG4qgKSeguLraGWmj24czezMJvvkq2OwFIylChj8m7p_YC2LYbD2nD50gDWjEMDueY7Sep5Yx9KpJl4maCOX7p6y12tsDlipS_sSPkWJpDXnT5b0j2mVLB-x1lWw/s1600-h/bapp2tx_latency_stock.png)

机器 B 的 UDP sendto() -> Tx 描述符

机器 B 的 send() -> Tx 描述符

与机器 A 一样，Tx 的一侧与 UDP 相当一致，甚至在几乎完全相同的位置有一些高峰，虽然略有偏移。有趣的是 TCP 在某种程度上竟然比 UDP 稍快地到达 NIC - 可能是数据大小上的差异。

我们已经探讨过了 TCP 与 UDP 之间的时间差的一半多，但剩下的时间去哪了呢？硬件？看起来不太可能。更可能的是 UDP 与 TCP 的测试数据足够不同？或者经过多次内核和驱动程序的重建后，设置稍有不同？

无论如何，小发送的性能表现非常接近。下一步的任务是查看 TCP 的 Rx 端，并看看为什么它与 UDP 的性能水平不相上下。
