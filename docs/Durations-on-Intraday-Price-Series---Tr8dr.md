<!--yml

类别：未分类

日期：2024-05-18 15:36:55

-->

# [一天内价格系列的持续时间 | Tr8dr

> 来源：[`tr8dr.wordpress.com/2009/11/27/durations-on-intraday-price-series/#0001-01-01`](https://tr8dr.wordpress.com/2009/11/27/durations-on-intraday-price-series/#0001-01-01)

2009 年 11 月 27 日 · 下午 1:55

正如在[之前的一篇文章](https://tr8dr.wordpress.com/2009/11/26/rethinking-variance/)中提到的，我打算模拟二次变化，涉及到多种强度（持续时间）和回报水平过程的多种配对。至少需要一对“非跳跃”相关回报和一对“跳跃”相关回报。

为了做到这一点，需要根据阈值将回报划分为不同的类别。我们可能还希望忽略低于一定水平的价格波动，除非它们在一段时间内累积起来形成具有重要性的回报。为此，我的持续时间测量函数使用阈值来确定是否将回报视为事件或不是。伪代码如下：

```
r ← {0} ∪ diff(log(series))
t ← times (series)
durations ← {}
for (i in 2:length(r))
{
    # determine cumulative return since last acceptance
    cumr ← *<cummulative return since last event or max cum window>*

    # determine whether qualifying event has occurred
    if (|cumr| ≥ threshold or |r[i]| ≥ threshold)
        durations ← durations ∪ {t[i] - *<Tlastevent>*}
}

```

对于过程的扩散部分，在这个 2 秒采样数据集（EUR/USD 低流动性时期）中，一个阈值为 3e-5（大约相当于 1/2 个点）似乎效果不错：

![](https://tr8dr.wordpress.com/wp-content/uploads/2009/11/picture-115.png)

过程的跳跃部分应设置为捕捉所需的跳跃特征，而不要太多，这里我显示了一个阈值为 2e-4（相当于约 3 个点）的情况：

![](https://tr8dr.wordpress.com/wp-content/uploads/2009/11/picture-215.png)
