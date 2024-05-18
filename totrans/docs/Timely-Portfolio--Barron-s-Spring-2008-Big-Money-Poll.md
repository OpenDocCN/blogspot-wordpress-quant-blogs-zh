<!--yml
category: 未分类
date: 2024-05-18 15:18:15
-->

# Timely Portfolio: Barron’s Spring 2008 Big Money Poll

> 来源：[http://timelyportfolio.blogspot.com/2011/04/barrons-spring-2008-big-money-poll.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/04/barrons-spring-2008-big-money-poll.html#0001-01-01)

[Barron's April 28, 2008, Cover Story "Back in the Pool"](http://online.barrons.com/article/SB120916344041346031.html#articleTabs_panel_article%3D1 "http://online.barrons.com/article/SB120916344041346031.html#articleTabs_panel_article%3D1") offers a great hindsight look at our wonderful foresight:

> **“AND NOW, FOR SOME GOOD NEWS: THE OTHER SHOE** isn't going to drop. After a winter of discontent marked by massive write-offs on Wall Street and a wilting economy on Main, America's portfolio managers have declared that the worst is over. More than half of the institutional investors participating in our latest Big Money poll say they're bullish or very bullish about the prospects for stocks through the end of 2008\. Their forecasts suggest they're even more upbeat about the first half of 2009.”

Even the world’s greatest investors had been trained by the market from 1980-2000 to buy every 20% dip and ignore fears.  However, as usual, the market trains you over rolling 5-20 year periods to make the wrong decision.  Closing your eyes and buying in 2008 was clearly the wrong decision, and I’m uncertain if closing your eyes and buying in 2009 was the right decision.  Closing your eyes and buying/holding anything now without regard to how we got here is very precarious.  It will be very interesting to see the results of this spring’s Barrons Big Money Poll.

**As always, I use this blog as my own record to avoid the errors of hindsight bias and cognitive dissonance.  In no way am I advising you to believe me since I could be as wrong as the money managers in Barrons April 2008.  You are responsible for your own investment gains and losses.**

R code:

require(quantmod)

tckr<-"^GSPC"

start<-"1990-01-01"
end<- format(Sys.Date(),"%Y-%m-%d") # yyyy-mm-dd

# Pull tckr index data from Yahoo! Finance
getSymbols(tckr, from=start, to=end, adjust=TRUE)

chartSeries(to.weekly(GSPC["2007::2009"]),theme="white",name="S&P 500-Safe to Get Back in the Pool?",TA=NULL)
#has to be a better way to label; let me know if you know how
text(230, GSPC["2008-05-02",4]+25, labels="Safe and Bullish???")