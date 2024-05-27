<!--yml

分类：未分类

日期：2024-05-18 14:54:54

-->

# 及时投资组合：研究附属机构的交互式发现 JoPM 论文

> 来源：[`timelyportfolio.blogspot.com/2014/03/interactive-discovery-of-research.html#0001-01-01`](http://timelyportfolio.blogspot.com/2014/03/interactive-discovery-of-research.html#0001-01-01)

##### 在我的上一篇文章[More on Rebalancing | With Data from Research Affiliates](http://timelyportfolio.blogspot.com/2014/02/more-on-rebalancing-with-data-from.html)中，我做了些非常基础的视觉化工作，但我认为这些数据非常适合使用一种有趣的 javascript SQL-like 查询语言[objeq](https://github.com/agilosoftware/objeq)以及[d3.js](http://d3js.org)图表库[dimple.js](http://dimplejs.org)进行更强大的交互式发现。接下来，我希望能扩展使用 lodash 或 lazy.js。

这个练习帮助我思考了一些悬而未决的问题：

1.  在创建图表之后，我们是否需要使用类似于 shiny 的东西来维护与 R 的连接 overhead，还是可以将一些聚合、过滤和计算工作像这个例子中一样转移到 javascript 上？

1.  我们如何使用 rCharts 模板与其他语言如 Python、Ruby 和 Javascript 结合使用？

1.  我们可以为 rCharts 做一些更具体和定制的页面模板吗？

1.  一个[Lyra](http://idl.cs.washington.edu/projects/lyra/)-like 界面更好，还是这种类型的界面更适合更高级的用户？

在尝试了[下面的示例](http://timelyportfolio.github.io/rCharts_objeq/examples/rCharts_objeq_researchaffiliates.html)之后，请用你的想法帮助我。以下是下面的截图。![image](http://timelyportfolio.github.io/rCharts_objeq/examples/rCharts_objeq_researchaffiliates.html)
