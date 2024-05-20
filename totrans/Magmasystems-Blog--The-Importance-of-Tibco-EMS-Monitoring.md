<!--yml
category: 未分类
date: 2024-05-18 05:01:37
-->

# Magmasystems Blog: The Importance of Tibco EMS Monitoring

> 来源：[http://magmasystems.blogspot.com/2008/06/importance-of-tibco-ems-monitoring.html#0001-01-01](http://magmasystems.blogspot.com/2008/06/importance-of-tibco-ems-monitoring.html#0001-01-01)

If you are using

Tibco

EMS, you should be aware that there is a decent tool that comes with the

Tibco SDK

that allows you to monitor all activity that goes on in your broker. In the directory

***c:\tibco\ems\bin***

, you will find a command-line application called

***tibemsmonitor.exe***

. If you run this utility, you can see every connect/disconnect, every creation and destruction of a

MessageProducer

and

MessageConsumer

, every creation of a topic or queue.

In a quest to optimize our code, I started spying on the interaction between EMS and our application. I found that we were creating

MessageProducers

too many times ... way too many times for an application that did a lot of real-time message processing.

I was curious to see what went on behind the act of creating a message producer and consumer. So, I fired up the invaluable Reflector (from

Lutz Roeder

) and peeked into the

***Tibco.EMS.dll***

assembly. What I found was that, every time a message producer or consumer is created, the

***Tibco.EMS._CreateMessageProducer***

function constructs a message, sends it into the broker, and synchronously waits for a response. This takes a lot of time and produces a lot of overhead.

I changed our code so that we now cache and reuse

MessageProducers

. I have to say that our code looks like it runs a lot faster now. A lot faster....

Since the code in question was something I wrote two years ago, I took it for granted that it was working fine, since about a dozen groups in our company use this code. And, it was working fine, except that it produced a lot of needless overhead. I will gladly accept 10 lashes with a wet noodle for this one ....

The lessons learned are:

1) Optimize, optimize, optimize

2) That old code that you are using that forms the basis of your framework probably can do with monitoring.

3) Use Reflector to see what the underlying libraries are doing.

***©2008 Marc Adler - All Rights Reserved.*** ***All opinions here are personal, and have no relation to my employer.***