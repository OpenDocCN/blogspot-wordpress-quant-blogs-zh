<!--yml

分类：未分类

日期：2024-05-12 19:31:19

-->

# 可复用的电子表格组件——SpreadServe | 编程市场

> 来源：[`etrading.wordpress.com/2015/08/14/reusable-spreadsheets-components-with-spreadserve/#0001-01-01`](https://etrading.wordpress.com/2015/08/14/reusable-spreadsheets-components-with-spreadserve/#0001-01-01)

## 可复用的电子表格组件——SpreadServe

### 2015 年 8 月 14 日

在[SpreadServe beta](https://groups.google.com/forum/#!aboutgroup/spreadserve)中有一些电子表格，它们展示了我在最近的“Spreadsheets are code”帖子中提到的第 3 点（组件复用）。其中的一个——[ycb_quandl_pub.xls](http://54.148.111.119:8888/ycb_quandl_pub.xls/Bootstrapping)——正在[AWS 主机](http://54.148.111.119:8888/dashboard.html)上运行，并且一篇最近的帖子详细解释了它是如何使用[Quandl 数据](https://www.quandl.com/data/FRED/DSWP10-10-Year-Swap-Rate)来驱动[QuantLib 的收益率曲线 bootstrap 函数](http://www.bnikolic.co.uk/ql/addindoc/f/qlPiecewiseYieldCurve.html)。ycb_quandl_pub.xls 与 ycb_quandl_sub.xls 配对使用。您可以从[这里](http://54.148.111.119:8888/repository.html)下载它们，正如它们的名称所暗示的，ycb_quandl_pub.xls 是一个发布者，而 ycb_quandl_sub.xls 是一个订阅者。ycb_quandl_pub.xls 在 Excel 或 SpreadServe 中都能运行得很好，但只有在 SpreadServe 中运行时它才成为一个可复用的组件。尝试下载 ycb_quandl_sub.xls 并在您桌面上的 Excel 中运行它。您需要安装[SSAddin](https://github.com/SpreadServe/SSAddin)才能使其工作。然后您会看到 ycb_quandl_sub.xls 用 ycb_quandl_pub.xls 计算出的 bootstrap 曲线的日期和利率进行了更新。您可能在几分钟内在单元格中看到#N/A，直到服务器首次从服务器发送滴答声，这每五分钟重新计算一次。ycb_quandl_sub.xls 中的 s2cfg 表配置了[SSAddin](https://github.com/SpreadServe/SSAddin)使用其[s2websock 函数](http://spreadserve-addin.readthedocs.org/en/latest/functions.html)订阅[RealTimeWebServer](http://spreadserve.readthedocs.org/en/latest/config.html)发布的利率，每当 ycb_quandl_pub.xls 表在 SpreadServeEngine 实例中重新计算时。RealTimeWebServer 可以支持许多订阅者，所以 ycb_quandl_pub.xls 中从 Quandl、QuantLib 以及工作表公式中的所有逻辑都由所有订阅者共享。具有编辑权限的用户可能在发布者侧更改模型的某些方面，比如 Interpolator 或 TermStructureCalendar，结果所有订阅者都会得到同样的更新数据。熟悉投资银行中典型定价引擎架构的人会认出这里定价引擎图表的构成要素。但主要区别是，实现这一切不需要服务器端的 C++、C#或 Java 编程。量化或交易开发人员电子表格的图表可以非常快地串联在一起。SpreadServe 所可能实现的电子表格级别组件复用的好处是显而易见的。
