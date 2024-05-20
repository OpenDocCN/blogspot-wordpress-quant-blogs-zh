<!--yml
category: 未分类
date: 2024-05-18 04:56:08
-->

# Magmasystems Blog: Real-time Messaging in Sybase 15

> 来源：[http://magmasystems.blogspot.com/2009/02/real-time-messaging-in-sybase-15.html#0001-01-01](http://magmasystems.blogspot.com/2009/02/real-time-messaging-in-sybase-15.html#0001-01-01)

If your organization is migrating from Sybase ASE 12.5.4 to Sybase 15, then you might want to take a look at

[these](http://www.sybase.com/files/Product_Overviews/Upgrading-to-ASE15-Migration-010708.pdf)

slides.

One slide caught my attention. It was a slide on the migration effort done by

[eSpeed](http://www.bgcpartners.com/)

. One of the things that eSpeed did in their Sybase migration was:

Replace "Polling-Broadcasting”legacy solution with integrated real-time messaging (RTDS 4.0) in ASE 15

I need to find out more about this. Sybase has some slides

[here](http://www.sybase.com/content/1030415/RTDS-SybaseTemplate.pdf)

.

Many financial companies who are using Sybase have applications that actually do database polling every 'n' minutes in order to find out what rows in a table have changed. If eSpeed did what I think they did, then this presents itself as a compelling reason to move to Sybase 15\. (Of course, this assumes that you are not goign to be moving eventually to SQL Server 2008/2010.)

©2009 Marc Adler - All Rights Reserved.

All opinions here are personal, and have no relation to my employer.