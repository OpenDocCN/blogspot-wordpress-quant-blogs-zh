<!--yml

类别：未分类

日期：2024-05-18 15:15:20

-->

# Timely Portfolio: Overoptimizing Chicago Fed

> 来源：[`timelyportfolio.blogspot.com/2011/05/overoptimizing-chicago-fed.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/05/overoptimizing-chicago-fed.html#0001-01-01)

**这应该在整个帖子中都很明显，但这不是投资建议。请千万不要遵循这个系统，因为它可能会导致严重的损失。**

系统构建的一个危险倾向是通过玩转/优化参数来拟合历史数据，无意中过度优化。它始于一些无害的数据操作，但非常可能出现一个像在[More St. Louis Fred Fun with National Financial Conditions](http://timelyportfolio.blogspot.com/2011/05/more-st-louis-fred-fun-with-national.html)中所示的具有某种潜力的系统。然后通过某种形式的迭代调整，似乎会发生一些神奇的事情。

然而，在进行了这种微妙的调整之后，我再也没有数据来测试那些可能值得的东西，所以我只能关注一些事情，而不是那些我会冒险我的资产的事情。

尽情操作，但请小心。从想法开始，用有限的数据测试这个想法，然后将测试扩展到涵盖时间框架、其他国家或其他资产类别的更全面的样本外数据，这样做要好得多。

R 代码：

```
#this bit of code will show a system after significant
#optimization and hindsight bias
#without any out-of-sample testing
#explore how SP500 behaves in different ranges of Financial Conditions
#see previous posts for more discussion   
```

```
require(quantmod)
require(PerformanceAnalytics)
require(ggplot2)   #get data from St. Louis Federal Reserve (FRED)
getSymbols("SP500",src="FRED") #load SP500
getSymbols("ANFCI",src="FRED") #load Adjusted Chicago Financial
getSymbols("CFNAI",src="FRED") #load Chicago National Activity
#do not use this but here in case you want to play
getSymbols("PANDI",src="FRED") #load Chicago Fed Production and Income     
```

```
#do a little manipulation to get the data lined up on weekly basis
SP500  <-  to.monthly(SP500)[,4]
ANFCI <- to.monthly(ANFCI)[,4]
CFNAI <- to.monthly(CFNAI)[,4]
PANDI <- to.monthly(PANDI)[,4]
index(SP500) <- as.Date(index(SP500))
index(ANFCI) <- as.Date(index(ANFCI))
index(CFNAI) <- as.Date(index(CFNAI))
index(PANDI) <- as.Date(index(PANDI))     
```

```
SP500_ANFCI <- na.omit(merge(ROC(SP500,n=1,type="discrete"),
	ANFCI,CFNAI,PANDI))         
```

```
#and just for fun an enhanced very basic system
signal <- runSum(-0.25*SP500_ANFCI[,2]-SP500_ANFCI[,3],n=4)
chartSeries(signal, name="Chicago Fed Signal")
signal <- lag(signal,k=1)
#go long if extremely negative (signal>10)
#or good but not too good (signal between -.25 and -2)
ret <- ifelse(signal>10 | (signal <= -0.25  & signal > -2.25) , 1, 0) * SP500_ANFCI[,1]
ret <- merge(ret, SP500_ANFCI[,1])
colnames(ret) <- c("ChicagoFed_LongOnlySystem","SP500")
charts.PerformanceSummary(ret, ylog=TRUE, main="Over-optimized Chicago Fed S&P 500 System",
	colorset=c("cadetblue","darkolivegreen3"))     
```

```
#I really like the boxplot by range, so let's do the same here
df <- na.omit(merge(round(signal,0),ROC(SP500,n=1,type="discrete")))
df <- as.data.frame(cbind(index(df),
	coredata(df)))
colnames(df) <- c("date","ChiFedSignal","SP500return")
ggplot(df,aes(factor(ChiFedSignal),SP500return)) +
	geom_boxplot(aes(colour = factor(ChiFedSignal))) +
	opts(title="Box Plot of SP500 Monthly Change by Chicago Fed Signal")
```

[由 Pretty R 在 inside-R.org 创建](http://www.inside-r.org/pretty-r "由 Pretty R 在 inside-R.org 创建")
