<!--yml
category: 未分类
date: 2024-05-18 13:59:33
-->

# Sharpe Ratio > 1 : Careful What You Wish For – Quantum Financier

> 来源：[https://quantumfinancier.wordpress.com/2018/06/02/sharpe-ratio-1-careful-what-you-wish-for/#0001-01-01](https://quantumfinancier.wordpress.com/2018/06/02/sharpe-ratio-1-careful-what-you-wish-for/#0001-01-01)

I had the pleasure to hang out with the good folks over at [Resolve Asset Management](http://www.investresolve.com) recently. Part of our discussion centered around the differences between our two worlds. As you can imagine, prop trading is fairly different from institutional asset management. A topic of particular interest to both of us however was how to manage expectations. On their end one can imagine that in order to be successful it is important to make sure that clients have a good understanding of the range of outcomes that one should reasonably expects. In my world, it is also important to have a good idea what a trade with particular returns statistics might look like in practice.

One such performance metric one usually looks at is the Sharpe ratio ![\frac{\mu - rf}{\sigma}](img/b23f04c81a7906783cf5b133d86c0a3d.png). Now long-term readers of this blog will be familiar with my hatred of this measure, but bear with me for a moment. It is common in the asset management industry to seek Sharpe ratios greater than 1\. An out of sample ratio like that would be an excellent selling point. However I posit that most people don’t really know what trading a strategy like that will actually look and, most importantly, feel like. Let’s be honest, although we all like to try to approach the market in a perfectly emotionless manner, it is seldom the case in practice. Drawdowns are heart wrenching and are a good indicator of the mental pain you will have to experience with a strategy. On the prop side drawdowns are when you start double guessing the strategy and wonder if it no longer works while in the asset management world you experience the same, but it is also made much worse since you have to deal with client calls and redemption requests etc.

This discussing made me want to take a look at what would be statistically reasonable to experience given say a backtested strategy with a 1.0 Sharpe ratio. For this I create a dataset of 1000 samples of 252 days of daily returns averaging 25 basis points with a standard deviation of ![\sigma = \frac{.0025}{\sqrt{252}} \approx .0396](img/9a9ac8576c3648192fd2fa27d498f5e3.png). You can think of that as if you had 1000 different strategies with the mythical 1.0 Sharpe backtest. Those samples represent potential out-of-sample results a year forward.

In the plot below you can find (for a starting capital of $10,000) the individual equity curves, the distributions of terminal NAV, sharpe ratios, and finally maximum drawdown. Keep in mind here that each one of these comes from a distribution of returns that would average to a sharpe of 1\. Some of these are just miserable and would test even the most dedicated and disciplined traders. A large drawdown is far more frequent than I would have imagined. How about you?

![normdist](img/65fe3a7fef443b10f00c59caf2d508eb.png)

Furthermore, this is from assuming the strategy returns are normally distributed. If I run the same analysis using a Laplace distribution instead (also symmetrical but with significantly fatter tail in comparison) you can see below that the average sharpe still is around 1 but the outcomes are widely different. In particular note the fat right tail on the terminal NAV along with the much changed maximum drawdown distribution.

![laplacedist](img/699be1eb2ed08d78734577479f59a711.png)

The point I am trying to make is that it is critical to consider a broad range of outcomes in order to properly shape expectations. The simple analysis above shows that even if the result conforms perfectly to the simulated distribution of returns it might not be as good as you might expect. Finally, the comparison between the normal and Laplace distributions also shows that it is important to consider more than the first two moments when assessing performance as does the Sharpe ratio (or Sortino for that matter). A good alternative worth looking into is the [omega ratio](https://en.wikipedia.org/wiki/Omega_ratio) which is defined as the probability weighted ratio of gains versus losses for some threshold return target.