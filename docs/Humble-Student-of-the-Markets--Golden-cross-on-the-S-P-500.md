<!--yml

category: 未分类

date: 2024-05-18 00:50:59

-->

# 谦卑的市场学生：标普 500 的黄金交叉

> 来源：[`humblestudentofthemarkets.blogspot.com/2009/06/golden-cross-on-s-500.html#0001-01-01`](https://humblestudentofthemarkets.blogspot.com/2009/06/golden-cross-on-s-500.html#0001-01-01)

人们对于 50 日移动平均线穿越 200 日移动平均线产生的“黄金交叉”现象产生了一些热议，标普 500 就经历了这样的现象。

![黄金交叉](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjO44YcQWoIdGqSI2U5I_M9D9Cx73b2Mx-SLTbXBzkPTyNT_O0w31AYlo9YVh6lj56ilf-bw5l1Fwgk2CxRQjOZf4XY3MxEP8Sjn1Bj1qNh2AhEYvO6ujKUoXLzBUwcbZQAigDrF9PZrVDr/s1600-h/Golden+Cross.JPG)**逆向投资？还是跟随大众？**

有言论称这样的黄金交叉事件对市场是利好的。这一观点基于趋势跟踪模型，而后者依赖于价格趋势的持续性。

<param name="movie" value="//www.youtube.com/v/jVygqjyS4CA&amp;hl=en&amp;fs=1&amp;"><param name="allowFullScreen" value="true"><param name="allowscriptaccess" value="always"><embed src="//www.youtube.com/v/jVygqjyS4CA&amp;hl=en&amp;fs=1&amp;" type="application/x-shockwave-flash" allowscriptaccess="always" allowfullscreen="true">

问题在于，你是想做一个逆向投资者，还是想做一个跟随大众的“羊”（跳上潮流的列车）？

**价格趋势会持续吗？**

显而易见，如果这些趋势跟踪系统要起作用，那么价格趋势必须持续。从量化角度来看，这些策略只有在价格变动存在自相关性时才是盈利的。

为了测试这些观点，我分析了标普 500 的日回报与之前一天的回报之间的相关性，以研究从 1993 年至今的价格动量持续性。尽管标普 500 一日回报的中位数相关性为-0.08，表明价格有反转的倾向，但我发现确实存在强劲动量的时期。基于自相关性指标预测这些时期的优化解决方案，最终产生了更好的风险调整回报。

下面的图表展示了结果。深蓝色线条显示了自 1993 年以来标普 500 的累积只做多回报。红色线条显示了一个 50-200 日移动平均交叉系统的回报，其中信号定义为：

**做多：**

50 日均线 > 200 日均线，且 50 日均线作为跟踪止损

**做空：**

50 日均线 < 200 日均线，且 50 日均线作为跟踪止损

当产生信号时，根据下一个交易日的收盘价采取行动。这里不考虑摩擦成本，当系统没有产生信号时，假设回报为 0%。

绿色线条显示的是优化策略，只有当标普 500 显示出趋势时，它才会使用 50/200 日移动平均趋势跟踪模型。

![趋势跟随+标普 500](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg-AvFfkI8kslnKeF_kRWVnm1Uqjb2e6STmjCYnH62v75fvEf-wCyvsSltjatnz87yShaGSbcnexWWIwJhW2zDj0o8KHGSfPTgWkBjp6URcNJdE_LAjjkTTb3ikuiDlnCTJS_ZZq_5NtX4F/s1600-h/TrendFollowing+SPX.JPG)

从这些结果来看，很明显，与仅持有多头头寸相比，趋势跟随模型可以赚钱并降低风险。将 50/200 日系统（红线）的结果与仅持有多头投资（蓝线）的结果进行比较，趋势跟随系统总体呈上升趋势，并且相对于仅持有多头头寸有更少的回撤。图表还显示，与未优化系统（红线）相比，优化系统（绿线）的回报相似，但优化系统的波动性和回撤要低得多。

**如果没有趋势会怎样？**

上文分析的标准普尔 500 指数在研究期间总体呈趋势性，这使得趋势跟随系统能够盈利。但如果将趋势跟随系统应用于一个总体无趋势的价格流会怎样呢？

下图显示了从 1959 年至今，将同样的 50/200 日移动平均趋势跟随系统应用于小麦期货。在大部分时间里，小麦价格相对平稳，没有趋势。

在这种情况下，趋势跟随系统（红线）表现不佳。1959 年投资的 100 美元，如今大约只能净赚 17 美元。优化系统（绿线）虽然也亏损，但其表现更好，波动性更低。

1959 年在优化系统中投资的 100 美元，如今可以净赚 62 美元，这比简单的 50/200 日移动平均趋势跟随者要强。

![趋势跟随+小麦](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhdK-S9rX-3_O0CS2_ZzihiKr60zRyQgQ8YAX4juM0ZSB1guKi01cnRdcAu362YhbJAy1rANSUgFS9GAACdIkp92BKznGAM_A1QMKDCGOZoGZiIp35RURA1LE-wyjA1qg7IlNkGXHmivig1/s1600-h/TrendFollowing+Wheat.JPG)**理解你的假设：构建一个元模型**

这个故事的寓意是

[理解你模型背后的假设](http://humblestudentofthemarkets.blogspot.com/2009/06/financial-modelers-need-to-thimk.html)

. 一旦你理解了这些假设，分析市场环境。你可能能够构建一个元模型来预测你模型的表现，并根据市场条件优化模型的性能。

**关于那个黄金交叉…**

那么标普 500 的黄金交叉呢？那是一个好的信号吗？

优化读数在 6 月 25 日周四收盘时从趋势信号转变为非趋势信号。此外，50 日移动平均的跟踪止损并不遥远，在 903。

模型读数波动较大，止损点并不遥远。请谨慎交易。
