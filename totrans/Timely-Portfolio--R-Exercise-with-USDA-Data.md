<!--yml
category: 未分类
date: 2024-05-18 15:17:29
-->

# Timely Portfolio: R Exercise with USDA Data

> 来源：[http://timelyportfolio.blogspot.com/2011/05/r-exercise-with-usda-data.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/05/r-exercise-with-usda-data.html#0001-01-01)

After the helpful comment by Bradley on my post [Commodity Index Estimators](http://timelyportfolio.blogspot.com/2011/05/commodity-index-estimators.html),

> How about the National Agricultural Statistics Service (NASS)? Looks like they have information for prices received back to 1908 for many agricultural goods ([http://www.nass.usda.gov/](http://www.nass.usda.gov/)).

I started trying to get this USDA price data in R, but after three hours struggling to find historical data from start to finish in any useable format, had no success.  However, I did notice some gaps in my R skills, so I decided to use some USDA data for practice.  The USDA 10 year price projections for major US crops interested me.  Three more hours of struggle yielded some new R skills and the following graphs and R code.

And in a slightly better cumulative return format.  Strangely, my favorite set of PerformanceAnalytics graphs returned a “format” error.

Looks like the dairy business might be attractive.  Maybe, I can make money there.

One beneficial byproduct of the exercise was the discovery of [http://www.farmdoc.illinois.edu/manage/uspricehistory/USPrice.asp](http://www.farmdoc.illinois.edu/manage/uspricehistory/USPrice.asp "http://www.farmdoc.illinois.edu/manage/uspricehistory/USPrice.asp") which offers monthly crop price data in graph or table form.

![](img/4b31b681e9284331a180c29ed5456e0a.png)

Now I need to determine how to get this monthly price data from the USDA or somewhere else for R research.

Also, I thought this research piece [www.farmdoc.illinois.edu/irwin/research/EmpiricalMethodsCommodity.pdf](http://www.farmdoc.illinois.edu/irwin/research/EmpiricalMethodsCommodity.pdf) was interesting but not helpful toward this objective.

R code:

require(gdata)
require(quantmod)
require(ggplot2)

URL<-"[http://usda.mannlib.cornell.edu/usda/ers/94005/2011/Table39.xls"](http://usda.mannlib.cornell.edu/usda/ers/94005/2011/Table39.xls%22)
#get Shiller data for inflation and US Treasury 10 year
USDAprice <- read.xls(URL,sheet="Table38",pattern="2009",stringsAsFactors = FALSE)

#strip out interesting information
USDAprice<-USDAprice[3:10,]

#change row names to crop names in column 1
rownames(USDAprice)<-USDAprice[,1]

#delete column 1 since now rowname
USDAprice<-USDAprice[,2:NCOL(USDAprice)]

#insure numeric data
USDAprice<-as.data.frame(data.matrix(USDAprice))

#switch rows and columns
USDAprice<-t(USDAprice)

#get an xts version for later
USDApricexts<-USDAprice
rownames(USDApricexts)<-paste(substr(rownames(USDAprice),2,5),rep("01-01",NROW(USDAprice)),sep = "-")
USDApricexts<-as.xts(USDApricexts)

#get dates for rownames
rownames(USDAprice)<-as.Date(paste(substr(rownames(USDAprice),2,5),rep("01-01-31",NROW(USDAprice)),sep = "-"))

USDApricemelt<-melt(USDAprice)
colnames(USDApricemelt)<-c("Date","Crop","USDA_Projected_Price")
ggplot(USDApricemelt, stat="identity", aes(x=Date,y=USDA_Projected_Price,colour=Crop)) + geom_line() +
    scale_x_date(format = "%Y") +
    opts(title = "USDA Projected Crop Prices through 2020")

#standardize to get cumulative return or wealth index
USDApricereturn<-USDApricexts/lag(USDApricexts)-1
USDApricereturn[1,]<-0
USDApricereturn<-cumprod(1+USDApricereturn)

#get in format that ggplot2 can use
USDApricereturnmelt<-cbind(as.Date(index(USDApricereturn)),coredata(USDApricereturn))
rownames(USDApricereturnmelt)<-USDApricereturnmelt[,1]
USDApricereturnmelt<-USDApricereturnmelt[,(2:NCOL(USDApricereturnmelt))]
USDApricereturnmelt<-melt(USDApricereturnmelt)
colnames(USDApricereturnmelt)<-c("Date","Crop","USDA_Projected_Cumulative_Return")
ggplot(USDApricereturnmelt, stat="identity", aes(x=Date,y=USDA_Projected_Cumulative_Return,colour=Crop)) + geom_line() +
    scale_x_date(format = "%Y") +
    opts(title = "USDA Projected Crop Price Cumulative Returns through 2020")