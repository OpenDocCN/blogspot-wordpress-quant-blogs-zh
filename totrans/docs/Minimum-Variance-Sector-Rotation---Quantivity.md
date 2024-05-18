<!--yml
category: 未分类
date: 2024-05-18 13:44:28
-->

# Minimum Variance Sector Rotation | Quantivity

> 来源：[https://quantivity.wordpress.com/2011/04/20/minimum-variance-sector-rotation/#0001-01-01](https://quantivity.wordpress.com/2011/04/20/minimum-variance-sector-rotation/#0001-01-01)

Numerous readers inquired how to rethink asset allocation in a world where [Portfolio Theory is Dead](https://quantivity.wordpress.com/2011/04/10/portfolio-theory-is-dead-now-what/). One approach is embracing [dynamic asset allocation](http://en.wikipedia.org/wiki/Dynamic_asset_allocation) while assuming zero risk premium, recognizing that estimating portfolio return moments via standard longitudinal time series analysis turns out to be [flawed in practice](https://quantivity.wordpress.com/2009/08/16/naive-backtesting-is-bogus/) (irregardless of robust statistical estimators). In this world, the notion of *strategic* asset allocation is *nonsense* and thus buy-and-hold investors are unknowingly gambling.

Acknowledging this trend, the historical distinction between short-term “trading” and long-term “investing” is gradually blurring. This post rethinks [sector rotation](http://en.wikipedia.org/wiki/Sector_rotation) by applying [minimum variance portfolios](https://quantivity.wordpress.com/2011/04/17/minimum-variance-portfolios/). Although Quantivity dislikes classic sector rotation as it’s both *discretionary* and *predictive*, applying minimum variance is interesting: systematic, prediction-free way to model rotation. In doing so, providing a quantitative lens to analyze rotation both *ex post* and *ex ante*.

Start with the following simple *minimum variance sector rotation* model, assuming no short sale restriction:

*   Instruments: nine sectors constituting the S&P 500, represented by their corresponding ETFs; materials, energy, financials, tech, industrial, staples, utilities, healthcare, discretionary (XLB, XLE, XLF, XLK, XLI, XLP, XLU, XLV, XLY)
*   Period: 2003 – 2010, which is interesting as it includes numerous fundamentally different market regimes, including one significant *endogenous* crash
*   Weighting: generate sector weights *once per year* on 1 Jan, based upon the preceding year of daily log returns

Note the choice of one year of daily returns is *arbitrary*, deliberately not based upon snooped or mined optimization. For easy reference, the log return performance of each sector is illustrated below:

[![](img/6c856f45ef439050dc17cdcbc3e97653.png "sector-rets")](https://quantivity.wordpress.com/wp-content/uploads/2011/04/sector-rets.png)

Given this model, begin by letting the data speak and consider two *ex post* exploratory analyses focused on visualizing the sector covariance structure. First, visualize the proportion of variance via longitudinal principal components evaluated annually over the period (again using [Ledoit-Wolf estimator](https://quantivity.wordpress.com/2011/04/17/minimum-variance-portfolios/)):

[![](img/76ea8154921b8da87501d5e81c563187.png "longitudinal-pca-decomp")](https://quantivity.wordpress.com/wp-content/uploads/2011/04/longitudinal-pca-decomp2.png)

This illustrates the primary component (labelled “Comp. 1”) is both *dominant yet fairly unstable* over the period: consistently explaining over 60% of variance, jumping nearly 20% year-over-year in 2007, and peaking at 84% in 2010\. Recall standard interpretation of the primary component as the *market component*, reflecting the common variance amongst all instruments in the “market” (*e.g.* see Tsay [2005], p. 424).

The discontinuity in 2007 implies a fairly significant *market correlation regime shift*, towards greater co-movement during and after 2007\. While this makes economic sense during 2007 – 2009 (crisis and subsequent grind down to capitulation in 2009), the continued increase in variance explained by the market component through 2010 is surprising given the steep recovery.

Second, turn attention to minimum variance and generate sector weights on an annual basis. Plot the temporal evolution of those weights over the period to see how each sector contributes to minimizing “risk” within the overall S&P 500 index at varying times during this period:

[![](img/b63aef83a749f29fa38817425a0bb200.png "annual-mv-sector-weights")](https://quantivity.wordpress.com/wp-content/uploads/2011/04/annual-mv-sector-weights.png)

Economic intuition suggests sector weights should broadly reflect macro trends, just as with principal components. Several observations provide positive corroboration:

*   Defensive sectors: stapes and healthcare (and utilities, to a lesser extent) are consistent and significant long weights, bearing out their mythology as “defensive” sectors; particularly interesting to compare with very strong post-crash performance of staples (see returns diagram above)
*   Financials: peak slightly above zero weight in 2005 and subsequently decrease to small short weights; consistent with intuition, given their central role in the financial collapse
*   Tech: negative weight coming out of post-tech bubble residual, increasing to modest long weight as the post-crash recovery accelerated in 2009 and tech helped lead the recovery
*   Energy: on a nearly linear trend downward from modest long to small short weight, arguably reflecting the increasing price volatility of oil

Consider now an *ex ante* perspective: a *minimum variance sector rotation* strategy, based upon weights calculated above. Specifically, open positions on 1 Jan which correspond to the portfolio of minimum variance weights, calculated from the previous year per the above model. Admittedly simple, this strategy remains fully-invested at all times, rebalances annually, and does not filter based upon market regime. In other words, a *simple systematic dynamic asset allocation* based on annual lookback with very low transaction costs.

Given combo of strategy simplicity and remarkably dynamic market environment, *a priori* intuition suggests performance of this strategy should be boring. The actual cumulative log returns per year are illustrated in the following graphic:

[![](img/3a0311076345c8483e981129cf6d7055.png "min-var-sector-rets")](https://quantivity.wordpress.com/wp-content/uploads/2011/04/min-var-sector-rets.png)

Next, concatenated into continuous cumulative daily returns and overlay with SPY log returns for corresponding time period:

[![](img/e9269a5143f0c1635a3fc51eec3184be.png "mvp-pl")](https://quantivity.wordpress.com/wp-content/uploads/2011/04/mvp-pl2.png)

The obligatory strategy summary statistics versus beta benchmark:

|  | MVP | SPY |
| Max drawdown    | 9.984622 % | 23.9207 % |
| Std Dev | 0.008390046 | 0.01359853 |
| Sharpe | 0.6171763 | 0.2172976 |
| Wins | 54.05559 % | 54.76731 % |
| Losses | 45.94441 % | 45.23269 % |
| Avg Win | 0.3218431 % | 0.4352086 % |
| Avg Loss | -0.2895475 % | -0.4163521 % |

In summary, performance of this strategy broadly matches aspirational intent for minimum variance portfolios: comparable performance during normal market environment, underperform during market exuberance, smaller comparative variance (*e.g.* average win/loss), higher sharpe, and significantly smaller max drawdown. All good stuff.

While hardy noteworthy, this analysis and toy strategy illustrates minimum variance portfolios applied to sector rotation do appear to trade consistent with their theoretical claims of benefit. Of course, there are many interesting avenues for improving this strategy.

* * *

For readers seeking to follow along in R, analysis and plotting code for this post are as follows:

```

require(xts)
require(tseries)
require(tawny)

# model parameters
s <- "2003-01-01"
spyS <- "2004-01-01"
e <- "2011-01-01"
q <- "AdjClose"
usEquities <- c("XLB", "XLE", "XLF", "XLK", "XLI", "XLP", "XLU", "XLV", "XLY")
usEquityNames <- c("materials", "energy", "financials", "tech", "industrial", "staples", "utilities", "healthcare", "discretionary")
colors <- c('black', 'red', 'blue', 'green', 'orange', 'purple', 'yellow', 'brown', 'pink');
usClose <- as.xts(data.frame(lapply(usEquities, get.hist.quote, start=s, end=e, quote=q)))
usRets <- xts(data.frame(lapply(log(usClose), diff)), order.by=index(usClose))[2:nrow(usClose)]
colnames(usRets) <- usEquities
spy <- get.hist.quote("SPY", start=spyS, end=e, quote=q)

# annualize trade returns and calculate MVP weights
annualNames <- array(c("2003", "2004", "2005", "2006", "2007", "2008", "2009", "2010"))
annualReturns <- do.call(rbind, sapply(annualNames, function (yr) { usRets[yr] }))
annualWeights <- t(sapply(c(1:length(annualNames)), function(i) { minvar(annualReturns[annualNames[i]]) } ))
colnames(annualWeights) <- usEquities
rownames(annualWeights) <- annualNames
annualTradeRets <- matrix(vapply(c(1:(nrow(annualNames)-1)), function (i) { r <- cumsum(annualReturns[annualNames[i+1]] %*% annualWeights[i,]); r[length(r)] }, -100))
dailyPnL <- do.call(rbind, sapply(c(1:(nrow(annualWeights)-1)), function (i) { matrix(annualReturns[annualNames[i+1]] %*% annualWeights[i,]) }))

# plot longitudinal evolution of pca component variance
pcaStds <- do.call(cbind, lapply(annualNames, function(yr) { sdev <- princomp(covmat=cov.shrink(annualReturns[yr]))$sdev; sdev^2/sum(sdev^2) }))
colnames(pcaStds) <- annualNames
pcaStdMeans <- matrix(rowMeans(pcaStds))
demeanedPcaStds <- sweep(pcaStds, 1, rowMeans(pcaStds), "-")
plot(pcaStds[1,], ylim=range(pcaStds), type='l', xaxt="n", xlab="Year", ylab="Proportion of Variance", main="Longitudinal PCA Variance Decomposition by Component")
lapply(c(2:5), function (i) { lines(pcaStds[i,], type='l', col=colors[i])})
axis(1, 1:nrow(annualNames), annualNames)
legend(.45,legend=rownames(pcaStds)[1:5], fill=c(colors[1:5]), cex=0.5)

# plot sector returns
par(mfrow=c(3,3))
sapply(c(1:(ncol(usRets))), function (i) { plot(cumsum(usRets[,i]), type='l', xlab="", ylab="Return", main=format(usEquityNames[i])) })

# plot longitudinal annual weights
plot(annualWeights[,1], ylim=range(annualWeights), type='o', ylab="Weight", xlab="Year", xaxt="n", main="Annualized Minimum Variance Sector Weights", col=colors[1])
axis(1, 1:nrow(annualWeights), rownames(annualWeights))
for (i in c(2:ncol(annualWeights))) {
lines(annualWeights[,i], col=colors[i], type='o')
}
legend(-.4,legend=usEquityNames, fill=c(colors), cex=0.5)

# plot cumulative daily returns
par(mfrow=c(3,3))
sapply(c(1:(nrow(annualWeights)-1)), function (i) { plot(cumsum(annualReturns[annualNames[i+1]] %*% annualWeights[i,]), type='l', xlab="Trading Day", ylab="Return", main=format(annualNames[i+1])) })

# plot daily PnL
cumDailyPnL <- cumsum(dailyPnL)
cumSpy <- cumsum(diff(log(coredata(spy))))
maxRange <- max(range(cumDailyPnL), range(cumSpy))
minRange <- min(range(cumDailyPnL), range(cumSpy))
plot(cumDailyPnL, type='l', xlab="Trading Day", ylab="Return", main="Annualized Minimum Variance Sector Strategy P&L", ylim=c(minRange, maxRange))
lines(cumSpy, type='l', col='red')
legend(.6,legend=c("MVP","SPY"), fill=c("black", "red"), cex=0.5)
axis(1,index(usClose))

# print strategy summary statistics
plSummary(dailyPnL)

# function to generat weights for MVP from a return series
minvar <- function(rets) {
  N <- ncol(rets)
  zeros <- array(0, dim = c(N,1))
  aMat <- t(array(1, dim = c(1,N)))
  res <- solve.QP(cov.shrink(rets), zeros, aMat, bvec=1, meq = 1)
  return (res$solution)
}

# function to pretty print strategy statistics
plSummary <-function(dailyPnL)
{
 	cumDailyPnL <- cumprod(1 + dailyPnL) - 1
	cat("Max drawdown:", (maxdrawdown(dailyPnL)$maxdrawdown * 100), "%\n")
	cat("Std dev:", sd(dailyPnL), "\n")
	cat("Sharpe:", sharpe(cumDailyPnL), "\n")
	win <- mean(ifelse(dailyPnL > 0, 1, 0))
	cat("Wins:", (win*100), "%\n")
	cat("Losses:", ((1-win)*100), "%\n")
	cat("Average Win:",(mean(ifelse(dailyPnL > 0, dailyPnL, 0)) * 100), "%\n")
	cat("Average Loss:",(mean(ifelse(dailyPnL < 0, dailyPnL, 0)) * 100), "%\n")
}

```