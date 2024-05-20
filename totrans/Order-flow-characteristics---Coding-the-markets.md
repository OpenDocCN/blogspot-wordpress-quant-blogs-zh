<!--yml
category: 未分类
date: 2024-05-12 19:40:55
-->

# Order flow characteristics | Coding the markets

> 来源：[https://etrading.wordpress.com/2008/11/05/order-flow-characteristics/#0001-01-01](https://etrading.wordpress.com/2008/11/05/order-flow-characteristics/#0001-01-01)

## Order flow characteristics

### November 5, 2008

[Patrick Hewlett’s presentation](http://www2.maths.ox.ac.uk/mcfg/OxfordPrincetonworkshops/Talks07/Hewlett.pdf) includes a page on “the stylised facts of order flow”. The facts he notes, with my comments in square brackets, are…

*   Limit order arrival rates are conditional on distance from best [the closer one’s order to best bid or offer, the more likely it is to trade]
*   Existing limit orders may be cancelled and immediately resubmitted [if you place a buy order a couple of ticks off best bid in the hope of price movement, and the market moves away due to big market buy orders, you’ll need to resubmit to chase the market]
*   Aggressiveness of orders depends on depth [understanding aggression as willingness to pay for liquidity, I read this as meaning one can only pay for order size if there is depth to match]
*   Fewer market orders when the spread is large [market orders pay the spread for immediate execution, so the bigger the spread, the higher the cost of immediacy]
*   More limit orders inside spread when depth at best is large [because orders placed at best will be at the back of a long queue]