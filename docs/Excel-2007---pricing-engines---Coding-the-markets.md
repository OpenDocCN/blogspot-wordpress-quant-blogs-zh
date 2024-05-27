<!--yml

category: 未分类

date: 2024-05-12 19:52:04

-->

# Excel 2007 和定价引擎 | 编码市场

> 来源：[`etrading.wordpress.com/2006/07/27/excel-2007-pricing-engines/#0001-01-01`](https://etrading.wordpress.com/2006/07/27/excel-2007-pricing-engines/#0001-01-01)

## Excel 2007 和定价引擎

### 2006 年 7 月 27 日

我参加了周二晚上在瑞士信贷的 Office 2007 活动。Jim Burns，微软英国金融服务首席技术官开启了这个活动。一位来自瑞士信贷的名叫 Leslie 的人讲了几分钟。他宣布他在瑞士信贷的研发部门工作，他们确定了未来 3 到 5 年的新兴趋势，并且虚拟化和 MS Office 2007 的分布式工作功能是即将到来的事物。然后 Ian Moulster，微软英国开发和平台组的产品经理简短地讲了几句。最后，我们得到了三明治的核心部分，由 Paul Foster，Excel Services 和 InfoPath 的开发者推广员进行了长达一小时的演示。

Excel 服务基于 Sharepoint，似乎提供了一些应用程序服务器般的托管新型 Excel 服务器计算引擎。Excel 服务器托管的工作表可以在浏览器中呈现，并支持使用 AJAX 技术进行交互。Excel 服务器托管的工作表也可以通过客户端使用 Web 服务 API 进行编程调用。Paul 几次提到了 [XLLs](https://etrading.wordpress.com/excel/)。我之后问了他有关它们的问题。从 [Excel 12 博客](http://blogs.msdn.com/excel) 看来，[客户端 Excel 上的 C/C++ XLLs](http://blogs.msdn.com/excel/archive/2006/01/03/508985.aspx) 将是类似的。但是，在 Excel 服务下运行的服务器端 XLL，[必须是托管代码](http://blogs.msdn.com/excel/archive/2006/05/03/589094.aspx)，虽然未托管代码可以包装。当我问 Paul 关于向服务器端工作表注入实时数据的问题时，他表示我的 [基于 DDE 的技术](https://etrading.wordpress.com/excel/) 对于 Excel 服务是行不通的，因为 Windows 权限将不允许它。现在 [cumgranosalis](http://blogs.msdn.com/cumgranosalis) 博客告诉我们 [RTD 实际上不适用于 Excel 服务](http://blogs.msdn.com/cumgranosalis/archive/2006/05/23/RTDPart1.aspx)。

为什么这是一个问题？交易员在 Excel 中实现临时定价引擎并不罕见。我曾经参与过一个基于 Excel 的系统，自动报价交易所交易的期权策略。重新计算由实时期货价格驱动 - 未来是期权的基础。我们使用 DDE 注入了期货价格。看起来可能无法使用 Excel 服务来实现这种类型的系统，这非常遗憾。
