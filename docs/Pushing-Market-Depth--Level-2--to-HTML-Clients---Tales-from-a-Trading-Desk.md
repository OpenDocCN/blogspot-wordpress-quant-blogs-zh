<!--yml

分类：未分类

日期：2024-05-18 05:42:41

-->

# 将市场深度（Level 2）推送到 HTML 客户端 | 交易桌边的 tales

> 来源：[`mdavey.wordpress.com/2015/05/01/pushing-market-depth-level-2-to-html-clients/#0001-01-01`](https://mdavey.wordpress.com/2015/05/01/pushing-market-depth-level-2-to-html-clients/#0001-01-01)

## 将市场深度（Level 2）推送到 HTML 客户端

Lightstreamer 最近[发布](http://blog.lightstreamer.com/2015/04/market-depth-with-lightstreamer.html#dontscroll84930)了一篇文章，介绍如何将 Level 2 市场数据推送到 HTML 客户端。这篇文章很有趣，提供了阅读源代码以及关于演示如何工作的适当评论。我认为缺失的部分，也许 Lightstreamer 可以在未来的文章中更新，在我看来应该是以下内容：

+   针对 WebSockets 和非 WebSockets 的性能数据

+   文章中提到的 Lightstreamer 可能拥有的关于数据适配器和过滤的其他文章的链接。当客户端（HTML）被数据淹没，无法跟上绘制（渲染）时，过滤尤其关键。

+   对客户端断开连接和重新连接以及这对市场数据推送的影响的评论。同样，对服务器（适配器死亡）以及故障转移、恢复的性能的评论。

+   带宽使用情况

总体来说，这篇文章很有趣

~ mdavey 于 2015 年 5 月 1 日。

发布在 [Java](https://mdavey.wordpress.com/category/languages/java/)，[JavaScript](https://mdavey.wordpress.com/category/languages/javascript/)，[交易](https://mdavey.wordpress.com/category/trading/)
