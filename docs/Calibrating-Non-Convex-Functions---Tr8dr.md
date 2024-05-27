<!--yml

类别：未分类

日期：2024-05-18 15:37:19

-->

# 对非凸函数进行校准 | Tr8dr

> 来源：[`tr8dr.wordpress.com/2009/11/19/calibrating-functions-with-multiple-local-optima/#0001-01-01`](https://tr8dr.wordpress.com/2009/11/19/calibrating-functions-with-multiple-local-optima/#0001-01-01)

我进行的许多校准都是针对非凸函数的，即具有多个局部最小值/最大值的函数。对这类函数的极小(大)化求解排除了基于梯度下降的广泛算法的使用（如 BFGS）。有许多解决非凸问题的“元启发式”方法，如：*模拟退火*、*遗传算法*、*微分进化*、*粒子群*和蛮力*网格搜索*，等等。

在过去几年里，我一直在使用[JGAP](http://jgap.sourceforge.net/)，这是一个通过遗传算法进行优化的库。有段时间我以为大多数遗传算法库在核心算法上都很相似，只是在 API 级别上有所不同。我在新的方差模型上遇到了一些问题，JGAP 并没有按照预期的方式收敛。

我最近开始在 R 中使用一个用于特定校准的软件包（[genoud](http://sekhon.berkeley.edu/rgenoud/)），发现它收敛得很快，而 JGAP 则与之相比表现很差。[DEoptim](http://cran.r-project.org/web/packages/DEoptim/DEoptim.pdf)是一个非常类似的软件包（对*differential evolution*进行了直接实现）。微分进化是遗传算法的表亲，但在群体演化方法上有所不同。

**微分进化**

微分进化与标准遗传算法方法非常相似，因为两者都通过随机生成的“试验向量”（θ）的群体和这些向量向最优解的定向演化来努力寻找最优解。微分进化的实现如下：

```
generate Population = { θ1, θ2, θ3, ... } where θ in domain of function
determine θbest ← maxarg [θ : fitness(θ)] forall θ
repeat
   foreach θi in Population
      draw { θa, θb, θc } randomly from P (without duplication)
      θd ← θa + F(θb - θc)
      θnew ← crossover (θd, θi) 

      # adjust ith vector if fitness of generated superior
      if fitness(θnew) > fitness(θi) then
         θi ← θnew

      # adjust best vector if new optimum seen
      if fitness(θnew) > fitness(θbest) then
         θbest ← θnew
   end
until fitness(θbest) approaches target
```

其中一个关键创新是创新（突变）的方差取决于向量的离散度。一开始，离散度会很大，随着优化的进行，离散度会减小，因此突变会更加集中。函数 F()对向量之间的差异进行操作，对收敛速度和对领域的探索有各种影响。我在这里不会详细介绍它。

**混合方法的改进**

假设在试验向量的邻域内具有连续的带有导数的函数，算法可以通过使用梯度下降（如 BFGS 算法）来提高，以在邻域内找到真正的最优解。必须注意不要过早优化，以免丧失试验的多样性。

**一些测试**

这里是关于上述两个 R 包的一些结果。最终我需要将其实现为 Java，但是我想先与现有的实现进行比较。我在一个特别病态的高斯混合模型上进行了优化（取自 genoud 包中的示例）：

![](https://tr8dr.wordpress.com/wp-content/uploads/2009/11/picture-102.png)

看起来像：

![](https://tr8dr.wordpress.com/wp-content/uploads/2009/11/picture-112.png)

很明显，使用梯度下降（上升）求解器会使得函数收敛到上述函数的其中一个局部最大值。测试 DEoptim，使用一个包含 100 个个体和类似的参数，两者都在 10 代内（没有任何 BFGS 优化）以 1e-4 的精度到达答案，并在 60 代内以 5e-6 的精度到达答案。

使用 BFGS 优化时，genoud 在 2 代内达到了 1e-10 的精度！不幸的是，对于一些其他（更复杂）的混合函数，genoud 达到了错误的最大值，而纯 DE 方法达到了正确的最大值。然而，通过适当的参数化可以避免这种情况。
