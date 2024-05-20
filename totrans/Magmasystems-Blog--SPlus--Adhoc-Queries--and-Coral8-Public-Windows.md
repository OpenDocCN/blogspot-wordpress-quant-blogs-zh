<!--yml
category: 未分类
date: 2024-05-18 05:00:31
-->

# Magmasystems Blog: SPlus, Adhoc Queries, and Coral8 Public Windows

> 来源：[http://magmasystems.blogspot.com/2008/07/splus-adhoc-queries-and-coral8-public.html#0001-01-01](http://magmasystems.blogspot.com/2008/07/splus-adhoc-queries-and-coral8-public.html#0001-01-01)

I am reading a

[Powerpoint presentation](http://www.insightful.com/news_events/webcasts/2004/03zivot/HighFrequencyWebCast.pdf)

by Prof. Eric

Zivot

on

SPlus

, and I was intrigued by the ad-

hoc

query facility that

SPlus

offers. For example, if you have

TAQ

tick data loaded into

SPlus

, you can use the following

SPlus

query to get the average price of Microsoft over a non-overlapping 5-minute window:

mean.5min = aggregateSeries(msftt.ts[,"Price"], + by="minutes",k.by=5,FUN=mean)

Coral8 recently implemented queryable "public windows" as a way to do ad-hoc queries. In order to get this feature out the door quickly, Coral8 embedded a version of SQLite into their system. So, you cannot use the Coral8 streaming query language, CCL, to do ad-hoc queries of windows. Instead, you need to use a dialect of SQL-92.

(Coral8 tells me that eventually. you will be able to use CCL for ad-hoc queries)

SPlus looks like it supports a lot of built-in functions for time-series financial data. This is something I would also like to see in Coral8\. (I guess there is an opportunity for a little cottage industry to be built around enhancing Coral8 for capital markets firms...)

I wonder if any of the CEP vendors considered SPlus/R as a query language before deciding on Streaming SQL? (I know that JOS has been on the R bandwagon for a while at Barcap. He hasn't blogged too much about it recently though...)

©2008 Marc Adler - All Rights Reserved.

All opinions here are personal, and have no relation to my employer.