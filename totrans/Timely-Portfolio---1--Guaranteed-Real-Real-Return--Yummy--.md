<!--yml
category: 未分类
date: 2024-05-18 15:12:21
-->

# Timely Portfolio: -1% Guaranteed Real Real Return! Yummy??

> 来源：[http://timelyportfolio.blogspot.com/2011/08/1-guaranteed-real-real-return-yummy.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/08/1-guaranteed-real-real-return-yummy.html#0001-01-01)

If we’re cooking up a bond return, we have access to 3 ingredients: inflation, credit, and real. Historically, the recipe looks like this (as described in [Historical Sources of Bond Returns](http://timelyportfolio.blogspot.com/2011/04/historical-sources-of-bond-returns.html)).

0-5 parts inflation
+ 1-2 parts credit
+ 1-3 parts real

and the chart looks like this.

In the good old days credit did not apply to U S Treasuries, but let’s just assume that given the current situation that there is a 1.4% chance of a loss of 50% due to credit (equivalent to the current CDS price on 10y US Treasuries of 0.70%). The inflation component should not include this credit risk compensation, so for US Treasuries with no credit component, this number must be included in the real component. When US 10y TIPS yield 0% but even worse -0.25% last week, that means investors find -1% real real returns a yummy recipe.

I think I need to look elsewhere for opportunity.

Access to the US 10y CDS for everybody is available at [Bloomberg](http://www.bloomberg.com/apps/quote?ticker=CT786916:IND).

R code:

```
require(quantmod)
require(PerformanceAnalytics)   getSymbols("GS10",src="FRED") #load 10yTreasury
getSymbols("BAA",src="FRED") #load Corporate for credit
getSymbols("CPIAUCSL",src="FRED") #load CPI for inflation    bondReturnSources<-na.omit(merge(ROC(CPIAUCSL,12,type="discrete")*100,
            BAA-GS10,GS10-ROC(CPIAUCSL,12,type="discrete")*100))
bondReturnSources<-merge(bondReturnSources,
            bondReturnSources[,1]+bondReturnSources[,2]+bondReturnSources[,3]) #add for total
colnames(bondReturnSources)<-c("Inflation","Credit","Real","Total")   chart.TimeSeries(bondReturnSources,legend.loc="bottom",
            main="Historical Sources of Bond Returns",
            ylab="Yield as %",
            colorset=c("darkolivegreen3","cadetblue","goldenrod","gray70"))
```

[Created by Pretty](http://www.inside-r.org/pretty-r "Created by Pretty R at inside-R.org") 

[](http://www.inside-r.org/pretty-r "Created by Pretty R at inside-R.org")