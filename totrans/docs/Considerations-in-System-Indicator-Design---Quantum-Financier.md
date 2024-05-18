<!--yml
category: 未分类
date: 2024-05-18 14:01:56
-->

# Considerations in System/Indicator Design – Quantum Financier

> 来源：[https://quantumfinancier.wordpress.com/2010/10/22/considerations-in-systemindicator-design/#0001-01-01](https://quantumfinancier.wordpress.com/2010/10/22/considerations-in-systemindicator-design/#0001-01-01)

The amount of noise in raw financial data makes it very hard to model. This is partly why we use indicators. They summarize information in a concise way that is easier to interpret that the raw market data. A lot of them are actually transforms borrowed from other fields adapted to financial markets. Engineering is an obvious one, considering the ever-growing number of engineers hired by hedge funds and trading firms. They are also quite appealing to the system designer also as they give a systematic way to code trading rules. I also found that designing indicator is one of the best exercises to further understanding of a certain market phenomena. Trying to find a way to process the financial data to expose a certain type of information in a novel way forces us to stop and think about the underlying mechanics of the market which can only be beneficial for a serious investor. It is this process we will look at in the remainder of the post.

In their basic sense, indicators are nothing more than a particular transform applied to the data to put into evidence selected aspects of it. Take the relative strength index (RSI) for example. It does nothing more than isolates and normalize the magnitude and the velocity of the recent price movements. Also note that there is many ways to extract the same type of information, think DVO.

First thing we need to do when looking at developing indicators or systems is to consider the statistical attributes of the process we want to model, in this case the market. Here are a few commonly accepted ones to get you started (by no mean an exhaustive list):

– Values tend to center around primary clusters (think market regimes)
– Outliers exist between clusters (think fat tails).
– Common statistical measures greatly diverge from their historical tendencies in times of crisis. Think about volatility clustering or correlation converging to 1 when the market goes south.

All these patterns (and a lot more but it is beyond the scope of the post) need to be considered when developing indicators or system (see [Michael Stokes’ TAA series](http://marketsci.wordpress.com/2010/10/20/roundup-tactical-asset-allocation/) for a good example). Doing this kind of analysis of the underlying process we want to model/evaluate, we get valuable insight and we are better prepared to tackle the creative thinking process by knowing more about what we are after. It also offers a framework to work with when thinking of the market in general, which in turn can only spark more ideas and keep the creative juices flowing!

QF