<!--yml
category: 未分类
date: 2024-05-18 13:55:50
-->

# Three Horsemen | Quantivity

> 来源：[https://quantivity.wordpress.com/2009/07/25/bias-stationarity-ergodicity/#0001-01-01](https://quantivity.wordpress.com/2009/07/25/bias-stationarity-ergodicity/#0001-01-01)

Conventional wisdom tells us quantitative trading is hard. Yet, few know specifically why it is difficult. Moreover, different types of quantitative trading suffer from differing complexities, such as: mathematical modeling, information access (*e.g.* tick-level data), computational facilities, execution facilities (*e.g.* low latency), risk management (*e.g.* real-time [VaR](http://en.wikipedia.org/wiki/Value_at_risk)), and leverage (*e.g.* RegT vs [portfolio margin](http://www.sec.gov/rules/sro/nyse/2006/34-54918.pdf)).

Amongst all complexity, much is due to the three horsemen of quantitative trading: *bias*, *stationarity*, and *ergodicity*.

Human psychology informs us humans are particularly susceptible to [attributional bias](http://en.wikipedia.org/wiki/Attributional_bias):

> Cognitive bias that affects the way we determine who or what was responsible for an event or action.

CNBC is literally in the business of attributional bias: talking heads trying to explain why the market did what it did, despite everyone knowing full well such explanations are incomplete at best (and completely fallacious, at worst). This bias motivates the hypothesis that computers can system and program trade better than humans.

This difficulty is further compounded by a fundamentally mistaken assumption about randomness in the financial markets ([black swans](http://www.amazon.com/exec/obidos/ASIN/1400063515/nassimtalebsfavo/002-8533486-7104820) aside). Specifically, the vast majority of statistical analysis techniques make the following (often unstated) assumption:

> A random process will not change its statistical properties with time and that such properties (such as the theoretical mean and variance of the process) can be deduced from a single, sufficiently long sample (realization) of the process. ([Wikipedia](http://en.wikipedia.org/wiki/Stationary_ergodic_process))

This fallacy is inherited from [probability theory](http://en.wikipedia.org/wiki/Probability_theory), and formally means an assumption that randomness can be modeled as a *stationary ergodic process*. Stationarity refers to statistic properties not changing over time. Ergodicity refers to such properties being deducible from a single, sufficiently long sample of the random process. Unfortunately, both are bogus for the vast majority of quantitative finance (otherwise, every first-year econometrics grad student would be rich).

Examples of this fallacy litter the financial landscape, not just the quantitative world:

*   Past performance: many people make investing decisions based upon past performance (aka “chasing the hot hand”), hoping the future will be similar to the past
*   Credibility: many people assign credibility to those individuals who have prognosticated successfully in the past, compounded by our [culture of celebrity](http://www.amazon.com/Life-Movie-Entertainment-Conquered-Reality/dp/0375706534)
*   Asset allocation: many people allocate their portfolio according to simplified techniques derived from [modern portfolio theory](http://en.wikipedia.org/wiki/Modern_portfolio_theory), ranging from classic 60/40 to new “Endowment” models
*   Option pricing: from [Black–Scholes](http://en.wikipedia.org/wiki/Black%E2%80%93Scholes) onward, the vast majority of mathematical finance is based upon mathematical formalism which assumes stationary ergodicity (*e.g.* martingales, Brownian motion, *etc.*)

And, arguably the most egregious, which seduces even the most rigorous statistical minds: time-series analysis (from [regression analysis](http://en.wikipedia.org/wiki/Regression_analysis) to [principal component analysis](http://en.wikipedia.org/wiki/Principal_component_analysis)) whose data spans many decades. This line of thinking is usually justified by appealing to the [law of large numbers](http://en.wikipedia.org/wiki/Law_of_large_numbers): “more data the better”. Unfortunately, lack of stationarity is far more statistically damaging than lack of large numbers.

These three factors often combine to confound quantitative trading: statistical techniques assuming stationary ergodicity are used to build systems, to which their authors attribute explanatory power for behavior of a set of instruments. Unfortunately, in practice, the *resulting statistical models tend to be insufficiently stable and thus have limited success in generating consistent profit*.

Given these three horsemen, challenge is trading in ways which minimize these fallacies.