<!--yml

category: 未分类

date: 2024-05-18 04:55:44

-->

# Magmasystems Blog: 请求：CEP 系统中的流式 R 或 R-like 函数

> 来源：[`magmasystems.blogspot.com/2009/02/request-streaming-r-or-r-like-functions.html#0001-01-01`](http://magmasystems.blogspot.com/2009/02/request-streaming-r-or-r-like-functions.html#0001-01-01)

我最近对 R 语言有所涉猎。我之前在这里写过关于将 R 转换为能够处理实时数据流的东西，或者将 R（或 SPlus）集成到 CEP 系统中的内容。这是一个小例子。假设你想每几秒从流数据中“窗口”样本中抽取一些数据，并对该样本执行某些函数。

让我们看看如何使用静态数据在 R 中实现这一点。

在 R 中，我们可以定义一个从 10.00 美元到 100.00 美元的股价范围，每 25 美分一个增量。

> StockPrices
> 
> StockPrices

[1] 10.00 10.25 10.50 10.75 11.00 11.25 11.50 11.75 12.00 12.25 12.50 12.75 13.00 13.25 13.50 13.75 14.00

...

[358] 99.25 99.50 99.75 100.00

我们可以像这样抽取 10 个随机股价样本：

> sample(StockPrices, 10, rep=F)

[1] 20.50 19.00 78.75 44.75 62.75 45.25 66.25 70.00 71.00 91.00

我们可以像这样计算 10 个随机价格样本的平均价格：

> mean(sample(StockPrices, 10, rep=F))

[1] 52.775

使用 Coral8 术语“窗口”，假设我们有一个名为 StockPrices 的窗口，其中包含了一分钟的股价。每隔 5 秒，我们想要从这个窗口中随机抽取 10 个价格并进行计算，得出这个随机样本的平均价格。

在您的 CEP 系统中如何实现呢？我欢迎 Coral8、Apama、Streambase、Aleri、Esper、StreamSQL 以及其他任何 CEP 系统的示例。

©2009 Marc Adler - 版权所有。

这里的所有观点都是个人的，与我的雇主无关。
