<!--yml

类别：未分类

日期：2024 年 5 月 18 日 15:34:58

-->

# 算法差异化 | Tr8dr

> 来源：[`tr8dr.wordpress.com/2010/01/11/algorithmic-differentiation/#0001-01-01`](https://tr8dr.wordpress.com/2010/01/11/algorithmic-differentiation/#0001-01-01)

在之前的帖子中，我概述了一个带有风险惩罚的投资组合效用函数：

![](https://tr8dr.wordpress.com/wp-content/uploads/2010/01/utility.png)

这个函数的一个组成部分，E[r]，被指定为加权几何平均数。我可以将其转换为使用对数和，但不能简化为添加的风险项：

![](https://tr8dr.wordpress.com/wp-content/uploads/2010/01/geometric.png)

我需要为上述函数构建梯度和海森矩阵：

![](https://tr8dr.wordpress.com/wp-content/uploads/2010/01/derivs.png)

并不是说第二个偏导数难以处理，事实上，它只需要应用链式法则。不幸的是，它会扩展成一个随着变量数量呈二次增长的巨大复杂表达式。

通过有限差分计算导数对于某些应用程序有效，但在“扰动”需要很小的情况下会出现问题。使用中心加权方案计算第二个导数：

![](https://tr8dr.wordpress.com/wp-content/uploads/2010/01/central.png)

可以看出，差分方法易受下溢影响。选择一个值为**h** **< 1e-7**的值会产生超出双精度精度的值（考虑分母）。一旦超出双精度的精度，结果将毫无意义。

**算法方法**

我开始考虑一种递归方法来评估第 n 个偏导数，因为我很难找到一个适合单个表达式的模式，适用于一般化的期数和维度。事实证明，许多其他人也在沿着这些思路思考。这种方法称为“算法微分”。

上述方程可以简化为仅关于其中的 2 个 N 个变量，以计算海森矩阵中的 1 个坐标：

![](https://tr8dr.wordpress.com/wp-content/uploads/2010/01/reexpression.png)

我们知道如何通过链式法则来区分上述内容，链式法则指出复合函数，比如 f(g(x))，可以被区分为 f'(g(x)) g'(x)。这意味着一系列基本规则：

![](https://tr8dr.wordpress.com/wp-content/uploads/2010/01/rules.png)

我们可以将表达式分解成一个（隐式或显式）表达式树，并使用导数规则重新组合成最终结果。例如，这是一个 f(x,y) = x y sin(x²) 的树形图。（我的函数图太大了，这里无法显示）：

![](https://tr8dr.wordpress.com/wp-content/uploads/2010/01/tree.png)

有一些库（用于 C ++和 Java），可以用正常的代码表达一个函数，但同时隐式地计算第一或第二阶导数。在表达式的评估过程中，会跟踪代表 f(x) 和 f'(x) 的“双重”。

不幸的是，我的实用函数的表达式（树）的大小巨大，特别是对于二阶导数。我将避免计算海森矩阵，并在优化的部分中使用 BFGS 最小化器，因为这比计算海森矩阵更便宜。
