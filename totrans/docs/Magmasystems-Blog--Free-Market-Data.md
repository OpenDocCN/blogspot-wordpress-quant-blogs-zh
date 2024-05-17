<!--yml
category: 未分类
date: 2024-05-18 05:14:49
-->

# Magmasystems Blog: Free Market Data

> 来源：[http://magmasystems.blogspot.com/2006/11/free-market-data.html#0001-01-01](http://magmasystems.blogspot.com/2006/11/free-market-data.html#0001-01-01)

Free ECN real-time data from

[OpenTick](http://www.opentick.com)

.

Very cheap ($1) monthly fees for some other data.

They have APIs in various languages, including C# for .Net 2.0\. This seems like a good way to test that async data handling part of a framework. Here is some example docs for one of their calbacks:

static void onQuote(OTQuote quote) **Description**

Provides real-time and historical quotes.

**Provides** [OTQuote](http://www.opentick.com/dokuwiki/doku.php?id=net:otquote "net:otquote")

©2006 Marc Adler - All Rights Reserved