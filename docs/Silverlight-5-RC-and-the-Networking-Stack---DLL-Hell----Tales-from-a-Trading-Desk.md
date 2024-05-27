<!--yml

分类: 未分类

日期: 2024-05-18 06:16:12

-->

# Silverlight 5 RC 和网络堆栈 – DLL 地狱？| 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2011/09/05/silverlight-5-rc-and-the-networking-stack-dll-hell/#0001-01-01`](https://mdavey.wordpress.com/2011/09/05/silverlight-5-rc-and-the-networking-stack-dll-hell/#0001-01-01)

## Silverlight 5 RC 和网络堆栈 – DLL 地狱？

周末我决定升级到微软的[Silverlight 5 RC](http://www.silverlight.net/learn/overview/what's-new-in-silverlight-5)。我目前正在开发两个概念验证（POC）应用，它们使用了不同的网络流媒体产品 – 一个喜欢在流媒体领域保持中立 🙂 遗憾的是，运行我的两个应用时似乎得到了混合的结果。

使用 Silverlight 5 RC (5.0.60818.0)和应用 One 的结果：

+   IE9 – 抛出异常告诉我无法连接到流媒体服务器

+   谷歌浏览器 – 这里没有问题，已连接。:)

+   火狐浏览器 – 这里没有问题，已连接 – 速度比谷歌浏览器稍慢。

使用 Silverlight 4 和应用 One 的结果：

+   所有浏览器均无任何问题正常工作

在应用 Two 和流媒体产品 B 的情况下，我能在浏览器中获取几秒钟的实时价格，然后所有三个浏览器都崩溃了 😦

在一台干净的 Win7 64 位机器上，安装有 VS2010，VS2010SP1 和 Silverlight 5 RC 工具，但我仍然在 IE9 上遇到问题。需要进一步调查 😦

有趣的是，Lightstreamer 的[演示](http://www.lightstreamer.com/demo/Silverlight_StockListDemo/)似乎在 Silverlight 5 RC 下通过 HTTP 连接时没有问题 – 但 HTTPS 可能又是另一个问题。

作者：mdavey on September 5, 2011.

发布在:.NET [`mdavey.wordpress.com/category/languages/net/`](https://mdavey.wordpress.com/category/languages/net/)

标签: [微软](https://mdavey.wordpress.com/tag/microsoft/)
