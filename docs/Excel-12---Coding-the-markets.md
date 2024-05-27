<!--yml

category: 未分类

date: 2024-05-12 19:52:52

-->

# Excel 12 | 编码市场

> 来源：[`etrading.wordpress.com/2006/06/09/excel-12/#0001-01-01`](https://etrading.wordpress.com/2006/06/09/excel-12/#0001-01-01)

## Excel 12

### 2006 年 6 月 9 日

[Excel 12](http://blogs.msdn.com/excel/)，也就是 Excel 2007，对前台开发人员来说将是一个重要的版本。我一直在思考，经过了[为实时定价编写 XLLs](https://etrading.wordpress.com/excel/) 和自动报价，我纳闷 Excel 何时才能支持多线程计算。[好消息](http://blogs.msdn.com/excel/archive/2006/01/03/508985.aspx) 是，Excel 12 添加了 XLL 工作表函数的多线程执行。这意味着定价表现在可以充分利用多处理器主机。

那么下一个问题就是：能否在新的[Excel Server](http://blogs.msdn.com/excel/archive/category/11361.aspx)环境中运行定价 XLLs？在交易桌上，我们对处理器的性能有限制。由于散热和功率限制，我们的交易员每个交易桌只限用两台 2CPU 的 PC。如果他们需要更多的 CPU，我们就必须在机房使用刀片服务器作为远程桌面。将定价表托管在服务器上将很好地解决这些问题。

幸运的是，看起来答案是肯定的，只要进行[托管代码的封装](http://blogs.msdn.com/excel/archive/2006/05/03/589094.aspx)。
