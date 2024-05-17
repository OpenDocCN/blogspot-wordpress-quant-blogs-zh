<!--yml
category: 未分类
date: 2024-05-12 19:17:50
-->

# Quantitative Trading: MATLAB as an Automated Execution System

> 来源：[http://epchan.blogspot.com/2009/05/matlab-as-automated-execution-system.html#0001-01-01](http://epchan.blogspot.com/2009/05/matlab-as-automated-execution-system.html#0001-01-01)

I just published an article "

[MATLAB as an Automated Execution System](http://www.epchan.com/subscription/matlabexecution.pdf)

". (It is available to readers of my book and subscribers to my

[Premium Content](http://www.epchan.com/subscriptions.html)

website.) It comes with

[example MATLAB codes](http://epchan.com/book/bollinger.m)

executing a simple Bollinger-band high-frequency E-mini trading strategy.

As I mentioned before, I now find MATLAB to be a good platform not just for backtesting, but for automated execution as well. Of course, not all brokerages have API's that connect to MATLAB. My example codes are for submitting orders automatically to an Interactive Brokers account.

In general, I find that writing execution programs in MATLAB is a breeze compared to C++, Java or even C#. It takes about 1/5 the development time of a C++ program. Any performance limitations will probably not be due to MATLAB, but to the latency of your brokerage in updating positions and order status.