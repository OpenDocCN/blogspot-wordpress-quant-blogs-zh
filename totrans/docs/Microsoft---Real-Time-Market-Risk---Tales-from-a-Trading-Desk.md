<!--yml
category: 未分类
date: 2024-05-18 06:19:36
-->

# Microsoft – Real-Time Market Risk | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2010/03/31/microsoft-real-time-market-risk/#0001-01-01](https://mdavey.wordpress.com/2010/03/31/microsoft-real-time-market-risk/#0001-01-01)

## Microsoft – Real-Time Market Risk

Looks like Microsoft has [acknowledge](http://www.microsoft.com/showcase/en/us/details/0faaf2f5-667e-4313-9bd5-071c9b6df811) that StreamInsight is appropriate for a real-time market risk solution. Unfortunately the video doesn’t talk about a complete Market Risk architecture, but then I suppose the video is only 4:43 long. I would have been nice to see if Microsoft is pushing HPC for the cashflow/PV calculations, leveraging StreamInsight to presumable feed SQL Server R2\. I wonder if Microsoft are pushing WPF or Silverlight for a Market Risk viewer?

Microsoft is also pushing [PowerPivot](http://www.powerpivot.com), for obviously reasons. From what I can see on the PowerPivot site the application deals with snaps shots of data – load, slice dice. What would actually be cooler (maybe I’ve missed this feature in the documentation) is the ability to [subscribe](http://blogs.adatis.co.uk/blogs/sachatomey/archive/2009/10/20/creating-a-custom-gemini-powerpivot-data-feed-method-1-ado-net-data-services.aspx) to real-time data. Basically I’d like to point PowerPivot at my Real-Time [Cube](http://business-intelligence.kdejonge.net/using-powerpivot-to-combine-cube-ssas-data-with-manual-data) (RTC) 🙂

~ by mdavey on March 31, 2010.

Posted in [.NET](https://mdavey.wordpress.com/category/languages/net/), [CEP](https://mdavey.wordpress.com/category/hpc/cep/)
Tags: [MarketRisk](https://mdavey.wordpress.com/tag/marketrisk/), [Microsoft](https://mdavey.wordpress.com/tag/microsoft/), [RealTimeOLAP](https://mdavey.wordpress.com/tag/realtimeolap/)