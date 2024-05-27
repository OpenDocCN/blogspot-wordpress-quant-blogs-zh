<!--yml

类别：未分类

日期：2024-05-18 14:59:09

-->

# 及时投资组合：使用 Sankey 探索网络

> 来源：[`timelyportfolio.blogspot.com/2013/07/exploring-networks-with-sankey.html#0001-01-01`](http://timelyportfolio.blogspot.com/2013/07/exploring-networks-with-sankey.html#0001-01-01)

受到 Tony Hirst 的一条推文的启发([`blog.ouseful.info/`](http://blog.ouseful.info/)），我开始尝试使用[rCharts](http://rcharts.io/site)实现[d3 sankey 插件](https://github.com/d3/d3-plugins/blob/master/sankey/sankey.js)。在准备示例的过程中，我发现自己在 sankeys 和网络分析方面的知识有很多空白。我不想让良好的学习机会浪费掉，所以我整理了这份快速教程，记录了我所学到的内容。点击[这里](http://timelyportfolio.github.io/rCharts_d3_sankey/example_build_network_sankey.html)或下面的屏幕截图查看。

对于那些想知道这如何在金融领域发挥作用的人，Sankey 图在投资组合评估/持有类型报告中可能会有很好的应用，其中节点代表家庭、客户账户、资产类别和证券类型。每条边的权重将是$或%的形式。

![image](http://timelyportfolio.github.io/rCharts_d3_sankey/example_build_network_sankey.html)
