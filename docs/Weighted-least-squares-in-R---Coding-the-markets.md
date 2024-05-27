<!--yml

分类：未分类

日期：2024-05-12 19:51:03

-->

# 在 R 中的加权最小二乘 | 编码市场

> 来源：[`etrading.wordpress.com/2006/08/18/weighted-least-squares-in-r/#0001-01-01`](https://etrading.wordpress.com/2006/08/18/weighted-least-squares-in-r/#0001-01-01)

## 在 R 中的加权最小二乘

### 2006 年 8 月 18 日

我正在使用 R 对具有由低观测次数支持的离群值的数据进行曲线拟合。我一直在尝试使用不同的 R 拟合方法，包括 [glm.fit](https://etrading.wordpress.com/2006/08/15/the-power-of-r-curve-fitting/)。但是线性拟合显然是错误的。作为一个非数学专业毕业生，我有点困惑，直到我和我们更数学和技术头脑的模型交易员交谈。他看了我的图表和数据，并建议使用加权最小二乘拟合。

在 R 中，我们可以使用 `loess()` 和 `predict()` 进行最小二乘拟合。给定包括权重在内的样本数据，`loess()` 将生成拟合参数。然后，你将数据点通过 `predict()` 传递给图表化，同时传递拟合参数，并绘制出漂亮的平滑结果。在 R 中执行 `example(loess)` 即可开始。
