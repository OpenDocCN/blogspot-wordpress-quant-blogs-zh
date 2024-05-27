<!--yml

类别：未分类

日期：2024 年 5 月 18 日 06:27:34

-->

# FPGA 杀手级应用 | 交易台的故事

> 来源：[`mdavey.wordpress.com/2013/04/18/fpga-killer-applications/#0001-01-01`](https://mdavey.wordpress.com/2013/04/18/fpga-killer-applications/#0001-01-01)

## FPGA 杀手级应用

+   通过量的减少，例如市场数据线的减少。 为了避免数据丢失，有益的是从某个场所消耗市场数据的 A 和 B 线。 但是，微爆发可能会导致排队延迟。 FPGA 网络适配器线路层允许服务器 CPU 消耗的吞吐量减半，从而提高应用延迟，并减少抖动（在应用消耗数据包之前对数据进行预处理）

+   FPGA 上的订单簿和服务器 CPU 上的离载。 附加价值：减少需要跨总线传输的数据量。

+   交易前检查。 附加价值：从服务器 CPU 中卸载。

+   存储 - 来自 FPGA。 附加价值：从服务器 CPU 中卸载。

+   以太网韧性

记住，与内存相比，从 PCI 读取的成本更高，因此在某些情况下，将任务离载到 FPGA 上是有益的。

~ 由 mdavey 于 2013 年 4 月 18 日发布。

发布在 [交易](https://mdavey.wordpress.com/category/trading/)
