<!--yml
category: 未分类
date: 2024-05-12 18:55:14
-->

# Quantitative Trading: Loss aversion is not a behavioral bias

> 来源：[http://epchan.blogspot.com/2018/06/loss-aversion-is-not-behavioral-bias.html#0001-01-01](http://epchan.blogspot.com/2018/06/loss-aversion-is-not-behavioral-bias.html#0001-01-01)

In his famous book "

[Thinking, Fast and Slow](https://amzn.to/2yU4IKr)

", the Nobel laureate Daniel Kahneman described one common example of a behavioral finance bias:

"You are offered a gamble on the toss of a [fair] coin.

If the coin shows tails, you lose $100.

If the coin shows heads, you win $110.

Is this gamble attractive? Would you accept it?"

(I have modified the numbers to be more realistic in a financial market setting, but otherwise it is a direct quote.)

Experiments show that most people would not accept this gamble, even though the expected gain is $5\. This is the so-called "loss aversion" behavioral bias, and is considered irrational. Kahneman went on to write that "professional risk takers" (read "traders") are more willing to act rationally and accept this gamble.

It turns out that the loss averse "layman" is the one acting rationally here.

It is true that if we have infinite capital, and can play infinitely many rounds of this game simultaneously, we should expect $5 gain per round. But trading isn't like that. We are dealt one coin at a time, and if we suffer a string of losses, our capital will be depleted and we will be in debtor prison if we keep playing. The proper way to evaluate whether this game is attractive is to evaluate the expected compound rate of growth of our capital.

Let's say we are starting with a capital of $1,000\. The expected return of playing this game once is initially 0.005.  The standard deviation of the return is 0.105\. To simplify matters, let's say we are allowed to adjust the payoff of each round so we have the same expected return and standard deviation of return each round. For e.g. if at some point we earned so much that we doubled our capital to $2,000, we are allowed to win $220 or lose $200 per round. What is the expected growth rate of our capital? According to standard

[stochastic calculus](http://epchan.blogspot.com/2017/05/paradox-resolved-why-risk-decreases.html)

, in the continuous approximation it is -0.0005125 per round - we are losing, not gaining! The layman is right to refuse this gamble.

Loss aversion, in the context of a risky game played repeatedly, is rational, and not a behavioral bias. Our primitive, primate instinct grasped a truth that behavioral economists cannot.  It only seems like a behavioral bias if we take an "ensemble view" (i.e. allowed infinite capital to play many rounds of this game simultaneously), instead of a "time series view" (i.e. allowed only finite capital to play many rounds of this game in sequence, provided we don't go broke at some point). The time series view is the one relevant to all traders. In other words, take time average, not ensemble average, when evaluating real-world risks.

The important difference between ensemble average and time average has been raised in this

[paper](https://aip.scitation.org/doi/full/10.1063/1.4940236)

by Ole Peters and Murray Gell-Mann (another Nobel laureate like Kahneman.) It deserves to be much more widely read in the behavioral economics community. But beyond academic interest, there is a practical importance in emphasizing that loss aversion is rational. As traders, we should

**not**

only focus on average returns: risks can depress compound returns severely.

===

Industry update

1)

[Alpaca](https://alpaca.markets/))

 is a new an algo-trading API brokerage platform with zero commissions.

2)

[AlgoTrader](https://www.algotrader.com/features/)

started a new quant strategy development and implementation platform.

**My Upcoming Workshop**

August 4 and 11:  

[Artificial Intelligence Techniques for Traders](http://www.epchan.com/workshops/)

I briefly discussed why AI/ML techniques are now part of the standard toolkit for quant traders

[here](https://www.youtube.com/watch?v=5-nG8NSzE1s&t=5s)

. This real-time online workshop will take you through many of the nuances of applying these techniques to trading.