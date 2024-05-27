<!--yml

分类: 未分类

日期: 2024-05-18 04:43:53

-->

# Intelligent Trading: IBS 反转（鳐鱼图）直觉使用 R vioplot 包

> 来源：[`intelligenttradingtech.blogspot.com/2013/04/ibs-stingray-reversion-intuition-using.html#0001-01-01`](http://intelligenttradingtech.blogspot.com/2013/04/ibs-stingray-reversion-intuition-using.html#0001-01-01)

Fig 1. Vioplot  of IBS 过滤的 SPY 次日回报。

Fig 2. 摘要表，比较 rtn.tom 与 IBS.class (H,L,M)的结果。

我和一位同事最近讨论了如何获得关于

[IBS 分类方法](http://intelligenttradingtech.blogspot.com/2013/01/ibs-reversion-edge-with-quantshare.html)

用于反转系统的 IBS。我想分享一个

[小提琴图](http://cran.r-project.org/web/packages/vioplot/index.html)

我生成的图表，可能会帮助大家获得一些关于它的视觉直觉。我们可以下载并处理像 SPY 这样的资产的次日回报，并将类别分为低（IBS < 0.2）、高（IBS > 0.8）和中（其他所有）三个组。在图表中，你可以看到低组有明显的右偏，而高组有左偏（它们有点像相反的鳐鱼——鳐鱼图可能是更恰当的术语来描述反转现象）；而中组往往更接近平衡。vioplot 可视化的好处是，它包括了回报分布的密度形状，这比常见的箱线图增加了直观性。
