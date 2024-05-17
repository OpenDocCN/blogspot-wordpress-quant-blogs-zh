<!--yml
category: 未分类
date: 2024-05-18 04:44:41
-->

# Intelligent Trading: Aug 4, 2011 "plunge" headlines are in the air tonight

> 来源：[http://intelligenttradingtech.blogspot.com/2011/08/aug-4-2011-plunge-headlines-are-in-air.html#0001-01-01](http://intelligenttradingtech.blogspot.com/2011/08/aug-4-2011-plunge-headlines-are-in-air.html#0001-01-01)

Today's financial headlines are littered with the word 'plunge.'  Considering today's (cl-cl) drop on the S&P500 was just about -5%, I don't know that I would exactly call that a plunge.

                      Fig 1\. Historical ts plot of S&P500 returns <= -5%

The following R code produced a time series plot of historical occasions where this occurred.

``###################################################` `library(quantmod)

getSymbols("^GSPC",from="1950-01-01",to="2012-01-01")

adj<-GSPC$GSPC.Adjusted

rtn<-(adj/lag(adj,1)-1)[2:length(adj)]

r05<-rtn[rtn<= -.05]

plot(sort(r05),type='o',main='S&P500 1950-present returns <= -5%')

``###################################################` `Although the frequency of such occurrences is  arguably rare, the 1987 drop is much more worthy of the 1 day label 'plunge.'

One other disturbing observation in the data, however, is the large temporal clustering of occurrences in the recent 2008 region.  Now that's behavior to be concerned about (not to mention revised flash crash data pts.).

filtered 1 day cl-cl returns <=-5% sorted by date````