<!--yml
category: 未分类
date: 2024-05-18 14:04:34
-->

# Volatility Distribution Analysis – Quantum Financier

> 来源：[https://quantumfinancier.wordpress.com/2010/08/11/volatility-distribution-analysis/#0001-01-01](https://quantumfinancier.wordpress.com/2010/08/11/volatility-distribution-analysis/#0001-01-01)

It’s been a long time since the Quantum Financier blog saw any action but today I am back (not home yet but back on the blogosphere nonetheless!). Today’s post will focus on the distribution of volatility and of the volatility of volatility in an attempt to examine which one is more stable. The implication of results here can tie nicely into CSS’s recent post [Random Regime Musing](http://cssanalytics.wordpress.com/2010/08/04/random-regime-musings/); I recommend you read it if you haven’t yet.

In the post David reach the following conclusion: *“by using forward [volatility] estimates we can respond more quickly to changes in volatility and how they will impact our mean-reversion strategies”*. Then a new very interesting blogging geek, [The Quanting Dutchman](http://quantingdutchman.wordpress.com/) commented suggesting that volatility of volatility is usually more predictable. The conversation grabbed my interest and I thought I would put the idea to the test. The following statistics are a comparison between the distribution of the volatility and of the volatility of volatility for different sample size and a visual comparison on the 500 bars time frame.

[![](img/59b36f360ebaaa486af6dfc3d96405d9.png "volatility analysis")](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/08/volatility-analysis.png)

Volatility

[![](img/889838089dc9a58b7d78bf59f4cca8f5.png "volatility analysis - vol")](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/08/volatility-analysis-vol.png)

Volatility of volatility

[![](img/f90dd10344fa528e3acadf3a50bfb751.png "volatility analysis - volofvol")](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/08/volatility-analysis-volofvol.png)

The numbers seem to confirm the theory, the distribution of the volatility of volatility seems to be more stable than that of simple volatility overall. From here, one can wonder if the added predictability can transfer to improved regime identification. The idea is appealing and will be discussed in a future post, we will also look at how concretely use this information and incorporate it into a trading strategy. You may find that I keep my analysis very shallow. Rest assured, the subject will come back on the blog in the coming week, I want to dig deeper into the phenomenon; more on this to come…

QF