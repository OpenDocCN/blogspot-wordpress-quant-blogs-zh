<!--yml

类别：未分类

日期：2024-05-18 08:09:10

-->

# 用 QuantLibXL 制作的欧式期权定价器 | Quant Corner

> 来源：[`quantcorner.wordpress.com/2012/10/08/a-european-type-option-pricer-with-quantlibxl/#0001-01-01`](https://quantcorner.wordpress.com/2012/10/08/a-european-type-option-pricer-with-quantlibxl/#0001-01-01)

有一段时间以前，我们为 [欧式期权定价器](https://quantcorner.wordpress.com/2011/01/27/a-pricer-for-european-style-options-on-stocks-a-smooth-start-with-quantlib/ "A pricer for European-style options on stocks. A smooth start with Quantlib") 编写了一段**C++/QuantLib** 代码。 今天，我们开始使用 [**QuantLibXL**](http://quantlib.org/quantlibxl/ "QuantLibXL")，这是一个将 **QuantLib** 函数导出到 **Excel** 的包装器。

我们提供了一个 [QLXL 欧式期权](https://quantcorner.wordpress.com/wp-content/uploads/2012/10/qlxl-european-option.xlsx) 工作簿。 希望仔细研究第二个选项卡能够指导如何使用 **QuantLibXL** 构建期权定价器。

![](https://quantcorner.wordpress.com/wp-content/uploads/2012/10/quantlibxl-european-option-pricer.jpg)
