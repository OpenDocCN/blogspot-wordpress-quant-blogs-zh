<!--yml

分类：未分类

日期：2024 年 05 月 12 日 19:37:54

-->

# 单一经销商平台的 F# | 编码市场

> 来源：[`etrading.wordpress.com/2009/12/21/f-for-single-dealer-platforms/#0001-01-01`](https://etrading.wordpress.com/2009/12/21/f-for-single-dealer-platforms/#0001-01-01)

## 单一经销商平台的 F#

### 2009 年 12 月 21 日

Matt [在这里](http://mdavey.wordpress.com/2009/12/21/thoughts-on-f-within-a-single-dealer-platform-sdp/) 分享了他的想法，关于 F#用于 SDP 实现的想法[在这里](http://mdavey.wordpress.com/2009/12/21/thoughts-on-f-within-a-single-dealer-platform-sdp/)。我对 F#的了解不及他，但我曾在家里的 Ubuntu 上尝试过 VS2010 并玩过 OCAML。我相信无状态的函数式方法将在结构化服务器进程的异步性和并发性方面提供很大帮助。所以我在这里同意他的论点的总体方向。

对于 Matt 的一句话我有些异议：“如果你考虑一个 SDP，它主要是一个集成构建”。我曾听过相同观点的经理们认为 SDP 的构建只是将一些供应商服务器（如 Caplin 的 Liberator）与内部中间件（如 TIB）连接起来的微不足道的事情，然后引用和执行就会流动。事实远非如此简单。我更愿意说，构建 SDP 就像构建 ECN 一样。把它想象成建立你自己的彭博或 TradeWeb。
