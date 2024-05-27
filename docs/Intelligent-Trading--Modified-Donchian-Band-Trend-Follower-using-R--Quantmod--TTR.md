<!--yml

类别：未分类

日期：2024-05-18 04:46:13

-->

# 智能交易：使用 R、Quantmod、TTR 的修改唐奇安通道趋势跟踪者

> 来源：[`intelligenttradingtech.blogspot.com/2010/03/modified-dochian-band-trend-follower.html#0001-01-01`](http://intelligenttradingtech.blogspot.com/2010/03/modified-dochian-band-trend-follower.html#0001-01-01)

我一直在玩味给出的例子

[FOSS 交易网站](http://blog.fosstrading.com/2009/04/testing-rsi2-with-r.html)

对于他们在 Quantmod 和 TTR 包中整理的一些出色工作。那些寻找一个漂亮（且免费）的回测套件来可能补充你们其他结果或工作在比如说 Weka 中的观众，应该熟悉 R。它不仅可以作为模拟思想和概念的画布，还可以处理更面向交易者的指标的后端结果，而不是使用 Weka 这样的独立工具。随着你在 Weka 中对数据挖掘和机器学习概念变得更加熟练，你也可以将工具集成到 R 中，因为 R 包含各种包中的大多数机器学习方案。

![唐奇安通道图](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg_n8wv9T8qEW-Mrx_SNJBP0bXk_zTGmeI4w4UYXQ7DKIjP6HEz_C_Z9oqDTJk0N80Gtm3rmFxGSh5UoBTpSEvN1sQLPt7tEtgCa1Mx9wWdtGZ7CFt7njGXu-zvfbAe9ULrGwRajbw9JCk/s1600-h/donch_ex.jpg)

图 1。修改后的唐奇安通道系统模拟

作为一个使用他们一些工具（以及传统的 R 包）进行快速原型的例子，我整理了一个修改后的唐奇安通道趋势跟踪系统的例子，以及如何使用 R 进行模拟。典型的唐奇安通道带被用作突破入场和离场信号。也就是说，一旦 n 周期的高点被突破，你就做多，然后在 n 周期的低点被突破时离场——做空相反。然而，在这个例子中，我们只要平均线突破就做多，只要它在平均线之上就持有。在平均线下方，平均线突破时做空。与价格/移动平均类型的系统不同，平均线周围没有造成很多假启动的波动，这是一个优点。

我仍在努力熟悉这些工具，并且仍处于我喜欢静态向量计算工作如此简单和快速的阶段（类似于 Python 中的 numpy），但我想知道更复杂的入场/离场，需要循环会怎样。我仍然期待着处理这些类型的场景，因为我真的很喜欢 R 以及这些面向交易的包的能力。

尽管这个系统（以 QQQQ 为例）根本没有经过优化，也没有分析其稳健性，但在过去的大约两年里，它返回了 60%的回报，而买入持有策略则亏损（展示了一个简单的趋势交易类型示例）。

Here is the complete code for you to replicate (I used the R version 2.7.10.1).

Note: if some of it looks familiar to the FOSS RSI example, it is exactly because I used that example as a starting point, so there will be some overlap in comments and actions.

# We will need the quantmod package for charting and pulling

# data and the TTR package to calculate Donchian Bands.

# You can install packages via: install.packages("packageName")

# install.packages(c("quantmod","TTR"))

# See Foss Trading Blog for RSI template

library(quantmod)

library(TTR)

tckrtckr_obj

startend

# Pull tckr index data from Yahoo! Finance

getSymbols(tckr, from=start, to=end)

QQQQ.clQQQQ.HQQQQ.Ldc

#Plotting Donchian Channel

ymin=25

ymax=55

par(mfrow=c(2,2), oma=c(2,2,2,2))

# max, avg, min plot(dc[,1],col="red",ylim=c(ymin,ymax),main="")

par(new=T)

plot(dc[,2],col="blue",ylim=c(ymin,ymax),main="")

par(new=T)

plot(dc[,3],col="green",ylim=c(ymin,ymax),main="")

par(new=T)

plot(QQQQ.cl,ylim=c(ymin,ymax),pch=15,main="donchian bands max/avg/min")

lines(QQQQ.cl,ylim(ymin,ymax))

###################################################

# Create the long (up) and short (dn) signals

sigup dc[,2],1,0)

sigdn

# Lag signals to align with days in market,

# not days signals were generated

sigup sigdn

# Replace missing signals with no position

# (generally just at beginning of series)

sigup[is.na(sigup)] sigdn[is.na(sigdn)]

# Combine both signals into one vector

sig

# Calculate Close-to-Close returns

ret ret[1]

# Calculate equity curves

eq_up eq_dn eq_all

#graphics

mfg=c(1,2)

plot(eq_up,ylab="Long",col="green")

mfg=c(2,2)

plot(eq_all,ylab="Combined",col="blue",main="combined L/S equity")

mfg=c(2,1)

plot(eq_dn,ylab="Short",col="red")

title("Modified Donchian Band Trend Following System (intelligenttradingtech.blogspot.com)", outer = TRUE)

##############################################################################################################

P.S. As always, please use your own due diligence in all work borrowed from this site. There are some areas that I believe are not quite correct in the simulation framework, needless to say, you have a complete script to start your own examples and backtesting.
