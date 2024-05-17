<!--yml
category: 未分类
date: 2024-05-12 19:02:18
-->

# Quantitative Trading: Trading platform and EC2 revisited

> 来源：[http://epchan.blogspot.com/2011/11/trading-platform-and-ec2-revisited.html#0001-01-01](http://epchan.blogspot.com/2011/11/trading-platform-and-ec2-revisited.html#0001-01-01)

Recently I opened a 

[discussion](http://epchan.blogspot.com/2011/09/more-on-automated-trading-platforms.html)

on the various software platforms which allow the programmers among us to build trading strategies easily. Here is one other addition:

[Quantopian](http://www.quantopian.com/)

. It is only in alpha stage, but I did get a preview of its features:

1) You can code in Python, which is an easier language to learn than Java, but no less powerful. In fact, I know of a superb programmer who uses Python to backtest HF strategies.

2) It is web-based, which means you can take advantage of collocation on a server much more stable than your own desktops. (For those who worry about the confidentiality of your strategies, the founder indicated to me that they can run an image of the software on an Amazon EC2 account that you owned so they won't have access to your codes. As for the confidentiality of codes residing on EC2 itself, please see below*.)

3) It is event-driven (or for those who like the latest jargon: CEP-enabled), like all the Java API's that I discussed in the previous article.

4) They have 1-min US equities data for backtesting. Tick-level data will be available soon.

5) Toolboxes for common technical indicators, mathematical algorithms, etc. will be available soon.

6) They will run a competition for trading models which makes it easier for independent traders to become trading advisers to others, or to raise money for their own funds.

Unfortunately, live walk-forward testing is not yet available.

* Some readers have wondered whether it is safe to run their trading models on Amazon's EC2\. Won't Amazon's employees have access to their wildly profitable strategies? The answer is no: Amazon's

[security policy](http://media.amazonwebservices.com/pdf/AWS_Security_Whitepaper.pdf)

:

**Guest Operating System: Virtual instances are completely controlled by the customer. Customers have full root access **

**or administrative control over accounts, services, and applications. AWS does not have any access rights to customer **

**instances and cannot log into the guest OS....**

Thanks to a reader OL from France who provided me with this info. He also told me that: 

"So, I finally deployed my momentum strategy on a Linux instance of EC2 (which is free btw).

I wrote it based on the java demo application provided by Interactive Brokers and some parts of Algoquant.

So far, I use a European instance of EC2 which alas doesn't have the best latency to IB US servers (90 ms) but still better than my bedroom connection. 

A test ping from a US instance to IB US servers results in only 15 ms ..."

So there you go: Java+Algoquant+IB+EC2=profit.