<!--yml

类别：未分类

日期：2024-05-18 15:15:16

-->

# 及时投资组合：美国经济状态的年度回报

> 来源：[`timelyportfolio.blogspot.com/2011/06/annual-returns-by-state-of-us-economy.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/06/annual-returns-by-state-of-us-economy.html#0001-01-01)

有时候仅仅查看年度回报也是有趣的，特别是当金融世界将关注点转移到微秒级的世界，面对不可思议的宏观失衡时。 [圣路易斯联邦储备银行(USREC)](http://research.stlouisfed.org/fred2)提供了经济状态的二进制表示，其中 1=衰退，0=扩张，但我们所有人都必须记住，经济周期的开始和结束日期的指定会有 1 到 2 年的滞后，因此即使按月度水平也无法用于实时交易。然而，由于上一年的经济状态，我们可能能够检查年度股本回报率。借助一点 ggplot2，我认为很多人会对自 1921 年以来道琼斯工业平均指数的年度回报感到惊讶。在衰退期间，市场要么非常正确，要么非常错误。在最后一张图表中，我的想法是，除非我们看到持续超过 1 年的衰退，否则股票不会再次变得便宜。

对于商业周期阶段的资产类别回报，有一篇非常好的文章[《2006 年 3 月/4 月金融分析师杂志》中的《商品期货的战略和战术价值》](http://www.cfapubs.org/doi/abs/10.2469/faj.v62.n2.4084)，展示了以下图表，遗憾的是我无法复制。

R 代码：

```
#explore relationships of best years in US Stocks
#and recessions   require(quantmod)
require(ggplot2)
require(PerformanceAnalytics)
```

```
getSymbols("DJIA",src="FRED")  #get Dow Jones Industrials
getSymbols("USREC",src="FRED") #get US Recession(1)/Expansion(0)   
```

```
DJIA <- to.yearly(DJIA)[,4]
USREC <- to.yearly(USREC)[,4]   
```

```
#align dates as 12-31 of each year
#probably better way to do this but it works
index(DJIA) <- as.Date(paste(
	format(index(DJIA),"%Y-%m"),rep("-31",NROW(DJIA)),sep=""))
index(USREC) <- as.Date(paste(
	format(index(USREC),"%Y-%m"),rep("-31",NROW(USREC)),sep=""))     
```

```
stocks_economy <- na.omit(merge(
	lag(USREC,k=1),ROC(DJIA,n=1,type="discrete")))   
```

```
#I really like the boxplot by range, so let's do the same here
df <- as.data.frame(cbind(index(stocks_economy),
	coredata(stocks_economy)))
colnames(df) <- c("date","economy","DJIAreturn")
ggplot(df,aes(factor(economy),DJIAreturn)) +
	geom_boxplot(aes(colour = factor(economy))) +
	opts(title="Box Plot of DJIA Yearly Change by State of Economy Previous Year (recession=1)")     
```

```
m <- ggplot(df, aes(DJIAreturn, colour=factor(economy)) )
m + geom_density(size=1,aes(y = ..scaled..)) +
	opts(title="Density Plot of DJIA Yearly Change by State of Economy Previous Year (recession=1)")     
```

```
m <- ggplot(df, aes(y=DJIAreturn, x=factor(economy)) )
m + geom_point() + geom_rug() +
	opts(title="Marginal Rug Plot of DJIA Yearly Change by State of Economy Previous Year (recession=1)")     
```

```
chartSeries(runSum(USREC,n=10),theme="white",
	name="Years in Recession by Decade")
```

【由 Pretty R 在 inside-R.org 创建】(http://www.inside-r.org/pretty-r "由 Pretty R 在 inside-R.org 创建")
