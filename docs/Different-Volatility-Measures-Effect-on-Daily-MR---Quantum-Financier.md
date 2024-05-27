<!--yml

类别：未分类

日期：2024-05-18 14:05:34

-->

# 不同波动率测量对每日 MR 的影响 - 量化金融师

> 来源：[`quantumfinancier.wordpress.com/2010/05/05/different-volatility-measures-effects-on-daily-mr/#0001-01-01`](https://quantumfinancier.wordpress.com/2010/05/05/different-volatility-measures-effects-on-daily-mr/#0001-01-01)

当今的日间摇摆交易策略通常更倾向于 MR 而不是趋势 FT。虽然有很多因素可以调节每日 MR 策略，但特别感兴趣的一个因素是波动率。通常，更高的波动率对短期策略（考虑 RSI 2）是有利的。对于这一小研究，我尝试了几种不同的时间框架上的几种波动率公式，并比较了对 RSI 2 收益的影响。

方法论：我将 RSI 2 策略应用于 2000 年以来的 SPY 收益，然后将波动率分类为百分位数。我使用了三种不同的方法来计算波动率数字，经典标准差、加曼·克拉斯 - 杨张和杨张方法。以下公式解释了我如何得出这些数字；我在 R 中使用了 [TTR package](http://cran.r-project.org/web/packages/TTR/index.html) 中的波动率函数：

加曼·克拉斯 - 杨张方法：

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/gk-yz-formula1.jpg)

杨张方法：

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/yz-formula.jpg)

其中：

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/symbols.jpg)

*GK-YZ 方法允许开放差距，而 YZ 方法与漂移和开放差距无关。

下表显示了按百分位数分类的每月（21 天）和每年（252 天）时间框架的平均交易结果和获胜百分比。请注意，这些时间框架是任意选择的，未来的一篇文章可能会用不同的时间框架来扩展此内容。

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/table.jpg)

乍一看，似乎增加了计算复杂度并没有显著提高我们的系统准确性。不过，在月度时间框架下，当受 YZ 指标缓和时，系统在较低百分位数的平均交易回报率较高。无论如何，其余的结果都不足以使我宣布一种波动率指标更适合 MR 系统。交易员可能希望简化并坚持使用经典的标准差。

QF
