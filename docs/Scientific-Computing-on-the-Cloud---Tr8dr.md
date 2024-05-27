<!--yml

分类：未分类

日期：2024-05-18 15:33:05

-->

# 云端科学计算 | Tr8dr

> 来源：[`tr8dr.wordpress.com/2010/05/28/scientific-computing-on-the-cloud/#0001-01-01`](https://tr8dr.wordpress.com/2010/05/28/scientific-computing-on-the-cloud/#0001-01-01)

2010 年 5 月 28 日 · 7:50 pm

我一直密切关注各种云服务与内部 CPU 农场成本的差异。[亚马逊 EC2](http://aws.amazon.com/elasticmapreduce/#pricing)对于**高性能 CPU map-reduce**的价格似乎与我在内部托管的成本相当。

我是基于对 3 年内折旧的 i7 920 CPU 进行计算，并考虑到每千瓦时 0.14 美元（连续运行 150 瓦）得出的这个结果。我得出的成本低于亚马逊的，然而在调整 CPU 性能后，每美元的性能指标与亚马逊的提议相当或更优。

亚马逊对于使用 map-reduce 计算的费用是正常实例成本的 1/5。我估计高性能的 8 核心 CPU 在 SPECfprate2006 的测试中大约能达到 150，是核心 i7 920 的两倍。成本是每小时 0.12 美元，而非 map-reduce 实例的成本是每小时 0.68 美元。

这对于那些进行短暂的大规模科学计算的人来说是个好消息（比如我自己）。我现在需要将我的机器学习和策略评估算法映射到 map-reduce 上。
