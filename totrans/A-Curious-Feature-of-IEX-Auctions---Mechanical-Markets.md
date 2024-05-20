<!--yml
category: 未分类
date: 2024-05-18 06:38:10
-->

# A Curious Feature of IEX Auctions | Mechanical Markets

> 来源：[https://mechanicalmarkets.wordpress.com/2017/09/20/a-curious-feature-of-iex-auctions/#0001-01-01](https://mechanicalmarkets.wordpress.com/2017/09/20/a-curious-feature-of-iex-auctions/#0001-01-01)

IEX is busy setting up its listing business and has designed an auction mechanism. If I understand IEX’s documentation properly — and I might not [[1](#bottom1iexauctions)] — their auctions may have some pretty weird functionality. [[2](#bottom2iexauctions)]

IEX’s auction [documentation](https://iextrading.com/docs/IEX%20Auction%20Process%20Specification.pdf) says:

> For the Opening/Closing Auction, non-displayed buy (sell) orders on the Continuous Book with a resting price within the Reference Price Range will be priced at the Protected NBB (NBO) for the purpose of determining the clearing price, but will be ranked and eligible for execution in the Opening/Closing Auction match at the order’s resting price.

Now, I’m not easily surprised by complex exchange logic, but this got my attention. Again, I may have misunderstood something, but if I haven’t, this logic could be controversial with long-term traders once they familiarize themselves with IEX auctions.

Take IEX’s “Example 1” [from](https://iextrading.com/docs/IEX%20Auction%20Process%20Specification.pdf) their “CLEARING PRICE EXAMPLES”:

> The Closing Auction Book includes the following orders:
>  LOC order to buy 1,500 shares with a limit price of $10.10; and
>  LOC order to sell 1,000 shares with a limit price of $10.10.
> Shares are maximized at $10.10; therefore
>  1,000 shares would execute at the IEX Official Closing Price of $10.10.

My understanding is that a hidden order submitted after these LOC orders could gain priority without providing a better price. If the NBBO were 10.09/10.13, and someone submitted a hidden bid at $10.11 100ms before the auction, I believe IEX’s auction logic would still price the auction at $10.10 [[3](#bottom3iexauctions)] — but the hidden order would be executed in place of the LOC bid. This may feel “unfair” because the hidden order was submitted long after the LOC order and had virtually zero risk of moving the matching price (because the hidden bid is priced at the $10.09 “for the purpose of determining the clearing price”). And unlike LOC (or MOC) orders, the hidden order does not have a “no-cancel” period, so could be canceled even 1ms before the auction.

“Example 2” in “PRIORITY OF EXECUTION EXAMPLES” provides a slightly more complex illustration of this behavior. [[4](#bottom4iexauctions)]

# Opaque, Non-Competitive Auctions

Under certain conditions, this functionality gives traders the opportunity to simultaneously gain priority while offering a less competitive price, a rare confluence in normal markets. One reason why traders submit LOC/MOC orders (and displayed orders) is because they want to announce their intentions to attract liquidity. IEX’s hidden order logic shouldn’t change that. But other auction traders only announce their intentions because they want priority. This latter group may find the advantages of hidden orders hard to resist.

Here is a potentially problematic example:

1.  After the final opportunity to submit LOC/MOC orders, a closing auction has a big sell imbalance: there is 1 LOC buy at $10.00 for 1,000 shares, and 1 LOC sell at $10.00 for 10,000 shares.
2.  In the remaining 10 seconds of the day, traders will compete to trade with the sell imbalance. On IEX, the only way they can do so is by using displayed and undisplayed orders.
3.  Maybe 10ms before the close, the NBBO is $10.05/$10.07 (with all displayed quantity on IEX).
4.  The bidder at $10.05 realizes they can get a better price and better priority in the auction by deleting their displayed order and resubmitting a hidden buy order at $10.06\. They do so, and the NBBO is now $10.04/$10.07.
5.  The bidder at $10.04 does the same thing. Likewise those at $10.03, $10.02, and $10.01\. The NBBO is now $10.00/$10.07.
6.  The auction occurs at $10.00\. The hidden orders are filled completely, but the LOC bid at $10.00 doesn’t receive any execution.[[*](#bottom*iexauctions)]

I can’t imagine that either LOC side would be happy in this circumstance. The LOC sell order was filled at a non-competitive price. And the LOC buy order was skipped-over in favor of hidden orders that were submitted after it, but effectively at the same price. This process could also negatively affect market stability by causing the NBBO to widen at the most important and volatile part of the day. [[5](#bottom5iexauctions)]

Now, I don’t think this sort of outcome will happen most of the time. But it certainly could happen some of the time. And even when it doesn’t, traders in the final second of the day may play a guessing game, trying to determine whether it’s worth submitting a displayed order on top of suspected hidden orders. (In our example, a trader might want priority over the hidden orders and submit a displayed bid at $10.06.)

I’m also not sure this functionality was an oversight. IEX [says](https://medium.com/boxes-and-lines/the-iex-auction-pursuing-better-price-discovery-a65cb9aeeadb) it exists “to protect the anonymity of resting non-displayed interest.” And “IEX Auctions were strategically designed after extensive research and informal discussion with various market participants.” But IEX did not find it appropriate to employ this functionality for auctions occuring after volatility pauses or halts, perhaps because those auctions can be chaotic and have a particular need for transparency. The thing is, some days the open and close can also be volatile, and those are the days when it’s most important for exchanges to run a smooth auction. [[6](#bottom6iexauctions)]

To be clear, I wouldn’t say that this feature is scandalous. The behavior (I think) is fully disclosed, and professional traders should always read the manual before using any exchange. But issuers are probably not equipped to do that. And if IEX [wants](https://medium.com/boxes-and-lines/the-iex-auction-pursuing-better-price-discovery-a65cb9aeeadb) its auction to be “simple,” I’m not sure this is the right approach.

[[1](#1iexauctions)] It’s hard for me to completely understand IEX’s [documentation](https://iextrading.com/docs/IEX%20Auction%20Process%20Specification.pdf). It has some clear errors in it — such as the “CLEARING PRICE EXAMPLES,” which say “Each example below assumes the Protected NBBO is $10.09 by $10.11 at the time of the Closing Auction,” but “Example 3” has displayed limit orders on IEX at $10.12 (buy) and $10.13 (sell) — so something is not quite right. Even aside from errors in the documentation, I may have made errors interpreting it.

[[2](#2iexauctions)] I don’t mean to write so much about IEX, but functionality like this has not gotten the attention it deserves.

[[3](#3iexauctions)] I think the auction would actually occur at $10.09 in this case, were it not for the [rule](https://iextrading.com/docs/IEX%20Auction%20Process%20Specification.pdf):

> If more than one price maximizes the number of shares that will execute, resulting in an auction price range, the Reference Price is set to the price at or within such range that is not lower (higher) than the most aggressive unexecuted buy (sell) order.

Which I think guarantees that even if the LOC bid at $10.10 is skipped-over and doesn’t receive an execution, it will still affect the auction price. I suppose this is better than performing the auction at $10.09, but it will still frustrate the LOC-sender who missed their execution and moved the closing price.

[[4](#4iexauctions)]

> The Regular Market Continuous Book Contains the following orders:
>  Midpoint Peg order to buy 2,500 shares with a resting price of $20.20.
> The Closing Auction Book includes the following orders:
>  LOC order to buy 500 shares with a limit price of $20.19; and
>  LOC order to sell 2,000 shares with a limit price of 20.18.
> For purposes of determining the clearing price, the Midpoint Peg order is priced to the Protected NBB ($20.19), but remains ranked and eligible to execute at its resting price;
> Accordingly, shares are maximized between $20.18 and $20.19 resulting in an auction price range, and $20.19 is the only price within such range that is not below the price of the most aggressive unexecuted buy order; therefore
>  2,000 shares would execute at the IEX Official Closing Price of $20.19;
>  The Midpoint Peg buy order would receive an execution of 2,000 shares;
>  The LOC sell order would receive an execution of 2,000 shares; and
>  The LOC buy order would not receive an execution, because the LOC sell order is fully filled after matching with the Midpoint Peg buy order with superior priority.

[[5](#5iexauctions)] It also seems potentially risky to have the auction price depend other exchanges’ order books. If somebody submits a 100-share order on another exchange, they could potentially move the IEX open or close by multiple ticks. Even ignoring the possibility of manipulation, it might not be the best idea for an important cross to be sensitive to small orders that aren’t eligible to participate in that cross.

[[6](#6iexauctions)] NYSE [learned](http://www.reuters.com/article/us-usa-stocks-rule48/u-s-sec-approves-nyse-request-for-new-market-volatility-rules-idUSKCN0ZM2ES) this the hard way after Rule 48 probably contributed to the market disruption on Aug. 24, 2015.

[[*](#*iexauctions)] I have edited this example because I made an error in the original version. The LOC bid in the original version was at $10.10\. In that circumstance, the LOC bid at $10.10 *would* get fully filled at $10.00 (because it’s more aggressively priced than the hidden orders), in contrast to what happens to the LOC bid at $10.00 in our example.