<!--yml

category: 未分类

date: 2024-05-12 23:45:48

-->

# 以每秒 500 张图片的速度黑客纳斯达克：PCIe 延迟

> 来源：[`hackingnasdaq.blogspot.com/2014/05/pcie-latency.html#0001-01-01`](http://hackingnasdaq.blogspot.com/2014/05/pcie-latency.html#0001-01-01)

曾经想知道 PCI Express 上的 RTT 是多少吗？或者你可能会问 PCIe RTT 是什么鬼？

PCIe 在某种意义上与以太网相似，它是一个数据包总线，而 PCI 和 PCI-X 是更传统的并行总线。简单地来看，你的 PC/服务器内部就是一个 MTU 为 128B 的小型以太网网络。关于 PCIe 可以大谈特谈，但建议阅读一篇优秀的文章

[here](http://xillybus.com/tutorials/pci-express-tlp-pcie-primer-tutorial-guide-1)

来看看它是如何运作的。

通过 PCIe RTT，它表示从一个端点（以太网 IP）到另一个端点并返回一个数据包的来回时间。就像对某个 IP 地址进行 ICMP ping 一样。你该如何编写这样的测试呢？……当然是用 FPGA！

Xilinx 的 Virtex 7 有多种 SKU，具有 1-4 个 PCIe Gen3 接口，每个接口宽度为 8 行 @ 8 GT/sec（注意 GT == Giga Transactions 而不是 GBytes）。因此，测试就是简单地回复一个合适寻址的 PCIe TLP 数据包。

对于视觉倾向的人，他看起来是这样的

注意，i7 4771 是英特尔最新和最好的 CPU，具有本地 PCIe Gen3 接口，直接连接到 CPU 的引脚/接点。另外，请注意这都是“台式机”级别硬件... 这个意义是值得商榷的。

数字是什么样的？.....实际上相当糟糕，令人惊讶地糟糕。

上面是 RTT 的纳秒绘图。X 轴是样本计数，Y 轴是纳秒。你可以看到完整的往返时间约为 850ns... 老实说有些高。是时候深入调查一下时间去了——是的，卡槽是正确的 PCIe 插槽！

为什么这么高？这里是一些想法的简短清单

+   V7 PCIe 端点

+   1337 ping 代码

+   英特尔 PCIe EP

+   英特尔内存模型

最简单的是我的“1337 ping 代码”，因为代码已经处于开发样式设置中，因此获得波形是直接的。

以上是典型调试会话的进行方式。运行一些模拟，稍等片刻再检查波形。在上图中，你可以看到时钟每 4ns 进行一次滴答，并且有 2（共 4 个）Xilinx`s 新 PCIe IPCore 接口。它们是 m_axis_cq_*信号和 m_axis_rq_*信号。CPU 的寄存器写入显示在 m_axis_cq_*接口上，而我们写入（到 CPU 的 DDR）被发出到 s_axis_rq_*接口。如果你想更深入地了解，请查看

[规格](http://www.xilinx.com/support/documentation/ip_documentation/pcie3_7x/v1_1/pg023_v7_pcie_gen3.pdf)

我们可以计算接收 CPU 写入（黄线）和“1337 ping 代码”写入 CPU DDR（红线）的第一个周期之间的周期数。在这里大约是 16 个周期，接口以 250MHz 运行意味着 4ns * 16 个周期 = 64ns - 并不是特别好但可以工作。这意味着寻找其余的~800ns 仍然....没有结论。

...接下来将研究直接从 FPGA 写入 CPU 的 L2 缓存，从而避免涉及 CPU 的 DDR 的任何把戏。
