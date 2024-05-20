<!--yml
category: 未分类
date: 2024-05-18 05:25:33
-->

# Magmasystems Blog: Tibco EMS and Financial Companies

> 来源：[http://magmasystems.blogspot.com/2005/09/tibco-ems-and-financial-companies.html#0001-01-01](http://magmasystems.blogspot.com/2005/09/tibco-ems-and-financial-companies.html#0001-01-01)

The last project that I headed up used Tibco EMS as the messaing system. The major financial company that I did this project for has an enterprise license for EMS, and is deploying it throughout the entire organization.

Tibco has created .NET assemblies for EMS. Since Tibco EMS implements the Java Messaging Service (JMS) spec, we have have a slew of .NET developers who are going to be exposed to JMS. Windows programmers who have be confined to using MSMQ in the past are now going to have to deal with a slightly different paradigm.

Before diving headfirst into JMS, it is best to get familiar with the Best Practices and AniPatterns associated with JMS. To help you along, here are some sites:

[http://www.precisejava.com/javaperf/j2ee/JMS.htm](http://www.precisejava.com/javaperf/j2ee/JMS.htm)

(Chapter 6, Bitter Messages, of Tate's

***Bitter Java***

AntiPatterns book)

[http://www.manning-source.com/books/tate2/tate2_ch06.pdf](http://www.manning-source.com/books/tate2/tate2_ch06.pdf)

Doing request/response is a bit tricky. Read about it in this article:

[http://java.sys-con.com/read/49089.htm](http://java.sys-con.com/read/49089.htm)