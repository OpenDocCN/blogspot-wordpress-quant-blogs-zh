<!--yml
category: 未分类
date: 2024-05-18 15:20:12
-->

# Timely Portfolio: Death Spiral Warning Graph

> 来源：[http://timelyportfolio.blogspot.com/2011/03/death-spiral-warning-graph.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/03/death-spiral-warning-graph.html#0001-01-01)

In the death spiral scenario, rates go up while the currency goes down.  Here is the way to watch that.  I’m not saying that death spiral of US Dollar and interest rates occurs, but without significant action to restore confidence in fiscal and monetary policies, it is almost certain.  Fortunately free markets and a democracy might stop the spiral early, but it appears a mini-crisis is necessary to force action.

[![](img/15e838bfa17538c5209a9412623d3bb8.png)](http://stockcharts.com/h-sc/ui?s=%24tnx:%24usd&p=m&st=1990-01-01&en=(today)&id=p76537466593)

via [StockCharts.com](http://stockcharts.com/h-sc/ui?s=%24tnx:%24usd&p=m&st=1990-01-01&en=(today)&id=p76537466593)

And when we add this as the denominator or pricing mechanism for the S&P 500 (transformation requires removing natural $ pricing first), the chart looks like this.  The transitory fake improvement in stock prices since 2008 driven by aggressive monetary action is much clearer.  Anything through 14.3 on the green line is indicative of the first phase of this spiral.

 ![fed fred rates dollar sp500](img/9c13e54170ef26d3b5c7d10afd735952.png "fed fred rates dollar sp500")

And to throw a little R into this, let’s look at the rolling correlation of the SP500 to the 10y/US$ ratio.  The correlation magically increases in Summer 1998 with Long Term Capital Management and Russia default, and the Fed put became entrenched.

R code:

require(quantmod)
require(PerformanceAnalytics)

#get currency rate and stock data from the FED FRED data series
getSymbols("DGS10",src="FRED") #load Fed 10y rate
getSymbols("DTWEXM",src="FRED") #load Fed Dollar
getSymbols("DTWEXO",src="FRED") #load Fed Dollar Other
getSymbols("SP500",src="FRED") #load Fed SP500

returns<-merge(monthlyReturn(to.monthly(DGS10/DTWEXM)),monthlyReturn(to.monthly(SP500)))

corSP10USD<-runCor(returns["1973::2011-02",1],returns["1973::2011-02",2],n=6)

chartSeries(corSP10USD,theme='white',name="S&P 500 Rolling 1y Correlation with US$ and US10y Rates")