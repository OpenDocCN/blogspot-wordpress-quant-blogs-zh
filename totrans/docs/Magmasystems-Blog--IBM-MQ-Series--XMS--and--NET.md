<!--yml
category: 未分类
date: 2024-05-18 04:55:48
-->

# Magmasystems Blog: IBM MQ Series, XMS, and .NET

> 来源：[http://magmasystems.blogspot.com/2009/02/ibm-mq-series-xms-and-net.html#0001-01-01](http://magmasystems.blogspot.com/2009/02/ibm-mq-series-xms-and-net.html#0001-01-01)

We have to be able to read in some information that another system is putting out over IBM MQ. There is a messaging implementation from IBM called XMS that seems like it's JMS over MQ. This is great for us because this means that we can (hopefully) clone our existing Tibco EMS adapters, and with a few little changes, be able to read off of MQ.

I am not sure if the original publisher of the data also has to use XMS ...

maybe someone here can tell me

. I know for a fact that the publishing system does not use XMS. If the publisher does have to use XMS in order for us to consume through XMS, then we will need to come up with an input adapter that uses the native MQ API.

The information about the IBM Messaging Client for .NET is

[here](http://www-01.ibm.com/support/docview.wss?rs=171&uid=swg24011756)

.

Update: A great comment by Richard Brown of IBM WebSphere pre-sales tells me that there is nothing to worry about if we are just a consumer ... which we are.

©2009 Marc Adler - All Rights Reserved.

All opinions here are personal, and have no relation to my employer.