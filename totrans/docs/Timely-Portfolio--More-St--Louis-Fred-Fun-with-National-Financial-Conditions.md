<!--yml
category: 未分类
date: 2024-05-18 15:15:24
-->

# Timely Portfolio: More St. Louis Fred Fun with National Financial Conditions

> 来源：[http://timelyportfolio.blogspot.com/2011/05/more-st-louis-fred-fun-with-national.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/05/more-st-louis-fred-fun-with-national.html#0001-01-01)

```
#explore how SP500 behaves in different ranges of Financial Conditions   
```

```
require(quantmod)
require(PerformanceAnalytics)
require(ggplot2)   #get data from St. Louis Federal Reserve (FRED)
getSymbols("SP500",src="FRED") #load SP500
getSymbols("ANFCI",src="FRED") #load Adjusted Chicago Financial   
```

```
#show a chart of ANFCI
chartSeries(ANFCI,theme="white",name="Adjusted National Financial Conditions (ANFCI)")
```

```
#do a little manipulation to get the data lined up on weekly basis
SP500  <-  to.weekly(SP500)[,4]
ANFCI <- to.weekly(ANFCI)[,4]
#get weekly format to yyyy-mm-dd with the first day of the week
index(SP500) <- as.Date(index(SP500))
index(ANFCI) <- as.Date(index(ANFCI))   
```

```
#use floor to get ranges for ANFCI so we can run boxplots
ANFCI <- floor(ANFCI)
#lag ANFCI signal
ANFCI <- lag(ANFCI,k=1)   #merge sp500 returns and ANFCI
SP500_ANFCI <- na.omit(merge(ROC(SP500,n=1,type="discrete"),ANFCI))
colnames(SP500_ANFCI) <- c("SP500","ANFCI")   
```

```
#convert xts to data frame for ggplot boxplot exploration
df <- as.data.frame(cbind(index(SP500_ANFCI),
	coredata(SP500_ANFCI[,1:2])))
ggplot(df,aes(factor(ANFCI),SP500)) +
	geom_boxplot(aes(colour = factor(ANFCI))) +
	opts(title="Box Plot of SP500 Weekly Change by Adjusted Financial Conditions")       
```

```
#show linked returns based on Adjusted Financial Conditions
ret_eq_neg3 <- ifelse(SP500_ANFCI[,2] == -3, SP500_ANFCI[,1], 0)
ret_eq_neg2 <- ifelse(SP500_ANFCI[,2] == -2, SP500_ANFCI[,1], 0)
ret_eq_neg1 <- ifelse(SP500_ANFCI[,2] == -1, SP500_ANFCI[,1], 0)
ret_eq_0 <- ifelse(SP500_ANFCI[,2] == 0, SP500_ANFCI[,1], 0)
ret_eq_pos1 <- ifelse(SP500_ANFCI[,2] == 1, SP500_ANFCI[,1], 0)
ret_eq_pos2 <- ifelse(SP500_ANFCI[,2] == 2, SP500_ANFCI[,1], 0)
ret_eq_pos3 <- ifelse(SP500_ANFCI[,2] == 3, SP500_ANFCI[,1], 0)
ret_eq_pos4 <- ifelse(SP500_ANFCI[,2] == 4, SP500_ANFCI[,1], 0)
ret_eq_pos5 <- ifelse(SP500_ANFCI[,2] == 5, SP500_ANFCI[,1], 0)   
```

```
#merge series for PerformanceSummary chart
ret_comp <- merge(ret_eq_neg3, ret_eq_neg2, ret_eq_neg1, ret_eq_0,
	ret_eq_pos1,ret_eq_pos2,ret_eq_pos3,ret_eq_pos4,ret_eq_pos5)
#name columns for the legend
colnames(ret_comp) <- c("ANFCI=-3","ANFCI=-2","ANFCI=-1","ANFCI=0",
	"ANFCI=1","ANFCI=2","ANFCI=3","ANFCI=4","ANFCI=5")   
```

```
charts.PerformanceSummary(ret_comp, main="SP500 Linked Returns by Financial Conditions")       
```

```
#and just for fun a very basic system
signal <- runMax(SP500_ANFCI[,2] , n=10)
#go long if Max of ANFCI over last ten weeks is 0; already lagged earlier
ret <- ifelse(signal <= 0, 1, 0) * SP500_ANFCI[,1]
ret <- merge(ret, SP500_ANFCI[,1])
colnames(ret) <- c("ANFCI_LongOnlySystem","SP500")
charts.PerformanceSummary(ret, ylog=TRUE, main="Very Simple ANFCI S&P 500 System",
	colorset=c("cadetblue","darkolivegreen3"))
```