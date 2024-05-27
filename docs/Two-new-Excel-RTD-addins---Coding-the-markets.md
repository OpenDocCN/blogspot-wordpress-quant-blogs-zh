<!--yml

分类：未分类

日期：2024-05-12 19:31:48

-->

# 两个新的 Excel RTD 插件 | Coding the markets

> 来源：[`etrading.wordpress.com/2015/06/30/two-new-excel-rtd-addins/#0001-01-01`](https://etrading.wordpress.com/2015/06/30/two-new-excel-rtd-addins/#0001-01-01)

## 两个新的 Excel RTD 插件

### 2015 年 6 月 30 日

我最近一直在做 Excel RTD 插件的编程工作，因为我正在为[SpreadServe](http://www.spreadserve.com)添加 RTD 支持。在那项工作中，我开发了两个新的插件，我都已经在[github](http://github.com)上发布了。当然，这两个插件都适用于 Excel 和 SpreadServe。第一个插件，[SSAddin](https://github.com/SpreadServe/SSAddin)，支持[quandl.com](http://quandl.com)的查询和在后台线程上执行 Unix cron 风格的事件。当然，这些都可以用 VBA 完成，quandl 的[现有 Excel 插件](https://www.quandl.com/tools/excel)就是这么做的。然而，SSAddin 为你提供了在没有 Visual Basic 和没有手动在 GUI 中输入的情况下，从 quandl 实现自动化、计划下载的手段。第二个插件，[kkaddin](https://github.com/osullivj/kkaddin)，基于[Kenny Kerr](http://kennykerr.ca/)的[C# RTD 示例代码](http://weblogs.asp.net/kennykerr/Rtd3)。在我研究 RTD 时，我阅读了 Kenny 关于这个主题的优秀材料。John Greenan 在他的博客上也有[一些高质量的内容](http://blog.alignment-systems.com/2014/05/excel-rtd-server-implementation-in.html)。然而，我没有找到一个简单的、带有 C#样板代码的下载，可以构建并运行；kkaddin 就是为了解决这个问题。
