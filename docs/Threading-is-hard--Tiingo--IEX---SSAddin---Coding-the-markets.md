<!--yml

分类：未分类

日期：2024-05-12 19:30:34

-->

# 线程化很难：Tiingo, IEX & SSAddin | 编码市场

> 来源：[`etrading.wordpress.com/2016/05/26/threading-is-hard-tiingo-iex-ssaddin/#0001-01-01`](https://etrading.wordpress.com/2016/05/26/threading-is-hard-tiingo-iex-ssaddin/#0001-01-01)

## 线程化很难：Tiingo, IEX & SSAddin

### 2016 年 5 月 26 日

最近我重新发现了一个事实：线程化很难。我一直扩展[SpreadServe Addin](https://github.com/SpreadServe/SSAddin)以支持[Tiingo](https://www.tiingo.com/)的[IEX 市场数据](https://api.tiingo.com/docs/iex/realtime)实时行情数据。通常只有投资银行、经纪人和大型对冲基金才能获取实时跳动的市场数据，因为要直接连接交易所或通过[路透社](http://www.reuters.com/finance/global-market-data)订阅，需要大量的资金和基础设施。即使是像[xignite](http://www.xignite.com/products)这样的新兴互联网竞争者也非常昂贵。Tiingo 的 IEX 数据提供了一种前所未有的价格点的实时跳动股票簿顶数据。这是我想在 SSAddin 中支持的一个激动人心的新发展。编写它使我重新认识到多线程代码可以有多复杂。SSAddin 用 C#编写，打包成一个[XLL](https://msdn.microsoft.com/en-us/library/office/bb687883.aspx)，使用[ExcelDNA](https://github.com/Excel-DNA/ExcelDna)。与任何 Excel XLL 一样，它定义的工作表函数在主 Excel 线程上执行。如果它们运行时间过长，它们将阻塞 GUI。因此，工作表函数将工作转交给后台线程。这意味着 SSAddin 可以在不阻塞主 Excel 线程的情况下进行[quandl](https://www.quandl.com/)和 tiingo 历史数据查询。查询结果被缓存，还有一组工作表函数可以从缓存中提取结果。到目前为止还不错。然而，向 Tiingo 的 IEX 市场数据添加订阅增加了更多复杂性。在.net 中，web socket 事件的回调在池线程上分派。跳动数据通过[RTD](https://support.microsoft.com/en-us/kb/285339)推回 Excel。因此，需要很多锁语句来协调访问队列，将工作从 Excel 线程传递到后台线程，以及协调访问订阅管理数据结构和 RTDServer 在线程和池线程之间传递 socket 回调。都是很好玩的事情，这也引发了一些思考。首先，线程化很难！其次，我必须抽时间学习[Rust](http://blog.rust-lang.org/)并理解[借用检查器](https://doc.rust-lang.org/book/ownership.html)。第三，谢天谢地，.net 中有[锁重入](http://stackoverflow.com/questions/391913/re-entrant-locks-in-c-sharp)！
