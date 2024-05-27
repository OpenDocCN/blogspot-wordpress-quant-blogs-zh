<!--yml

分类：未分类

日期：2024-05-18 15:37:03

-->

# 跳变解剖 | Tr8dr

> 来源：[`tr8dr.wordpress.com/2009/11/27/anatomy-of-a-spike/#0001-01-01`](https://tr8dr.wordpress.com/2009/11/27/anatomy-of-a-spike/#0001-01-01)

2009 年 11 月 27 日 · 上午 11:36

跳变在日内市场中经常出现。这些跳变通常很短暂，并且更多地与买卖程序有关，而不是基本因素的变化，特别是在低流动性时期。在评估持续时间和方差度量时，试图确定合理的跳变阈值。

以下是展示各种跳变行为的价格序列：

![](https://tr8dr.wordpress.com/wp-content/uploads/2009/11/picture-104.png)

我们注意到，在高频率跳变周围的区域内，跳变不是由一次交易引起的，而是在很短的时间内进行了多次交易：

![](https://tr8dr.wordpress.com/wp-content/uploads/2009/11/picture-114.png)

从持续时间的角度来看，如果我们想将跳变捕捉为一次具有给定幅度的事件，我们需要考虑在给定窗口内的累积回报或使用较长周期进行采样。这是一个 2 秒采样的例子：

![](https://tr8dr.wordpress.com/wp-content/uploads/2009/11/picture-121.png)

这是原始范围的 2 秒采样。较长的采样周期使回报中的跳变更为明显（与帖子中的第一个图形进行比较）：

![](https://tr8dr.wordpress.com/wp-content/uploads/2009/11/picture-131.png)
