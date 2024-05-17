<!--yml
category: 未分类
date: 2024-05-18 06:43:19
-->

# Blind Analysis, Inefficient Markets, and UK Polling Accuracy | Mechanical Markets

> 来源：[https://mechanicalmarkets.wordpress.com/2015/05/08/blind-analysis-inefficient-markets-and-uk-polling-accuracy/#0001-01-01](https://mechanicalmarkets.wordpress.com/2015/05/08/blind-analysis-inefficient-markets-and-uk-polling-accuracy/#0001-01-01)

Everybody knows that market prices do not perfectly reflect all available information. This is partly due to human biases, one reason that algorithmic trading has become so successful.

The polls published prior to yesterday’s UK General Election generally predicted a hung parliament. Those polls were obviously very wrong. Why? One factor seems to be the influence of human bias on data analysis. Here is [Damian Lyons Lowe](http://survation.com/snatching-defeat-from-the-jaws-of-victory/), CEO of pollster Survation, which nearly published a poll that would have closely predicted the election results:

> the results seemed so “out of line” with all the polling conducted by ourselves and our peers – what poll commentators would term an “outlier” – that I “chickened out” of publishing the figures – something I’m sure I’ll always regret

So, at least one pollster held back results that would have [completely changed the prediction landscape](https://twitter.com/davidaxelrod/status/596700185553547264). Others may have done the same, or may have unconsciously manipulated their analysis so that the final results were closer to what everybody else had been reporting. When the first exit poll was announced, which closely agreed with Survation’s never-released data, markets reacted strongly. GBP/USD immediately rose over 1%, indicating that the [trading community](http://www.bloomberg.com/news/articles/2015-05-07/pound-jumps-as-exit-poll-shows-tories-win-most-seats-in-election) found the results just as surprising as political experts.

This is a fantastic opportunity to learn about blind analysis. Blind analysis is a technique, primarily used in particle physics, to reduce the influence of human biases on reported results of an experiment. Physicists learned the hard way that human psychology is an important source of systematic error. See, for example, how some experimental values [evolved over time](http://pdg.lbl.gov/2014/reviews/rpp2014-rev-history-plots.pdf), courtesy of the [Particle Data Group](http://pdg.lbl.gov/2014/reviews/contents_sports.html). Some of these plots may be reminiscent of markets, which at times have very poorly predicted both future prices and their uncertainty.

Joel Heinrich has written an [approachable and excellent summary](http://www-cdf.fnal.gov/physics/statistics/notes/cdf6576_blind.pdf) of the motivations and methods of blind analysis. Heinrich mentions an example that should sound familiar given the biased polling discussed above. A physical quantity appeared, in its reported measurements, to become less uncertain over time, eventually being reported about 8 sigma away from its now-established value:

> It is quite likely that the experimenters during this period paid too much attention to the level of agreement between their new result and the measurements of the recent past. If one judges whether a result is ready for publication by its agreement with the current world average, such disasters can happen…
> [N]aturally when one sees an 8 [sigma] disagreement between one’s current result and the world average, one goes back and checks everything very carefully. On the other hand, when the new number is consistent with the old, there is a tendency to declare victory and move on. This asymmetry results in a statistical bias. A better procedure would be to list and schedule all the checks in advance of knowing the answer, and carry them out in either case

The techniques of blind analysis can be readily applied outside of physics. The general principles are to have strict procedures written ahead of time, and to hide whatever possible from the individuals analyzing the data. This may mean hiding the final result, adding in some kind of constant or noise to the data which can later be subtracted, or allowing the analysts to work with only a subset of unblinded data. I strongly encourage everybody who works with data to read Heinrich’s review or [others](http://www.slac.stanford.edu/econf/C030908/papers/TUIT001.pdf). It is immensely frustrating to see human knowledge obfuscated for such a silly, avoidable reason. Blind analysis could dramatically improve the quality of all data-oriented disciplines, and I hope that it becomes more widespread.