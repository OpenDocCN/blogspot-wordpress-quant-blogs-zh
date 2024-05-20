<!--yml
category: 未分类
date: 2024-05-12 20:21:36
-->

# Falkenblog: Bank Stock Timing Strategy

> 来源：[http://falkenblog.blogspot.com/2012/10/bank-stock-timing-strategy.html#0001-01-01](http://falkenblog.blogspot.com/2012/10/bank-stock-timing-strategy.html#0001-01-01)

My

[bank vega theory](http://falkenblog.blogspot.com/2011/12/business-cycles-and-barrier-options.html)

I alluded to yesterday argued that when banks are weak, they are in a negative vega zone: the potential for getting stopped out makes them want to avoid risks, not take them. For fun, I looked at a trading implication, based on the idea that I alone, via my theory, know when banks will be timid or growing.  A timid bank doesn't make money, so it's best to avoid it then. It's not short term enough for it to be really useful, so I'm sharing, and I think all investors thinking about their bank index allocation should find this interesting.

A calculated a backward-looking correlation of the past 252 days of daily bank returns with the changes in the VIX index, because

[Ken French's website](http://mba.tuck.dartmouth.edu/pages/faculty/ken.french/data_library.html)

has daily returns for a bank index going back to 1986, I have VIX data from 1986, and I can update this with the KBX bank index for more recent daily data.

I then take this correlation, and find its median. I then say, invest in the SP500 when this correlation is high in absolute terms (very negative, all correlations with the changes in the VIX are negative), I don't want to invest, because the banks won't be investing and making money. In the 50% of the time that correlation is low (again, in absolute value), I'm in the banks. Here's a comparison of that strategy, and clearly timing based on the bank-VIX change correlation outperforms simply being always long banks.

Here's what it looks like in Scatter-Plot, comparing the future 3-month return in the two regimes.  The black vertical line in the center is my best stab at putting a median in there.

We are currently at -70% for a correlation, still bad for banks (median around -62%). This is all out of sample, and a pretty simple rule. I did try this with Ken French's other industries, and found no similar pattern.