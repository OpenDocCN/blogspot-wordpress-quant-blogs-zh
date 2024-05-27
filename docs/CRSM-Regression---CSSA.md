<!--yml

category: 未分类

date: 2024-05-12 17:51:26

-->

# CRSM 回归 | CSSA

> 来源：[`cssanalytics.wordpress.com/2014/11/07/crsm-regression/#0001-01-01`](https://cssanalytics.wordpress.com/2014/11/07/crsm-regression/#0001-01-01)

在上一篇文章中，我介绍了如何使用[聚类随机子空间（CRSM）](https://cssanalytics.wordpress.com/2014/11/05/cluster-random-subspace-a-process-diagram/ "聚类随机子空间-过程图解")进行投资组合优化的示意图。但这个概念可以扩展到预测和分类。显然，“随机森林”可以将这个概念纳入，以用更少的样本构建优秀的决策树——但我要警告说，决策树在预测金融时间序列时往往表现不佳（这是由于二元阈值化和过拟合导致的）。然而，标准的多元回归在金融领域一直是一个重要工具，因为它比其他机器学习方法更稳健，不容易过拟合。回归的一个挑战是当你有很多变量可供选择时，其中一些变量高度相关时，它就会崩溃。有许多已建立的解决此问题的方法（PCA、逐步回归等），但 CRSM 仍然是一个优秀的选择，因为它可以从大量的预测变量中形成一个稳健的集成预测。它并不解决变量的初始选择，但至少它可以自动处理可能包含一些高度相关变量的大量候选变量。CRSM 回归是一个很好的方法，当你有很多可能的指标，但没有任何预先构建一个好模型的想法时。这是一个应用 CRSM 回归的许多可能方法的流程图之一：

![crsm-regression](https://cssanalytics.files.wordpress.com/2014/11/crsm-regression2.png)
