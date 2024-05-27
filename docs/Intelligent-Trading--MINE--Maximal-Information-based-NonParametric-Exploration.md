```yml

分类：未分类

日期：2024-05-18 04:44:21

```

# Intelligent Trading: MINE: Maximal Information-based NonParametric Exploration

> 来源：[`intelligenttradingtech.blogspot.com/2012/01/there-was-lot-of-buzz-in-blogosphere-as.html#0001-01-01`](http://intelligenttradingtech.blogspot.com/2012/01/there-was-lot-of-buzz-in-blogosphere-as.html#0001-01-01)

博客圈和科学界对一类新算法产生了很大关注，这类算法能够在大数据集上找到非线性关系。其特别有用之处在于，所使用的度量基于互信息，而不是基于标准皮尔逊相关系数的度量，后者不能很好地捕捉非线性关系。

（基于 Java 的）软件可以在此处下载：http://www.exploredata.net/ 此外，软件还有直接从 R 运行的能力。

图 1. 由跨市场关系示例的典型非线性关系。

算法似乎很有希望，因为它将允许我们可能挖掘非常大的数据集（如金融跨市场关系），并找到可能具有意义的非线性关系。如果我们使用典型的皮尔逊相关系数衡量，这种关系将显示出非常小的 R² 值，因此被视为不显著的关系。

我决定在一个非线性示例上尝试一下，该示例来自 M. Katsanos 的《跨市场交易策略》一书（第 25 页，图 2.3）。在图 1 中，我们可以清楚地看到市场之间的关系是非线性的，因此传统的线性拟合返回了一个低 R² 值 of .143（红线），也展示了蓝色的局部加权回归拟合。在将相同数据通过 MINE 处理后，结果以 .csv 文件返回...

MIC    （强度）   MIC-p²  （非线性度）

0.16691002    0.62445      7.129283    -0.3777441

`.167` 的 MIC（互信息系数）并不比上面提到的 .143 的 R² 度量高很多。然而，论文中提到的一个提及是，随着信号被噪声更多地模糊，MIC 将相应地退化。

下一步将是寻找某种类型的拟合，以最小化噪声成分并进行更新比较。

为了更好地说明它可能有多么有用，我在这里附上参考资料的屏幕截图。

图 2. 来自 'www.sciencemag.org/cgi/content/full/334/6062/1518/DC1' 的 Fig 6 复制

请注意，MIC 评分度量在许多非线性结构关系上超过了其他传统方法。

以下是完整 R 代码以重复基本实验。

###############################################

# MINE 示例来自 intelligenttradingtech.blogspot.com 1/31/2012

`library(quantmod)`

`library(ggplot2)`

`getSymbols('^GSPC', src = 'yahoo', from = '1992-01-07', to = '2007-12-31')`

`getSymbols('^N225', src = 'yahoo', from = '1992-01-07', to = '2007-12-31')`

`sym_frame` <- merge(GSPC[, 6], N225[, 6], all = FALSE)

`names(sym_frame)` <- c('GSPC', 'N225')

`p<-qplot(N225, GSPC, data=data.frame(coredata(sym_frame)),`

`geom=c('point'), xlab='NIKKEI',ylab='S&P_500',main='S&P500 对 NIKKEI 1992-2007')`

`fit<-lm(GSPC~ N225, data=data.frame(coredata(sym_frame)))`

`summary(fit)`

`fitParam<-coef(fit)`

`p+geom_abline(intercept=fitParam[1], slope=fitParam[2],colour='red',size=2)+geom_smooth(method='loess',size=2,colour='blue')`

### `MINE` 结果

`library("rJava")`

`setwd('/home/self/Desktop/MINE/')`

`write.csv(data.frame(coredata(sym_frame)),file="GSPC_N225.csv",row.names=FALSE)`

`source("MINE.r")`

`MINE("GSPC_N225.csv","all.pairs")`

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

参考的论文是，“在大数据集中检测新关联”

大卫·N·雷舍夫，等人

《科学》 334, 1518 (2011)

顺便说一下，我一直沉迷于一部情景喜剧，叫《数字追凶》，在亚马逊 Prime 上播放。这是关于一名 FBI 特工从他的天才兄弟那里获得帮助的故事，他是一位知名大学的数学教授。到目前为止，他们讨论了马尔可夫链、贝叶斯统计、数据挖掘、计量经济学、热图以及一系列其他类似的概念，这些概念应用于法医学。
