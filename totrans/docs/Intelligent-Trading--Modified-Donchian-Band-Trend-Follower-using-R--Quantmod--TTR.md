<!--yml
category: 未分类
date: 2024-05-18 04:46:13
-->

# Intelligent Trading: Modified Donchian Band Trend Follower using R, Quantmod, TTR

> 来源：[http://intelligenttradingtech.blogspot.com/2010/03/modified-dochian-band-trend-follower.html#0001-01-01](http://intelligenttradingtech.blogspot.com/2010/03/modified-dochian-band-trend-follower.html#0001-01-01)

I've been toying around with the examples given on the

[FOSS trading site](http://blog.fosstrading.com/2009/04/testing-rsi2-with-r.html)

for some of the great work they've put together in the Quantmod and TTR packages. Those viewers who are looking for a nice (and free) backtesting suite to possibly complement some of your other results or work in say, Weka, should familiarize yourselves with R. Not only can it serve as a canvas to simulate ideas and concepts, but can process the backend results towards more trader oriented metrics, than using something like Weka as a standalone tool. As you gain more proficiency in data mining and machine learning concepts in Weka, you can also make the move to integrate the tools inside of R, as R contains the majority of machine learning schemes inside of various packages.

[![](img/42c34520ad0e160166d6fe70dbbe31aa.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg_n8wv9T8qEW-Mrx_SNJBP0bXk_zTGmeI4w4UYXQ7DKIjP6HEz_C_Z9oqDTJk0N80Gtm3rmFxGSh5UoBTpSEvN1sQLPt7tEtgCa1Mx9wWdtGZ7CFt7njGXu-zvfbAe9ULrGwRajbw9JCk/s1600-h/donch_ex.jpg)

Fig 1\. Modified Donchian Channel System Simulation

As an example of how to use some of their tools (along with traditional R packages) for fast prototyping, I put together an example of a modified Donchian Channel trend following system along with how you might simulate it using R. The typical Donchian Channel Bands are used as breakout entry and exit signals. I.e. once an n period high has been breached you go long, then exit when the n period low has been breached -- visa versa for short. In this example, however, we simply enter long on the average line break and stay long as long as it is above. A short signal is entered on the average line break to the downside. Unlike a price/moving average type system, there wasn't a lot of choppiness causing false starts around the average line, which is a plus.

I am still trying to familiarize myself more with the tools, and am still at the point where I like how simple and fast the static vector computations work (similar to numpy in Python), but I am wondering how fast more sophisticated entry/exits requiring loops will work. I still expect to work on some of these types of scenarios, as I am really enjoying the capabilities of R along with some of these trading oriented packages.

Although the system (using QQQQ as an example) is in no way optimized nor analyzed for robustness, it returned a respectable 60% versus a buy and hold loss over the past roughly two years (showing a simple example of trend type trading).

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