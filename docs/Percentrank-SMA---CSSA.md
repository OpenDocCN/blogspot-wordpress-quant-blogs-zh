<!--yml

category: 未分类

date: 2024-05-12 18:25:20

-->

# Percentrank SMA | CSSA

> 来源：[`cssanalytics.wordpress.com/2010/05/19/percentrank-sma/#0001-01-01`](https://cssanalytics.wordpress.com/2010/05/19/percentrank-sma/#0001-01-01)

以下是一些值得一读的近期链接：*

Rob Hanna 在 Quantifiable Edges 网站上研究了日内行为：[#mce_temp_url#](http://quantifiableedges.blogspot.com/2010/05/from-1-up-intraday-to-1-down-close.html)

Dave 在 MindMoneyMarkets 网站上研究了一个常被忽视的细节——指数价格与实际交易的 ETF 指标表现对比：[`davesbrain.blogs.com/mindmoneymarkets/`](http://davesbrain.blogs.com/mindmoneymarkets/)

Michael 在 MarketSci 网站上研究了金叉的不同变体：[`marketsci.wordpress.com/2010/05/18/the-golden-cross-daily-vs-weekly-vs-monthly/`](http://marketsci.wordpress.com/2010/05/18/the-golden-cross-daily-vs-weekly-vs-monthly/)

Quantum Financier（一个新成立但非常有前景的博客）研究了使用概率密度函数创建自适应 RSI 的方法：[`quantumfinancier.wordpress.com/2010/05/14/using-probability-density-as-an-adaptive-mechanism/`](http://quantumfinancier.wordpress.com/2010/05/14/using-probability-density-as-an-adaptive-mechanism/)

Engineering Returns（一个新成立但非常有前景的博客）从均值回归策略的角度对内部蜡烛图过滤进行了有趣的探讨：[`engineering-returns.com/2010/05/18/spy-a-quantitative-view-at-inside-bars/`](http://engineering-returns.com/2010/05/18/spy-a-quantitative-view-at-inside-bars/)

这是对臭名昭著的“percentrank”函数的一个简单改进，用于创建一个趋势跟踪指标。percentrank SMA（P-SMA）的优势在于它是连续的，捕捉了价格序列的分布，而不仅仅是二进制信号。它也比价格的 percentrank 更稳定。本文中使用的计算指标如下：**P-SMA= percentrank(sma(n),250)**你可以选择你喜欢的移动平均长度，但由于计算性质，我建议使用等于或低于 50 的值，以便与金叉或 200sma 的时间跨度相匹配。 general idea 是避免查看价格，因为价格往往波动较大且噪声干扰，而是查看价格序列的平均值/中点，并将其随时间正常化。在这种情况下，与使用 percentrank 的其他指标不同，我们并不专门关注 median 之上/之下，因为已经使用了比价格更稳定的平均值。与相对较短的分布测量（250）相比，长移动平均引入的滞后要求我们降低构成上升趋势的阈值。

在这种情况下，我查看了在过去 12000 根 K 线图中，50 日 P-SMA 在标普 500 指数上的表现，以及在各种阈值下与金叉相比的长短线操作。结果如下，展示了自成立以来 1 美元的复合年化增长率（CAGR）和累积回报。请注意，在过去 2000 根 K 线图中，SPY 的表现为.5 阈值下的 10% CAGR，这表明该指标在近期过去对于交易性工具相对于指数表现也很好。

总体来看，50 参数的百分比排名 SMA 表现优于金叉，以及更短期的变化虽然未展示，但相对于可比较的移动平均线或交叉线表现相当好。在我看来，卖点不仅仅是超越表现（这是很好的），而是你可以在系统创建层面上使用连续趋势指标做更多的事情，而不是使用交叉线。可能的应用涉及百分比暴露模型，或者更有趣的是，使用指标值来调整更短期指标值/信号。

百分比排名 SMA 各种入场阈值与金叉对比（12000 根 K 线）（请确认是否需要翻译成“不同阈值进入的百分比排名 SMA 与金叉的对比”）

金叉 >.5 >.45 >.4 >.35 CAGR 6.13% 6.18% 6.45% 7.44% 6.84% 累积乘数 17.40 17.74 20.071 31.27 23.97 因子
