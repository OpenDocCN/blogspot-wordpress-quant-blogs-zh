<!--yml
category: 未分类
date: 2024-05-18 15:40:18
-->

# Tick Databases | Tr8dr

> 来源：[https://tr8dr.wordpress.com/2008/01/30/tick-databases/#0001-01-01](https://tr8dr.wordpress.com/2008/01/30/tick-databases/#0001-01-01)

January 30, 2008 · 8:29 pm

Ok, so the street has largely embraced KDB as a tick database for high-frequency algo. It is by far the worst DB I have every worked with in terms of reliability and functionality. The one thing it does have going for it is that it is fast.

Other than that, if you want to deal with the agony of a database that falls over on simple operations, has a largely unintelligable language Q (a dialect of APL) that noone cares for, and has next to nothing in the way of support from the vendor, be my guest.

KDB is a very (very!) raw database, not much more than a process or two around a a bunch of binary files, one for each timeseries per day.

Stay away.