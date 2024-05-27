评论：/*yml

类别：未分类

日期：2024-05-18 15:17:29

*/

# 及时投资组合：使用美国农业部数据的 R 练习

> 来源：[`timelyportfolio.blogspot.com/2011/05/r-exercise-with-usda-data.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/05/r-exercise-with-usda-data.html#0001-01-01)

在 Bradley 在我的帖子[商品指数估算器](http://timelyportfolio.blogspot.com/2011/05/commodity-index-estimators.html)上的有用评论之后，

> 那么国家农业统计局（NASS）怎么样？看起来他们有很多从 1908 年以来许多农产品价格收到的信息([`www.nass.usda.gov/`](http://www.nass.usda.gov/)）。

我开始尝试在 R 中获取美国农业部的价格数据，但在三个小时的挣扎中，我未能以任何可用的格式找到从开始到结束的历史数据，没有成功。然而，我注意到了自己在 R 技能上的一些不足，所以我决定用一些美国农业部的数据来练习。美国农业部对主要美国作物的 10 年价格预测引起了我的兴趣。三个小时的挣扎让我掌握了一些新的 R 技能，并产生了以下图表和 R 代码。

以稍微更好的累计回报格式。奇怪的是，我最喜欢的绩效分析图表集返回了一个“格式”错误。

看来乳品业务可能很有吸引力。也许，我可以在那里赚钱。

这次练习的一个有益的副产品是发现了[`www.farmdoc.illinois.edu/manage/uspricehistory/USPrice.asp`](http://www.farmdoc.illinois.edu/manage/uspricehistory/USPrice.asp "http://www.farmdoc.illinois.edu/manage/uspricehistory/USPrice.asp")，它提供按月分的作物价格数据，可以是图表或表格形式。

![](img/4b31b681e9284331a180c29ed5456e0a.png)

现在我需要确定如何从美国农业部或其他地方获取这个月度价格数据，以便进行 R 研究。

此外，我还以为这篇研究文章[www.farmdoc.illinois.edu/irwin/research/EmpiricalMethodsCommodity.pdf](http://www.farmdoc.illinois.edu/irwin/research/EmpiricalMethodsCommodity.pdf)很有趣，但不符合这个目标。

R 代码：

需要(gdata)

需要(quantmod)

需要(ggplot2)

网址<-"[`usda.mannlib.cornell.edu/usda/ers/94005/2011/Table39.xls"`](http://usda.mannlib.cornell.edu/usda/ers/9

获取 Shiller 数据进行通胀和美国国债 10 年

美国农业部价格 <- read.xls(URL,"Table38"，"2009"，stringsAsFactors = FALSE)

删除有趣的信息

美国农业部价格 <- USDAprice[3:10,]

将行名更改为列 1 中的作物名称

美国农业部价格的行名<-USDAprice[,1]

删除第 1 列，因为现在有行名

美国农业部价格 <- USDAprice[,2:NCOL(USDAprice)]

确保数值数据

美国农业部价格 <- as.data.frame(data.matrix(USDAprice))

行和列切换

美国农业部价格 <- t(USDAprice)

获取稍后的 xts 版本

美国农业部价格 xts<-美国农业部价格

美国农业部价格 xts 的行名<-paste(substr(美国农业部价格的行名,2,5),rep("01-01",NROW(USDAprice)),sep = "-")

美国农业部价格 xts<-as.xts(USDApricexts)

获取行名的日期

`rownames(USDAprice)<-as.Date(paste(substr(rownames(USDAprice),2,5),rep("01-01-31",NROW(USDAprice)),sep = "-"))`

`USDApricemelt<-melt(USDAprice)`

`colnames(USDApricemelt)<-c("Date","Crop","USDA_Projected_Price")`

`ggplot(USDApricemelt, stat="identity", aes(x=Date,y=USDA_Projected_Price,colour=Crop)) + geom_line() +`

`scale_x_date(format = "%Y") +`

`opts(title = "USDA Projected Crop Prices through 2020")`

`#standardize to get cumulative return or wealth index`

`USDApricereturn<-USDApricexts/lag(USDApricexts)-1`

`USDApricereturn[1,]<-0`

`USDApricereturn<-cumprod(1+USDApricereturn)`

`#get in format that ggplot2 can use`

`USDApricereturnmelt<-cbind(as.Date(index(USDApricereturn)),coredata(USDApricereturn))`

`rownames(USDApricereturnmelt)<-USDApricereturnmelt[,1]`

`USDApricereturnmelt<-USDApricereturnmelt[,(2:NCOL(USDApricereturnmelt))]`

`USDApricereturnmelt<-melt(USDApricereturnmelt)`

`colnames(USDApricereturnmelt)<-c("Date","Crop","USDA_Projected_Cumulative_Return")`

`ggplot(USDApricereturnmelt, stat="identity", aes(x=Date,y=USDA_Projected_Cumulative_Return,colour=Crop)) + geom_line() +`

`scale_x_date(format = "%Y") +`

`opts(title = "USDA Projected Crop Price Cumulative Returns through 2020")`
