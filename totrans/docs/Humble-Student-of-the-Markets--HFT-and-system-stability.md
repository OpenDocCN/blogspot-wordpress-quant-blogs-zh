<!--yml
category: 未分类
date: 2024-05-18 04:24:01
-->

# Humble Student of the Markets: HFT and system stability

> 来源：[https://humblestudentofthemarkets.blogspot.com/2011/02/hft-and-system-stability.html#0001-01-01](https://humblestudentofthemarkets.blogspot.com/2011/02/hft-and-system-stability.html#0001-01-01)

I spend a lot of time thinking about risks to my models and forecasts. In my readings, one of the risks that doesn't seem to get mentioned very much is the instability from high frequency trading (HFT) algorithms. For the newbies, see this

[video](//www.youtube.com/watch?v=9ddoha-34gg)

for a primer on HFT.

**The evolution of HFT**

Long ago, before trading algos dominated stock exchange volume, trading was a relatively simple matter. Buyers and sellers met on the stock exchange floor in a price discovery process. Eventually trades got done and prices reflected the supply and demand dynamics of real buyers and sellers. Brokers acted as agents and got paid a commission for acting as an agent.

Then broker-dealers came along.

[Jeremy Grantham](//www.google.com/url?sa=t&source=web&cd=6&ved=0CC4QFjAF&url=http://www.wealthstrategygroup.net/_uploads/GMA_Quarterly_July_2010.pdf&ei=TBIzTdbfDoi_gQfJtqDPCw&usg=AFQjCNHlJOonToEWFaSfir3d48x5ovh2IA)

complained that:

> The problem of asymmetrical information is compounded by the confusion between the roles of agent and counterparty. I grew up in a world where stocks and other financial instruments were traded by the client with a high degree of trust in the agent. Millions of dollars traded on a word, without a tape recording. Somewhere along the way, without any formal announcement of the change, the “client” in a trade mutated into a “counterparty” who could be exploited. Steadily along the way, the agents’ behavior became more concerned with the return on their own trading capital than with the well-being of their clients. One of my nastiest shocks in 45 years was the realization one day in 1985 that we had been ripped off by our then favorite broker on one of the early program trades we were doing. We had supposed we had developed a trusting relationship. We had certainly done many incentive trades that were successful from our point of view. Perhaps, with hindsight, our strong incentives might have merely motivated them to rip off some other client.

Brokers stopped viewing clients as clients and began to view them as trading adversaries. Somewhere along the way, the quants took over and market making became more automated. Today we have a proliferation of HFT algorithms on the virtual floor of the exchange.

But what happens when a good idea becomes widely adopted and becomes the market? That's what seems to be happening with HFT algos trading the market.

[Paul Wilmott](http://www.wilmott.com/blogs/paul/index.cfm/2010/12/3/The-Inbox-Test-for-Stability-of-the-Global-Financial-Market)

wrote that his inbox is now stuffed with announcements about HFT and HFT conference - which is an ominous sign.

With HFT, it's an arms race. You need to be faster and have more information than the next guy. As part of that evolution, we have

[algos that adjust order flow for latency](http://www.theglobeandmail.com/globe-investor/putting-the-hammer-to-high-frequency-traders/article1871294/)

and we even have a

[hedge fund that scrapes data from Twitter](http://www.bloomberg.com/apps/news?pid=newsarchive&sid=a0HeKpjwajW8)

to trade the market as part of that evolution.

**Algos gone wild?**

Here is my nagging worry: What happens if too many HFT algos start to dive on the same information source? Would that create an informational and price cascade? We know how quickly computers can generate orders, were similarly (momentum) oriented algos tried to trade on the same data and started to stampede, how long would it move the market before intelligent adults stepped in to shut the whole thing down?

[Felix Salman](http://blogs.reuters.com/felix-salmon/2011/01/13/algorithmic-trading-and-market-structure-tail-risks/)

pointed to a comment from Michael Kearns of the University of Pennsylvania, who believes that these systems are unpredictable and possibly unstable under certain circumstances [emphasis added]:

> There’s a growing understanding and belief on Wall St, especially intraday, that there’s a strong game-theoretic aspect to the market: the performance of a given strategy depends on what other strategies are trading in the market at the same time. My payoff is a function of what I do and what the other players in the game do.
> 
> The concepts of strategic interaction are important. Game theory is hard to understand even in simple cases. And now strategies are adaptive, so it’s especially difficult. I’m not frightened by it, but it’s a legitimate concern. People who build good machine learning algos have a fair amount of knowledge about what they’re doing, but they’re still adaptive. It’s natural to have the model retrain itself each night based on each day’s data. Humans might not know what incremental modifications today’s data introduced in this adaptive process. If everybody’s doing this, you can easily imagine various effects. That could be a bad thing from a stability standpoint in the markets.
> 
> Our financial markets have become a largely automated adaptive dynamical system, with feedback. Furthermore, a dynamical adaptive system with feedback is challenging ordinarily, but this one is also strategic. A flight controller is dynamical, but not strategic. Add an adversarial environment, and ***there’s no science I’m aware of that’s up to the task of understanding the potential implications of that system***.

In addition, we know that hackers can introduce latency into HFT systems, which cause instability. What happens in a fast moving market? Is the instability "stable" or would it create wild price oscillations?

Before anyone flames me to tell me how implausible such a scenario is, recall how dynamic delta-hedging/portfolio insurance strategies contributed to the downside volatility in the Crash of 1987.