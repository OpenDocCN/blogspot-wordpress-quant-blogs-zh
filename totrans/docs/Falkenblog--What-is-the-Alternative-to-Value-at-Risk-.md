<!--yml
category: 未分类
date: 2024-05-12 22:08:05
-->

# Falkenblog: What is the Alternative to Value at Risk?

> 来源：[http://falkenblog.blogspot.com/2009/04/what-is-alternative-to-value-at-risk.html#0001-01-01](http://falkenblog.blogspot.com/2009/04/what-is-alternative-to-value-at-risk.html#0001-01-01)

VAR has taken a lot of heat lately, mainly by people who never use it. If you are managing a desk of diverse instruments, it remains the best way to amalgamate risk. Consider you run a trading operation, and your desk has, at the end of the day, the following positions:

$100 Euro (Long Euro)

$100 US 30 year Tbond

$100 SPX stock index

What, other than a Value at Risk, would you use to amalgamate this portfolio of risks in USD risk?

I would say, this basket has a 95% daily VAR of $7.04\. This is because the daily standard deviations are {2.74%, 0.97%, 1.58%}, and the correlation matrix is

[![](img/2590c7dc16ec3929693ce625359f97a2.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjACIKGEQBPDiFXSnUVFWQ6G75yRsMwFg2xp8izNAFNJCqWjKLhH4ujivoS6tLnrWvQi0vlYzT-rtzKrFjp1mrCrYI35S5Vk3avPaofD6gIoApuK6xAKCn1yOXa-GmYWomfxBZGmQ/s1600-h/correl.png)

The basic idea is to take a 95% extremum move in dollars, or whatever you base currency is, and then run it through the correlation matrix. To assume the correlation matrix is filled with ones, that all correlations are perfect, is not 'conservative' because that could be easily gamed, encouraging eople to put on hedges that will not work as well asthe perfect correlation assumes. One should probably apply a bayesian assumption so that a sample correlation is modified by some common sense.

Value at risk is not useful for long maturity assets, (most of what is in a bank portfolio), but is very useful for a trading desk, anything with a liquid daily mark-to-market. It gives you a measure of a worst-case scenario that you should see several times a year. If you see it too much, or too little, you need to adjust your formula. The main advantage of this approach is allowing one to aggregregate different asset types into a common denominator: dollar pnl change. By using the 95% tail, you should capture some of the nonlinearities in your book. Of course, for a highly nonlinear trading desk, like a desk with a lot of credit risk, or optionality, there are other limits and measures that are essential.

Anyway, if someone has an alternative to Value at Risk for such a portfolio, I'd be interested in hearing what it is.