<!--yml
category: 未分类
date: 2024-05-12 19:56:40
-->

# Falkenblog: Perp Funding Rate Fraud

> 来源：[http://falkenblog.blogspot.com/2022/11/perp-funding-rate-fraud.html#0001-01-01](http://falkenblog.blogspot.com/2022/11/perp-funding-rate-fraud.html#0001-01-01)

 Supposedly, perp funding rates enable a futures/swap market to equilibrate at a spot price without delivery, so the market is a perpetual swap, hereafter denoted as a 'perp.' This mechanism is superficially like the basis in futures markets but ultimately profoundly different in theory and practice. The fact people are satisfied with this flawed but plausible feedback control system story implies some necessary detail is involved to see why it does not work. The basic disconnect is that the best predictor of the funding rate is not the current perp/spot price ratio but a moving average of the funding rate. Yet, if that is so, why is the perp/spot ratio purportedly defining the funding rate that is equilibrating the market?

As a practical matter, the perp premium does not equilibrate supply and demand on perp markets; the spot price is sufficient for that job. The primary reason perp markets track spot markets can be explained as a [Schelling point](https://en.wikipedia.org/wiki/Focal_point_(game_theory)) or [correlated equilibrium](http://www.millenniumpost.in/sundaypost/beacon/the-ace-game-theorists-453467). The perp premium does not determine the funding rate but is determined by a funding rate decision made by insider market makers specific to each exchange. The exchange controls these insiders to various degrees in general. As tens of billions of dollars are currently outstanding on Defi perp exchanges and multiples more on centralized exchanges, the economic significance of this charade is immense, even if your typical perp trader seems blissfully indifferent.

Seven years ago, it was impossible to short or leverage a long position in bitcoin. All one could do was swap one token for another and generate an unleveraged long position. There were no stablecoins or wrapped Bitcoin, so the quest was to find a way to trade the Bitcoin without USD. In 2016 the centralized exchange BitMex created the first popular perp, enabling leveraged positions while only transacting in Bitcoin.

Instead of expiration dates and settlement, a perp anchors its price to the spot via a funding rate mechanism. When the perpetual contract's price exceeds the spot price, the standard story is that this implies more long than short demand. To equilibrate the market, the long traders pay short traders a fee proportional to this price premium. Crypto funding rates prevent continuing divergence in the price of both markets. The funding rate at BitMex is applied every 8 hours to every position that is active at that time. The 8-hour window is now a convention for quoting, though today's funding rate applications are sometimes hourly or continuously.

The perp premium is defined as the percent difference of the perp price from a spot price. The spot price could be from external markets like Coinbase, or for centralized perps, from spot markets on their own exchange:

Perp premium = perpPrice/spotPrice - 1

The funding rate is like the future expiring once per day. For example, if you sell a BTC perpetual future that is trading 0.03% above the underlying index all day—it's perp premium—then over that day or the next day, you will receive a total funding payment of 0.03%. If bitcoin's current market price across a range of exchanges is $20,000, the funding rate mechanism will help make sure the perpetual swap contract price is also priced around the same $20,000 level over time.

At 30k feet, this all seems reasonable. I have not seen anyone dispute its logic. Even [Campbell Harvey](https://www.youtube.com/watch?v=BZSARSWrnaA), a prominent finance professor well-acquainted with traditional futures data and theory, accepts this logic. Perps vaulted BitMex into prominence and inspired new exchanges to offer perps. This was often necessary because of the many limitations back then (no stablecoins or wrapped coins from other blockchains). Over time, traders have become comfortable with the product and trust that its perp-premium/funding-rate mechanism works.

A hundred years ago, bucket shops were a common way for people to trade stocks listed on major exchanges. A shop would take bets and give leverage up to 100 to 1, trading on stocks, grain, oil, etc. There was no transfer or delivery of the stock or commodities nominally traded, so customers were essentially betting against the bucket shop operator. Often the ticker prices were not real, but even when real, the more capitalized bucket shop manager could manipulate prices to exhaust client margins. While some were deluded into thinking they were trading against 'real' security prices, others knew it was not necessarily related to exchange-traded prices but figured it was close enough. These were effectively banned by 1922 after a 50-year run, highlighting how long bad business practices can persist even if patently unsustainable.

Current perp crypto perp markets share much in common with bucket shops: manipulation, lack of true settlement, 100-1 leverage, indifferent gamblers happy to trade. Unfortunately, the high-handed approach of regulators gives willing and able crypto investors few and unattractive alternatives. You can short on the CME, but the minimum notional is $100k (5 bitcoin), and the margin for a short position has been 150%. The onboarding costs for trading futures are high in terms of time, moving money from an equity brokerage to one that handles futures, and the many questions about where you got your money. If there were simply an ETF for crypto, millions of investors would be able to go long in a much safer way and avoid unsavory perp markets, and an ETF would give people the ability to short. This has kept most crypto investors in the unregulated exchanges, whether via exchanges one can access through the blockchain (e.g., [dydx](https://dydx.exchange/)), or more explicitly centralized exchanges overseas via a VPN and a fake identity. The zero-tolerance approach of regulators has significantly hurt retail crypto investors by severely limiting regulated opportunities for crypto investors.

I do not expect regulators to embrace crypto. It will be forced upon them in how government bureaucrats discovered that banning encryption was technically futile or how UBER exposed the inefficient taxi monopolies and made it politically unpopular to return to the old system. However, the key to accelerating the future in crypto dapps such as perps is to expose bad practices so that consumers can make informed decisions. Competition is the best regulator in history and involves active constructive criticism as opposed to the status quo of naïve criticisms by ignorant bureaucrats worried about their monopoly power versus the credulous reporting by crypto media funded by the latest incarnation of Bitconnect.

**Theory of a Funding Rate**

To understand the problem, you must first understand how funding rates work in futures/swap markets. The basis in futures markets acts as a funding rate in swap markets, defined as the difference between the futures and spot price. Figure 1 shows the horizontal time axis moving from a current futures price to its delivery/expiry date if the black line represents the current spot price.

**Figure 1**

The' basis' is the difference between the futures and spot price. It can be positive or negative. The amortization of this basis can be considered a daily funding rate; in *contango,* the longs pay the shorts, while in *backwardation*, the shorts pay the longs. The funding rate is implicit in the amortization of the basis over time, in that, at expiration, the spot price equals the futures price, so the basis is certain to be zero at that time.

There is no basis for swap markets; instead, a funding rate is applied daily, acting precisely the same way as the basis in futures markets. They are settled daily using a funding rate known in advance. Here the basis goes from being implicit to explicit.

LongSwapPnL(t+1) = Notional(t)*[p(t+1) / p(t) - 1 - fundingRate]

Unfortunately, the literature on basis rates and funding rates is not uniform when defining the basis or funding rate. You can see the basis = 'futures – spot' in one book and 'spot – futures' in another. I will stick to the crypto convention in defining the funding rate as follows:

Positive funding rate: longs pay shorts (contango).

Negative funding rate: shorts pay longs (backwardation).

Arbitrage ensures various costs and benefits of possessing the asset are reflected in the futures' basis or swap funding rate. They all are based on the following reasoning.

Assume you have $1 and want to compare two investments. First, buying a Treasury bill. This generates a simple interest rate return

$1*(1+R(us))

Secondly, you have asset A. Many things affect its net return, but this can be represented by *Ret(A)*. To get this return, you must first translate from USD into asset A; with $1, you get 1/Prc(A) units of A. You will turn this back into F(A) dollars at the end of a certain period. A futures market allows you to set that futures price today at f(t+1)

$1/spotPrice(t) * (1 + R(A)) * futuresPrice(t+1)

Here we define the futures (F) and spot (S) prices in terms of USD/A. We expect equality of these two equations, as otherwise, it would not be an equilibrium. With some rearranging, we get

F(t+1) / S(t) = {1 + R(us)} / {1 + R(A)}

If we put this in terms of the perp premium, it would be

F(t+1) / S(t) - 1 = {R(us) - R(A)} / {1 + R(A)}

The perp premium is driven by the net returns of USD relative to asset A. These factors are defined as follows:

*   Interest rates

Going long $100 in a spot position has the opportunity cost of forgoing the return of a riskless asset like Treasury Bills. Without this adjustment, one could go long an asset using a swap and make the riskless rate on the cash needed to buy spot. Gold has none of the other attributes listed below, so its futures price is determined solely by US interest rates, always in contango (futures price > spot price). For currencies, however, there are interest rates on both, so the net interest rate is positive only half the time. It is not obvious whether a stablecoin should be assumed to carry the US Treasury rate, as one cannot directly purchase a US Treasury with a stablecoin but instead must first go into fiat. Whatever the case, US interest rates have been near zero for the past decade, so this effect is second order in explaining perp funding rates (at most 2% annualized).

Standard storage costs are like interest rates, subtracted from *R(A)*. They include insurance and warehouse costs, as with oil, as well as deterioration as with agriculture products. A long spot position pays for them, so the long swap position must pay as well, in the form of the long futures price declining over time, a positive funding rate. These are irrelevant to crypto.

For a stock that pays dividends, its price in the future will be adjusted to account for this dividend. For example, if a $100 stock has a $10 dividend before an imminent futures expiry, it will be expected to be worth $90 at expiration, so the dividend is subtracted from the current price to generate the forward price. These are irrelevant for crypto, which has no dividends.

*   Option value (aka convenience yield, theory of storage)

Inventory for commodities has a floor of zero and a maximum as well. For assets like wheat or oil that have a continuous positive consumption stream, the inventory floor causes price spikes as desperate users bid up prices. This option value in shortages causes the spot price to be above the futures price, which is why backwardation is the general rule for oil prices. However, sometimes the oil tanks become filled, as in the depths of the global recession in April 2009 or during the covid shut-down in April 2020 when the front-month oil futures price went negative. This is irrelevant to crypto.

*   Risk premium aka hedging pressure

If hedgers are net short or long, they must pay speculators to take the other side to transfer their risk. Keynes famously asserted this was the general case, which he called 'normal backwardization.' His example was when farmers sell their anticipated wheat output in the futures market, paying a premium via the appreciation to the long futures price as it approaches maturity. There are also cases where hedgers are naturally short, such as when airplane manufacturers lock in the cost of their aluminum inputs by buying futures, the shorts are paid via the futures price declining to the spot price (contango). The natural long story fits best for crypto because miners generate a stream of crypto and may wish to hedge that by locking in prices now. This would imply a negative funding rate. I cannot think of a natural short story, a group that must buy crypto regularly.

This theory is the standard argument for explaining why crypto funding rates are positive (see Binance [here](https://www.binance.com/en/blog/futures/a-beginners-guide-to-funding-rates-421499824684900382)). It is not in the traditional literature explaining funding rates. A shock in the demand for an asset should be reflected in the current price, not the future price; it is wrong to say there are ever ‘more longs than shorts’ for any market. [Samuelson (1965)](https://investmenttheory.org/uploads/3/4/8/2/34825752/paulsamuelson-proof.pdf) proved that if you know demand will be higher tomorrow, that gets reflected in the price today, not in future or expected spot prices. This reasoning is the basis for the random walk assumption, which is an excellent general first-order approximation to any asset price time series despite its criticisms. Nonetheless, one must admit the special case for crypto: there are unprecedented regulatory restrictions on owning or leveraging crypto. Thus, it is possible that in bull markets like late 2017 and early 2021, the extra demand constrained by regulators pushed up the leveraged perp price, and longs were willing to pay a funding rate for access they could not get anywhere else.

Financing rates are generally positive in crypto, indicating contango. Storage costs, dividends and option value are irrelevant for crypto. The risk premium would only imply a negative funding rate, as the only demographic with a natural position to hedge are those long, such as miners or dapps that need crypto to function. US interest rates are a couple of percentage points, but it is not obvious that stablecoins should be assumed to have this interest rate, in that you cannot directly buy a US Treasury with a stablecoin. That leaves the sentiment theory, which is a stretch, but potentially plausible.

#### **Data on Funding Rates**

On average, perp funding rates have been positive: longs pay shorts. Most perp exchanges set their default funding rate at 0.01% per 8-hour period, which annualized out to 10.95%. Figure 2 below compares the bitcoin per rates on BitMex and Binance with the futures-implied funding rate on the CME. On average, the funding rate on Binance has been 10% higher than that BitMex or the CME. I used the second to front month premium times 12 to get the CME’s annualized funding rate, and this might be a bad number because the second month is so illiquid there may be a bias due to infrequent trading.

**Figure 2**

Average Annualized BTC Funding Rates

9/2019-6/2022

The higher funding rate on Binance reflects the more general funding rate and is driven by episodes where the funding rate spikes to 50% to 100% (annualized) over certain months. There is a clear correlation between funding rate spikes and bull markets, which is why most commenters consider the perp funding rate an indicator of market sentiment. Over time we can see that Binance, like many perp exchanges, charges insanely high funding rates during big bull markets and rarely offers the symmetric negative funding rate (BitMex is exceptional in this aspect).

**Figure 3**

While the perp funding rates are highly correlated across exchanges, the divergences can be substantial. These markets are clearly affected by limits to arbitrage via various regulatory restrictions, which highlights the potential plausibility of the sentiment theory.

**Figure 4**

#### Contemporaneous vs. Lagged Return Effects

Regressing the daily Binance funding rate against that day's return and the prior month's ETH or BTC return shows that both returns positively correlate with funding rate: higher returns imply higher funding rates. Yet the preceding month's price return has a significantly stronger effect than the contemporaneous daily return in explaining the daily ETH and BTC funding rates.

**Figure 5**

Regression Analysis of Daily Funding Rates

Binance, 8/2019-6/2022

###### The dependent variable is the daily funding rate for ETH and BTC. Data are generated every 8 hours, so daily funding rates are the sum of these three observations. Returns were calculated using minute downsampled data from Gemini. The daily return and the prior month's return do not overlap. ETH funding rates used ETH returns, and BTC funding rates used BTC returns.

In traditional financial markets, the primary stylized fact about past price changes and the basis is that price increases are associated with negative financing rates and price declines with positive financing rates. The general explanation is that a price spike is due to an inventory problem—a drought—so continuous consumption demand requires an abnormally high price today that is not expected to continue. A significant price decline, say from a lack of oil storage, is also likely to be temporary so that futures prices will be above the spot price.

It is easy to conflate 'past price jump' with 'current price jump' and think the sentiment funding rate correlation makes sense for a rational market. The fact that the past return is much stronger than the current return is contrary to that argument. The positive correlation between crypto funding rates and prior returns is an anomaly.

#### Perp Premiums are Not Emergent Indicators of Bullishness

The 'gaming insider market maker' theory is clear if we look at BitMex's ETH perp. This perp has the strange property of incorporating the ETH-BTC covariance, in that BitMex denominates the payoff in BTC, though the contract is priced in USD. This post explains more fully [here](https://efalken.substack.com/p/bitmexs-ethusd-funding-rate-anomaly), but the gist is that the return for the ETH perp is

ret(ETH) * (1 + ret(BTC)) = ret(ETH) + ret(ETH) * ret(BTC)

The term E[ret(ETH)×ret(BTC)] is also known as the covariance of ETH and BTC. Thus the return on the BitMex perp is the return on the eth plus its covariance. Few people mention this, highlighting that, like in the old bucket shop days, most customers are so eager to gamble that they do not care. When I google "[BitMEX eth funding rate too high](https://www.google.com/search?q=BitMEX+eth+funding+rate+too+high&rlz=1C1RXQR_enUS934US934&oq=BitMEX+eth+funding+rate+too+high&aqs=chrome..69i57j69i59.537j0j4&sourceid=chrome&ie=UTF-8)" as per explanations, I get my blog post circa 2019; the other articles just note the rate levels. Customers are blissfully indifferent.

Nonetheless, obviously, some BitMex insiders have figured this out. Looking at the ETHUSD return data from 8/2018 through 6/2022, you see the covariance term accounted almost perfectly. The total return data on their ETH contract without funding was 149%, while the annualized ETH return over that period was 83%. The difference, 66%, matches the covariance and the funding rate (63%).

**Figure 6**

**Annualized Data from BitMex ETHUSD perp daily funding and return data**

**2018-2022**

This all makes rational sense. BitMex has [stated](https://archive.ph/ONG7E) that its market-making desk's goal is to break even. Given the boatloads of money they are making off fees and the strong desire by regulators to punish them, it’s a wise tactic. The data on the ETH perp suggests that their ETHUSD funding rate is genuinely neutral, in that after accounting for the covariance, it is zero. Good on them!

The fun part is that few see the direct relationship between the funding rate and the covariance. As the correlation between bitcoin and Ether is positive, it implies convexity in the long position. Like convexity everywhere, this is something you can hedge to minimize risk, but it is an unavoidable cost to the side short convexity. Arthur Hayes wrote a [blog post](https://blog.bitmex.com/is-the-ethusd-swap-fairly-priced/) about whether the ETHUSD perp was fairly priced and did not mention this explicit formula.

**Figure 7**

Bloomberg Eurodollar/Swap Page

In traditional markets, convexity adjustments are explicit once known. For example, figure 7 above shows a Bloomberg page showing the detailed [convexity adjustment](https://www.cmegroup.com/education/courses/introduction-to-eurodollars/understanding-convexity-bias.html) needed when comparing Eurodollar futures with a Eurodollar swap. Before this relationship was understood, several large investment banks made actual arbitrage profits going long the futures and short the swaps. Around 1995, however, many prominent academic articles highlighted the arbitrage and noted the precise convexity adjustment needed. Eurodollar futures and swap traders have this convexity adjustment built into pricing models used to compare the two markets, and arbitrage equilibrates prices based on this adjustment. Traders do not implicitly adjust for convexity; they apply it precisely via models like those above.

Like many CEOs, Hayes seems unaware of various technical tactics his company uses to achieve his objectives (a flat market-making pnl). The ETHUSD market makers are using explicit adjustments, but as there is little demand for this information, it’s better to not mention it because having a better model than most gives one a useful option.

#### **Perp Theory**

The two academic articles are generally referenced when presenting perps. The first is by [Gehr (1988)](https://www.gwern.net/docs/economics/1988-gehr.pdf), which describes how gold was traded on the Chinese Gold and Silver Exchange Society of Hong Kong (CGSE). One should remember this was back when trading was not possible around the clock, and there was no internet, so a closing price had little volatility outside trading hours. The CGSE was unique in that its futures market was undated, perpetual (it’s [still around](https://industrialhistoryhk.org/the-chinese-gold-silver-exchange-society-hong-kong-established-1910-new/), and I’m not sure about its protocol today). The market effectively settled daily and then held a 30-minute auction process to determine the funding rate. Those long gold compare the cost of paying storage and interest on a long position vs. the funding rate; those short gold futures take delivery if they feel the funding rate is too low. This funding rate was added to the spot price to create a basis for the subsequent day's pnl.

The effect on prices and cash flows in the CGSE futures market was as follows. If the market price closed at 100.00, and the funding rate was determined to be 0.01% over the next day, the basis for the next day's PNL is 100.01\. If the price stayed constant at 100.00, each day, the longs would lose 0.01 because the daily pnl would be 100.00 – 100.01 on a long position, where 100.00 is the spot close, and 100.01 is the prior day's futures close. The traded price would never be 100.01; it would just be used in the daily calculation of trader margin adjustment, transferring from longs to shorts.

Nobel laureate Robert [Shiller (1993)](https://www.nber.org/system/files/working_papers/t0131/t0131.pdf) proposed a perpetual futures contract for things like single-family homes. Unlike a stock index or a commodity, the underlying asset is difficult to create into a futures commodity because it is difficult to define a housing unit. A hundred houses? 100k square feet of houses? Quality varies considerably, creating a [lemons problem](https://en.wikipedia.org/wiki/The_Market_for_Lemons). Shiller proposed a rental index to create a rental return proxy for a housing price index. One would apply statistical methods to estimate real estate's average rental return, net of depreciation. This rental return would then be paid by the short to the long.

s(t+1) = f(t+1) - f(t) + d(t+1) – r×f(t)

Here *s* is the daily margin change in a trader's account;  *f* is the perpetual futures price, *r* is a precise fiat interest rate adjustment, and *d* is determined outside the market. While this is interesting, the difficulty in generating a robust rental index for *d* is probably why this has never been implemented. Rental income, like profits in the economy, is non-trivial to estimate via macroeconomic indicators, and people do not like to trade assets built on models with low R2s. Nonetheless, the market was supposed to merely trade at a spot price that did not contain the daily funding charge, *d*.

The perp premium is *like* the CGSE funding rate charge added to the market's spot price after trading. A direct funding rate is a periodic payment like the *d(t+1)* term in Shiller's model. However, the Shiller and Gehr perp models are substitutes, not complements; the funding rate is either added to the spot price periodically or is regularly charged. Further, Gehr's brief, never-traded perp premium is *determined by* an explicit funding rate auction, not vice versa. Thus, at 30k feet, the connection between the perp premium and the funding rate seems consistent with Gehr's model, but it is entirely backward; the perp funding rate mechanism seems consistent with Shiller's model via the explicit funding rate charge, but it is determined entirely differently (exogenous to the market).

#### **Plank scale of asset prices**

In crypto perps, the modal daily funding rate and perp premium is 0.03%, which annualizes to a hefty 11%. Considering interest rates have been near zero over the past several years, that is a significant funding rate. Yet 0.03% is below the precision of any estimate of 'true value,' or a transaction cost. The average transaction costs for the most liquid US equities, which are more efficient than any crypto market, are estimated at least 0.1% (see [here](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3229719)). It is unlikely crypto prices have lower transaction costs, especially given explicit fees start at around 0.1%. Gemini trade data show a 0.15% standard deviation in the price from one trade to the next. A one-way trading fee of 0.2% means the price must deviate by at least 0.2% from its ‘true’ price before an arb would transact, giving the perp market price a 0.2% zone of indeterminably. Yet, with all this uncertainty, we expect the market to determine the funding rate with precision orders of magnitude more precise than these limits.

#### **Locking in funding rates**

The crypto perp is like a standard deliverable futures basis in that the price always reflects both the basis and the spot price. However, as the perp premium is applied continuously, its magnitude is irrelevant to any trading decision. Consider the perp trader who sees the perp price at a 0.0685% premium to the spot, implying a rich 25% funding rate for the short. The problem is not only that such a premium is below the asset price Plank length, but also that the perp premium at the time of her trade does not determine the funding rate she will receive. Instead, this premium is the average over the time she holds her position. Given the next tick will move the perp price by 0.1%, a 0.06% current perp premium has little forward-looking value. Perp premiums implying insanely large funding rates are insufficient for motivating initiating a position because the information content of a current perp premium is so low (especially compared to a simple moving average of past funding rates). 

Arbitrage is much simpler in deliverable futures markets. A futures trader locks in a cumulative funding rate at the time of a trade. The funding rate implied from the basis of a future is a cumulative rate over many days, generating a target return above transaction costs. Monthly or quarterly delivery implying a 11% annualized funding rate will show up as a hefty 1% or 3% premium to the spot price, not a 0.03% premium. Given identical daily funding rates, true arbitrage, profits without uncertainty, is possible in futures markets, but not perp markets.

#### **TradFi swap funding rates**

Many hedge funds use swap accounts for their international equity positions. There are several regulatory reasons for this, but the net result is that an investment bank acts as the custodian for the equities bought or sold short, holds the hedge fund's equities, charges a funding rate, and applies margin treatment on a portfolio basis. Notably, the hedge fund directs their trades like they would manage transactions they hold on their books. The funding rate is determined independently of the trade.

In the US, shorting stocks requires one first gets a locate, in that naked shorting is no longer allowed. For a stock with a lot of short demand, the short seller is presented with the number of shares they can short *and* the idiosyncratic short rebate. Once this is known, the trader then sells this short in the market just like any other short trade. Like the CGSE, the traded spot price and funding rate are determined in separate markets, not simultaneously as with futures.

#### **Trust them**

Regulated markets are subject to presenting an audited tape of their market trades and orders. For example, [MIDAS](https://www.sec.gov/marketstructure/midas-system) collects about 1 billion records daily from all national equity exchanges time-stamped to the microsecond. They are looking for front-running or not giving clients the best trade given the consolidated set of bids and offers at a particular time. Crypto exchanges are not subject to such auditing, giving them considerable discretion at magnitudes that matter.

Perp exchanges post funding rates at various frequencies based on a weighted average of the perp premium. The spot prices they use to benchmark against parochial indexes they construct themselves must be seen in real-time, not the downsampled historical data, so their ‘index’ price cannot be known with great precision. A perp price can be calculated in various ways, such as using the previous ending price or the 'impact price,' which looks at the limit order book at the time of the trade to see the average mid-price to bids and asks that sum to $10k in notional value. Linking the perp and spot price (aka the ‘mark’ price and the ‘index’ price) to get a premium will depend on several unmentioned rules. Given each trade tick bounces around by 0.15%, any perp premium they generate given these degrees of freedom will have a standard error of at least 0.05%, giving them the freedom to post any funding rate within a 36% band (0.05% —> 18% annualized, -0.05% —> -18% annualized).

#### **Insiders**

Market makers dominate the price setting in all exchanges. They can decide to target 0.03% or 0.13% above the current spot index. As market makers, this will dictate a general pattern that will generate the desired funding rate when aggregated using the various discretionary parameters mentioned above. These professionals either post bid-ask spreads in centralized limit order books (CLOBs) or act as arbitrageurs for Automated Market Makers.

Often they are working explicitly for the exchange, as with BitMex's fair ETHUSD market makers, or doing so in a less explicit partnership. Exchanges need liquidity, and often they get this by giving certain groups privileged access to their order book or high-speed access unavailable to retail traders. In general, we should expect crypto perp market makers to be net flat but short perps because it is much easier to be long outside your perp market than to be short. For example, if Binance's market markets were net long perps, they would have to trust another exchange like FTX for their short positions, and regulators would then have a choke point along the route such a position is maintained. In contrast, if Binance market makers were short perps, they could just own crypto on the blockchain and be hedged. The net result would be that in addition to standard market maker profitability from the spread and fees, they get an additional 10% funding rate from their natural short perp position within their riskless crypto position. It’s ridiculous that customers accept this as the status quo default funding rate.

A [conspicuous example](https://insights.deribit.com/market-research/the-quest-for-perp-amms/) of this was provided by perp.fi’s ‘virtual’ AMM, where insiders provided liquidity for traders (shut down this spring). As the price of ETH went up, the traders were net long via the logic of the constant product AMM. Yet the funding rate was negative, meaning the longs were getting paid the funding rate. This was contrary to every other perp exchange in 2021\. It happened because the longs, unaffiliated with the perp.fi insiders, decided to be the market makers on the perp.fi’s exchange, and perp.fi had to ability or plan to stop them. Clearly, the market makers set the perp premium and thus, the funding rate. That is what market makers do. The perp/spot price ratio does not reflect ‘long demand,’ but the market makers funding preference.

#### **Conclusion**

This bizarre situation arose from a need to provide people with a way to trade crypto with leverage, long and short. The perp premium model cannot work and does not work the way it is advertised, and more importantly, it cannot work. It encourages sloppy thinking that pervades DeFi and gives rise to unsustainable business models built on Ponzi economics. For example, [one website](https://phemex.com/user-guides/funding-rate) explains why the perp prices are higher than the spot price as follows: "logically, this means that there are more traders with long positions." No one should put money into dapps run by people with such logic because it invariably extends to their tokenomics.

The theory that explains the positive return/funding-rate correlation is a typical non-equilibrium story that sounds good but makes no sense. Like the explanation that there are "more buyers than sellers," the idea that long demand shows up in futures price premiums sounds plausible but is logically incoherent. Standard arbitrage, and the law of iterated expectations, imply current sentiment is reflected in spot prices, not forward rates. This is why funding rates are generally independent of asset prices and why a big demand for auto purchases does not materially affect the auto financing rate. Further, the return over the prior month, not the contemporaneous return, best predicts funding rates.

Past returns correlate with the basis during supply shocks where inventories are near zero or maxed out. Yet, outside of crypto, we see high prices correspond to negative funding rates and low prices to positive funding rates. This is the exact opposite of what we see in crypto.

The perp funding mechanism is supposedly an emergent market process, undirected, but hides the fact that perp exchanges control market makers who then manipulate funding rates when feasible. When prices are mooning, customers do not mind 100% annualized funding rates, which amounts to a mere 0.1% daily charge. It's like how big winners in Vegas often give the dealer a big tip: people do not respect [house money.](https://www8.gsb.columbia.edu/sites/decisionsciences/files/files/thaler_and_johnson.pdf) The extra 50%+ increase in funding rates on perps relative to the CME back in February 2021 reflects insiders taking what they can.

Perp customers and crypto enthusiasts like believing that crypto projects are decentralized like a market economy: efficient, emergent, and uncensorable. The more plausible story is that perp market makers are generally short and charge a hefty 11% funding rate, which all goes into the market maker's pnl. Given the regulatory issues, it is easy for insiders at BitMex or FTX to target a net flat position by having a net short position on the perp contract and a long position on the blockchain. If they were net long on their perp contract, they would have to be short somewhere else, which would be problematic.

The solution is to get rid of perps and return to futures with a settlement. When BitMex first proposed perps, there were no stablecoins or wrapped BTC, etc., but now there are. With a settlement, you do not need an explicit funding rate, as the basis serves nicely for accommodating storage costs and fiat interest rates.