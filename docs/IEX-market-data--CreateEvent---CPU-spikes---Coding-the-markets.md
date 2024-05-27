<!--yml

分类：未分类

日期：2024-05-12 19:30:09

-->

# IEX 市场数据、CreateEvent 与 CPU 波动|编码市场

> 来源：[`etrading.wordpress.com/2017/02/23/iex-market-data-createevent-cpu-spikes/#0001-01-01`](https://etrading.wordpress.com/2017/02/23/iex-market-data-createevent-cpu-spikes/#0001-01-01)

## IEX 市场数据、CreateEvent 与 CPU 波动

### 2024 年 5 月 12 日 19:30:09

本周，我一直在测试[SpreadServe 插件](https://github.com/SpreadServe/SSAddin)与[Tiingo 的 IEX 市场数据](https://api.tiingo.com/docs/iex/realtime)。我在我的[sscalc0.online](http://sscalc0.online)的[AWS](https://aws.amazon.com/)主机上检查了一组[SpreadServeEngines](http://spreadserve.readthedocs.io/en/latest/guide.html)执行各种测试和演示电子表格的表现，包括一个通过[Tiingo API websockets](https://api.tiingo.com/docs/general/overview)订阅[IEX](https://www.iextrading.com/)跳动器用于 AAPL 和 SPY 的电子表格。该 API 为我们提供了 IEX 上现金股票交易的实时最前线以及最后的交易价格和数量。在我的测试场景中，我运行了五个引擎，其中两个闲置，三个运行电子表格，其中一个是一个简单的 IEX 市场数据订阅者。使用[进程浏览器](https://technet.microsoft.com/en-us/sysinternals/processexplorer.aspx)，我发现一些空闲引擎上有奇怪的 CPU 波动。使用进程浏览器缩小查看，我可以看到忙碌是在一个本应空闲的线程中，在[WaitForSingleObject](https://msdn.microsoft.com/en-us/library/windows/desktop/ms687032(v=vs.85).aspx)调用中休眠，等待一个信号来检查其输入队列。等待的对象事件是由一些通用代码调用的[win32 的 CreateEvent](https://msdn.microsoft.com/en-us/library/windows/desktop/ms682396(v=vs.85).aspx)创建的，并在另一个线程中使用。阅读文档，我发现 CreateEvent 的第四个参数，事件对象名称，意味着如果名称匹配，调用者将获得一个先前创建的事件对象的句柄。而我使用的是一个固定的名称！所以我的线程反复被另一个线程的事件唤醒。为使名称唯一，快速修复，产生了没有不必要的 CPU 烧毁的空闲引擎。这一切都非常富有教益，部分原因是运行在 AWS 上会让人非常注意按 CPU 小时付费。
