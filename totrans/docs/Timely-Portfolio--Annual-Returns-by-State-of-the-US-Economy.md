<!--yml
category: 未分类
date: 2024-05-18 15:15:16
-->

# Timely Portfolio: Annual Returns by State of the US Economy

> 来源：[http://timelyportfolio.blogspot.com/2011/06/annual-returns-by-state-of-us-economy.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/06/annual-returns-by-state-of-us-economy.html#0001-01-01)

Sometimes it is fun to just look at annual returns, especially as the financial world has shifted its focus to microseconds in a world of inconceivable macro imbalances.  [St. Louis Fed (USREC)](http://research.stlouisfed.org/fred2) offers a binary state of the economy with 1=recession and 0=expansion, but we all must remember that the assignment of the beginning and end dates of recessions occurs with a 1 to 2 year lag, so we cannot use them for real-time trading even at a monthly level.  However, we might be able to examine equity returns on a yearly level given the state of the economy in the previous year.  With a little ggplot2, I think a lot of folks might be surprised at a simple look at annual Dow Jones Industrial returns since 1921\. In and around recessions, the market is either really right or really wrong.  Then in the last chart, my thought is that stocks will not be cheap again until we see a recession that lasts greater than 1 year.

For asset class returns by phase of the business cycle, there is a great article [The Strategic and Tactical Value of Commodity Futures in the March/April 2006 Financial Analysts Journal](http://www.cfapubs.org/doi/abs/10.2469/faj.v62.n2.4084) that shows the following graph, which I have unfortunately not been able to replicate.

R code:

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

[Created by Pretty R at inside-R.org](http://www.inside-r.org/pretty-r "Created by Pretty R at inside-R.org")