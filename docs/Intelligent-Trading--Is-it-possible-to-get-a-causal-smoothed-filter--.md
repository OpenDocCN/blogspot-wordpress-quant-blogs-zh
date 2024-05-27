<!--yml

分类：未分类

date: 2024-05-18 04:45:35

-->

# 智能交易：是否可以得到一个因果平滑滤波器？

> 来源：[`intelligenttradingtech.blogspot.com/2010/05/is-it-possible-to-get-causal-smoothed.html#0001-01-01`](http://intelligenttradingtech.blogspot.com/2010/05/is-it-possible-to-get-causal-smoothed.html#0001-01-01)

虽然我一直不是移动平均方法的大粉丝，但我观察了一些讨论，并试图确定是否可以得到一个实际的因果模型平滑滤波器。任何从事过金融时间序列滤波器的人都知道，滤波器的噩梦是获得延迟非常低时的平滑响应。讽刺的是，您可能会认为为了实现具有相当延迟属性的因果滤波器，需要一个非常小的移动平均长度；通常是在选择大参数以获得良好的平滑性，而牺牲延迟之间做出妥协。

我用大约一年的 QQQQ 日数据组装了以下基于 FIR 的滤波器。它是完全因果的，由... 250 个系数描述。

它看起来是否平滑？您来决定。

![图](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjAyNaaR5RtC37mZdiftYvrW3jVfc1fktHL9yj5fe35PnsHinIpPWRY2IS7fofyilKRAil2xNs4HK9plHlqFA32Asb1ZVFIxKT4o7HFa8n7qNyMAX4U5iCVujihQy9P6RgTLOLPzPwea9k/s1600/causal1.jpg)

图 1. 250 抽头的前馈 FIR 滤波器

![图](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiXuJP0xhnyxJGhDYbXclFCSC1AQ-X36qc3JpLVfZKm0gGi4Y0UuBVFbB7TUGw305OVDDcLe8q2DvB_iB38QYkGkOAi4THp4-Fs_iZMqQyUiCVtH0GZWh4dPrD6cOdjCrQWBcDQLNM2hNY/s1600/impulse.jpg)

图 2. 确定系数的 250 权重冲激响应

冲激响应大约是一个 sinc 函数，这是理想 '砖墙' 低通滤波器的离散逆变换。

实际上我目前并没有对外部样本进行太多验证，所以模型可能表现不佳，还有待进一步调查。然而，我想分享这项工作，以提供关于因果滤波方法潜力的想法。
