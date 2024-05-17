<!--yml
category: 未分类
date: 2024-05-18 05:24:37
-->

# Magmasystems Blog: NHibernate

> 来源：[http://magmasystems.blogspot.com/2005/10/nhibernate.html#0001-01-01](http://magmasystems.blogspot.com/2005/10/nhibernate.html#0001-01-01)

I am reading docs on

[NHibernate](http://wiki.nhibernate.org/display/NH/Home)

, an O/R mapper for .NET (it comes from Hibernate in the Java world). This is one of

[many](http://csharp-source.net/open-source/persistence)

O/R mappers available for .NET. The main impetus for learning NHibernate is that Hibernate seems to be the defacto standard on the other side of the fence. Since Finetix is a hybrid .NET/Java shop, I figure that I will come up against Hibernate eventually on our projects in the financial space.

I have been using a home-grown O/R layer for the past 2 years on all of my .NET projects. It uses custom attributes (as opposed to NHibernate's use of XML files) on classes and properties in order to generate calls for a back-end data provider. The providers can be SQL Server, Oracle, ODBC, OLE DB, and Tibco/JMS messaging.

The last project that I architected used an O/R mapper called

[Castor](http://www.castor.org/index.html)

on WebLogic 8.1\. It was recommended that I use Castor, as some people had trouble getting JaxB to work with WebLogic. And, I am happy to say that Castor worked out just fine on this project.

*(What happened to Microsoft's ObjectSpaces?)*