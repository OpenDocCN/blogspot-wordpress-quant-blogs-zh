<!--yml

类别：未分类

日期：2024 年 05 月 18 日 13:44:28

-->

# 最小方差部门轮换 | Quantivity

> 来源：[`quantivity.wordpress.com/2011/04/20/minimum-variance-sector-rotation/#0001-01-01`](https://quantivity.wordpress.com/2011/04/20/minimum-variance-sector-rotation/#0001-01-01)

许多读者询问如何在[投资组合理论已死](https://quantivity.wordpress.com/2011/04/10/portfolio-theory-is-dead-now-what/)的世界中重新思考资产配置。一种方法是采用[动态资产配置](http://en.wikipedia.org/wiki/Dynamic_asset_allocation)，同时假设零风险溢价，认识到通过标准的纵向时间序列分析估计投资组合回报时刻的方法实际上是有缺陷的（无论采用何种健壮的统计估计量）。在这个世界中，*战略性*资产配置的概念是*无意义*的，因此持有并持有的投资者是在不知不觉中赌博。

认识到这一趋势，短期“交易”和长期“投资”之间的历史区别逐渐变得模糊。这篇文章通过应用[最小方差投资组合](https://quantivity.wordpress.com/2011/04/17/minimum-variance-portfolios/)重新思考[部门轮换](http://en.wikipedia.org/wiki/Sector_rotation)。尽管 Quantivity 不喜欢经典的部门轮换，因为它既是*自由裁量的*，又是*预测性的*，但应用最小方差是有趣的：系统性、无需预测的方式来模拟轮换。通过这样做，提供了一个定量的视角来分析旋转*事后*和*事前*。

从以下简单的*最小方差部门轮换*模型开始，假设没有做空限制：

+   工具：构成标准普尔 500 指数的九个部门，分别用它们对应的 ETF 表示；材料、能源、金融、技术、工业、主食、公用事业、医疗保健、消费者（XLB，XLE，XLF，XLK，XLI，XLP，XLU，XLV，XLY）

+   时间段：2003 年至 2010 年，这段时间很有趣，因为它包括了许多根本不同的市场制度，包括一个显著的*内生*崩盘。

+   权重：每年 1 月 1 日基于前一年的每日对数收益率生成部门权重

请注意，选择一年的每日收益率是*任意*的，故意不基于窥探或挖掘的优化。为了方便参考，下面说明了每个部门的对数收益表现：

![](https://quantivity.wordpress.com/wp-content/uploads/2011/04/sector-rets.png)

鉴于这个模型，首先让数据说话，考虑两个*事后*的探索性分析，重点是可视化部门协方差结构。首先，通过每年评估的纵向主成分来可视化方差的比例（再次使用[Ledoit-Wolf 估计器](https://quantivity.wordpress.com/2011/04/17/minimum-variance-portfolios/)）：

![纵向主成分分解](https://quantivity.wordpress.com/wp-content/uploads/2011/04/longitudinal-pca-decomp2.png "longitudinal-pca-decomp")

这说明主要成分（标记为“Comp. 1”）在期间既是*主导却又相当不稳定*：一致性地解释超过 60% 的方差，在 2007 年跃升了近 20%，并在 2010 年达到顶峰 84%。回顾主要成分的标准解释为市场成分，反映了所有市场工具（*例如*参见 Tsay [2005]，第 424 页）的常见方差。

2007 年的不连续性暗示了一个相当显著的市场相关性制度转变，在 2007 年后以及 2009 年 crash 后的期间内更大程度地共同移动。虽然在 2007-2009 年期间（危机以及随后在 2009 年触底的磨底）这种转变在经济上是有道理的，但市场成分解释的方差持续增加到 2010 年是令人惊讶的，考虑到复苏的陡峭程度。

第二，将注意力转向最小方差和每年生成的行业权重。在期间内绘制这些权重的时空演变，以了解在每个时期内，各个行业如何为最小化整体 S&P 500 指数内的“风险”做出贡献：

![年度最小方差行业权重](https://quantivity.wordpress.com/wp-content/uploads/2011/04/annual-mv-sector-weights.png "annual-mv-sector-weights")

经济直觉表明，行业权重应该广泛反映宏观趋势，正如主成分一样。几个观察提供了积极的证实：

+   防御性行业：镫骨和医疗保健（以及公用事业，在一定程度上）是持续且显著的长期权重，这证实了它们作为“防御性”行业的神话；特别是与 crashes 后表现非常强劲的固定收益产品（参见上面的回报图）进行比较很有趣。

+   金融：2005 年略微超过零权重后，随后减少到小的空头权重；与他们在金融崩溃中的核心角色一致。

+   科技：由于科技泡沫残余而出现的负权重，在 2009 年 crash 复苏加速后增加到适度的长期权重，科技帮助引领复苏。

+   能源：从适度的长期权重以几乎线性的趋势向下到小的空头权重，可以说反映了石油价格波动的增加。

考虑现在一个 *ex ante* 视角：基于上述计算的权重的一个*最小方差行业轮动*策略。具体来说，在 1 月 1 日开放与最小方差权重对应的头寸，根据上一年的上述模型计算得出。承认这个策略很简单，但始终保持 fully-invested，每年重新平衡，且不根据市场制度过滤。换句话说，一个基于年度回顾且交易成本非常低的*简单系统动态资产配置*。

考虑到策略的简单性和市场的动态性，先验直觉表明这个策略的表现应该是平淡无奇的。下面图表中展示了每年的累积对数收益：

![](https://quantivity.wordpress.com/wp-content/uploads/2011/04/min-var-sector-rets.png)

接下来，将它们连续累积的日收益叠加到相应时期的 SPY 对数收益上：

![](https://quantivity.wordpress.com/wp-content/uploads/2011/04/mvp-pl2.png)

相对于贝塔基准的强制性策略总结统计数据：

|  | MVP | SPY |
| --- | --- | --- |
| 最大回撤 | 9.984622 % | 23.9207 % |
| 标准差 | 0.008390046 | 0.01359853 |
| 夏普比率 | 0.6171763 | 0.2172976 |
| 胜利 | 54.05559 % | 54.76731 % |
| 损失 | 45.94441 % | 45.23269 % |
| 平均胜利 | 0.3218431 % | 0.4352086 % |
| 平均损失 | -0.2895475 % | -0.4163521 % |

总结来说，此策略的表现与最小方差投资组合的期望目标大致相符：在正常市场环境中表现相当，市场过热时表现不佳，相对波动(*例如*平均赢/亏)，夏普比率更高，且最大回撤显著更小。这些都是优点。

虽然这分析和小策略并不是特别值得注意，但它们确实表明将最小方差投资组合应用于板块轮动确实与他们理论上的好处一致。当然，有许多有趣的途径可以改进这个策略。

* * *

对于希望跟随 R 语言的读者，本篇文章的分析及绘图代码如下：

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
pcaStds <- do.call(cbind, lapply(annualNames, function(yr) { sdev <- princomp(covmat=cov.shrink(annualReturns[yr]))$sdev; sdev²/sum(sdev²) }))
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
