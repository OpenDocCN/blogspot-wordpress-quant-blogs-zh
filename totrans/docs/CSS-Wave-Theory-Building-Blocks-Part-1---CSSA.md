<!--yml
category: 未分类
date: 2024-05-12 18:11:13
-->

# CSS Wave Theory Building Blocks Part 1 | CSSA

> 来源：[https://cssanalytics.wordpress.com/2011/04/10/css-wave-theory-building-blocks-part-1/#0001-01-01](https://cssanalytics.wordpress.com/2011/04/10/css-wave-theory-building-blocks-part-1/#0001-01-01)

There are a lot of very successful traders that subscribe to some of the concepts underlying “Elliot Wave Theory.”  The general idea behind this theory is that markets move in fractal waves with sequences and  movements that are predictable using historical precedent and Fibonacci ratios. Furthermore, there are a lot of academic researchers that also believe in the linkage between fractals and predictable underlying movements in the financial markets. The field is complementary to traditional data-mining based technical analysis in that it is capable of defining generalizable principles of market movements and structure.  The problem with a lot of Elliot Wave and fractal theory applications is 1) that they contain too many specific assumptions 2) finding a clear interpretation that experts in the field can agree upon that leads to a set of testable hypotheses has proven highly elusive 3) very few practical applications have emerged from this area that are accessible to the average quant.  Surely there must be a simpler way to create building blocks that can reconcile some of these issues.

One of the concepts that I have always stressed is to normalize market movements versus their actual distribution to increase the success rate  out of sample. Another concept I try to emphasize is the ability to simplify or “fuzzify” rules so that they can also be more generalizable.  Both of these concepts are critical to this approach.  When I think of wave theory, I think in terms of both price and time- both aspects create a more dynamic and nuanced interpretation of market movements.  In this post we will simply look at creating a set of definitions that also include different types of blocks:

1) **Wave**: a consecutive move in price blocks either up or down.

2) **Price Block**: this is similar to a renko brick in that it is not affected by time. A price block is every “n” ATR or Standard Deviation unit that a price moves. For example if “n” is equal to 1 and we are using ATRs, then every 1 atr move we will record as an individual block. These blocks stack up in the direction of the first block and only change direction if price retraces by 1 atr.

3) **Time Block:** this  captures the time in “n” days or weeks of one wave (as defined by price blocks) .