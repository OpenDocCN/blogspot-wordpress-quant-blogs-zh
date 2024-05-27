<!--yml

类别：未分类

日期：2024-05-18 15:18:03

-->

# 及时投资组合：金融动荡统计测量的优秀 FAJ 文章第二部分

> 来源：[`timelyportfolio.blogspot.com/2011/04/great-faj-article-on-statistical_26.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/04/great-faj-article-on-statistical_26.html#0001-01-01)

![faj 摘要](http://www.cfapubs.org/doi/abs/10.2469/faj.v66.n5.3)

我并不打算让这成为一个多部分系列，但在周末海滩上经过一番清晰的思考后，我决定它需要更多的分析。对于那些阅读了文章或了解[马哈拉诺比斯距离](http://en.wikipedia.org/wiki/Mahalanobis_distance)的人，我在我的帖子[金融动荡统计测量的优秀 FAJ 文章](http://timelyportfolio.blogspot.com/2011/04/great-faj-article-on-statistical.htmlhttp://timelyportfolio.blogspot.com/2011/04/great-faj-article-on-statistical.html)中呈现的度量是实际马哈拉诺比斯距离的派生物。为了弥补实际计算和我的度量之间的差距，我认为我应该展示两种计算方法。

这里的马哈拉诺比斯计算基于整个数据集。当然，在交易中我们没有后见之明的奢侈，所以我认为我的实时度量如第一篇帖子中所示的系统表现良好。

R 代码：

require(quantmod)

require(PerformanceAnalytics)

#从圣路易斯联邦储备（FRED）获取数据

getSymbols("GS20",src="FRED") #加载 20yTreasury；20 年中间有间隙 86-93；30 年中间有早期 2000 年代的间隙

getSymbols("GS30",src="FRED") #加载 30yTreasury 以填补 20y 间隙 86-93

#getSymbols("BAA",src="FRED") #加载 BAA

getSymbols("SP500",src="FRED") #加载 SP500

#从 csv 文件获取 CRB 数据

CRB<-as.xts(read.csv("crb.csv",row.names=1))[,1]

#用 30y 填补从中止的 20y 国库券中的 20 年间隙

GS20["1987-01::1993-09"]<-GS30["1987-01::1993-09"]

#进行一些操作，使数据在月度基础上排列

SP500<-to.monthly(SP500)[,4]

#将月度格式转换为 yyyy-mm-dd，以月初为准

index(SP500)<-as.Date(index(SP500))

#我的 CRB 数据是月底的；可能会改变，但在 R 中更有趣

CRB<-to.monthly(CRB)[,4]

index(CRB)<-as.Date(index(CRB))

#让我们将所有这些合并到一个 xts 对象中；CRB 最晚在 1956 年开始

assets<-na.omit(merge(GS20,SP500,CRB))

#使用 SP500 和 CRB 的 ROC，以及收益数据的动量

assetROC<-na.omit(merge(momentum(assets[,1])/100,ROC(assets[,2:3],type="discrete")))

#获取协方差并将 100000 乘以 20 年到 sp500 和 crb，以及将 1000 乘以 sp500 到 crb 以标准化

#不喜欢这种手动干预；下一篇文章将使用相关性

assetCovar<-runCov(assetROC[,1],assetROC[,2],n=2)*100000+runCov(assetROC[,1],assetROC[,3],n=2)*100000+runCov(assetROC[,2],assetROC[,3],n=2)*1000

assetROCSum<-assetROC[,1]+assetROC[,2]+assetROC[,3]

turbulence<-abs(assetCovar*assetROCSum)

Sx <- cov(assetROC)

马氏湍流 <- mahalanobis(assetROC, colMeans(assetROC), Sx)

马氏湍流<-as.xts(cbind(mahalanobisturbulence))

湍流比较<-merge(mahalanobisturbulence,turbulence)

湍流比较的列名<-c("马氏","我的估计")

时间序列图(turbulencecompare,主标题="马氏距离与我的测量比较",

颜色设置=c("军兰色","深橄榄绿 3"),图例位置="顶部左方")

相关性图(turbulencecompare)
