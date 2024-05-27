<!--yml

分类：未分类

日期：2024-05-12 19:03:18

-->

# 量化交易：做空 VIX 日历价差

> 来源：[`epchan.blogspot.com/2011/01/shorting-vix-calendar-spread.html#0001-01-01`](http://epchan.blogspot.com/2011/01/shorting-vix-calendar-spread.html#0001-01-01)

最近在

博客圈

关于做空 VXX-VXZ 价差的盈利性。 (参见

[量子博客](http://matlab-trading.blogspot.com/2010/12/vix-buy-hold-strategy.html)

和

[投机者的球](http://speculators-ball.blogspot.com/2010/12/is-vxx-due-for-bounce.html)

.) 作为背景知识，VXX 是一种跟踪 VIX 未来第一个和第二个月份的 ETN，而 VIX 未来则跟踪 VIX 波动率指数，后者又跟踪 SPX 的波动率。VXZ 是跟踪 VIX 未来第四至第七个月的 ETN。在 2009-2010 年间，有两个不同的原因使做空这种“日历价差”策略有利可图：

1) VIX 期货处于正向市场：即远期期货比近期期货更贵。

2) SPX 的波动率随时间降低。

然而，一些交易员似乎认为这些条件中的任何一个都足以确保做空日历价差的盈利性。这不是真的。否则，期货交易员的生活就会太简单了！

为了看到这一点，让我们求助于一个简单的线性近似模型来描述期货价格。从

[约翰·赫尔](http://www.amazon.com/gp/product/0132164949?ie=UTF8&tag=quantitativet-20&linkCode=as2&camp=1789&creative=9325&creativeASIN=0132164949)

在埃德温·费雪的书籍《衍生品》第 3.12 节中，到期时间为 T 的期货的价格是

F(t, T)=E(S

T

)exp(c(T-t)),

其中 E(S

T

) 是到期时点的现货价格的期望值，c 是一个常数，t 是当前时间。如果期货处于正向市场（contango），那么 c > 0。

如果我们假设 |c| 很小，T-t 也很小（即距离到期时间不远），且现货价格的期望值变化缓慢，我们可以将这个公式线性化：

F=(a+b(T-t))*(1+c(T-t))

如果市场预期未来现货价格会增加，那么 b > 0。

经过一些简单的代数步骤，你可以验证日历价差的价格与

F(t, T

1

)-F(t, T

2

) ~ bct

其中 T

1

< T

2

（即 F(t, T

1

) 是当月价格，而 F(t, T

2

) 是远月价格）。

这是一个令人满意的有说明性的结果。它说明，如果

A) 期货处于正向市场

*和*

未来现货价格在减少；或者

B) 期货处于反向市场

*和*

未来现货价格在增加。

那么现状如何呢？做空这个价差是否仍然有利可图？正如我们的博客作者们所指出的，VIX 期货仍然处于正向市场，但市场预期未来一个月或几个月的波动率会增加。所以这可能不再是一个盈利的交易了。
