<!--yml

category: 未分类

date: 2024-05-18 05:12:27

-->

# Magmasystems Blog: Syncfusion GridControl 与 GroupingGrid 对比

> 来源：[`magmasystems.blogspot.com/2007/02/syncfusion-gridcontrol-vs-groupinggrid.html#0001-01-01`](http://magmasystems.blogspot.com/2007/02/syncfusion-gridcontrol-vs-groupinggrid.html#0001-01-01)

我正在为我的客户端框架编写网格抽象。开发者将针对“虚拟网格”API 进行编码，并将为网格的实际实现（Syncfusion、Infragistics、WinForms、DevExpress 等）提供适配器。

由于大多数华尔街公司使用 Syncfusion 网格进行交易应用，这是我需要编写的第一个适配器。

Syncfusion 有 3 种不同的网格：普通的 GridControl、数据绑定的 DataBoundGrid 和分组网格 GroupingGrid。在我所在的地方，分组网格被广泛用于提供数据的汇总。你会以为 GroupingGrid 会从 GridControl 继承，但令人难以置信的是，它并没有。API 集合甚至都不一致。

我花时间使用 Lutz Roeder 开发的非常出色的 Reflector 工具，试图通过对 Syncfusion 类层次结构的搜索，寻找实现与 GridControl 相同功能的 GroupingGrid 中的各种类和函数。处理两个不兼容的 API 集合使我的工作增加了 100%。

Syncfusion，你们应该知道更好的做法！

©2007 Marc Adler - 版权所有
