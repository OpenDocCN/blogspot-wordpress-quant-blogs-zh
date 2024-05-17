<!--yml
category: 未分类
date: 2024-05-12 21:55:55
-->

# Falkenblog: Robert Haugen Champions Safe Stocks

> 来源：[http://falkenblog.blogspot.com/2009/07/robert-haugen-champions-safe-stocks.html#0001-01-01](http://falkenblog.blogspot.com/2009/07/robert-haugen-champions-safe-stocks.html#0001-01-01)

Bob Haugen has been writing about the

[inefficient stock market](http://www.amazon.com/Inefficient-Stock-Market-Robert-Haugen/dp/0130323667/ref=sr_1_1?ie=UTF8&s=books&qid=1246918923&sr=1-1)

for a long time. His JFE piece (Commonality in the determinants of expected stock returns) with Nardin Baker back in 1996\. His recent SSRN paper revists these themes and declares

[Case Closed](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1306523)

:

> This article provides conclusive evidence that the U.S. stock market is highly inefficient. ... Stunningly, the ten percent of stocks with highest expected return, in aggregate, are low risk and highly profitable, with positive trends in profitability. They are cheap relative to current earnings, cash flow, sales, and dividends. ... Undeniably, the highest expected return stocks are, collectively, highly attractive; the lowest expected return stocks are very scary - results fatal to the efficient market hypothesis. While this evidence is consistent with risk loving in the cross-section, we also present strong evidence consistent with risk aversion in the market aggregate's longitudinal behavior. These behaviors cannot simultaneously exist in an efficient market.

My book

[Finding Alpha](http://www.amazon.com/Finding-Alpha-Search-Return-Finance/dp/0470445904/ref=pd_rhf_p_t_2)

is consistent with his findings. That is, firms that have low volatility, high profitability, low leverage, and just about anything correlated with 'safe' or 'not risky' tend to outperform their opposite. The standard approach is trying to find a 'risk factor' that explains why Coca-Cola type companies are riskier than GM type companies, which I think is impossible.

Yet, I find myself disagreeing with Haugen in two major areas. First, he says that he finds people are risk averse in general, because markets fall when volatility rises. This fact is true, whether one measures this using an equity implied volatility, or an contemporaneous measure of volatility (eg, those months with the highest daily vol will have the lowest returns). Yet going forward, this result does not hold. A higher implied volatility, or historical vol, does not augur higher returns. Thus, all we know is that when volatility rises, the stock market will fall. This is only consistent with risk aversion if such a fall presages a higher future return, as where the dividend forecast is the same, but the immediate price decline (and negative return) is just capitalizing this higher return. It does not work like that. You get a lower return immediately, and no higher return in the future.

Think of it this way. If you were averse to volatility, you would want an asset that would be a relative outperformer in these periods, not a relative underperformer. But those stocks with the highest covariation with volatility changes are those same crappy stocks with the lowest overall return. In sum, contemporaneous inverse correlation between volatility and returns is inconsistent with risk aversion because forward-looking volatility and return correlations are weak if not negative as well.

Given he hates market efficiency, he should jump over to my side, and see it as an equilibrium where people pay for hope. There is generally risk neutrality, with a little risk loving at the high end, and premium for cash-type assets, creating a slight bow in risk and return.

His other issue where I find myself in disagreement is his rather over-ambitious embrace of anomalies. He had a book, the

[Incredible January Effect](http://www.amazon.com/Incredible-January-Effect-Markets-Unsolved/dp/1556238711/ref=sr_1_1?ie=UTF8&s=books&qid=1246918964&sr=1-1)

, which was a big deal in the 1980s, but you can't make money off this any more, and perhaps given transaction costs you never could. That is, much of what drives historical database anomalies are thinly traded stocks that move from $1 to $1 1/8, a massing 12.5% return, annualizing to a 3150% return! As there is a power law to stock distributions, a large proportion of stocks invariably are small and untradeable, and inferences therefrom are uninteresting.

In the early 2000's, he had a model where he ran rolling regressions on 50 or so factors, and allowed these coefficients to flip around from positive to negative. Many of the 50 factors are highly correlated (profit margin, ROE, ROA), and this causes their coefficients to have the 'wrong sign', because correlated explanatory variables tend to do this. He is vague about how he computes 'profits' in his backtests, and this can be problematic if, say, you use 1994 profits for 1995 returns, considering the '1994' fiscal year ends in June 1995 for many companies, and is released with a lag of up to 3 months. It is straightforward to account for this, but unless the author notes his explicit care for these issues, one has to assume he did not do a good job. I remember seeing his 1-10 portfolios back in 2003, and they took a nasty beating that year. A couple years later I visited

[his website](http://www.quantitativeinvestment.com/)

and it was like a Soviet history text with that drubbing wiped out of the historical record, presumably because a new model was now applied to the past.

In my experience, those who use a lot of correlated factors are overfitters, and this makes their back tests look great, their out-of-sample tests horrible. His 1996 paper argues for 3% monthly excess returns. His current model implies a similar level of outperformance (40% between the top and bottom decile, annualized). Fama and French's

[recent study](http://www.dimensional.com/famafrench/2009/06/luck-versus-skill-in-mutual-fund-performance.html)

of mutual funds finds out of thousands, the top outperformers were in the 5% annualized range, so proposing your long picks outperform the market by 25% is bat-shiat crazy talk. That is transparently overfit, like internet spam advertising 50%+ returns. It's a shame, because he does not need to overfit the data to make his basic point, but he overfits nonetheless, and overfitting is one of those predilections that few economists are immune to.