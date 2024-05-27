<!--yml

分类：未分类

日期：2024 年 5 月 18 日 15:40:38

-->

# 期权定价的 GP | Tr8dr

> 来源：[`tr8dr.wordpress.com/2008/01/20/gp-for-option-pricing/#0001-01-01`](https://tr8dr.wordpress.com/2008/01/20/gp-for-option-pricing/#0001-01-01)

2008 年 1 月 20 日 · 上午 8:19

正如您可能知道的，GP（遗传编程）是 GA 的延伸，它重新排列代数或功能指令树以适应一个解决方案。

![](http://upload.wikimedia.org/wikipedia/en/7/77/Genetic_Program_Tree.png)

之前我从未想过，但在使用一组正确的构造函数时，可以采用这种方法来收敛到期权定价 GP 模型。现在，如果我们要做的只是复制 Black/Scholes、CEV 或其他基于高斯分布的模型，那就没什么意思了。

我们知道实际分布往往是非高斯的。我们能否用 GP 更准确地近似对非高斯分布的对冲成本（意味着期权的真实无风险价格）？

有趣的是，神经网络只是 GP 树的特殊情况，因此从根本上说，GP 是非线性回归的最一般方法。
