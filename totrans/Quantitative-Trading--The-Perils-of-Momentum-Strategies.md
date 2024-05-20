<!--yml
category: 未分类
date: 2024-05-12 19:22:13
-->

# Quantitative Trading: The Perils of Momentum Strategies

> 来源：[http://epchan.blogspot.com/2007/08/perils-of-momentum-strategies.html#0001-01-01](http://epchan.blogspot.com/2007/08/perils-of-momentum-strategies.html#0001-01-01)

Not so long ago I was an agnostic with respect to choosing between mean-reverting and momentum models: I felt that depending on the particular model or environment, each can be profitable. Lately, however, I am increasingly skeptical about the long-term profitability of momentum models. The main reason is the increasing competition among traders, algorithmic or otherwise.

As I mentioned in my

[previous post](http://epchan.blogspot.com/2007/08/further-debate-on-factor-models.html)

, when more and more traders decide to adopt mean-reverting strategies, all they do is to eliminate the trading opportunity. The market becomes efficient, and nobody makes any money, but nobody loses either. In contrast, when more and more traders decide to adopt momentum strategies, the momentum will be established sooner and sooner. For e.g. in the case of event-driven strategies which are mostly momentum-based, the new equilibrium price will have been established almost instantaneously after the event is publicly disclosed. Under this circumstance, any momentum trades that are entered just a little bit late will not only suffer zero profit, but will likely suffer losses as mean-reversion almost inevitably takes over. But how soon do we need to enter in order to avoid this fate? (It can't be too soon either because often a trend need to be established first in order to trigger an entry signal.) It is unfortunately a moving target as competition increases: 1 day earlier might work now, but may not be sufficient a few months from now. (The exit trade also suffers the same problem, as we don't know how long the momentum will last.) It is a dangerous game to play.

Indeed, time is often a friend of the mean-reversion trader: the longer s/he waits, perhaps the more profitable the trading opportunity. And if s/he enters too early and suffers a loss, s/he can always double the position. As I explained in a

[previous article](http://epchan.blogspot.com/2007/01/what-is-your-stop-loss-strategy.html)

, stop-loss should generally not be applied to mean-reverting trades on a short time-scale. So even if the trader does not double-up the position, an eventual re-couping of the loss is more than likely. On the other hand, time is an enemy of the momentum trader: if s/he loses the first-mover advantage and suffers heavy loss, I argued in that article that a stop-loss is advised, and thus the loss is forever locked-in.

Given this asymmetry, it is no wonder that algorithmic traders have been warning me long ago that it is hard to find a profitable momentum trade. And I was silly enough not to pay heed to them until now.