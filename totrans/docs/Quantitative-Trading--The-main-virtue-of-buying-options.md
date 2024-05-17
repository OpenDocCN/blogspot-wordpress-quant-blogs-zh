<!--yml
category: 未分类
date: 2024-05-12 19:03:32
-->

# Quantitative Trading: The main virtue of buying options

> 来源：[http://epchan.blogspot.com/2010/10/main-virtue-of-buying-options.html#0001-01-01](http://epchan.blogspot.com/2010/10/main-virtue-of-buying-options.html#0001-01-01)

I realized that I have omitted the most obvious virtue of trading options instead of stocks in my last post: the much more attractive reward-risk ratio for options.

Suppose your stock strategy generated a buy signal. You can either buy the stock now, or you can buy an ATM call. If you buy the stock, you are of course benefiting from 100% of the upside potential of the stock price movement, but you are similarly exposed to 100% of the downside risk. Indeed you can lose the entire market value of the stock. If you buy the call, you will benefit from > 50% of the upside potential of the stock price, assuming that your holding period is so short that the time value will not dissipate much. As the stock price rises, so does your delta. (It increases from 0.5 to 1.) But what about the downside risk? All you can lose is the option premium, usually << 50% of the market value of the stock.

In other words, while one may be tempted to hedge a large stock position with stock index futures, there is no need to hedge an equivalent call option position. This should simplify your strategy implementation and reduce risk management costs (i.e. the probable loss on your short futures position).

Given that I am a short-term trader anyway, I can't figure out why I have been trading stocks instead of options all these years! (Aside from the caveats detailed in the previous post.)