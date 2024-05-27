<!--yml

分类：未分类

日期：2024-05-18 06:00:13

-->

# Lightstreamer：WebSocket 全双工、双向、实时数据传输 | 交易桌面故事

> 来源：[`mdavey.wordpress.com/2013/10/07/lightstreamer-websocket-full-duplex-bi-directional-real-time-data-delivery/#0001-01-01`](https://mdavey.wordpress.com/2013/10/07/lightstreamer-websocket-full-duplex-bi-directional-real-time-data-delivery/#0001-01-01)

## Lightstreamer：WebSocket 全双工、双向、实时数据传输

Lightstreamer 提供了[洞察](http://blog.lightstreamer.com/2013/10/optimizing-multiplayer-3d-game.html)信息，介绍其实时 Web 服务器如何能够助力多玩家 3D 游戏提供令人印象深刻的带宽使用，尽管使用了 Lightstreamer 的节流算法（起源于金融行业）。动态变量对用户数据的实时重塑是关键。

+   **带宽分配**：对于每个客户端，可以为其多路复用流连接分配最大带宽。这样的分配可以随时更改，并且 Lightstreamer 保证它始终得到尊重，无论原始数据流带宽是多少。

+   **频率分配**：对于每个客户端的多路复用流连接中的每个数据流（在 Lightstreamer 术语中称为订阅），可以分配最大更新频率。同样，这样的分配可以随时更改。

+   **实时带宽检测**：互联网拥堵会自动检测，并且 Lightstreamer 持续适应可用的实际带宽。

文章中也提到了合并（conflation），这在带宽有限和客户端计算能力有限时非常重要：

> 重塑与**合并**效果更好。合并意味着，在重塑过程中，发送者应该尝试合并更新，以保存尽可能多的信息，而不是简单地丢弃更新。

最后，源代码在 GitHub 上提供，让读者能够尝试 Lightstreamer 订阅模式和消息路由等功能。

~ mdavey 于 2013 年 10 月 7 日。

发布于[JavaScript](https://mdavey.wordpress.com/category/languages/javascript/)、[交易](https://mdavey.wordpress.com/category/trading/)

标签：[Lightstreamer](https://mdavey.wordpress.com/tag/lightstreamer/)、[WebSocket](https://mdavey.wordpress.com/tag/websockets/)
