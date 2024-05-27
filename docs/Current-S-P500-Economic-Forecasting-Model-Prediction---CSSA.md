<!--yml

类别：未分类

日期：2024 年 5 月 12 日 17:42:04

-->

# 当前 S&P500 经济预测模型预测 | CSSA

> 来源：[`cssanalytics.wordpress.com/2019/05/27/current-sp500-economic-forecasting-model-prediction/#0001-01-01`](https://cssanalytics.wordpress.com/2019/05/27/current-sp500-economic-forecasting-model-prediction/#0001-01-01)

我们将我们的[机器学习经济预测模型](https://cssanalytics.wordpress.com/2019/05/14/shiny-new-toys/)介绍为一种新颖的、压缩大量经济数据以衡量经济健康从而预测股票市场周期性（而非情绪驱动）回落的新方法。当前预测使用了两种不同的模型：

1) **时间点复合** - 该模型仅在所有模型所需的数据在可用时创建预测。如果模型正在等待数据，则简单地延续上一次在所有数据可用时做出的预测。[历史预测表](https://cssanalytics.wordpress.com/2019/05/15/current-sp500-economic-forecasting-model-introduction/)是使用该模型生成的。

2) **初步** - 该模型使用可用数据进行训练，并且能够在复合模型正在等待的缺失数据时进行预测。它通过对缺失数据进行插值来实现这一点。当前由于有三个缺失数据，我们只能对到 6 月底进行初步预测。

## 当前预测-初步

针对预测期间 **2019 年 4 月 - 2019 年 6 月**，该模型根据截至 **2019 年 3 月 31 日** 的经济数据预测以下结果：

+   在 2019 年 4 月至 2019 年 6 月之间发生大幅修正的可能性合理吗？ **不可预期**

+   2019 年 4 月至 2019 年 6 月之间的收益预测方向是什么？ **平稳**
