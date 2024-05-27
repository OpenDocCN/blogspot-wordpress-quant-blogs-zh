<!--yml

类别：未分类

日期：2024 年 05 月 12 日 17:56:05

-->

# 使用 FTCA 的免费基于 Web 的聚类应用程序 | CSSA

> 来源：[`cssanalytics.wordpress.com/2013/12/17/free-web-based-cluster-application-using-ftca/#0001-01-01`](https://cssanalytics.wordpress.com/2013/12/17/free-web-based-cluster-application-using-ftca/#0001-01-01)

了解聚类最有用的方法之一是使用可视化应用程序，在一段时间内看不同的聚类分组。 在之前的一篇文章中，我介绍了[快速阈值聚类算法](https://cssanalytics.wordpress.com/2013/11/26/fast-threshold-clustering-algorithm-ftca/ "快速阈值聚类算法（FTCA）")-  FTCA- 作为一种简单直观的资产聚类方法。一位同行的量化研究员和长期读者 Pierre Chretien 很友好地与 Michael Kapler 合作在 R 中构建了一个 FTCA Shiny Web 应用。 它展示了在使用指数数据进行回溯的广泛资产类别上，使用 FTCA 进行聚类的情况。用户可以尝试不同参数，如聚类时的时间段（图表日期），聚类形成的相关阈值，以及用于相关性计算的回溯期。  另一个有用的输出是在聚类形成时每个资产的回报和波动性，以及每个资产的历史聚类成员资格的转换图。 应用程序的两个图像如下所示。 非常酷的东西，做得很好！ 我个人很享受使用它来看不同参数的影响，以及不同时间段的历史聚类。

应用程序的链接可以在这里找到：

[聚类 Web 应用程序](http://glimmer.rstudio.com/heuristica/clusters/)

![cluster application1](https://cssanalytics.files.wordpress.com/2013/12/cluster-application1.png)

![cluster application2](https://cssanalytics.files.wordpress.com/2013/12/cluster-application2.png)
