<!--yml

分类：未分类

日期：2024-05-12 17:58:40

-->

# 社会学习算法：粒子群优化（PSO）| CSSA

> 来源：[`cssanalytics.wordpress.com/2013/09/06/social-learning-algorithms-particle-swarm-optimization-pso/#0001-01-01`](https://cssanalytics.wordpress.com/2013/09/06/social-learning-algorithms-particle-swarm-optimization-pso/#0001-01-01)

![swarm1](https://cssanalytics.files.wordpress.com/2013/09/swarm1.png)

上面的图片不是[鲨卷风](http://www.imdb.com/title/tt2724064/)。这是一群一起游动的鱼，展示了智能社会行为的性质。这一观察与其他自然界的例子一起，帮助启发了粒子群优化（PSO）的创造。

粒子群优化是一种基于自然界中观察到的群体行为的[随机优化方法](https://cssanalytics.wordpress.com/2013/08/30/the-mighty-but-humble-micro-genetic-algorithm-mga/ "The Mighty (but humble) Micro-Genetic Algorithm (mGA)")。该方法捕捉了社会智能和合作的概念。PSO 是由社会心理学家詹姆斯·肯尼迪和工程师罗素·埃伯哈特于 1995 年开发的。PSO 方法使用在搜索空间内寻找解决方案时展示个体和群体行为的粒子。这些粒子还具有它们去过的地方的记忆。PSO 适用于具有连续变量的复杂优化问题——比如寻找投资组合或方程权重。我已经创建了一个简化版的 PSO 方法的分解，这实际上比它看起来要简单得多且不那么深奥。本质上，PSO 使用熟悉的动量概念来推动粒子向解决方案移动。

![pso equations](https://cssanalytics.files.wordpress.com/2013/09/pso-equations.png)

下面展示了全局最优和粒子最优在确定新粒子位置之间的紧张关系：

![pso graphic](https://cssanalytics.files.wordpress.com/2013/09/pso-graphic.png)

粒子群优化（PSO）是一种非常简单且实用的方法，其优势在于比[遗传算法](https://cssanalytics.wordpress.com/2013/08/30/the-mighty-but-humble-micro-genetic-algorithm-mga/ "The Mighty (but humble) Micro-Genetic Algorithm (mGA)")更快。然而，其相对优越性高度依赖于问题的类型。通常变量越连续，搜索空间越无噪声且连续，其性能相较于遗传算法就会更好——这是一个宽泛的说法。但像其他在现实世界中实用的东西一样，最好考虑使用混合方法论，利用每种方法的优点来创建更加灵活和高效的方法。

![](https://cssanalytics.files.wordpress.com/2013/09/pso-equations.png)
