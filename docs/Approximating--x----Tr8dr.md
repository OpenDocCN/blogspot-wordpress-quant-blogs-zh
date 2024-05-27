<!--yml

类别：未分类

日期：2024-05-18 15:35:21

-->

# 近似 |x| | Tr8dr

> 来源：[`tr8dr.wordpress.com/2010/01/02/approximating-abs-x/#0001-01-01`](https://tr8dr.wordpress.com/2010/01/02/approximating-abs-x/#0001-01-01)

我正在改变我的投资组合策略，使用内点优化器解决带约束的非线性问题。 该方法解决了以下形式的非线性问题：

![](https://tr8dr.wordpress.com/wp-content/uploads/2010/01/screen-shot-2010-01-02-at-1-42-24-pm.png)

其中 f(x) 是要最小化的主要函数，g(x) 表示一个或多个约束（相等或不等式）。 有很多关于解决这类问题的内点方法的好 [论文](http://www.math.kth.se/~andersf/doc/sirev41494.pdf)，所以我在这里不会详细介绍该方法。

在我这种情况下，其中一个约束如下：

![](https://tr8dr.wordpress.com/wp-content/uploads/2010/01/screen-shot-2010-01-02-at-1-50-33-pm.png)

尽管这看起来很简单，但它提出了一个问题，因为内部点算法要求约束具有两次可微性。 |x| 在 0 处连续但不可微。 在构建解决方案时，我需要构造约束的梯度（雅可比）和黑塞矩阵。

我开始考虑其他描述约束的方法。 基本上，我希望我的投资组合能够在交易期间分配多头和空头头寸。 上述约束将多头和空头资本视为对称（这符合我的目的）。 也就是说，如果我的投资组合中只有两个资产，并且将其中一个资产分配为 -0.75% 的空头，另一个资产分配为 0.25% 的多头，我将认为这是完全分配的（从风险资本的角度来看）。

我进行了一些思想实验，考虑了以下变化：

![](https://tr8dr.wordpress.com/wp-content/uploads/2010/01/screen-shot-2010-01-02-at-2-01-19-pm.png)

但这显然是错误的，因为将允许分配 > 100%。 我开始思考 |x| 的导数函数。 见（蓝色为 |x|，红色为导数）：

![](https://tr8dr.wordpress.com/wp-content/uploads/2010/01/abs-derivative.png)

这让我想到，导数可以通过 S 型函数进行渐近近似，带有偏移和加速指数：

![](https://tr8dr.wordpress.com/wp-content/uploads/2010/01/sigmoid.png)

通过使 β 足够大，我们可以以任意分辨率逼近 |x| 的导数。

不幸的是，S 型函数的积分在 **R** 中没有解，只在复平面上有解，这意味着如果我们要采用这种方法，将必须用 Σ|x| 评估 g(x) 和缩放和平移的 S 型函数的导数。

不幸的是，将 |x| 用于约束评估，而使用 Sigmoid 用于导数的混合方法会导致不稳定性。需要有一个具有积分的导数近似。

**附录**

原来这是机器学习和优化中的一个常见问题。Chen 和 Mangasarian 定义了对 Sigmoid 积分的近似。问题可以重新表述如下。将问题分解为两个部分，x ≥ 0 和  x ≤ 0。如果我们可以解决 x ≥ 0 的问题，那么我们也有 x ≤ 0 的解：

![](https://tr8dr.wordpress.com/wp-content/uploads/2010/01/screen-shot-2010-01-03-at-11-25-02-am.png)

基于对 Sigmoid 积分的近似，他们确定 (x)+ 为：

![](https://tr8dr.wordpress.com/wp-content/uploads/2010/01/screen-shot-2010-01-03-at-11-28-58-am.png)

与 Sigmoid 函数一样，增加 β 可以使我们逼近 |x|。现在我们有一个在 0 点周围定义了导数的 |x| 函数。
