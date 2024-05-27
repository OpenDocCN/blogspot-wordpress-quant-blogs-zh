<!--yml

类别：未分类

日期：2024-05-18 15:17:59

-->

# 及时投资组合：关于金融动荡统计测度的伟大 FAJ 文章 第三部分

> 来源：[`timelyportfolio.blogspot.com/2011/04/great-faj-article-on-statistical_6197.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/04/great-faj-article-on-statistical_6197.html#0001-01-01)

在 [关于金融动荡统计测度的伟大 FAJ 文章](http://timelyportfolio.blogspot.com/2011/04/great-faj-article-on-statistical.html) 和 [关于金融动荡统计测度的伟大 FAJ 文章 第二部分](http://timelyportfolio.blogspot.com/2011/04/great-faj-article-on-statistical_26.html) 的基础上，我现在将建立一个系统，其中包含了一种新的基于相关性的动荡测度和一个简单的相对强度技术。首先，新的基于相关性的测度如下：

如果我们只使用这种基于相关性的动荡来建立一个系统，结果还不错。但是，如果我们再迈出一步，应用基于斜率的相对强度来选择 S&P500 或 CRB，而不是平均权重两者，我们将获得更好的结果。

我总是希望在国家和年份方面有更多的数据，但 1957 年已经相当详尽了。请告诉我您如何改进这个系统。

R 代码：

require(quantmod)

require(PerformanceAnalytics)

#从圣路易斯联邦储备银行（FRED）获取数据

getSymbols("GS20",src="FRED") #加载 20 年期国债；20 年期间存在缺失（1986-1993）；30 年期间存在缺失（2000 年代初）

getSymbols("GS30", src="FRED") #加载 30 年期国债以填补 20 年期间的空缺（1986-1993）

getSymbols("BAA", src="FRED") #加载 BAA

getSymbols("SP500",src="FRED") #加载 SP500

#从 csv 文件获取 CRB 数据

CRB <- as.xts(read.csv("crb.csv", row.names=1))[,1]

#用中断的 20 年期国债填补 20 年期间的空缺

GS20["1987-01::1993-09"] <- GS30["1987-01::1993-09"]

#进行一些操作以使数据按月对齐

SP500 <- to.monthly(SP500)[,4]

#将日期格式转换为年-月-日，并以每月的第一天表示

index(SP500) <- as.Date(index(SP500))

#我的 CRB 数据是每月末的；可以更改，但在 R 中操作更有趣

CRB <- to.monthly(CRB)[,4]

index(CRB) <- as.Date(index(CRB))

#将所有数据合并为一个 xts 对象；CRB 数据从 1956 年开始

assets <- na.omit(merge(GS20, SP500, CRB))

#使用 S&P500 和 CRB 的 ROC，以及收益数据的动量

assetROC <- na.omit(merge(momentum(assets[,1])/100,ROC(assets[,2:3],type="discrete")))

#获取相关性

corrBondsSp <- runCor(assetROC[,1], assetROC[,2], n=7)

corrBondsCrb <- runCor(assetROC[,1], assetROC[,3], n=7)

corrSpCrb <- runCor(assetROC[,2], assetROC[,3], n=7)

#资产类别之间相关性的复合测度和 ROC 加权相关性

assetCorr <- (corrBondsSp + corrBondsCrb + corrSpCrb +

(corrBondsSp * corrSpCrb * assetROC[,2]) +

(corrBondsCrb * corrSpCrb * assetROC[,3]) -

assetROC[,1]) / 6

#各资产类别的 ROC 总和

assetROCSum <- assetROC[,1] + assetROC[,2] + assetROC[,3]

#最后是动荡测度

turbulence <- abs(assetCorr * assetROCSum * 100)

colnames(turbulence) <- "动荡-相关性"

chartSeries(湍流, theme="white", name="作为金融湍流衡量标准的关联度和%变化")

abline(h=0.8)

chart.ACF(湍流, main="湍流的自相关")

# 真希望我能记住我从哪里得到一些这段代码

# 最有可能是 www.fosstrading.com

# 如果你知道来源请告知我

# 这样我可以给予适当的信用

# 使用湍流来决定进入或退出等权重的 CRB 和标普 500

信号 <- ifelse(湍流 > 0.8, 0, 1)

# 使用标普 500/CRB 的斜率来决定标普 500 或 CRB

信号 <- 延迟(信号, k=1)

# 用没有位置替换缺失的信号

# (通常在序列的开始)

信号[is.na(信号)] <- 0

# 从等权重 CRB 和标普 500 位置获取回报；Return.portfolio 出现问题，所以采取了艰难的方式

回报 <- (资产 ROC[,2]+资产 ROC[,3])/2

回报[1] <- 0

# 获取系统表现

系统表现 <- 回报 * 信号

系统等权重 <- cumprod(1 + 回报 * 信号)

表现比较 <- merge(延迟((资产 ROC[,2]+资产 ROC[,3])/2, k=1), 系统表现)

表现比较$列名 <- c("等权重", "带湍流过滤器的系统")

charts.PerformanceSummary(表现比较, ylog=TRUE, main="基于湍流的系统 vs 等权重的 CRB 和标普 500")

# 让我们用基本的相对强度来选择标普 500 或 CRB

# 知道我可以用 R 做得更好，但这是我的丑陋代码

# 计算标普 500/CRB 的 12 个月斜率

宽度=12

for (i in 1:(NROW

模型 <- lm(资产[i:(i+宽度),2]/资产[i:(i+宽度),3]~指数(资产[i:(i+宽度)]))

ifelse(i==1, 资产斜率 <- 模型$系数[2], 资产斜率 <- rbind(资产斜率, 模型$系数[2]))

}

资产斜率 <- xts(cbind(资产斜率), order.by=指数(资产)[(宽度+1):NROW(资产)])

# 使用湍流来决定进入或退出等权重的 CRB 和标普 500

信号 <- ifelse(湍流[(宽度):NROW(湍流)] > 0.8, 0, 1)

# 使用标普 500/CRB 的斜率来决定标普 500 或 CRB

信号 2 <- ifelse(资产斜率 > 0, 1, 2)

信号 <- 延迟(信号, k=1)

信号[1] <- 0

信号 2 <- 延迟(信号 2, k=1)

信号 2[1] <- 0

# 根据斜率获取标普 500 或 CRB 回报

回报 <- ifelse(信号 2 == 1, 资产 ROC[(宽度):NROW(资产 ROC),2], ifelse(信号 2 == 2, 资产 ROC[(宽度):NROW(资产 ROC),3], 0))

# 获取系统表现

系统表现 <- 回报 * 信号

系统等权重表现 <- cumprod(1 + 信号 * 回报)

表现比较 <- merge((资产 ROC[,2]+资产 ROC[,3])/2, 资产 ROC[,2], 资产 ROC[,3], 系统表现, 系统表现 RS)

表现比较$列名 <- c("等权重", "标普 500", "CRB", "带湍流过滤器的系统", "带湍流过滤器和 RS 的系统")

charts.PerformanceSummary(表现比较, ylog=TRUE, main="基于湍流的系统与 RS vs 等权重的, CRB, 和标普 500")
