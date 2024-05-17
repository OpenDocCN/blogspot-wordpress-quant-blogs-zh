<!--yml
category: 未分类
date: 2024-05-18 05:05:43
-->

# Magmasystems Blog: OpenAdaptor, SQL Server 2005, and Aleri

> 来源：[http://magmasystems.blogspot.com/2007/12/openadaptor-sql-server-2005-and-aleri.html#0001-01-01](http://magmasystems.blogspot.com/2007/12/openadaptor-sql-server-2005-and-aleri.html#0001-01-01)

This posting was made in the interests of any Aleri or OpenAdaptor users who are trying to connect to a named SS2005 instance.

I have multiple "instances" installed of SQL Server 2005\. According to the documentation at

[http://msdn2.microsoft.com/en-us/library/ms378428.aspx](http://msdn2.microsoft.com/en-us/library/ms378428.aspx)

, this JDBC connection string should have worked:

jdbc:sqlserver://MAGMALAPTOP\RPT;databaseName=MyDatabase;integratedSecurity=true;

In Microsoft's

[JDBC Driver 1.2 for SQL Server 2005](http://msdn2.microsoft.com/en-us/data/aa937724.aspx)

, there is a sample Java app called connectURL. With the connection string above, this sample app worked fine, and was able to connect to the RPT instance of my SS2005 database.

However, I could not get

[OpenAdaptor](https://www.openadaptor.org/)

to work with this connect string. In case you are wondering why I was messing around with OpenAdaptor, it is because this is what

[Aleri](http://www.aleri.com/)

uses for its adapters to external data sources.

After spending several hours this weekend trying to get Aleri to connect to SQL Server using the connection string above, I finally stumbled upon an alternative syntax for the connection string.

The new connection string is:

jdbc:sqlserver://MAGMALAPTOP;instanceName=RPT;databaseName=MyDatabase;integratedSecurity=true;

Notice that the

*instanceName*

is specified with a separate parameter.

So, there may be an issue with OpenAdaptor. Or, another theory that I have is that the backslash character in the connection string is being considered as an escape character.

©2007 Marc Adler - All Rights Reserved