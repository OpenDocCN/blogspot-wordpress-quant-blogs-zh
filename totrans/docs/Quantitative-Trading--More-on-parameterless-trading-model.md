<!--yml
category: 未分类
date: 2024-05-12 19:19:51
-->

# Quantitative Trading: More on parameterless trading model

> 来源：[http://epchan.blogspot.com/2008/08/more-on-parameterless-trading-model.html#0001-01-01](http://epchan.blogspot.com/2008/08/more-on-parameterless-trading-model.html#0001-01-01)

I have written

[before](http://epchan.blogspot.com/2008/05/parameterless-trading-models.html)

that my ideal trading model is one that has no parameters, and what ways there are to accomplish this. Actually, I forgot to mention that a

[trading strategy](http://epchan.blogspot.com/2007/10/how-mean-reversion-strategy-performed.html)

proposed by Dr. Andrew Lo discussed previously is in fact parameterless, and the technique is so general that it can be applied to any mean-reverting strategy.

The technique is simply this: maintain a long (or short) portfolio with capital proportional to the distance between a supposedly mean-reverting measure and its long-term mean value.

For e.g. if you are pair-trading PEP vs KO, and you believe that the spread between PEP and KO is mean-reverting, then this spread is the mean-reverting measure you should employ.

As the spread moves away from its mean, keep buying (or shorting) the spread in equal dollar amount. And as the spread reverts, keep selling (or buying) the spread in the same dollar amount. What this dollar amount should be depends on: a) the total buying power you possess, b) the expected maximum deviation of the spread from its mean, and c) how often you intend to buy/short. Note that point c is not a parameter: it is arbitrary and limited only by transaction costs, technology, and other operational issues. As for the expected maximum deviation, it can be obtained by observing the history of the spread since inception.

This scheme thus obviates the need for entry or exit thresholds, and with them, the possibility of data-snooping bias. (You may still want to impose an entry threshold based on transaction cost consideration - but that would not count as a free parameter.)