<!--yml

分类：未分类

日期：2024-05-18 06:20:51

-->

# Microsoft 和 WebSockets - 想法 | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2011/05/04/microsoft-and-websockets-thoughts/#0001-01-01`](https://mdavey.wordpress.com/2011/05/04/microsoft-and-websockets-thoughts/#0001-01-01)

## Microsoft and WebSockets – Thoughts

Microsoft 最近围绕[WebSockets](http://codebetter.com/glennblock/2011/04/24/websockets-riajs-and-wcf-web-api-at-mix-a-whole-lotta-love-for-the-web/)产生了一定程度的噪音——从[MIX11](http://channel9.msdn.com/events/mix/mix11/HTM10)开始。Paul 在 MIX11 上的[博文](http://www.paulbatum.com/)提供了可以从微软实验室获取的源代码的详细信息。

所以微软最终将通过[WebSockets](http://blogs.msdn.com/b/interoperability/archive/2010/12/21/introducing-the-websockets-prototype.aspx) W3C WebSockets API 规范进入网络“推送”领域，这是一个积极的消息。然而不幸的是，微软 Silverlight 推送数据应用程序的大多数在过去几年在金融服务领域开发，都是由 Java 推送服务器支持的。

上周在水星会议上，我遇到了 STAC 的 Peter Lankford @ [STAC](http://www.stacresearch.com)，他告诉我 STAC 研究正处于开发“最后一段”推送基准规范的早期阶段。希望微软[WebSockets](http://blogs.msdn.com/b/interoperability/archive/2011/03/09/latest-websockets-release-interoperates-with-eclipse-s-jetty.aspx)的实现将考虑与这个领域的其他各种供应商（如 Kaazing，my-Channels，Caplin，Lightstreamer，Migratory，Solace Systems 等）一起基准测试。

最后想法：我想鉴于 Azure 服务总线的功能集，如果我实现[“云中的交易”](https://mdavey.wordpress.com/2009/02/02/trading-in-the-cloud/)，我最终可能不得不自己将 WebSockets 桥接到服务总线（想想流价格）？微软扩展 Azure 服务总线以支持 WebSockets 岂不是更好？

~ mdavey 于 2011 年 5 月 4 日。

发布于[.NET](https://mdavey.wordpress.com/category/languages/net/)，[JavaScript](https://mdavey.wordpress.com/category/languages/javascript/)

标签：[Microsoft](https://mdavey.wordpress.com/tag/microsoft/)
