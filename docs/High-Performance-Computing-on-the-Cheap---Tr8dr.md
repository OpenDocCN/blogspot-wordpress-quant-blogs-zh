<!--yml

类别: 未分类

日期: 2024-05-18 15:40:10

-->

# 便宜的高性能计算 | Tr8dr

> 来源：[`tr8dr.wordpress.com/2009/07/27/high-performance-computing-on-the-cheap/#0001-01-01`](https://tr8dr.wordpress.com/2009/07/27/high-performance-computing-on-the-cheap/#0001-01-01)

我有一些正在研究的交易策略需要进行非常计算密集的校准，可能需要在多核计算机上运行多天甚至几周。幸运的是，这个问题适合大规模并行计算。

我正准备启动自己的交易操作，因此确定如何最大化我的 gflops/$ 尤为重要。一些初步方案：

+   我的校准不具有 SIMD 特性（因此 GPU 不会有太大帮助）

+   我需要至少有 8GB 内存可用

+   我的问题的性能最好由 SPECfprate 基准来描述

我开始调查网格解决方案。如果我可以在几个小时内使用数千台服务器，会花费多少？

商业性网格平台 我调查了亚马逊 EC2 和谷歌应用引擎。在这两者当中，只有亚马逊似乎有更高性能的服务器。对于亚马逊和谷歌的成本核算后，发现这两个平台对于高性能计算的成本均不合理。

亚马逊按每个计算小时收费 0.80 美分，一个“额外大型高性能 CPU” 服务器的月租是 $580 或者每年 $7000。这款服务器的配置是 2007 年的 Opteron 或 Xeon。这意味着是双路 Xeon X5300 系列、8 核心服务器，SPECfprate 最高才能达到 66。$7000 每年的计算费用太贵了，一定有更便宜的选择。

主机服务 原来有一些便宜的主机服务可以提供 SPECfprate 约 70 的服务器，月租约为 $150。这样每年的花费是 $1800。还不错，但我们能找到更好的方案吗？

这些“高规格”服务器有多昂贵？基于 Xeon 的服务器中，高端的 MacPro 8 核 X5570 价格最低。然而，如果可以进行分布式计算，它并不提供性价比最高！X5500 家族的性能在 140-180 SPECfprates，至少需要花费 $2000 只买 2 组 CPU。

现在出现了新的配置，Core i7 家族。售价为 $230 的 Core i7 920 可以产生约 80 SPECfprates 的性能，超频后可达 100。一个裸机计算服务器的成本约为 $550。如果我建造 2 台这样的服务器，就能超过双 CPU X5500 系统的性能，节省 $2000（最便宜的 X5500 系统约 $3000）。

成本比较总结

这是各种替代方案的 100 SPECfprate 计算年度成本比较。我们将假设每个 CPU 的功耗为 150 瓦，电价为 0.10 美元/千瓦时，还有系统成本。

1.  亚马逊 EC2

    $10,600 / 年。100/66 性能 x 0.80 / 小时 x 365 x 24

1.  主机服务

    $2,700 / 年。100/70 性能 x $150 x 12

1.  MacPro 2009 8 核双路 X5570

    $1070 / 年。100 / 180 性能 x $3299 / 2 + $160 电费

1.  Core i7 920 自定义配置

    $430 / 年。100 / 80 perf x $550 / 2 + $88 功耗

1.  Core i7 920 自定义构建 超频

    $385 / 年。100 / 100 perf x $550 / 2 + $100 功耗

Core i7 920 构建是明显的赢家。以每台 X5570 系统的成本可以构建 5-6 台这样的系统。将建立一个这样的集群。
