<!--yml
category: 未分类
date: 2024-05-18 04:56:28
-->

# Magmasystems Blog: Reuters Feeds and Market Cap (Grrrr....)

> 来源：[http://magmasystems.blogspot.com/2009/01/reuters-feeds-and-market-cap-grrrr.html#0001-01-01](http://magmasystems.blogspot.com/2009/01/reuters-feeds-and-market-cap-grrrr.html#0001-01-01)

We need to find out the market cap of a company that we are receiving quotes on from Reuters using RFA 6.x. We see a field called "MKT_CAP" coming through on the initial quotes. Looking at the Reuters documentation, this should contain the market capitalization of the company.

However, every MKT_CAP field has the value of zero.

Reuters support has confirmed that the MKT_CAP field will ALWAYS be 0 for every quote.

So, Reuters ... why are you sending this field with every quote if you are never populating it? And, how many other fields that come with each quote are not being populated with valid values? Don't you realize that low-latency means that you should be sending the minimum of data for a quote .... and we expect each and every field to contain something useful?

Brian ... please clean this up if you can.

©2009 Marc Adler - All Rights Reserved.

All opinions here are personal, and have no relation to my employer.