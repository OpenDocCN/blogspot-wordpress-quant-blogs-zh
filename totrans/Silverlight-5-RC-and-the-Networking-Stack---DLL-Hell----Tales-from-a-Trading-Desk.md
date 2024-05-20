<!--yml
category: 未分类
date: 2024-05-18 06:16:12
-->

# Silverlight 5 RC and the Networking Stack – DLL Hell? | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2011/09/05/silverlight-5-rc-and-the-networking-stack-dll-hell/#0001-01-01](https://mdavey.wordpress.com/2011/09/05/silverlight-5-rc-and-the-networking-stack-dll-hell/#0001-01-01)

## Silverlight 5 RC and the Networking Stack – DLL Hell?

Over the weekend I decided to upgrade to Microsoft [Silverlight 5 RC](http://www.silverlight.net/learn/overview/what's-new-in-silverlight-5). I’m currently working on two Proof Of Concept (POC) applications that use different web streaming products – one likes to remain neutral in the streaming space 🙂 Unfortunately I appear to be getting mixed results from running my two applications.

The results with Silverlight 5 RC (5.0.60818.0) and Application One:

*   IE9 – Exceptions thrown that tell me I can’t connect to the streaming server
*   Chrome – No issues here, connected. 🙂
*   Firefox – No issues here, connected – slightly slowed than Chrome.

The results with Silverlight 4 and Application One:

*   All browser’s work without any issue

In the case of application Two and Streaming Product B, I get real-time prices into the browser for a few seconds, and then all three browsers crash 😦

With a clean Win7 64bit machine, VS2010, VS2010SP1 and the Silverlight 5 RC tools I still seem to get issues with IE9\. More investigation needed 😦

Interestingly, Lightstreamer’s [demo](http://www.lightstreamer.com/demo/Silverlight_StockListDemo/) appears to be find with Silverlight 5 RC – at least over HTTP, HTTPS maybe another questions

~ by mdavey on September 5, 2011.

Posted in [.NET](https://mdavey.wordpress.com/category/languages/net/)
Tags: [Microsoft](https://mdavey.wordpress.com/tag/microsoft/)