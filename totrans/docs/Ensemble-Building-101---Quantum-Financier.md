<!--yml
category: 未分类
date: 2024-05-18 14:00:26
-->

# Ensemble Building 101 – Quantum Financier

> 来源：[https://quantumfinancier.wordpress.com/2011/07/01/ensemble-building-101/#0001-01-01](https://quantumfinancier.wordpress.com/2011/07/01/ensemble-building-101/#0001-01-01)

In continuation with last post, I will be looking at building a robust ensemble for the S&P 500 ETF and mini-sized future. The goal here will be to set-up a nice framework that will be (hopefully) of good use for readers interested in combining systems in creating strategies. In order to make it more tangible, I want to create a simplified example that will be used as we move forward in development. I would encourage readers to actively comment and contribute to the whole process.

Before we do anything, as with any project, I want to have an idea of the scope so I don’t get entangled in an infinite loop of development where I am never satisfied and continuously trying to replace indicator after indicator for a marginal increase in CAGR on the backtest. For this example, I want to use 4 indicators (two with a momentum flavour and two with a mean-reversion flavour), a volatility filter and an environmental filter. The strategy will also have an adaptive layer to it.

Now that the foundation idea has been laid, let’s examine the mechanics at a high level, keep in mind that this is only one way you could about it. Basically I will be evaluating each strategy individually, looking at performance under different volatility environment and also with the global environment filter. Based on historical performance and current environment, exposure will be determined.

This series will have R code for the backtest (still debating using quanstrat/blotter) and the simple example will be available for download. My point is to provide reader a way to replicate results and extend the framework significantly. More to follow!

QF