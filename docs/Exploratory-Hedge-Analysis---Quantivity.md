<!--yml

category: 未分类

date: 2024-05-18 13:47:42

-->

# 探索性对冲分析 | 量化

> 来源：[`quantivity.wordpress.com/2011/10/22/exploratory-proxy-cross-hedge-analysis/#0001-01-01`](https://quantivity.wordpress.com/2011/10/22/exploratory-proxy-cross-hedge-analysis/#0001-01-01)

关于实证[分位数](https://quantivity.wordpress.com/2011/10/03/empirical-quantiles-proxy-cross-hedging-selection)和[库普拉](https://quantivity.wordpress.com/2011/10/10/empirical-copulas-and-proxy-cross-hedge-basis-risk/)的先前帖子对[代理 / 交叉对冲](https://quantivity.wordpress.com/2011/10/02/proxy-cross-hedging)进行了图形可视化的潜在见解。本文延续了这一主题，使用经典统计技术说明了*代理对冲的探索性数据分析*。

在一个充斥着象征性模型的世界中，在金融领域有充分的空间进行图形探索性分析，因为现实世界的细微纹理与数学形式主义和标准心理模型都不同。实际上，α 值隐藏在模型和现实之间的*分歧*中。

统计学家[约翰·图基](http://en.wikipedia.org/wiki/John_Tukey)是最著名的[探索性数据分析](http://en.wikipedia.org/wiki/Exploratory_Data_Analysis)倡导者之一，他在 1977 年的[同名书籍](http://books.google.com/books?id=UT9dAAAAIAAJ&q)中对此进行了描述。图基在他的书的开篇章中很好地捕捉了探索性分析的本质（第 1 页）：

> 探索性数据分析是侦探工作——数值侦探工作——或计数侦探工作——或图形侦探工作。

本文说明了使用 R 进行图形探索分析，特别是针对之前帖子中的代理对冲：知名科技公司和 QQQ。虽然专注于特定股票，但这些分析技术*适用于其他股票和更高频率*。

从过去 5 年的每日价格和收益率的散点图开始，重叠了适配的 OLS 和离散度椭圆图：

![](https://quantivity.wordpress.com/wp-content/uploads/2011/10/explore-proxy-scatters1.png)

左上图说明了几个不同的价格模式。右上图说明了大量收益率远超离散度椭圆图，与之前的帖子一致。左下图说明了按符号拆分的收益率，展示了正收益和非负收益之间拟合的分歧。右下图说明了收益率在 0.5 标准差以上和以下的分歧，其拟合非常相似。

接下来，对 CRM 的滞后散点图：

![](https://quantivity.wordpress.com/wp-content/uploads/2011/10/explore-crm-return-lags.png)

描述了在所有滞后期间尾部呈现出适度非球形回报，与之前帖子中讨论的分位数一致。QQQ 表现出类似的非球形滞后回报，尽管形状与 CRM 不一致：

![](https://quantivity.wordpress.com/wp-content/uploads/2011/10/explore-qqq-return-lags.png)

为了更深入地了解收益动态，以下图表考虑了经验密度、绝对交叉相关性、差异比率和离散变化率：

![探索性代理回报](https://quantivity.wordpress.com/wp-content/uploads/2011/10/explore-proxy-returns1.png)

左上角的图是比较*过度峰度*的教科书风格插图，其中 CRM 回报尾部延伸至+/- 10%。右上角图中的交叉相关性展示了绝对回报的前向和后向线性依赖，与前文关于自回归估计的帖子一致。左下角的差异比率图说明了经验性贝塔范围从 1 到*几百*，无论是日度、周度还是月度测量回报都是如此——*这证实了使用线性工具进行代理套期保值的困难性*。这些比率提供了第一个证据，即 2010 年末也许对这对货币甚至比 2008 年更异常，这相当引人注目。最后，右下角插图说明了回报 ROC 的进一步对比，因为 CRM 和 QQQ 的 ROC 在 2008 年比 2010 年要高得多。

最后，可视化*滚动*代理方差比率（不要与下面探讨的标准统计方差比率混淆）和样本期间不同持续时间的相关性：

![滚动探索性代理](https://quantivity.wordpress.com/wp-content/uploads/2011/10/explore-proxy-rolling.png)

或许最有趣的是顶部图表，它例示了所有滚动期间方差比率（VR）在 2010 年 8 月开始的 12 个月内均达到最大值。将这些比率与*金融危机期间几乎平坦的各种持续时间的 VR 对比一下*。底部图表提供了这种比较行为的一个维度洞见，说明了在这两个时期代理相关性的反向行为：相关性在金融危机期间最大化，在 2010/2011 年最小化。

两个图表都展示了另一个有趣的效应，即*时间尺度行为*：随着滞后窗口的增加，相关性呈现*单调平滑*（概念上类似于低通滤波）的现象，正如相关性随着黑色（每日）、红色（双周）、蓝色（每月）和绿色（每季度）而逐渐减小。相比之下，滚动方差比率没有这样的尺度（单调或非单调）效应。例如，2007 年初的 60 天 VR *显著地* 超过了所有时期。类似地，每月的 VR 经常超过了双周的 VR。

最后，考虑对 CRM（顶部图）和 QQQ（底部图）进行经典非标准化方差比率的计算，使用*整个 5 年样本期间*，这说明了均值回归与趋势性（由[Lo and Mackinlay (1998)](http://press.princeton.edu/books/lo/chapt2.pdf)导致）：

![探索性代理方差比率](https://quantivity.wordpress.com/wp-content/uploads/2011/10/explore-proxy-vr.png)

两者都表现出类似的定性行为：在持有期小于 30 天时强烈的均值回归，随后在较长时期内回归较弱。方差比率分析值得进一步考虑，特别是更丰富的图形技术（*例如* [Lindemann *et al.* (2004)](http://www.ljmu.ac.uk/AFE/AFE_docs/VR_AND_REGR.PDF)）和多变量方法。

* * *

生成前述探索性对冲分析的 R 代码：

```

require("tseries")
require("vrtest")
require("fSeries")

colors <- c('black', 'red', 'blue', 'green', 'orange', 'purple', 'yellow', 'brown', 'pink', 'coral', 'cyan', 'darkgreen', 'darkred' ,'darkblue', 'darkgrey');

exploreProxyHedge <- function(p, doMonthlyScatter=TRUE, freq="daily", doQuantilePlots=TRUE)
{
  # Plot various proxy hedge exploratory analysis.
  #
  # Args:
  #   p: matrix of instrument price data, including valid colnames
  #   doMonthlyScatter: flag indicating whether monthly scatter should
  #           be plotted
  #   freq: text string for frequency, used for graphing
  #   doQuantilePlots: flag indicating whether quantiles should be plotted
  #
  # Returns: None

  oldpar <- par(mfrow=c(2,2))

  # discrete first differences (not logged)
  pROC <- ROC(p, type="discrete", na.pad=FALSE)
  p1ROC <- ROC(p[,1], type="discrete", na.pad=FALSE)
  p2ROC <- ROC(p[,2], type="discrete", na.pad=FALSE)

  # scatter analysis
  plot(coredata(p[,2]), coredata(p[,1]), xlab=colnames(p)[2], ylab=colnames(p)[1], main="Prices")
  plm <- lm(p[,1] ~ p[,2])
  abline(plm, col=colors[2], lty=2)
  mtext(text=paste("slope=",plm$coefficients[2]), side=3, cex=0.75, col=colors[2])

  plot(coredata(p1ROC), coredata(p2ROC), xlab=colnames(p)[2], ylab=colnames(p)[1], main="Returns")
  rlm <- lm(p1ROC ~ p2ROC)
  abline(rlm, col=colors[2], lty=2)
    par(xpd=TRUE)
    d <- dataEllipse(as.vector(coredata(p1ROC)),as.vector(coredata(p2ROC)),draw=FALSE)
    lines(d[[1]], col=colors[2], lty=3)
    lines(d[[2]], col=colors[3], lty=3)
    par(xpd=FALSE)
  mtext(text=paste("slope=",rlm$coefficients[2]), side=3, cex=0.75, col=colors[2])

  # split positive/negative scatter analysis
  plot(coredata(p2ROC[(coredata(p1ROC)>0)]), coredata(p1ROC[(coredata(p1ROC)>0)]), xlab=colnames(p)[2], ylab=paste(colnames(p)[1], "(Positive Only)"), xlim=c(min(p2ROC),max(p2ROC)), ylim=c(min(p1ROC),max(p1ROC)), main="Split Sign Return Scatter")
  prlm <- lm(coredata(p1ROC[(coredata(p1ROC)>0)]) ~ coredata(p2ROC[(coredata(p1ROC)>0)]))
  abline(prlm, col=colors[1], lty=2)
  points(coredata(p2ROC[(coredata(p1ROC)<0)]), coredata(p1ROC[(coredata(p1ROC)<0)]), xlab=colnames(p)[2], ylab=paste(colnames(p)[1], "(Negative Only)"), col='red')
  nrlm <- lm(coredata(p1ROC[(coredata(p1ROC)<0)]) ~ coredata(p2ROC[(coredata(p1ROC)<0)]))
  abline(nrlm, col=colors[2], lty=2)
  abline(rlm, col=colors[3], lty=2)
  legend("topleft",legend=c("Positive", "Negative", "Both"), fill=colors, cex=0.5)

  # split magnitude scatter analysis
  magBound <- sd(p1ROC) / 2
  plot(coredata(p2ROC[(abs(coredata(p2ROC))>=magBound)]), coredata(p1ROC[(abs(coredata(p2ROC))>=magBound)]), xlab=colnames(p)[2], ylab=paste(colnames(p)[1], "(Positive Only)"), xlim=c(min(p2ROC),max(p2ROC)), ylim=c(min(p1ROC),max(p1ROC)), main="Split Magnitude Return Scatter (0.5 SD)")
  orlm <- lm(coredata(p1ROC[(abs(coredata(p2ROC))>=magBound)]) ~ coredata(p2ROC[(abs(coredata(p2ROC))>=magBound)]))
  abline(orlm, lty=2)
  points(coredata(p2ROC[(abs(coredata(p2ROC))<magBound)]), coredata(p1ROC[(abs(coredata(p2ROC))<magBound)]), xlab=colnames(p)[2], ylab=paste(colnames(p)[1], "(Positive Only)"), xlim=c(min(p2ROC),max(p2ROC)), ylim=c(min(p1ROC),max(p1ROC)), main="Split Magnitude Return Scatter", col=colors[2])
  irlm <- lm(coredata(p1ROC[(abs(coredata(p2ROC))<magBound)]) ~ coredata(p2ROC[(abs(coredata(p2ROC))<magBound)]))
  abline(irlm, lty=2, col=colors[2])
  legend("topleft", legend=c("Outer", "Inner (+/- 0.5 SD)"), fill=colors, cex=0.5)

  # monthly scatter analysis
  if (doMonthlyScatter)
  {
    plot(coredata(xts(p)["2011-05"][,2]), coredata(xts(p)["2011-05"][,1]), ylim=c(min(p[,1]),max(p[,1])), xlim=c(min(p[,2]),max(p[,2])), col=colors[1], xlab=colnames(p)[2], ylab=colnames(p)[1], main="Prices by Month")
    points(coredata(xts(p)["2011-06"][,2]), coredata(xts(p)["2011-06"][,1]), col=colors[2])
    points(coredata(xts(p)["2011-07"][,2]), coredata(xts(p)["2011-07"][,1]), col=colors[3])
    points(coredata(xts(p)["2011-08"][,2]), coredata(xts(p)["2011-08"][,1]), col=colors[4])
    points(coredata(xts(p)["2011-09"][,2]), coredata(xts(p)["2011-09"][,1]), col=colors[5])
    points(coredata(xts(p)["2011-10"][,2]), coredata(xts(p)["2011-10"][,1]), col=colors[6])
    legend("topleft", legend=c("05", "06", "07", "08", "09", "10"), fill=colors, cex=0.5)
    abline(lm(coredata(xts(p)["2011-05"][,1]) ~ coredata(xts(p)["2011-05"][,2])), col=colors[1], lty=2)
    abline(lm(coredata(xts(p)["2011-06"][,1]) ~ coredata(xts(p)["2011-06"][,2])), col=colors[2], lty=2)
    abline(lm(coredata(xts(p)["2011-07"][,1]) ~ coredata(xts(p)["2011-07"][,2])), col=colors[3], lty=2)
    abline(lm(coredata(xts(p)["2011-08"][,1]) ~ coredata(xts(p)["2011-08"][,2])), col=colors[4], lty=2)
    abline(lm(coredata(xts(p)["2011-09"][,1]) ~ coredata(xts(p)["2011-09"][,2])), col=colors[5], lty=2)
  }

  # quantile plots
  if (doQuantilePlots)
  {
    qqplot(coredata(p2ROC), coredata(p1ROC), xlab=paste(colnames(p)[2], "Returns Quantiles"), ylab=paste(colnames(p)[1], "Returns Quantiles"), main="Empirical Returns QQ-Plot")
    abline(0,1,lty=2)
    grid(20)
    par(xpd=TRUE)
    d <- dataEllipse(as.vector(coredata(p1ROC)),as.vector(coredata(p2ROC)),draw=FALSE)
    lines(d[[1]], col=colors[2], lty=3)
    lines(d[[2]], col=colors[3], lty=3)
    par(xpd=FALSE)
  }

  # Price lag dependence
  lag.plot(p1ROC, 9, do.lines=FALSE, main=paste(colnames(p)[1], "Returns Lag Auto Dependence"))

  lag.plot(p2ROC, 9, do.lines=FALSE, main=paste(colnames(p)[2], "Returns Lag Auto Dependence"))

  par(mfrow=c(2,2))

  # return distributions
  p1Density <- density(p1ROC)
  p2Density <- density(p2ROC)

  plot(p1Density, ylim=c(0, max(p1Density$y, p2Density$y)), main="Return Distribution With Median")
  lines(p2Density, col=colors[2])
  abline(v=median(p1ROC), lty=2)
  abline(v=median(p2ROC), col=colors[2], lty=2)
  legend("topleft", legend=colnames(p), fill=colors, cex=0.5)

  # cross correlation
  ccf(data.frame(abs(coredata(p1ROC))), data.frame(abs(coredata(p2ROC))), main="Absolute Return Cross Correlation")

  # diff ratio analysis (exclude periods with zero return QQQ)
  p1NoZeros <- diff(p[(p[,2] != 0),])
  p5NoZeros <- diff(p, lag=5)
  p5NoZeros <- p5NoZeros[(p5NoZeros[,2] != 0),]
  p22NoZeros <- diff(p, lag=22)
  p22NoZeros <- p22NoZeros[(p22NoZeros[,2] != 0),]

  diff1Ratio <- p1NoZeros[,1] / p1NoZeros[,2]
  diff5Ratio <- p5NoZeros[,1] / p5NoZeros[,2]
  diff22Ratio <- p22NoZeros[,1] / p22NoZeros[,2]

  plot(diff22Ratio, main="Difference Ratios", ylab="Diff Ratio", xlab="")
  lines(diff5Ratio, col=colors[2])
  lines(diff1Ratio, col=colors[3])            
  legend("topright", legend=c("lag-22", "lag-5", "lag-1"), fill=colors, cex=0.5)

  # ROC analysis
  plot(xts(p1ROC), ylab="ROC", xlab="", main="Return Rate of Change")
  lines(xts(p2ROC), col=colors[2])
  legend("topleft", legend=colnames(p), fill=colors, cex=0.5)

  # variance ratio analysis
  vratio <- sd(p[,1]) / sd(p[,2])
  cat(paste("variance ratio:", round(vratio,2)),"\n")

  vRatio5 <- rollingVarianceRatio(p,5)
  vRatio10 <- rollingVarianceRatio(p,10)

  np <- nrow(p)
  vRatio22 <- c()
  vRatio60 <- c()
  if (np > 22)
  {
    vRatio22 <- rollingVarianceRatio(p,22)
    if (np > 60)
    {
      vRatio60 <- rollingVarianceRatio(p,60)
    }
  }

  par(mfrow=c(2,1))
  plot(vRatio5, type='l', xlab="", ylab="VR", main="Rolling Variance Ratio", ylim=c(min(vRatio5, vRatio10,vRatio22,vRatio60), max(vRatio5, vRatio10,vRatio22,vRatio60)))
  lines(vRatio10, col=colors[2])

  if (np > 22)
  {
    lines(vRatio22, col=colors[3])
    if(np > 60)
    {
      lines(vRatio60, col=colors[4])
    }
  }
  legend("topleft", legend=c("5", "10", "22", "60"), fill=colors, cex=0.5)

  # correlation analysis
  vCorr5 <- rollingCorrelation(pROC, 5)
  vCorr10 <- rollingCorrelation(pROC, 10)

  vCorr22 <- c()
  vCorr60 <- c()
  if (np > 22)
  {
    vCorr22 <- rollingCorrelation(pROC, 22)
    if (np > 60)
    {
      vCorr60 <- rollingCorrelation(pROC, 60)
    }
  }

  plot(vCorr5, type='l', xlab="", ylab="Correlation", main="Rolling Correlation", ylim=c(min(vCorr5, vCorr10,vCorr22,vCorr60), max(vCorr5, vCorr10,vCorr22,vCorr60)))
  lines(vCorr10, col=colors[2])

  if (np > 22)
  {
    lines(vCorr22, col=colors[3])
    if (np > 60)
    {
      lines(vCorr60, col=colors[4])
    }
  }
  legend("topleft", legend=c("5", "10", "22", "60"), fill=colors, cex=0.5)

  # classic variance ratios (unstandardized)
  VR.plot(p1ROC,60)
  VR.plot(p2ROC,60)

  par(oldpar)
}

rollingVarianceRatio <- function(p, winLen)
{
  # Calculate rolling variance ratio with a given window length
  #
  # Args:
  #   p: matrix of instrument price data, including valid colnames
  #   winLen: length of window over which to calculate variance
  #
  # Returns: xts of rolling variance ratio

  return (xts(sapply(c(1:(nrow(p)-winLen)), function(i) { sd(p[i:(i+winLen),1]) / sd(p[i:(i+winLen),2]) }), order.by=index(p[((winLen+1):nrow(p)),])))
}

rollingCorrelation <- function(p, winLen)
{
  # Calculate rolling correlation with a given window length
  #
  # Args:
  #   p: matrix of instrument price data, including valid colnames
  #   winLen: length of window over which to calculate correlation
  #
  # Returns: xts of rolling correlation

  return (xts(sapply(c(1:(nrow(p)-winLen)), function(i) { cor(p[i:(i+winLen)], method="kendall")[2,1] }), order.by=index(p[((winLen+1):nrow(p)),])))
}

```
