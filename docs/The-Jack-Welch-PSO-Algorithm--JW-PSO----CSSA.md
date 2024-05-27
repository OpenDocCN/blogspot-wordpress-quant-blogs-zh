<!--yml

分类：未分类

日期：2024-05-12 17:58:23

-->

# [杰克·韦尔奇粒子群优化算法（JW-PSO）](https://cssanalytics.wordpress.com/2013/09/12/the-jack-welch-pso-algorithm-jw-pso/) | CSSA

> 来源：[`cssanalytics.wordpress.com/2013/09/12/the-jack-welch-pso-algorithm-jw-pso/#0001-01-01`](https://cssanalytics.wordpress.com/2013/09/12/the-jack-welch-pso-algorithm-jw-pso/#0001-01-01)

![杰克·韦尔奇](https://cssanalytics.files.wordpress.com/2013/09/jack-welch.png)

杰克·韦尔奇是企业界的标志人物，可以说是历史上最伟大的首席执行官之一。他采用的一种独特方法（20-70-10 系统）就是基于此来优化他的员工队伍，该方法识别出三个不同的层次——20%的高价值员工，70%的中等水平但对运营至关重要的人员，以及 10%的生产力较低的员工。在之前的一篇文章中，我详细介绍了[杰克·韦尔奇投资组合算法](https://cssanalytics.wordpress.com/2011/10/13/the-jack-welch-portfolio-algorithm/)的概念，为了更好地理解这个主题，阅读这篇文章是值得的。20-70-10 系统有一些有趣的组成部分，这激发了我创建一个新的混合启发式优化算法。

最近，我向读者介绍了[粒子群优化](https://cssanalytics.wordpress.com/2013/09/06/social-learning-algorithms-particle-swarm-optimization-pso/ "Social Learning Algorithms: Particle Swarm Optimization (PSO)")（PSO）和[微遗传算法](https://cssanalytics.wordpress.com/2013/08/30/the-mighty-but-humble-micro-genetic-algorithm-mga/ "The Mighty (but humble) Micro-Genetic Algorithm (mGA)")（mGA）。对于这些方法非常有意思且详细的分析，我建议读者看看博客 roll 中的新来者——[巴特勒的数学](http://butlersmath.wordpress.com/2013/09/07/a-quick-analysis-of-heuristic-optimization-by-stochastic-genetic-algorithms-and-particle-swarm/)。安德鲁·巴特勒是一位有着优化背景的数学家，他对这些算法在不同数学函数求解中的表现进行了有趣的比较。PSO 恰好是一个非常实用且直观的算法，用于解决投资组合问题和金融建模中的不同方程。使用 PSO 的主要缺点是，它可能收敛较慢（相对于确定性或梯度优化器），而且它比遗传算法（GA）更容易陷入局部最优。在传统说法中，GA 更擅长探索，但 PSO 在利用方面更胜一筹，这两种方法都进行了大量的迭代——因此，相对于梯度求解器，在计算机上运行较慢。PSO 从一定数量的粒子开始，这些粒子是随机生成的。这个初始的群体用来将粒子聚集在一起以找到最优解。不幸的是，与混沌理论类似，PSO 对初始条件很敏感——初始粒子的位置会影响找到最优解的概率以及达到解决方案的速度。我建议考虑混合算法，特别是为了解决不同算法的弱点。在这种情况下，杰克提出的 20-70-10 系统为改进原始 PSO 概念提供了一些很好的思路。

在**JW-PSO**中，对原始算法的第一项关键性改变是“解雇”表现最差的 10%的粒子或者说是“C 级玩家”。这些粒子被全新的粒子所替代。这一改变有两个好处：1) 它通过允许新粒子搜索空间来启用潜在更优的探索；2) 它通过将资源从搜索空间的潜在无用区域重新分配，来启用潜在更优的开发和更快地收敛。第二项关键性改变是让粒子向“A 级玩家”移动，即按照目标函数排名前 20%的粒子。这也通过将粒子向搜索空间可能更富饶的区域移动，有助于开发和潜在更快地收敛。最后的改变是将全局最优解变为一个“精英”全局最优解，这一点从 mGA 中的精英主义概念借鉴而来。精英全局最优解是在目标函数方面自诞生以来找到的最好的位置，而不仅仅是当前时刻粒子群中的最佳位置。这有助于确保通过连续迭代不会丢失最优位置——防止粒子浪费计算资源。**JW-PSO**的新方程如下所示：

![jw pso](https://cssanalytics.files.wordpress.com/2013/09/jw-pso.png)

我鼓励读者尝试这个概念，并思考如何将混合 PSO 算法扩展到新的和独特的方法，以使它们更加实用和高效。
