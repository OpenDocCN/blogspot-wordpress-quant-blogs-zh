<!--yml

类别: 未分类

日期：2024 年 05 月 12 日 19 时 31 分 24 秒

-->

# 使用 QuantLib 和 Quandl 进行收益率曲线拟合 | 编程市场

> 来源：[`etrading.wordpress.com/2015/08/08/yield-curve-bootstrapping-with-quantlib-quandl/#0001-01-01`](https://etrading.wordpress.com/2015/08/08/yield-curve-bootstrapping-with-quantlib-quandl/#0001-01-01)

## 使用 QuantLib 和 Quandl 进行收益率曲线拟合

### 2015 年 8 月 8 日

[在昨天的帖子中](https://etrading.wordpress.com/2015/08/07/spreadserve-resources/)，我承诺会详细介绍在[托管在亚马逊的 SpreadServe 实例](http://54.148.111.119:8888/dashboard.html)上运行的[收益率曲线拟合表](http://54.148.111.119:8888/ycb_quandl_pub.xls/Bootstrapping)。如果你想在自己的桌面上运行该表格，可以从[存储库](http://54.148.111.119:8888/repository.html)下载；只需点击 ycb_quandl_pub.xls。要在自己的 Excel 中运行该表格，你需要下载 [QuantLib](http://quantlib.org/quantlibxl/) 和 [SpreadServe 插件](https://github.com/SpreadServe/SSAddin)。ycb_quandl_pub.xls 基于 QuantLibXL 的一个示例电子表格，[YieldCurveBootstrapping.xls](https://github.com/arthurpham/quantlib-full/blob/master/QuantLibXL/Workbooks/StandaloneExamples/YieldCurveBootstrapping.xls)，提供了一个常见的固定收益率数学问题的 QuantLib Excel 解决方案示例：收益率曲线的拟合。如果你查看原始表格，你会发现所有的输入数据都以简单的单元格值的形式存在。要更改它，你必须重新输入。理想情况下，这应该是自动化的，这样存款、期货和掉期利率就可以定期从干净的数据源中提取，并重新计算并发布拟合结果。ycb_quandl_pub.xls 使用 SpreadServe 插件从 quandl 获取存款、期货和掉期利率。在 ycb_quandl_pub 工作簿的 Quandl 表格的左上角区块中，你可以看到从 quandl.com 将利率拉入表格的 s2quandl 函数的调用。在同一表格的较低位置，你可以看到 s2cron 的调用，它安排一个定时器每 5 分钟触发一次新的数据下载。相同的触发器用作 QuantLib 的 qlPieceWiseYieldCurve 函数在拟合表格上的输入，以在刚下载的数据到达时强制重新计算。所有这些都非常适用于自动化 Excel 电子表格。有了 SpreadServe，我们可以更进一步，将表格从桌面移到服务器上。整个过程都是自动化的、集中化的，并且不受桌面可能的手动干扰的影响。

注意 QuantLib 的日期计算意味着此表格的结果仅在工作日（周一至周五）有效，而非周六或周日。
