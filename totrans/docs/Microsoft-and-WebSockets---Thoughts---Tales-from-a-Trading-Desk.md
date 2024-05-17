<!--yml
category: 未分类
date: 2024-05-18 06:20:51
-->

# Microsoft and WebSockets – Thoughts | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2011/05/04/microsoft-and-websockets-thoughts/#0001-01-01](https://mdavey.wordpress.com/2011/05/04/microsoft-and-websockets-thoughts/#0001-01-01)

## Microsoft and WebSockets – Thoughts

Microsoft has generated a degree of noise around [WebSockets](http://codebetter.com/glennblock/2011/04/24/websockets-riajs-and-wcf-web-api-at-mix-a-whole-lotta-love-for-the-web/) recently – [MIX11](http://channel9.msdn.com/events/mix/mix11/HTM10) onwards. Paul’s [posting](http://www.paulbatum.com/) on MIX11 provides details of the source code available from the Microsoft labs.

So Microsoft is finally going to enter the web “push” space via the [WebSockets](http://blogs.msdn.com/b/interoperability/archive/2010/12/21/introducing-the-websockets-prototype.aspx) W3C WebSockets API Spec – which is positive news. It’s however unfortunate that a majority of the Microsoft Silverlight push data application developed within financial services over the last few years are all powered by Java push servers.

Whilst at the Waters conference last week I met Peter Lankford @ [STAC](http://www.stacresearch.com) who tells me that STAC Research are in the early stages of developing a “last mile” push benchmark spec. Hopefully [Microsoft](http://blogs.msdn.com/b/interoperability/archive/2011/03/09/latest-websockets-release-interoperates-with-eclipse-s-jetty.aspx) will consider benchmarking their WebSockets implementation along with the various other vendors in this space such as Kaazing, my-Channels, Caplin, Lightstreamer, Migratory, Solace Systems etc

Final thoughts: I guess given the feature set of [Azure](http://www.microsoft.com/windowsazure/AppFabric/Overview/default.aspx) Service Bus, if I happen to implement [“Trading in the Cloud”](https://mdavey.wordpress.com/2009/02/02/trading-in-the-cloud/), I end up having to bridge WebSockets to Service Bus myself (think streaming prices)? Surely Microsoft would have been better to extend Azure Service Bus to support WebSockets?

~ by mdavey on May 4, 2011.

Posted in [.NET](https://mdavey.wordpress.com/category/languages/net/), [JavaScript](https://mdavey.wordpress.com/category/languages/javascript/)
Tags: [Microsoft](https://mdavey.wordpress.com/tag/microsoft/)