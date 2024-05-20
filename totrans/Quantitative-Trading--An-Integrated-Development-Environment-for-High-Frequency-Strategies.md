<!--yml
category: 未分类
date: 2024-05-12 18:59:47
-->

# Quantitative Trading: An Integrated Development Environment for High Frequency Strategies

> 来源：[http://epchan.blogspot.com/2013/04/an-integrated-development-environment.html#0001-01-01](http://epchan.blogspot.com/2013/04/an-integrated-development-environment.html#0001-01-01)

I have come across many software platforms that allow traders to first specify and backtest a strategy and then, with the push of a button, turn the backtest strategy into a live trading program that can automatically submit orders to their favorite broker. (See all my articles on this topic

[here](http://epchan.blogspot.com/search/label/Automated%20trading%20platforms)

.)  I called these platforms "Integrated Development Environment" (IDE) in my

[new book](http://www.amazon.com/gp/product/1118460146/ref=as_li_qf_sp_asin_il_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1118460146&linkCode=as2&tag=quantitativet-20)

, and they range from the familiar and retail-oriented (e.g. MetaTrader, NinjaTrader, TradeStation), to the professional but skills-demanding (e.g. ActiveQuant, Marketcetera, TradeLink),  and finally to the comprehensive and industrial-strength (e.g. Deltix, Progress Apama, QuantHouse, RTD Tango). Some of these require no programming skills at all, allowing you to construct strategies by dragging-and-dropping, others use some simple scripting languages like Python, and yet others demand full-blown programming abilities in Java, C#, or C++. But which of these allow us to backtest and execute high frequency strategies?

To state the obvious: backtesting HFstrategies is quite hard. The volume of data is one issue. But in addition, the execution details are very important to such strategies: details such as the exact exchange/venue to which we are routing our orders, the precise state of the order book that triggers our orders, the order types we are using, and finally the probability of getting filled if we use non-marketable orders. Messing up one of these details and the backtest will be far from realistic. I often tell people that it is easier to paper trade a HF strategy than to backtest one. While many of the platforms I reported above do allow backtesting using tick data, I don't know that they enable backtesting using the full order book and choice of execution venue. With this background, I am happy to report I have recently come across just such a platform called

[Lime Strategy Studio](http://www.limebrokerage.com/services/marketdata/simulation)

.

~~First, the bad news. LimeTrader is useful only to traders who trade with Lime Brokerage, as it is configured to send live orders to Lime only.~~

[

**UPDATE:**

I have since learned that there are adapters available for 3rd party brokers.] However, if you are going to trade HF stocks and futures strategies, why not go with Lime, since they provide you with a comprehensive API, direct ultra-low latency feeds from the exchanges, and allow (nay, insist on) colocation either at the exchanges or at their data center at a reasonable fee? (Full Disclosure: I have no current business relationship with Lime, though I was a customer.) Another piece of bad news: the specification of the strategy must be in C++.

But once you get over these two hurdles, the benefits are manifold. Every detail that you can specify for a live trading strategy can be specified for the backtest and paper trading. As I said, these details may include order type, trading venue, state of order book, and even statistics of the order book, not to mention fundamental data such as earnings, corporate actions, and other user-provided data such as news. A fill simulator is included for your non-marketable orders. As with other IDEs, once you backtested a strategy in its every detail and are satisfied with the performance metrics, you can go live (either for paper or production trading) with the push of a button.

If any reader know of other IDEs that have similar features and useful for backtesting HF strategies, please let us know!

===

Speaking of HF strategies, traders often lament the ultra-high secrecy around them and the difficulty of gathering knowledge in this field. A friend (hat tip: Dave) referred me to this

[paper](http://www.math.stevens.edu/~ifloresc/Research/Publications/ProjectpricevolFinalwithDragos.pdf)

by Prof. Dragos Bozdog

*et. al.*

that gives a flavor of what sort of modeling may be involved. I find it very readable and thought-provoking.

===

There are still 2 slots available in my online 

[Mean Reversion Strategies workshop](http://www.epchan.com/my-workshops/)

scheduled for May.