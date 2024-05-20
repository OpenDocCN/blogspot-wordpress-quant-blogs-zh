<!--yml
category: 未分类
date: 2024-05-18 06:43:57
-->

# Who Executes Retail Trades? A Look at Market Share and Payment for Order Flow | Mechanical Markets

> 来源：[https://mechanicalmarkets.wordpress.com/2015/03/10/who-executes-retail-trades-a-look-at-market-share-and-payment-for-order-flow/#0001-01-01](https://mechanicalmarkets.wordpress.com/2015/03/10/who-executes-retail-trades-a-look-at-market-share-and-payment-for-order-flow/#0001-01-01)

The trading strategies posted on this blog have so far focused on identifying resting limit orders that are likely to have come from a human. There are all kinds of human traders, but probably the most coveted counterparties are retail traders. So coveted, in fact, that wholesalers will pay to interact with them and exchanges will pay to get them into their order books.

Public data that shows where brokers choose to direct customer orders is scarce. The most readily available source is probably SEC 606 reports. 606 reports are generally in a non-standardized format, lack important details, and appear even at a glance to have significant data quality issues. Nonetheless we will try to glean from them what we can. I’ve undertaken the tedious task of converting the unformatted reports, by hand, into something machine readable. I hope the results make the effort worthwhile.

SEC 606 reports generally disclose the following:

1.  The proportional share of destination Broker-Dealers (i.e. wholesalers, ELPs, dark pools, exchanges) for the entirety of a broker’s orders.
2.  The proportional share of a broker’s orders that are market, limit, or “other” orders.
3.  The proportions of orders in each of these 3 categories that were directed to each destination Broker-Dealer.
4.  The average payment per share received by the broker from each destination Broker-Dealer.

Unfortunately, I am not inspired with confidence in the reports’ accuracy or consistency in how they define the various categories. There are data fields that are often missing outright. And there could be additional errors since some of the data entry and cleaning was done manually. Given these limitations, I try to manipulate the data as little as possible to avoid propagating distortions.

First, we need a list of the largest online retail brokerages. I figured that most large brokers would have the money, brand, or shared business interests to be advertised on Nasdaq’s [website](http://www.nasdaq.com/investing/online-brokers/). I picked all of the “Online Broker Partners,” except LOYAL3 because I couldn’t immediately find a 606 report from them. The aggregated 606 reports from Q4 2014 are [here](https://mechanicalmarkets.wordpress.com/wp-content/uploads/2015/03/raw_606.zip), with sourced notes about volume, AUM, regulatory net capital (‘Net Cap’), revenue per trade, and whatever else struck me from public filings. [[1](#bottom1)]

The attached [R script](https://mechanicalmarkets.wordpress.com/wp-content/uploads/2015/03/read_regularized_606_r_script.zip) uses the more regularized data [here](https://mechanicalmarkets.wordpress.com/wp-content/uploads/2015/03/regularized_606.zip). See [[2](#bottom2)] for a rough overview of some of its assumptions.

# Market Share and Payments

After some formatting, the script generates the following market share breakdown for destinations receiving a high share of marketable orders:

| Order Destination | Market Share (%) | Avg Payment ($/shr) | Marketability Index (Between 0 and 1, lower numbers more marketable) |
| UBS | 29.7 | 0.0015 | 0.28 |
| Citadel | 23.2 | 0.0009 | 0.35 |
| KCG | 18.7 | 0.0011 | 0.38 |
| G1 Execution Services | 14.8 | 0.0015 | 0.24 |
| IB ATS | 4.1 | NA | 0.12 |
| Two Sigma | 3.8 | 0.0018 | 0.22 |
| Goldman Sachs | 3.6 | 0.0010 | 0.36 |
| BatsY | 1.1 | NA | 0.14 |
| National Financial Services | 0.7 | NA | 0.26 |
| NITE | 0.2 | NA | 0.34 |
| AUTO | 0.1 | NA | 0.27 |
| AMEX | 0.0 | NA | 0.00 |

And for destinations receiving orders that are less marketable:

| Order Destination | Market Share (%) | Avg Payment ($/shr) | Marketability Index (Between 0 and 1, lower numbers more marketable) |
| Nyse | 28.2 | NA | 0.75 |
| DirectEdge | 27.7 | 0.0032 | 0.89 |
| Nasdaq | 20.6 | 0.0029 | 0.71 |
| Arca | 13.6 | NA | 0.77 |
| Lava | 8.3 | 0.0031 | 0.95 |
| Nyse Mkt | 1.2 | NA | 0.88 |
| Bats | 0.3 | 0.0020 | 1.00 |
| EDGA | 0.1 | NA | 0.74 |

See [[3](#bottom3)] for an overall table.

# Non-Marketable Orders

One of the very first things we see is the higher payments brokers tend to receive for non-marketable orders. This shouldn’t be too surprising, since a broker has an incentive to post non-marketable limit orders on exchanges with high liquidity-provider rebates, which they receive upon execution. Could brokers get their clients a higher fill rate by posting these orders on exchanges with no rebate? Maybe. It’s well known that orders executed on inverted exchanges tend to perform better after trading, by roughly the amount of the rebate difference (we saw this in an earlier [post](https://mechanicalmarkets.wordpress.com/wp-content/uploads/2015/01/toa-exchangesummary-13661.png)). Retail orders may be a bit different though; we shouldn’t ignore the possibility that resting retail orders are almost destined to lose a penny upon trading. Should a client mind if their broker managed to capture a third of that through a rebate instead of feeding all of it to whoever else is trading? Maybe clients should get a commission discount for sending a resting order instead of a marketable one? I can see why brokers might shy away from that kind of pricing transparency. Some [brokers](https://www.robinhood.com/) already offer commission-free trading; going any further down this road would mean clients actually getting paid to trade. At a certain point, brokers might invite [uncomfortable comparisons](https://mechanicalmarkets.wordpress.com/wp-content/uploads/2015/03/casino_rebate.png).

I don’t really know how best to make payments for order flow transparent. Maybe in the distant future there will be some sort of auction process where even non-marketable retail orders can receive price improvement. In the meantime we have to ask whether a broker seeking to pocket a large rebate might sacrifice their customer’s desire to get filled. I find it a bit unlikely since the broker won’t get paid at all if the customer isn’t executed. Ultimately, even with the seemingly perverse system of payment for order flow, brokers and clients probably have similar interests when it comes to resting orders.

We can see that resting orders are generally directed to major exchanges. Nyse, EdgeX, Nasdaq, and Arca make up about 90% of their volume. These exchanges are highly active and I’d expect that they get customers filled without increasing adverse selection by more than their roughly 0.30 cent rebates. I was a bit surprised to see so much volume directed to Nyse, because some exchanges, particularly EdgeX, offer much higher rebates for retail orders (see “[Retail Order Tier](http://www.batsglobalmarkets.com/us/equities/membership/fee_schedule/edgx/)“). Interactive Brokers was the only broker directing signficant volume to Nyse and their fee [schedule](https://www.interactivebrokers.com/en/index.php?f=commission&p=stocks2#america) indicates that at least some of their clients receive part of the liquidity-provider rebate. Maybe because they don’t receive some of it, Interactive Brokers cares less about squeezing the maximum rebate out of client orders (that, or their revenues from rebates are more complex due to the partial pass-through and presence of exchange tiers).

I was more surprised to see Lava getting about 8% market share. I don’t have much experience with Lava, and it would depend a lot on the specific stocks in question, but Lava’s volume during this time would have been an order of magnitude lower than these other exchanges. That could mean orders resting on it did receive noticeably lower fill rates than expected. Hopefully, brokers directed orders to that exchange only when it showed significant activity on the relevant stock. In any case, if there was an issue with Lava, there isn’t one any longer; Lava has been [shut down](http://www.reuters.com/article/2014/12/02/us-citigroup-lavaflow-idUSKCN0JG1R520141202).

It’s also interesting that almost all of Schwab’s orders are directed to UBS. For the other brokers, UBS appears to be mainly a destination for marketable orders. But Schwab had a [contract](http://www.reuters.com/article/2013/04/02/us-retailbrokers-paymentfororderflow-ins-idUSBRE9310M120130402) with UBS during this period and appears to have sent UBS passive orders as well. Could some of these orders have found their way to Nasdaq, marked with UBS’s MPID? It seems like a definite possibility, given that we [saw](https://mechanicalmarkets.wordpress.com/wp-content/uploads/2015/02/toa-mpid-ubss-1366.png) that orders marked UBSS performed as expected for retail orders (poorly), were larger than most non-retail orders, and numbered about 10,000 executions per day (Schwab as a whole executes hundreds of thousands of trades per day). I wonder if UBS might have kept the rebates from these orders, which were probably worth about 10-15k/day.

# Marketable Orders and Conflict Of Interest

This brings us to the question of whether Schwab has extracted maximal value out of their customers’ orders. They were only getting about 0.10 cents per share from UBS during this period. Some brokers managed to get more than that from marketable orders alone – for instance, TD Ameritrade, which apparently received 0.18-0.19 cents/share from each of Citadel, G1, Two Sigma, and UBS itself. Adding some non-marketable orders into the mix like Schwab presumably has should only make that rebate higher, suggesting that maybe Schwab did not negotiate as hard as Ameritrade with UBS. Or, perhaps, that Schwab demanded better execution prices and faster fills than Ameritrade. If indeed Ameritrade’s higher received payments came at the expense of customers’ executions, it raises an interesting question about whether that expense can be argued as being baked in to their commissions, or if disgruntled customers could claim that Ameritrade is violating the spirit of [best execution requirements](http://www.sec.gov/answers/bestex.htm). Although it sounds similar to a broker pocketing the rebate on non-marketable orders, this would not be identical to what we discussed above; the executed prices of retail marketable orders are to some extent chosen by their counterparty. Executing clients at a worse price somehow feels different to me than getting them a slightly lower fill rate, but still at their chosen price. It seems to me that payment for marketable order flow may entail greater legal risk for brokers when they knowingly accept higher payments than their competitors (but I’m far from an expert on such things).

Brokers’ businesses can be complex though, as seen in the ([above-linked](http://www.reuters.com/article/2013/04/02/us-retailbrokers-paymentfororderflow-ins-idUSBRE9310M120130402)) article by John McCrank. Evidently, Fidelity’s retail orders may first interact with institutional flow (possibly Fidelity clients as well), reducing the economic value of any orders left over. I don’t know if and how any orders internalized by Fidelity itself would appear on their report. One potential sign in Fidelity’s 606 report is that a bit more than 1% of their flow is executed at a sister company, National Financial Services. It’s conceivable Schwab is doing something similar and the real reason they receive smaller payments is that they send UBS less attractive order flow. Or it’s conceivable that Ameritrade charges more for order flow and gets worse prices for their customers.

Remember, in contrast to resting orders, brokers are almost automatically guaranteed a commission for every marketable order sent to them. That means their incentives are not completely aligned with the interests of their clients.

[[1](#1)] One thing that struck me in particular was the very large [loss](http://www.sec.gov/Archives/edgar/data/1381197/000138119714000069/c197-20140930x10q.htm) that Interactive Brokers experienced in their market making division:

> During the quarter ended September 30, 2014, income before income taxes in our market making segment decreased to a loss of $111.8 million from income of $87.5 million in the year-ago quarter. This reflects a $198.9 million decrease in trading gains from the year-ago quarter. Removing the effects of currency translation, the market making segment produced $21.2 million pretax income in this quarter, compared to $41.3 million for the same period last year. Currency translation losses were $133.0 million this quarter, compared to a $46.2 million gain in the year-ago quarter. The decrease in market making profits, excluding translation effects, can be attributed to the ongoing competitive environment, lower volatility as measured by the CBOE Volatility Index, or VIX® and a trading error that resulted in a loss of approximately $16 million.

You might expect that kind of loss would prompt a review of risk management. If there was a review, I’m not sure how effective it was; just a few months later Interactive Brokers [possibly lost $120M](http://www.nasdaq.com/article/interactive-brokers-ceo-unlikely-to-recover-most-losses-20150120-01336) when the Swiss Franc peg was broken. I guess retail market makers can lose money just as easily as HFT market makers [can](http://www.reuters.com/article/2012/10/17/us-knightcapital-results-idUSBRE89G0HI20121017).

If you’re interested, there was slightly more detail given in their [earnings call](http://seekingalpha.com/article/2581145-interactive-brokers-groups-ibkr-q3-2014-results-earnings-call-transcript?part=single):

> Rich Repetto – Sandler O’Neill
> I guess the first question, Thomas, could you just give us a little bit more details on the $16 million trading loss, because that certainly weighed on the results for this quarter, the Market Making results.
> 
> Thomas Peterffy – Chairman and CEO
> Well, it was in an area of our software that is used from time-to-time and it’s kind of technical to really go into it in much detail. At this time the situation that it was applied to had a strange twist in it and the software misunderstood the situation and did their own thing.
> 
> Rich Repetto – Sandler O’Neill
> So, could something like this — is this like – it could ever happen again or do you think it’s prevented now?
> 
> Thomas Peterffy – Chairman and CEO
> Well, this same thing will not happen again. But software, from time-to-time, errors can always happen in a software, as you know. Apple comes out with a — or anybody comes out with a new chip, sooner or later you find the bug in the chip.

And in [Q4](http://seekingalpha.com/article/2834936-interactive-brokers-groups-ibkr-ceo-thomas-peterffy-on-q4-2014-results-earnings-call-transcript?part=single):

> [W]e took several steps to make our currency strategy more transparent which we believe will bring more clarity to understanding the results of our operating businesses. First, we transferred nearly all of the currency spot positions held as part of our global composition from the market making unit to the parent holding company IBG LLC.

[[2](#2)] 606 reports are split by ticker tape. To aggregate the tapes I weighted the results by the Q4 2014 overall market volume [statistics](http://www.batstrading.com/market_data/market_volume_history/market_history_monthly_2014.csv-dl?mkt=bzx), which have about 53% of volume on Tape A, 19% on Tape B, and 27% on Tape C. Retail participants may trade a different mix than the global market average (e.g. they may trade more on the ETF-heavy Tape B), but I doubt the difference would affect the overall results much.

Exchange rebates and payments for order flow are not always disclosed. And sometimes when they are, there is an accompanying note that the disclosed payments are an upper bound. I assumed that the upper bounds were representative of the actual payments.

To evaluate the marketability of the orders a broker sends to a given destination, I used a very simple ratio: MarketabilityIndex = PercentOfLimitOrdersSentToDestination / ( PercentOfLimitOrdersSentToDestination + PercentOfMarketOrdersSentToDestination ). There are other possible measures, but I thought this was best given the data quality (sometimes proportions don’t even sum to near 100%). A destination was marked as accepting mainly marketable orders if this ratio, after weighting, was less than 0.4\. Destinations were marked as mainly non-marketable if this ratio was greater than 0.7\. The only destinations that didn’t fall into these two categories had less than 1% market share combined; these were: FBCO, Citi (which may be a blend of destinations, including Lava), and “Other.”

For statistics on overall market share, I approximated each broker’s overall market share as being proportional to their net capital, which is the only number that was available and reliable for every broker. Net capital may somewhat measure the risk of the trading that goes through a broker, which may be representative of the overall level of activity for their customers. TD Ameritrade and Fidelity have similar levels of both net capital and daily volume, even though net capital is usually posted well in excess of the regulatory minimum. Interactive Brokers has less AUM but a greater level of net capital than these two, which makes sense given its reputation for highly active clients.

[[3](#3)]

| Broker | Order Destination | Share of Broker (%) | Marketability Index (Between 0 and 1, lower numbers more marketable) | Avg Payment ($/shr) | Broker Portion of Net Cap (%) |
| Etrade | G1 Execution Services | 50.3 | 0.30 | 0.0010 | 8.9 |
| Etrade | DirectEdge | 20.8 | 1.00 | 0.0031 | 8.9 |
| Etrade | Citadel | 9.2 | 0.16 | 0.0010 | 8.9 |
| Etrade | Lava | 8.4 | 1.00 | 0.0027 | 8.9 |
| Etrade | KCG | 5.5 | 0.14 | 0.0010 | 8.9 |
| Etrade | Nasdaq | 3.2 | 1.00 | 0.0028 | 8.9 |
| Fidelity | KCG | 33.1 | 0.38 | NA | 22.8 |
| Fidelity | Citadel | 28.8 | 0.34 | 0.0002 | 22.8 |
| Fidelity | DirectEdge | 16.9 | 1.00 | 0.0031 | 22.8 |
| Fidelity | Goldman Sachs | 7.4 | 0.30 | NA | 22.8 |
| Fidelity | UBS | 3.5 | 0.38 | NA | 22.8 |
| Fidelity | National Financial Services | 1.4 | 0.26 | NA | 22.8 |
| Fidelity | Bats | 0.5 | 1.00 | 0.0020 | 22.8 |
| InteractiveBrokers | Nyse | 35.5 | 0.75 | NA | 35.5 |
| InteractiveBrokers | Nasdaq | 23.8 | 0.61 | NA | 35.5 |
| InteractiveBrokers | Arca | 17.2 | 0.77 | NA | 35.5 |
| InteractiveBrokers | IB ATS | 5.5 | 0.12 | NA | 35.5 |
| InteractiveBrokers | Lava | 4.4 | 0.92 | NA | 35.5 |
| InteractiveBrokers | Nyse Mkt | 1.5 | 0.88 | NA | 35.5 |
| InteractiveBrokers | BatsY | 1.2 | 0.14 | NA | 35.5 |
| InteractiveBrokers | DirectEdge | 1.0 | 0.73 | NA | 35.5 |
| InteractiveBrokers | UBS | 0.9 | 0.16 | NA | 35.5 |
| OMSL | KCG | 42.7 | 0.40 | NA | 0.0 |
| OMSL | Lava | 32.8 | 1.00 | NA | 0.0 |
| OMSL | Citadel | 21.4 | 0.34 | NA | 0.0 |
| Schwab | UBS | 94.2 | 0.49 | 0.0010 | 12.8 |
| Schwab | Citadel | 2.9 | 0.68 | 0.0009 | 12.8 |
| Schwab | KCG | 1.3 | 0.58 | 0.0012 | 12.8 |
| Schwab | Citi | 1.1 | 0.58 | 0.0010 | 12.8 |
| Schwab | Goldman Sachs | 0.4 | 0.46 | 0.0010 | 12.8 |
| Scottrade | KCG | 26.3 | 0.18 | 0.0010 | 3.1 |
| Scottrade | Citadel | 20.7 | 0.16 | 0.0010 | 3.1 |
| Scottrade | Nasdaq | 14.9 | 1.00 | 0.0031 | 3.1 |
| Scottrade | DirectEdge | 14.2 | 1.00 | 0.0029 | 3.1 |
| Scottrade | Citi | 10.0 | 0.15 | 0.0010 | 3.1 |
| Scottrade | G1 Execution Services | 5.3 | 0.16 | 0.0010 | 3.1 |
| Scottrade | Two Sigma | 3.3 | 0.15 | 0.0010 | 3.1 |
| TDAmeritrade | DirectEdge | 34.9 | 1.00 | 0.0034 | 16.4 |
| TDAmeritrade | Citadel | 17.1 | 0.24 | 0.0018 | 16.4 |
| TDAmeritrade | G1 Execution Services | 15.5 | 0.22 | 0.0018 | 16.4 |
| TDAmeritrade | Two Sigma | 10.5 | 0.23 | 0.0019 | 16.4 |
| TDAmeritrade | Lava | 8.5 | 1.00 | 0.0033 | 16.4 |
| TDAmeritrade | UBS | 7.5 | 0.21 | 0.0018 | 16.4 |
| TradeStation | DirectEdge | 26.8 | 1.00 | NA | 0.5 |
| TradeStation | NITE | 23.0 | 0.34 | NA | 0.5 |
| TradeStation | BatsY | 19.4 | 0.17 | NA | 0.5 |
| TradeStation | FBCO | 14.5 | 0.50 | NA | 0.5 |
| TradeStation | EDGA | 9.7 | 0.74 | NA | 0.5 |
| TradeStation | AUTO | 6.2 | 0.27 | NA | 0.5 |
| TradeStation | Citadel | 2.6 | 0.43 | NA | 0.5 |
| TradeStation | AMEX | 2.3 | 0.00 | NA | 0.5 |
| TradeStation | Other | 2.2 | 0.49 | NA | 0.5 |
| TradeStation | KCG | 0.7 | 0.63 | NA | 0.5 |