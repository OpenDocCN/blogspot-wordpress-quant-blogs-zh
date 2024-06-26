<!--yml

类别：未分类

日期：2024 年 5 月 18 日 15:31:33

-->

# 因果关系与传递性 | Tr8dr

> 来源：[`tr8dr.wordpress.com/2010/09/12/causality-transitivity/#0001-01-01`](https://tr8dr.wordpress.com/2010/09/12/causality-transitivity/#0001-01-01)

2010 年 9 月 12 日 · 下午 1:13

我有一些不同的股票之间因果关系的图表（我使用的一个度量标准是格兰杰因果关系）。我对知道 A ↔ B ↔ C 在多大程度上暗示着弱的 A ↔ C 感兴趣，这里我使用 ” ↔” 表示格兰杰因果关系是单向的还是双向的。

在大多数情况下，A ↔ B 的斯皮尔曼相关性很高，因此可以粗略地将其视为观察到的相关性随着关系路径的进展而下降的一种模拟。因此，如果一个图表从 A 到 A 有关联的“直接”关系，那么“直接”关系返回到 A 的相关性是多少，依此类推：

+   **A**

    ρ(A,A) = 1

+   **A ↔ {B,C,D}**

    ρ(A, {B,C,D}) =  0.84, 0.76, 0.90

+   **B ↔{E,F}, C↔G, D↔{H,I,J}**

    ρ(A, {E,F,G,H,I,J})  = 0.62, 0.54, 0.59, …

结果显示相关性急剧下降。这并不能直接证明任何关于因果关系的事情，但似乎暗示传递性受到限制或几乎不存在，或者至少下降得非常快。

这是对两种不同股票进行的分析：

![](https://tr8dr.wordpress.com/wp-content/uploads/2010/09/screen-shot-2010-09-12-at-2-11-55-pm.png)

![](https://tr8dr.wordpress.com/wp-content/uploads/2010/09/screen-shot-2010-09-12-at-2-12-12-pm.png)
