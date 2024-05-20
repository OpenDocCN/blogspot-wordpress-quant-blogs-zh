<!--yml
category: 未分类
date: 2024-05-18 06:14:01
-->

# Thoughts on OData | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2010/06/15/thoughts-on-odata/#0001-01-01](https://mdavey.wordpress.com/2010/06/15/thoughts-on-odata/#0001-01-01)

## Thoughts on OData

I was at the Microsoft OData [Roadshow](http://www.odata.org/roadshow) today which 11 people attended, driven by [Douglas Purdy](http://www.douglaspurdy.com/) and [Jonathan Carter](http://www.lostintangent.com/) (Building 3, Microsoft Reading). Nice to see Douglas had an iPad 🙂

*   The WebAPI is the centre of the world
*   [NetFlix](http://odata.netflix.com/) was used as the OData service for most of the morning discussion
*   OData filters via the URL is pretty [cool](http://odata.netflix.com/Catalog/Titles?Sfilter=AverageRating%20gt%204%20and%20ReleaseYear%20eq%202008)
*   Pages, Top, [Select](http://odata.netflix.com/Catalog/Titles('BVeKh')), etc are supported by OData
*   Today you can’t plug your own MIME types into OData so you are stuck with the usual suspects – JSON etc
*   Edm data model is used as per Entity Framework
*   [Metadata](http://odata.netflix.com/Catalog/%24metadata) is accessible on an OData service
*   History of OData: ASMX -> WS* -> OData. Microsoft bet on XML (WS*) but it was possible the wrong bet. OData is a bet on HTTP. OData is browser friendly!
*   Open Data Protocol = HTTP/ATOM + QUERY + JSON + METADATA
*   [IBM](http://www.douglaspurdy.com/2010/01/28/websphere-extreme-scale-supports-odata/) has implemented OData on WebSphere
*   [LINQPad](http://dougfinke.com/blog/index.php/2009/12/16/new-linqpad-beta-supports-data-in-the-cloud-odata/) has [OData](http://odataprimer.com/Default.aspx?Page=UseLinqPadToQueryODataServiceWithLINQ&NS=&AspxAutoDetectCookieSupport=1) support 🙂
*   OData Objective-C library is available for iPad support
*   When adding an OData service to Visual Studio (Service reference) you can select the “View Diagram” menu option to generate a nice metadata view of the service
*   MSFT has a standardised wireform for Expression Trees (LINQ to URL) enabling LINQ Expression tree to OData Url syntax and the reverse on the server
*   Had a very brief discussion with Jonathan around how finance is building RIA using streaming servers instead of web services. Net out Microsoft is going after the 80% data case, and streaming (push) of data in the financial world (real-time web) is a small subset of the world today and hence very not in the current vision
*   SQL Azure OData [Services](http://blogs.msdn.com/b/netservices/archive/2010/04/20/how-to-use-the-odata-for-sql-azure-with-appfabric-access-control.aspx)
*   Custom [IQueryable](http://weblogs.asp.net/cibrax/archive/2010/03/15/odata-to-the-rescue-exposing-the-eventlog-as-a-data-feed.aspx) OData is of most interest from my perspective
*   Windows [“Dallas”](http://www.microsoft.com/windowsazure/dallas/) – The iTunes store for data. Provides security, business model and hosting. There are a number of data [provides](https://www.sqlazureservices.com/Catalog.aspx) leveraging this infrastructure today, curious to see if a financial services gets on this bandwagon (maybe from a trade research perspective)
*   Douglas personal view appears to be that the web (browser) is the only cross platform solution. Steve Jobs and his Adobe Flash would therefore appear to be the correct view – HTML5 and open web standards. Adobe Flash and Microsoft Silverlight (the RIA world) are native platforms). Hence OData is betting on HTTP, and is geared to the web.

~ by mdavey on June 15, 2010.

Posted in [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)
Tags: [Microsoft](https://mdavey.wordpress.com/tag/microsoft/)