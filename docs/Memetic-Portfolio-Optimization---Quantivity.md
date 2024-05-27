<!--yml

分类：未分类

日期：2024-05-18 13:53:26

-->

# 遗传投资组合优化 | Quantivity

> 来源：[`quantivity.wordpress.com/2010/02/18/memetic-portfolio-optimization/#0001-01-01`](https://quantivity.wordpress.com/2010/02/18/memetic-portfolio-optimization/#0001-01-01)

在研究大型搜索空间的多目标优化和聚类时，Quantivity 偶然发现 Aranha 和 Iba 应用了遗传和生物算法的一些有趣的新工作。后者的研究沿着 Brabazon 和 O’Neill [生物启发算法在金融建模中的应用](http://www.springerlink.com/content/q763h7lxj7701v76/)的方向进行（回应此前的[评论](https://quantivity.wordpress.com/2010/02/15/trading-the-unobservable/#comments)，这可能对那些寻找将遗传算法应用于交易的已发表示例的人有用，因为它在第 III 部分包括了众多简单的案例研究）。

首先，将遗传算法应用于投资组合优化和交易规则演化。遗传算法似乎很有趣，因为它将局部搜索与遗传进化相结合，因此可能在经典遗传算法已证明不成功的地方有一些有趣的使用：

> 遗传算法在大范围内改进解决方案，而局部优化则细化遗传算法生成的解决方案。

来自[GECCO 09](http://www.sigevo.org/gecco-2009/workshops.html)和[ACSE 09](http://www.iasted.org/conferences/pastinfo-646.html)的有趣论文：

+   Aranha 和 Iba，使用遗传算法提高静态和动态交易场景下的投资组合性能

+   Aranha 和 Iba，基于遗传树的遗传算法及其在投资组合优化中的应用

+   Aranha 和 Iba，使用遗传算法优化外汇交易规则

第二，将生物（蚁）算法应用于复杂形状的聚类：

> 已经证明，从这个低层次规则中会发生某种形式的聚类。与传统的 k-means 等方法相比，蚁群聚类有其优点和缺点，但它对于形状复杂的数据聚类非常有用。

由于从未在实践中使用过蚁群聚类，保持一定程度的怀疑似乎是合理的（如果只是因为它的名字）。

完整的[Aranha 出版物](http://www.iba.t.u-tokyo.ac.jp/~caranha/published/index.html)列表包括更经典的遗传算法的一些早期工作。
