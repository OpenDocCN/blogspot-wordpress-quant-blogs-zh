<!--yml
category: 未分类
date: 2024-05-12 21:07:51
-->

# Falkenblog: When A Stop-Loss Makes Sense

> 来源：[http://falkenblog.blogspot.com/2011/02/when-stop-loss-makes-sense.html#0001-01-01](http://falkenblog.blogspot.com/2011/02/when-stop-loss-makes-sense.html#0001-01-01)

Tuesday I posted on the

[stop loss myth](http://falkenblog.blogspot.com/2011/02/stop-loss-myth.html)

, but it's actually a more complex issue. The post criticized the thought that given an expected return on an asset, a stop loss rule can change an asset's expected return. It isn't often stated this boldly, but implied, and this is just wrong. A stop-loss merely adjusts the expected return by the expected time horizon you are in the trade. An asset does not have a different expected return because of what the holder does with it by definition in the paper referenced.

Yet, stop loss rules can be very useful when you

do not know

the expected return of the asset, or strategy, you are applying. In those cases, almost everyone prudently stops doing something if it loses some arbitrary amount. I hear Millenium had a rule that once a trader had a 3% loss of his initial capital allocation, he was gone; harsh, but with hundreds of traders of uncertain ability, a reasonable rule of thumb.

The idea comes from the

[optimal stopping problem](http://en.wikipedia.org/wiki/Optimal_stopping)

, which has a large literature, and has been applied to picking secretaries. The idea is, you sample things, and can move on, and you want to choose the secretary/asset that will generate the greatest annuity. When you sample from a strategy/asset, it is like pulling a ball labeled x from an urn that are distributed with mean μ and standard deviation σ. Each sample costs c>0, which can be considered an opportunity cost. An any stage you can stop and keep your asset/secretary for the remainder of the 'game', generating x each period. In this case, the optimal rule is to sample until x>f(c,σ), where f'(c)<0, so the criteria is a decreasing function of the cost of sampling. Further, f'(σ)>0, so as the volatility goes up, you would do better searching still further, hoping to get a really high valued secretary/strategy, etc.

This has been applied to

[optimal dating strategies](http://news.cnet.com/8301-17852_3-10309716-71.html?part=rss&subj=news&tag=2547-1_3-0-5)

, where you date X women, then after that, proposing to the next one who is 'better' than any of those X (this assumes each of X would accept your proposal). X is derived by taking the number of chances you think you will get and dividing by

e

(2.72). So, if you date 10 girls a year, and figure you'll date for 10 years (100 total), take the first 37 to find your max, and of the next 63 take the first greater than the best of the max (you aren't allowed to 'go back' at any time). That maximizes your chances of finding your soulmate.

A related problem with similar intuition is if you think returns can have a mean of -μ or +μ, then a rule that exits a strategy when the cumulative return is X standard deviations below zero over any horizon will get you out of the low mean return strategies with a greater probability than the high mean return strategies, surely a good thing over the long run. The exit rule is a function of volatility and the costs of sampling.

This is a great strategy towards life in general. You should expect to pay to find what you are specially suited for, whether it's a career or mate. This is why people don't mind paying to take risks as they frequently do, because such plays are not made in a one-time mean-variance setting, but as part of a strategy of finding your alpha or comparative advantage. To never take risk but merely work really hard is to never find your best, but rather, do best in what may be a very suboptimal match (eg, I would be a bad piano player no matter how hard I practiced). When young, failing is OK, you just have to know when to stop (not too soon or too late) and try something else. Life is finite, and so at some point you have to settle down at what you are best at, or what works best for you, even if you aren't great at it, and stick with it. Optimizing does not mean you will be very successful, it just means you are maximizing your potential, which is all anyone can do.