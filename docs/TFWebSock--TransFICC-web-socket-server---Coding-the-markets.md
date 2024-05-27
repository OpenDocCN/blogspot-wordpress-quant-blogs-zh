<!--yml

分类：未分类

日期：2024-05-12 19:29:27

-->

# TFWebSock: TransFICC 网络 Socket 服务器 | 编码市场

> 来源：[`etrading.wordpress.com/2017/09/05/tfwebsock-transficc-web-socket-server/#0001-01-01`](https://etrading.wordpress.com/2017/09/05/tfwebsock-transficc-web-socket-server/#0001-01-01)

## TFWebSock: TransFICC 网络 Socket 服务器

### 2017 年 9 月 5 日

我刚刚更新了我的基于 Netty 的 TransFICC 网络 Socket 服务器，以支持[版本 330cb31-3670](https://github.com/TransFICC/client-library/releases/tag/2de5581)的[TransFICC API](https://transficc.com/products)和服务。[TFWebSock](https://github.com/SpreadServe/TFWebSock)允许网络 Socket 客户端订阅来自 TransFICC 的市场数据。这些网络 Socket 客户端当然可以是浏览器，但在[此演示](http://sscalc0.online/tfsock3.xls/Swaps)中，客户端是[SSAddin Excel 插件](https://github.com/SpreadServe/SSAddin)。这意味着你可以使用 TFWebSock 和 SSAddin 将实时的计价[ICAP iSwap](http://www.icap.com/what-we-do/electronic-markets/i-swap.aspx)掉期汇率拖拽到你的桌面 Excel 中。如果你想要自动化并服务器化那个电子表格，你可以使用[SpreadServe](http://spreadserve.com)来实现。

我应该指出，此演示中的计价率来自 iSwap 测试系统，并非实时生产率。感谢 TransFICC 和 ICAP 团队提供此数据！
