<!--yml

category: 未分类

date: 2024-05-18 15:23:48

-->

# Timely Portfolio：没什么新鲜事，但不认为应该被忽视——沃伦·巴菲特和 MCO

> 来源：[`timelyportfolio.blogspot.com/2011/01/nothing-new-but-dont-think-it-should-be.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/01/nothing-new-but-dont-think-it-should-be.html#0001-01-01)

这已经在[`www.businessinsider.com/moodys-ceo-dumped-stock-sec-wells-notice-2010-5`](http://www.businessinsider.com/moodys-ceo-dumped-stock-sec-wells-notice-2010-5 "http://www.businessinsider.com/moodys-ceo-dumped-stock-sec-wells-notice-2010-5")上讨论过，但我没有看到事件的图表或时间轴。

> 2010 年 3 月 18 日 - SEC 向穆迪发出韦尔斯通知，但公众不知道
> 
> 2010 年 3 月 18 日 - 2010 年 3 月 26 日 沃伦·巴菲特卖出超过 100 万股穆迪的股票
> 
> 2010 年 5 月 7 日 - 穆迪披露韦尔斯通知，股价比巴菲特的售价下跌了 28%

![2011-01-27](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjqifcXT3QIXakvH3LqpD2_Npi06ygJ2bqFknwfkmNpidqsaXcA_zmWL7ghMGEZo1aFV9DaH9JTeTMzr8oK6mdsEKYAxqIp3RQNcw3lA7xG5DR_Z_7SCWa4g0EQtD45mE7ViDBBI-iq4A/s1600-h/2011-01-27%5B3%5D.jpg)

此外，有趣的现象是在公众完全不知道韦尔斯通知的情况下，大规模抛售。还有谁知道？直到 2010 年 4 月底，标普 500 指数才开始下跌，所以这不是一个充分的解释。

对于 R 爱好者，这是代码（我在两个标签上作弊了）：

library(quantmod)

library(TTR)

library(PerformanceAnalytics)

tckr<-"MCO"

start<-"2008-06-30"

end<- format(Sys.Date(),"%Y-%m-%d") # yyyy-mm-dd

# 从 Yahoo! Finance 获取 tckr 指数数据

getSymbols(tckr, from=start, to=end)

MCOdaily<-dailyReturn(MCO)

Return.cumulative = cumprod(1+MCOdaily) - 1

Return.cumulative = (1+Return.cumulative) * 34.44 #price of MCO at start of period

colnames(Return.cumulative)<-c("穆迪")

chart.TimeSeries(Return.cumulative, colorset = "darkblue", legend= NULL, period.areas = cycles.dates, period.color = "lightgreen", event.lines = risk.dates, event.labels = risk.labels, event.color = "red", lwd = 2, main="穆迪股价",sub="绿色阴影表示销售",xlab=NULL)

abline(h=15.87,col="red",lty=2)

cycles.dates = list(

c("2009-07-21","2009-07-22"),

c("2009-09-01","2009-09-02"),

c("2009-10-28","2009-10-29"),

c("2009-12-07","2009-12-18"),

c("2010-03-18","2010-03-26"),

c("2010-09-10","2010-09-20"),

c("2010-10-12","2010-10-21"))

# 事件列表 - 为了最佳效果，请按顺序保留这些日期

risk.dates = c("2008-11-07","2010-03-18","2010-05-07")

risk.labels = c("巴菲特以 4.99 亿美元购买 3150 万股","SEC 发布穆迪韦尔斯","穆迪报告韦尔斯")

*45 分钟*
