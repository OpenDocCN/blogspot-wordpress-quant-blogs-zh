<!--yml
category: 未分类
date: 2024-05-12 18:56:34
-->

# Quantitative Trading: Predicting volatility

> 来源：[http://epchan.blogspot.com/2015/11/predicting-volatility.html#0001-01-01](http://epchan.blogspot.com/2015/11/predicting-volatility.html#0001-01-01)

Predicting volatility is a very old topic. Every finance student has been taught to use the GARCH model for that. But like most things we learned in school, we don't necessarily expect them to be useful in practice, or to work well out-of-sample. (When was the last time you need to use calculus in your job?) But out of curiosity, I did a quick investigation of its power on predicting the volatility of SPY daily close-to-close returns. I estimated the parameters of a GARCH model on training data from December 21, 2005 to December 5, 2011 using Matlab's Econometric toolbox, and tested how often the sign of the predicted 1-day change in volatility agree with reality on the test set from December 6, 2011 to November 25, 2015\. (One-day change in realized volatility is defined as the change in the absolute value of the 1-day return.) A pleasant surprise: the agreement is 58% of the days.

If this were the accuracy for predicting the sign of the SPY return itself, we should prepare to retire in luxury. Volatility is easier to predict than signed returns, as every finance student has also been taught. But what good is a good volatility prediction? Would that be useful to options traders, who can trade implied volatilities instead of directional returns? The answer is yes, realized volatility prediction is useful for implied volatility prediction, but not in the way you would expect.

If GARCH tells us that the realized volatility will increase tomorrow, most of us would instinctively go out and buy ourselves some options (i.e. implied volatility). In the case of SPY, we would probably go buy some VXX. But that would be a terrible mistake. Remember that the volatility we predicted is an unsigned return: a prediction of increased volatility may mean a very bullish day tomorrow. A high positive return in SPY is usually accompanied by a steep drop in VXX. In other words, an increase in realized volatility is usually accompanied by a decrease in implied volatility in this case. But what is really strange is that this anti-correlation between change in realized volatility and change in implied volatility also holds when the return is negative (57% of the days with negative returns). A

*very*

negative return in SPY is indeed usually accompanied by an increase in implied volatility or VXX, inducing positive correlation. But on average, an increase in realized volatility due to negative returns is still accompanied by a decrease in implied volatility.

The upshot of all these is that if you predict the volatility of SPY will increase tomorrow, you should short VXX instead.

====

**Industry Update**

*   **[Quantiacs.com](http://quantiacs.com/)

    just launched a trading system competition with guaranteed investments of $2.25M for the best three trading systems. (

    Quantiacs helps Quants get investments for their trading algorithms and helps investors find the right trading system.)**

*   Another new book called "[Algorithmic and High-Frequency Trading](http://amzn.to/1PQSOlv)" by 3 mathematical finance professors describes the sophisticated mathematical tools that are being applied to high frequency trading and optimal execution. Yes, calculus is required here.

**My Upcoming Workshop**

January 27-28: Algorithmic Options Strategies

This is a new online [course](http://epchan.com/workshops) that is different from most other options workshops offered elsewhere. It will cover how one can backtest intraday option strategies and portfolio option strategies.

These courses are highly intensive training sessions held in London for a full week. I typically need to walk for an hour along the Thames to rejuvenate after each day's class.

The AI course is new, and to my amazement, some of the improved techniques actually work.

**My Upcoming Talk**

I will be speaking at [QuantCon](http://www.quantcon.com/)[ 2016](http://www.quantcon.com/) on April 9 in New York. The topic will be "The Peculiarities of Volatility". I pointed out one peculiarity above, but there are others.

====

QTS Partners, L.P. has a net return of +1.56% in October (YTD: +11.50%). Details available to Qualified Eligible Persons as defined in CFTC Rule 4.7.

====

Follow me on Twitter: @chanep