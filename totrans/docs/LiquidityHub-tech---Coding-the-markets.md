<!--yml
category: 未分类
date: 2024-05-12 19:45:06
-->

# LiquidityHub tech | Coding the markets

> 来源：[https://etrading.wordpress.com/2007/10/23/liquidityhub-tech/#0001-01-01](https://etrading.wordpress.com/2007/10/23/liquidityhub-tech/#0001-01-01)

## LiquidityHub tech

### October 23, 2007

LiquidityHub have a [new website](http://www.liquidityhub.com) up. Definitely an improvement on the last effort. Of interest to coders will be the [tech page](http://www.liquidityhub.com/about_technology.html), detailing the various Java products used as building blocks. Notable are the Cameron FIX gateway, BEA servers and Fiorano messaging. Using Cameron to present a FIX wire protocol to dealers is a moot point since most talk to LH via the ION MarketView gateway which hides the FIX implementation. The BEA app server comes with a [real time VM](http://dev2dev.bea.com/pub/a/2006/04/introduction-wlrt.html) – which will be a relief to any dealer technologists worried about garbage collection delaying their streaming quotes. [Fiorano](http://www.fiorano.com) is a JMS implementation that supplies pubsub and MQ style messaging.