<!--yml

category: 未分类

date: 2024-05-12 19:41:56

-->

# 使用 Caplin 构建 | 编码市场

> 来源：[`etrading.wordpress.com/2008/07/08/building-with-caplin/#0001-01-01`](https://etrading.wordpress.com/2008/07/08/building-with-caplin/#0001-01-01)

## 使用 Caplin 构建

### 2008 年 7 月 8 日

所以，让我们想象一下，你正在使用 [Caplin Trader](http://www.caplin.com/caplintrader) 从 [Caplin Systems](http://www.caplin.com/about/) 构建银行的全新单一经销商渠道。你选择了 Caplin，因为它在流媒体 [comet server](http://cometdaily.com/) 领域是明显的领导者，并且你希望将你的电子交易应用程序交付到浏览器中，以便客户端桌面上零安装。还有其他供应商提供了与 Caplin 的 Liberator 相竞争的可行方案作为 [comet server](http://www.freeliberator.com/documentation/)，其中 [Lightstreamer](http://www.lightstreamer.com/) 是明显的第二名。还有一些有趣的新供应商进入了这个领域，比如 [Kaazing](http://www.kaazing.com/)，还有 [开源产品](http://cometdproject.dojotoolkit.org/)。但是，没有一个像 Caplin Liberator 那样成熟或在生产中的电子交易应用程序中被广泛部署。

向浏览器实时传送报价的服务器只是构建 web 2.0 电子交易应用的谜题中的一部分。你需要在浏览器中构建 GUI，并且你需要一个执行系统来处理 RFQ/RFS。与其他供应商不同，Caplin 提供了 Caplin Trader GUI 和 Trading Data Source。GUI 基于 [SoCentric](http://www.socentric.com/) 的 JavaScript 小部件工具包，而 Trading Data Source 则提供可配置的状态机，以在 RFQ 票证的生命周期内将 GUI 和服务器端状态保持同步。
