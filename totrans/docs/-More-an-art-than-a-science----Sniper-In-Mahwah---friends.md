<!--yml
category: 未分类
date: 2024-05-18 14:14:08
-->

# “More an art than a science” – Sniper In Mahwah & friends

> 来源：[https://sniperinmahwah.wordpress.com/2015/07/16/more-an-art-than-a-science/#0001-01-01](https://sniperinmahwah.wordpress.com/2015/07/16/more-an-art-than-a-science/#0001-01-01)

I am currently classifying the thousands of thousands of pages of articles, academic papers, press releases, etc., I have printed since I am immersed in HFT (from January 2012), and I rediscover an interesting discussion I had with a high-frequency trader. Sometimes the fierce discussions on Twitter about HFT and market structure push some anonymous people to drop me a line (as I sometimes ask questions on Twitter), and someone (not on Twitter, and anonymous) has been good enough to answer to some technical questions I had about different issues I am/was trying to understand (since then I have a better view on those issues).

The different topics approached in the lines below (the ban on locked markets, the jitter in and/or around the matching engines, quote stuffing, the way you “make the market”, etc.) will be developed in various posts later, that’s why I don’t comment them here. In the meantime, here are some raw comments about some parts of the small world of high-frequency trading. I had many other (more or less anonymous) discussions by email or face to face with different people from the HFT industry, but the comments below were especially clear. Given that this blog is mostly visited by people from HFT firms (I have a tracker, so I have a lottttt of names), these people will probably learn nothing, but others may be interested. (I slightly edited some parts for a better understanding; minor comments in [brackets] are mine.)

##### THE BAN ON LOCKED MARKET

> “[Regulation NMS] bans exchanges from displaying a quote that would lock the price of any other market (bid=ask) . Since the US markets have rebates, the effective price of passively trading (place a limit order that rests on the book, another trader comes along and trades with you) *versus* actively trading (your price crosses an order resting on the limit order book) is different.
> 
> Say BATS is showing 10.01 bid, 10.02 offer.
> 
> If I buy the 10.02 offer, I am paying 10.0230 due to the taker fee. If the market widens, going to 10.01 bid, 10.03 offer, if I add a bid for 10.02 and wait to trade passively, I get a rebate and will effectively pay 10.0170\. Now this is not a huge difference to normal people, but to HFT market-makers who may earn something like 0.0010 a share net of costs, it’s a huge difference.
> 
> Now say BATS goes 10.01 bid, 10.03 offer, but [NYSE] ARCA still shows 10.02 offer. As an HFT, my valuation model may say I can trade profitably buying at 10.0170, but not at 10.0230\. I want to post a bid on BATS, but can’t unless someone trades the order on ARCA, or I do it myself and send an ISO order. This creates a sort-of friction in the marketplace and has led to order types where I can put my 10.02 order on BATS, but they won’t show it until ARCA moves, which just makes the market more complex, and prevents others from trading with my order which they may prefer to waiting for a passive fill on another market. This also makes it difficult for someone to say, buy all the shares on the offer, and then post their remainder at that price passively to buy more, which is a completely natural thing to do in the market. Instead their order will get rejected or slid and HFTs may jump into that price first.
> 
> Some people think the order types were unfairly preferencing HFTs. I don’t think that’s the case since they’re public [ahem, Mister Bodek will undoubtedly disagree], but it’s just a lot of unnecessary complexity [on this everyone agrees] and makes people think the market is unfair.”

##### MARKET MAKING

> “What I do is come up with a statistical forecast of a “fair value” for each security I trade. What goes into such models is proprietary but generally imagine any order book event that could affect its price in the short term: supply/demand imbalance, movements in correlated securities in the same industry, my own inventory in that stock or others, etc. Some of these models are statistical where I use historical data and others are mechanical economic relationships e.g. where an ETF should not trade at a discount/premium to its constituent stocks, or a stock should trade around the same price on every market, [I’ll go into further details about arbitrage in the *Xenia of Saint Petersburg* series in September], etc.
> 
> Once I determine a fair value, I place orders to bid and offer some distance around it, aiming to passively sell the offer and buy the bid such that on average I capture some portion of this spread. As my valuation changes, I update these orders to reflect my views and to control my risk exposures. My models have many variables and are driven by order book events; this is why you often hear about HFTs having high quote/trade ratios since they constantly adjust their prices in the market to reflect their views and risk tolerances.
> 
> Coming up with a fair spread and deciding how much size to bid and offer is more an art than a science and I constantly run experiments to maximize my risk-adjusted returns and market share. Speed matters since one must set the most aggressive price fastest to win order flow in a price-time priority world, and one must use a smart forecasting model to cancel orders that may be hit by aggressive arbitrage traders [those with microwave dishes?], informed market participants, etc.
> 
> Imagine my model generally resting at the best bid and offer with occasional times where we try to “get out of the way” when buying or selling looks particularly bad for me so we step my bid or offer away. Our aim is not to speculate on price, but rather to be “not wrong” so on average our expected win rate (the spread) is slightly higher than my scratch (buy/sell same price). While a lot of people claim HFTs “scalp” people for pennies, in reality we capture a small fraction of the spread most of the time. Our net profit is fractions of a cent. On average when someone elects to trade with our quote, the price moves in their favor. Our aim is to have it move a bit less than the spread on average, so we can make a small amount and do enough volume to… [censured].”

##### MATCHING ENGINES AND THE JITTER

> Most exchange matching engines are structured where there is a central matching engine for each symbol, and gateway processes for each member to send their orders through that handle protocol translation, maybe some safety checks, and message throttling to keep one member from taking the exchange down.
> 
> Most generally matching engines have order entry gateways for each firm that maintain a queue of incoming messages to add, cancel, or amend orders. The exchange matching engine will check each gateway in turn and process one message from each sequentially. The claim that “quote stuffing” can benefit a participant is dubious for several reasons due to this: 1. If we rapidly send messages, we will queue them at my own gateway, so other participants’ orders will be processed first. 2. Sending orders is computationally expensive; we must encode a message and send it out on my network which takes more time than doing nothing and 3. Every order book event is reflected on a multicast feed to all participants. If I send many messages rapidly, my own software or hardware must process them all just like everyone else. Most “quote stuffing” is due to software bugs or interactions between algorithms both trying to set the best price, etc. [some are going to scream by reading this point of view, but that was not the first time I heard that].
> 
> Exchange’s software has inherent latency and jitter. Currently, there is more jitter between exchange gateways, even on the top exchanges, than the difference between top HFT firms. What this means is that if you have two very fast firms, say one responds to the event in 5 microseconds, and the other in 10, the guy who takes 10 microseconds can beat the 5 microsecond guy into the exchange matching engine some of the time due to gateway jitter [!]. The end result of this is that if you have a bunch of firms with response times < 10 microseconds or some other low number, shaving extra microseconds off their latency isn’t enough to win trades anymore. It just makes it a bit more likely statistically. Instead of one or two firms dominating now, a bunch of smaller firms are sharing the same pie. Because of this, I think the “arms race” in internal latency is basically over, though there are still gains to be had through faster network lines [and microwave dishes].

##### CONCLUSION

> Without traders like ourself, the books there would be nearly empty.
> 
> Apologies if this is long. I have to keep things fuzzy since competitors are always looking to figure out what others are doing.

No need to apologize – it was too short.