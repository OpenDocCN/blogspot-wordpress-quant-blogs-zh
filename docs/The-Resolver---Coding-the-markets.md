<!--yml

分类：未分类

日期：2024-05-12 19:44:18

-->

# 解决者 | 编写市场代码

> 来源：[`etrading.wordpress.com/2008/02/01/the-resolver/#0001-01-01`](https://etrading.wordpress.com/2008/02/01/the-resolver/#0001-01-01)

## 解决者

### 2008 年 2 月 1 日

所以我对[Resolver One](http://www.resolversystems.com/)小试了一下，现在它已经完成了测试版，发布了 1.0 版本。为了提供一个稍微简单的看法，它是一个用 IronPython 实现的 Excel 克隆。它在暴露其内部结构方面超过 Excel 的是，它将计算模型和工作表以一种无缝的方式展示出来。在 Excel 中，我们有几种不同的 API 可以将我们自己的逻辑注入到电子表格中：Excel 自身的内部 C API 用于编写 XLLs，VBA 和 COM。这些 API 允许我们用 C、VB 和任何 COM 语言表达工作表功能。Resolver 以其内部结构在我们最喜欢的编程语言 Python 中提供了一个无缝的视图给我们。简单的例子[在此](http://www.resolversystems.com/documentation/index.php/The_Auto-Total)。

这对于那些已经使用 Python 进行前端系统的人来说是有吸引力的。我不确定它对其他人会有多大的吸引力……
