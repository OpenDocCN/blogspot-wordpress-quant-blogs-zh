<!--yml
category: 未分类
date: 2024-05-18 06:42:41
-->

# Could HFTs Benefit from a Cancellation Tax? | Mechanical Markets

> 来源：[https://mechanicalmarkets.wordpress.com/2015/10/14/could-hfts-benefit-from-a-cancellation-tax/#0001-01-01](https://mechanicalmarkets.wordpress.com/2015/10/14/could-hfts-benefit-from-a-cancellation-tax/#0001-01-01)

You’ve probably seen Hillary Clinton’s [proposal](https://www.hillaryclinton.com/p/briefing/factsheets/2015/10/08/wall-street-work-for-main-street/) for a tax that “would hit HFT strategies involving excessive levels of order cancellations.” I don’t want to discuss politics, but the proposal brings up an interesting thought-experiment: What would markets be like if HFTs couldn’t cancel orders?

Let’s say that there’s an extremely high order cancellation tax that’s designed such that it won’t affect fundamental traders: [[1](#bottom1cancels)]

1.  There’s no tax for traders that cancel fewer than ~10 orders per day, providing they hold positions from those orders for over a week. Otherwise, the tax makes cancelling unfeasible for everybody.
2.  Cancel-replace messages are taxed the same way. So are hidden order cancellations and orders cancelled/modified via exchange algorithm (e.g. peg orders).
3.  IOC (Immediate-Or-Cancel) orders are not taxed. Orders cancelled automatically at the end of the day are not taxed.
4.  There are no ELPs (Electronic Liquidity Providers), wholesalers, internalizers, etc.
5.  There are no loopholes or exemptions.

I really doubt this scheme is what Clinton has in mind, and market dynamics are extremely unpredictable, so the below is purely for fun.

Many HFTs might think this tax would put them out of business. I’m [not so sure](https://www.youtube.com/watch?v=SJUhlRoBL8M). I think it would transform markets, with the resulting market structure having the same opportunity and need for algorithmic traders.

The tax would clear out almost all automated resting liquidity. A few medium-frequency algorithms might thriftily use their 10 order allotment. But most orders resting in the book would belong to fundamental and retail traders. [[2](#bottom2cancels)]

Now, without market makers, would the market become a utopia where long-term traders seamlessly match with each other? In some sense, that’s the dark pool dream. [[3](#bottom3cancels)] In that dream, large fundamental traders use minimum quantity orders to hide their intentions and wait for peers to trade with them. But, block trading’s current volume suggests that it usually doesn’t offer liquidity as cheaply as intermediaries do. [[4](#bottom4cancels)]

I’m inclined to think that many long-term traders would still find it cheap and expedient to post orders on ordinary exchanges. And I’d bet that algorithms would fill most of those orders. Programs like to interact with orders that they consider mispriced. To maximize fill probability, sophisticated institutional traders might deliberately price orders more aggressively, but still inside the widened spreads. [[5](#bottom5cancels)] Unsophisticated traders, having an imprecise view of fair market value because of the wide spreads, would price orders less efficiently than they do now. Aggressive algorithms would also have much more certainty as to the nature of their counterparties, because market-makers would be absent from the order book. The increased certainty and the abundance of inefficiently priced resting orders would make aggressive algorithmic trading dramatically easier. I think the result would be that many electonic market-makers’ current pricing models could be profitably used to remove liquidity with IOC orders. [[6](#bottom6cancels)] Intermediation would undergo a regime change from passive to aggressive market-making. [[7](#bottom7cancels)] Market-restructuring generally benefits sophisticated traders who quickly grasp new dynamics, so I wouldn’t be at all surprised if this shakeup actually increased HFT revenues, at least for the few years it would take other participants to adapt to the new landscape.

# Exceptions to the Hypothetical Tax

My feeling is that the current population of market participants [[8](#bottom8cancels)] need professional intermediaries to help determine prices during continuous trading [[9](#bottom9cancels)]. In the scenario above, that need would be met by aggressive algorithmic traders. I deliberately specified the tax above to offer as few loopholes to traders as possible. What if we loosened some of those constraints?

Matt Levine, while answering the question of [“Why Do High-Frequency Traders Cancel So Many Orders?”](http://www.bloombergview.com/articles/2015-10-08/why-do-high-frequency-traders-cancel-so-many-orders-), says that

> Regulating the parts of Wall Street that you don’t like can help out the parts of Wall Street that you do like.

I think the most glaring beneficiaries of a loosened tax could be ELPs, wholesalers, and internalizers. If other market-makers couldn’t realistically submit resting quotes, but ELPs (etc) could still receive incoming orders and decide whether to fill them, long-term traders seeking liquidity would have no option but to trade with ELPs. The removal of competitors would be a huge boon to the ELP business. [[10](#bottom10cancels)] Similarly, if large, established market-makers received exemptions from the tax, they would stand to benefit at the expense of upstarts. If cancellations of hidden orders were tax-exempt, then we’d expect to see a surge in the share of trading on dark pools, as well as the further transformation of lit exchanges into dark pools. If traders could cancel 10 orders per day without the holding requirement, we might also get an army of retail traders trying to fill the shoes of market-makers. [[11](#bottom11cancels)] If the exemption were 10,000 orders instead of 10, capital-rich entities like hedge funds could profitably become market-makers. And, if cancel-replace messages were tax exempt, I think pretty much nothing would change.

Our markets are complex. Occasionally complex enough for the predicted effects of new regulation to be the opposite of the actual effects. I’m not very confident in my speculation about the consequences of a strict cancellation tax, but I’m skeptical of anybody who is. Eliminating market inefficiencies is not straightforward. And as long as they exist, I suspect algorithmic traders will do just fine. [[12](#bottom12cancels)] [[13](#bottom13cancels)]

[[1](#1cancels)] Assuming that fundamental traders didn’t use execution algorithms and only traded manually (or via manual broker).

[[2](#2cancels)] There’s no clear line separating “fundamental” and “speculative” traders, and for brevity I’m just going to wrap speculative traders into the fundamental category if they hold positions for at least a week. Some might call anybody exiting their positions after a week a “high-frequency” trader, but the logic in this post wouldn’t really change if the holding period were changed to a year.

[[3](#3cancels)] In “Flash Boys”, Michael Lewis [paraphrases](https://books.google.com/books?id=UcIkAwAAQBAJ&lpg=PP1&dq=editions%3A36ZaAiOcQqEC&pg=PA102#v=onepage&q=%22the%20technology%20existed%20that%20eliminated%20entirely%20the%20need%20for%20financial%20intermediaries%22&f=false) IEX COO John Schwall:

> For the first time in Wall Street history, the technology existed that eliminated entirely the need for financial intermediaries.

[[4](#4cancels)] There are many definitions of “block trades.” One definition by Tabb Group labels any trade over 20% of average daily volume (ADV) a “block.” These “blocks” are about 1/8 of institutional [volume](http://tabbforum.com/opinions/the-block-is-back?page=1&ticket=ST-14446760297014-cCQ8XQcTNXcIkXozTIbTRe2LPShsAfVs09cFFmG3) (and presumably much less of overall volume). Another [Tabb](http://tabbforum.com/opinions/building-blocks-in-a-post-reg-nms-world?page=1) definition calls any transaction over 10,000 shares (a size well within the range of HFTs) a “block”. These “blocks” are about 1/6 of total volume. “Block” sales to banks’ equity desks are in the range of several hundred million dollars, generally [proceed](http://www.wsj.com/articles/SB10001424052702303887804579501922083507360) at a discount of 3-4%, and are a minute portion of ADV.

On the other hand, it’s conceivable that a renaissance in block trading is inhibited by the renaissance in block trading exchanges. Norway’s SWF [says](http://www.nbim.no/contentassets/1b25761cb30e4025b627865627610dab/asset-manager-perspective_1-15.pdf) that fragmentation in block venues “can increase the search cost for buyside traders” and that monolithic “utility-like block crossing venues” would “increase the fill probability.” So maybe if all institutions agreed to execute at a single venue, we’d see a resurgence in block volumes.

It does seem that, in this new market with ultra-wide spreads, negotiating a price for block trades would be harder. There would be less certainty about the fair value of a stock, making block traders more cautious of their counterparties ripping them off.

[[5](#5cancels)] Both to incentivize counterparties to trade and to disincentivize what John Arnold [calls](http://www.bloombergview.com/articles/2015-01-23/high-frequency-trading-spoofers-and-front-running) “front-running,” where other traders react to an order by submitting their own orders at slightly more aggressive prices. In this scenario, the “front-runners” would be other long-term traders.

[[6](#6cancels)] With some level of modification. Many of today’s informative signals would become useless. But I’m sure changes in the market would also create new signals. Creative, flexible firms may succeed at the expense of those that haven’t been investing in talent.

[[7](#7cancels)] Markets today really exist somewhere in the middle of these two regimes — particularly because marketable, low-alpha flow is typically filled by wholesalers, making the population of low-alpha orders on lit exchanges disproportionately passive. The spirit of some [example strategies](https://mechanicalmarkets.wordpress.com/2015/02/16/protecting-client-interests-anonymity-in-us-equities/) on this blog is to identify and fill these low-alpha resting orders, saving them the cost of crossing the spread. This is an untraditional use of the term, but I think it’s fair to call the activity of these aggressive strategies “market-making.”

[[8](#8cancels)] Participants on public markets, that is. Traders in the rapidly growing private market seem to be doing fine [without](http://www.ft.com/intl/cms/s/0/27e9444c-0879-11e5-85de-00144feabdc0.html) price transparency, so far.

[[9](#9cancels)] Auctions, particularly those with large volumes, are probably different.

[[10](#10cancels)] Wider spreads on lit exchanges would allow ELPs (etc) to fill incoming orders at worse prices than they do now, while still bettering the prices on exchanges. This is absolutely not trading or investment advice: But, since Knight is publicly traded, it may be possible to bet on a tax with ELP exemptions becoming reality.

[[11](#11cancels)] 100,000 retail traders submitting 10 orders per day could partly fill the shoes of automated market-makers. Though, I doubt they’d do the job as well, and it would be a spectacular waste of labor.

[[12](#12cancels)] The history of market structure so far has led to cheaper executions and open access. I can, however, imagine a future cycle that’s quite different:

1.  The market structure changes, because of technology, greater access, regulation, etc.
2.  Many participants continue their old habits, and trade inefficiently.
3.  Savvy traders notice distortions created by this inefficient behavior. They trade to correct these incongruities, and profit.
4.  The less specialized market participants learn to be more efficient, and the savvy traders compete more fiercely with each other. This drives down their profit margins.
5.  People gradually find out how much money savvy traders *used* to make. Some get upset.
6.  People clamor for change, and get it. Return to step 1 and repeat.

[[13](#13cancels)] There are, of course, potential regulations that would eliminate algorithmic trading, such as a high transaction tax.