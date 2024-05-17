<!--yml
category: 未分类
date: 2024-05-12 19:18:53
-->

# Quantitative Trading: Algorithmic Trading Technology Update

> 来源：[http://epchan.blogspot.com/2009/01/algorithmic-trading-technology-update.html#0001-01-01](http://epchan.blogspot.com/2009/01/algorithmic-trading-technology-update.html#0001-01-01)

Lately a number of new (at least to me) technologies useful to the algorithmic trader came to my attention:

1) Matlab2IB API

I said in my book that it is difficult to use Matlab as an execution platform. As

[Max](http://www.maxdama.com/)

has pointed out, this is no longer true. This inexpensive

[API](http://www.exchangeapi.com/ProductOverview.htm)

connects Matlab to your Interactive Brokers' account. It allows you to retrieve historical data, get real-time quotes, and send orders. In other words, all the basic functions you need to create your own execution engine.

2) R

Many people (hat tip: Steve H.) know that

[R](http://www.nytimes.com/2009/01/07/technology/business-computing/07program.html?partner=permalink&exprod=permalink)

is an open-source (i.e. free) alternative to Matlab. I find that there is also an

[API](http://cran.r-project.org/web/packages/IBrokers/vignettes/IBrokers.pdf)

that connects R to Interactive Brokers, though I have not tried it myself.

3) Trade Ideas

[Trade Ideas](http://www.trade-ideas.com/)

(hat tip: Russell M.) is a complete automated trading platform that provides connections to different brokerages (scottrade, IB, TD Ameritrade, etc.)

4) Amazon EC2 cloud computing platform

Running out of PC's to run your myriad strategies? Try Amazon's

[EC2](http://aws.amazon.com/ec2/)

cloud computing platform. For a modest hourly fee, you get access to an instance of either Linux or Windows environment, and you can add as many instances as you want. The connection speed is supposed to be at least 10x T-1 line, well-suited to high frequency traders .

[Here](http://www.maxdama.com/2008/08/amazon-ec2-re-test.html)

is some other performance benchmarks.