<!--yml
category: 未分类
date: 2024-05-18 05:15:17
-->

# Magmasystems Blog: SQl Server 2005 Performance Tips

> 来源：[http://magmasystems.blogspot.com/2006/11/sql-server-2005-performance-tips.html#0001-01-01](http://magmasystems.blogspot.com/2006/11/sql-server-2005-performance-tips.html#0001-01-01)

[Here](http://www.microsoft.com/technet/prodtechnol/sql/bestpractice/oltp-performance-issues.mspx)

Good performance hints if you are doing a lot of OLTP processing. Most of the tips will work for Sybase as well.

It is remarkable what performance improvements you can make in an OLTP system if you hire a true database tuning expert to go over your systems with a fine-tooted comb. Unfortunately, the tuning does not usually extend into refactoring the data model. This is because a lot of apps touch the databases, and you would then have to go in and start refactoring app code.

SQL Server 2005 comes with new, easy-to-use profiling tools, and I encourage you to take advantage of them as you are developing new apps. If you are a dev manager, try to get funding for two weeks of a SQL Server 2005 expert's time once your data model is written.

In addition, try to get your SANs tuned correctly, and optimize the interaction between frequenty-used database indexes and the spindles.

How about hardware acceleration, like Solid State Disks?

Kudos go out to

[this](http://www.sql-server-performance.com/)

site, completely devoted to SQL Server performance tuning.

Final word - if you have a mission-critical application that involves heavy database access, spend the bucks and hire a DB architect who knows how to tune databases like a 1964 Fender Strat.

©2006 Marc Adler - All Rights Reserved