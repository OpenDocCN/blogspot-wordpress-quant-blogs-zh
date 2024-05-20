<!--yml
category: 未分类
date: 2024-05-12 21:30:52
-->

# Falkenblog: Options on Options on Options

> 来源：[http://falkenblog.blogspot.com/2010/06/options-on-options-on-options.html#0001-01-01](http://falkenblog.blogspot.com/2010/06/options-on-options-on-options.html#0001-01-01)

Equity is an option on the asset of a company, with the strike price being its total liabilities. Most 'options' are thus really options on options, and indeed some people (

[Geske](http://www.global-derivatives.com/index.php/pricing-models-topmenu-37/31?task=view)

) have made such explicit models (they aren't used much as a practical matter)

The VIX is a weighted blend of prices for a range of options on the S&P 500 index. In 2006 the index itself became directly tradeable via futures. Now we have the

[VXX](http://www.google.com/finance?client=ob&q=NYSE:VXX)

and VXV, new ETFs that allow equity investors access to the VIX volatility index. The VXX trades a shload, about 30MM shares per day. This means, we now have options on the VIX. These aren't options on options, but options on implied vols of options on options (ack!). Looking at the implied volatilities by strike, and comparing them to the implieds on the SPY, we see they are quite different little beasts.

[![](img/9cd4a26eb8b0e4d2426b35642b23356c.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiTkyMdWwYNKP2bDKunmkxUGT6Hkc_rzmD8mPUsQ2Fg2BJwCVrsMjtf8OKHFyhVB5pBlKethWceG5XG9qKgi2AClnxjVJOtDmVy2RqlxJUtaF1xmslBRp5meUfQpDWsv8Gqsamvig/s1600/ivol.gif)

Note that for the SPY, volatilities increase as the strike goes down, because the market anticipates that downward movements in the index are correlated with higher volatility. The

[VXX](http://www.google.com/finance?client=ob&q=NYSE:VXX)

, in contrast, has an upward sloping implied curve, because as the volatility increases, its volatility increases too.

The fact that volatility curve is not flat implies that the standard option models, such as Black-Scholes, are misspecified, as they assume a constant volatility. As Peter Carr has said, 'the implied volatility is the

wrong

volatility we use in the

wrong

model in order to get the

right

price'. Black-Scholes, and its American option counterparts, are still very useful, but this highlights that any model in practice is implemented within a kluge of

ad hoc

rules informed by reality. Having more price points to nail down how to adjust implied vols by strike/expiration is very useful, what

[Sandy Grossman](http://www.jstor.org/pss/1942852)

called 'complete markets', allowing one to see more market derived probability estimates of various states of nature, where in this case the state is not just a price, but a volatility of a volatility of a price.