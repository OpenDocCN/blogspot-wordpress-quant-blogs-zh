<!--yml

category: 未分类

date: 2024-05-12 17:54:46

-->

# 自适应投资组合分配 | CSSA

> 来源：[`cssanalytics.wordpress.com/2014/05/06/adaptive-portfolio-allocations/#0001-01-01`](https://cssanalytics.wordpress.com/2014/05/06/adaptive-portfolio-allocations/#0001-01-01)

![适应](https://cssanalytics.files.wordpress.com/2014/05/adapt.jpg)我和一位同事 Jason Teed 为 [NAAIM](http://www.naaim.org/) 比赛撰写了一篇论文。概念是应用基本的机器学习算法，利用传统的输入（如收益、波动率和相关性）生成自适应投资组合配置。与 [自适应资产配置](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=2328254)（Butler,Philbrick, Gordillo）等具有开创性的作品不同，后者侧重于创建随着时间变化而适应的历史输入的配置，我们关于自适应投资组合配置（APA）的论文侧重于如何适应性地整合这些变化的输入，而不是使用已建立的理论框架。论文可以在这里找到：[自适应投资组合配置论文](https://cssanalytics.files.wordpress.com/2014/05/adaptive-portfolio-allocations-paper.pdf)。许多其他有趣的论文也提交给了 NAAIM 比赛，其余的可以在[这里](http://www.naaim.org/wagner-award-whitepapers/whitepapers/)找到。APA 对这些投资组合输入的整合方法不像 MPT 那样由理论或模型驱动，而是基于了解它们如何相互作用以从夏普比率的角度产生最佳投资组合。结果显示，传统的均值-方差/马科维茨/MPT 框架在最大化夏普比率方面表现不佳。数据进一步暗示，传统的 MPT 进行了过多的交易并采取了过多的极端立场，这是由于它应该生成投资组合权重的输入-尤其是收益-非常嘈杂，也可能展示出非线性或违反直觉的关系。相反，通过学习输入如何在历史上映射到资产级别的最佳投资组合，所产生的配置随时间演变得更加稳定。这个简单的学习框架可以通过更加优雅的框架大幅扩展，以产生比论文中更优越的结果。用于多资产投资组合的方法被限制为对读者而言简单的成对投资组合配置的聚合。论文没有赢得（甚至没有获奖），但与此博客上做出的许多贡献一样，它旨在激发新思路，而不是销售模板化解决方案或听起来过于正式或学术性。在一天结束时，在市场不断变化的环境中，没有简单的 ABC 配方或交易系统能够无限期生存下去。没有任何程度的严谨性、模拟或复杂性能够改变这一点。因此，希望能够提供洞察力，了解如何利用真正的自适应方法来应对制定投资组合配置的挑战。
