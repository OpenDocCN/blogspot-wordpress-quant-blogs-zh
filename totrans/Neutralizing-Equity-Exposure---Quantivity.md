<!--yml
category: 未分类
date: 2024-05-18 13:55:27
-->

# Neutralizing Equity Exposure | Quantivity

> 来源：[https://quantivity.wordpress.com/2009/09/19/neutralizing-equity-exposure/#0001-01-01](https://quantivity.wordpress.com/2009/09/19/neutralizing-equity-exposure/#0001-01-01)

An equity trader recently posed the following question:

> Given an equity position, how can I “borrow” some part of the capital tied up in that position to undertake another short-term trade without liquidating the equity position.

This question boils down to hedging, and thus is interesting as its solution is relevant to numerous other trading and investment challenges—and one which many retail investors may underappreciate its usefulness and broad applicability:

*   Derivatives: use of leverage *without* being directional speculation
*   Portfolio management: constructing an [alpha](http://en.wikipedia.org/wiki/Alpha_%28investment%29) overlay (*i.e.* any short-term trading strategy) on a standard beta index strategy (*e.g.* S&P 500 via SPY)
*   Employee stock options: hedging for unvested or non-exercised employee stock options (ISO or NQO)
*   Tax avoidance: satisfy holding period to qualify for long-term capital gains

To answer this question, start by considering a position composed of a single stock: say, long 100 shares of GE.

Solution is an offsetting position which satisfies two requirements:

*   Neutrality: if GE prices decreases $1, offset should increase in value close to $1
*   Cash: offset should generate cash close to being equal to the price of GE (*e.g.* $16.44 @ close) multiple by the number of shares being offset (100 shares); $1,644 in this example

Numerous approaches exist to solve this problem. One approach is to statically hedge via a deep in the money (DITM) option on GE, say a Jan 2010 $2.50 call (GEWAS). Given the option contract multiplier of 100, 1 GEWAS contract is required per 100 shares. Thus, a single option in this example.

To satisfy the neutrality requirement from above (glossing over several derivative complexities for brevity), the [option greeks](http://en.wikipedia.org/wiki/Greeks_%28finance%29) ([delta](http://en.wikipedia.org/wiki/Greeks_%28finance%29#Delta) and [gamma](http://en.wikipedia.org/wiki/Greeks_%28finance%29#Gamma), in particular; [vega](http://en.wikipedia.org/wiki/Greeks_%28finance%29#Vega) is zero in this example, so conveniently ignored) indicate GEWAS should increase very nearly $1 for every $1 decrease by GE.

To satisfy the cash requirement from above, the call option should be sold short: when GE decreases in value, the short call option must increase in value. Most recent midpoint close quote for GEWAS is $14.05, thus shorting 1 GEWAS generates $14.05 in cash for each share—for a total of $1,405 in this example (less transaction costs).

Thus, the equity trader can solve this problem by shorting a single option contract (-1 GEWAS), use the $1,405 proceeds to execute the desired short-term trade, and then buy the option back (thus, generating the P&L to match the underlying change in GE which occurs in the meantime) once the short-term trade is closed.

One caveat: if GE consistently decreases in price, this hedge will need to be closed or dynamically adjusted. This adjustment becomes required because the option delta/gamma decreases away from 1 as GE decreases. For example, if GE decreases to $2.50 (GEWAS strike price), then the option becomes [at the money](http://en.wikipedia.org/wiki/Moneyness#ATM:_At-the-money) (ATM) and thus delta is 0.5\. As such, this hedge should be closed or adjusted well in advance of GE price decreasing to approach this strike price.