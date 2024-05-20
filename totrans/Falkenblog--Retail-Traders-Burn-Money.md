<!--yml
category: 未分类
date: 2024-05-12 23:01:50
-->

# Falkenblog: Retail Traders Burn Money

> 来源：[http://falkenblog.blogspot.com/2008/08/retail-traders-burn-money.html#0001-01-01](http://falkenblog.blogspot.com/2008/08/retail-traders-burn-money.html#0001-01-01)

From

[The Extent of Individual Investory Trading Losses](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1246890)

by Fong, Gallagher, and Lee over at New South Wales:

> This paper investigates the trading performance of retail brokerage investors on the Australian Securities Exchange (ASX) from 1990 to 2005\. We document average losses per day, before transaction costs, of USD$120,000 (AUD$190,000) or 27 basis points per day from individual investors buying (selling) higher (lower) than the closing price on the day. This loss is robust across calendar years, stock size, order type, time of day and broker service offerings. Net of this loss, individual buy trades are statistically indistinguishable to sells at a 254-day/1 year window.

It seems this documents two important points. First, the average investor pays a bid-ask spread, independent of his commission. He also is no better than throwing darts.

My only issues is I wish they would have compared the fill price to the open, because by comparing it to the close that day, or the VWAP (value weight average price) that day, you ignore how much you actually move the price. This 'trade impact' is often large, especially for big trades. There's a tradeoff, such that really small traders with little trade impact tend to pay the highest in bid ask spread, and commissions, while the big guys have fancy trading algorithms to minimize the effect of the bid-ask spread (buy, say, having a program that patiently buys at the bid), but their trade impact is significant. By comparing the fill price to the prior day's close, you capture trade impact.

I remember brokers touting their VWAP algorithms, noting by how little it 'misses' the value-weighted average price. But they ignored the fact that if you move the VWAP upward significantly, equalling the VWAP doesn't mean it was a good fill.