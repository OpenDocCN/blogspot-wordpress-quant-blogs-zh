<!--yml
category: 未分类
date: 2024-05-12 20:02:11
-->

# Falkenblog: AQR's Quality at a Reasonable Price

> 来源：[http://falkenblog.blogspot.com/2013/08/aqrs-quality-at-reasonable-price.html#0001-01-01](http://falkenblog.blogspot.com/2013/08/aqrs-quality-at-reasonable-price.html#0001-01-01)

Our intrepid equity researchers at AQR have come out with a new paper adding to the color on how to pick a strategy given value considerations.  In Asness, Frazzini and Pedersen's latest paper,

[Quality Minus Junk](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=2312432)

, they first try to create a 'quality' metric, and then try to meld it with value.

Quality is defined very clearly as the composite of 4 factors (each of which is made up of 3-5 ratios):

*   Profitability (eg, Net Income/Assets)
*   Growth (eg, change in Profitability)
*   Safety (eg, volatility, leverage)
*   Payout (eg, equity issuance, dividend payout)

They find that

1) Stocks with higher 'quality' have higher market/book ratios (higher price

*ceteris paribus*

)

2) A long-short portfolio, where one goes long high quality, short low quality, generates significant, positive excess and total returns

They assert that a value-quality portfolio that tries to balance quality with value has nice properties, and the Sharpe maximizing combination is about 70% quality, 30% value.  This is coming from Asness, who is a pretty big value proponent, so I think this is rather telling (value losing it's pre-eminence!).

Their quality metric has a kitchen-sink aspect to it, with about 20 ratios that go into those 4 different groupings.  I could imagine many people would find this an attractive framework to develop and tweak their own quality metric, substituting for various ratios, or subtle changes to the functional form.  Haugen and Baker's (2008)

[Case Closed](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1306523)

, and Zack's

[Handbook of Investment Anomalies](http://www.amazon.com/Handbook-Equity-Market-Anomalies-Inefficiencies/dp/0470905905)

are good places to look for alternative ratios.

I would like to see how this QMJ factor compares to Analytic Investor's

[Volatile Minus Stable](http://www.iijournals.com/doi/abs/10.3905/jpm.2010.36.2.052)

(VMS) factor...they seem similar, though obviously 1) they are negatively correlated and 2) the VMS factor is simply a vol factor, which is just one part of the 'quality' metric.

Lastly, I love the little note at the end:

> Our results present an important puzzle for asset pricing: We cannot tie the returns of quality to risk

By construction their return-generating metric seems patently 'anti-risk', as quality implies 'low risk'. The risk-begets-return theory obviously has a lot of intuition, because empirically it's counterfactual when not irrelevant.  I think if you divided the data described by asset pricing theory into 'puzzles' and 'consistent', it's mainly puzzles.