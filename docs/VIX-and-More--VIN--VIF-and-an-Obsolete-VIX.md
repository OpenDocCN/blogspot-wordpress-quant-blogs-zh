<!--yml

分类：未分类

日期：2024-05-18 16:52:35

-->

# VIX 和更多：VIN、VIF 和一个过时的 VIX

> 来源：[`vixandmore.blogspot.com/2011/03/vin-vif-and-obsolete-vix.html#0001-01-01`](http://vixandmore.blogspot.com/2011/03/vin-vif-and-obsolete-vix.html#0001-01-01)

[Option Pit](http://www.optionpit.com/) 的 Mark Sebastian 发表了一篇有趣的文章，[VIX 会过时吗？](http://www.optionpit.com/blog/could-vix-become-obsolete)，我猜*VIX 和更多*的读者会喜欢思考。在这篇文章中，Mark 认为由于 VIX 的计算方法，SPX [周期](http://vixandmore.blogspot.com/search/label/weeklys)经常比 VIX 更能深入了解当前波动性的状态。Mark 进一步分析并公开怀疑这一发展是否意味着 VIX 的消亡。

对于不熟悉 VIX 计算方法细节的人来说，VIX 的计算基于 SPX 的前期月份和次月份，大部分到期周期都是如此。在 VIX 期权到期的八天前，用于计算的 SPX 期权向前滚动一个月，以第二个和第三个月为基础。

请记住，VIX 将 SPX 期权与两个不同到期日期混合，以得出 SPX 隐含波动率的 30 天加权平均值，一个示例可能有助于说明正在发生的事情。下个月，[VIX 期权](http://vixandmore.blogspot.com/search/label/VIX%20options)将于 4 月 20 日（星期三）到期。从今天起到 4 月 11 日（星期一），VIX 是基于 SPX 的前一个月（4 月）期权以及第二个月（5 月）期权计算出来的。4 月 11 日，VIX 期权到期前的八个交易日，用于计算的 SPX 期权向前滚动一个月，这样计算中使用的近期月份是 5 月，计算中使用的远期月份是 6 月。

现在，来玩个有趣的游戏。很少有人知道，芝加哥期权交易所实际上为近期月份的 VIX（[VIN](http://vixandmore.blogspot.com/search/label/VIN)）和远期月份的 VIX（[VIF](http://vixandmore.blogspot.com/search/label/VIF)）分别维护着独立的指数。只需将这些代码输入到你的实时行情中，你也可以观察到不仅 VIX，还有 VIX 恒定到期混合中使用的两个组成部分。比如，我现在显示 VIX 为 17.88，VIN 为 16.98，VIF 为 18.23。只需确保在 VIX 期权到期前的八个交易日内跟踪 SPX 期权系列的变化。

当然，VIX 并不会很快过时。就像任何指数一样，它受到仅仅是一个数字的一些限制。如果你想快速了解市场波动性的情况，VIX 是金标准。如果你想要一些更详细的信息，并且是那些喜欢深入了解并稍作调整的人之一，[VIX 期货](http://vixandmore.blogspot.com/search/label/VIX%20futures)和 SPX 期权本身可能是最重要的市场波动数据组。对于那些没有轻松获得 VIX 期货数据的人来说，考虑将 VIN 和 VIF 加入您的观察列表，以拓宽您对驱动 VIX 水平的因素的理解。

相关帖子（在这组帖子中有一些优秀的信息，以及在[XXV 和新的 VIX ETN 景观](http://vixandmore.blogspot.com/2010/07/xxv-and-new-vix-etn-landscape.html)中特别有帮助的图形）:

***披露：*** *无*
