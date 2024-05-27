<!--yml

分类：未分类

日期：2024-05-18 15:03:42

-->

# 及时组合：另一个伟大的 Google 夏季代码 2012 R 项目

> 来源：[`timelyportfolio.blogspot.com/2012/08/another-great-google-summer-of-code.html#0001-01-01`](http://timelyportfolio.blogspot.com/2012/08/another-great-google-summer-of-code.html#0001-01-01)

[Tradeblotter 宣布](http://tradeblotter.wordpress.com/2012/08/29/now-with-more-bacon-2008/)了由于 Google 夏季代码（GSOC）2012 项目将添加到 PerformanceAnalytics 包中的非常不错的功能：

> “...Mathieu 开始制作数十个新函数，扩展了几个现有的函数，并为 PerformanceAnalytics 增加了 40 多页的附加文档（包括公式和示例）。他包括了 Bacon 的小型数据集和几个新的`table.*`函数，用于测试和演示函数与已发表结果一致。一切都在计划之中，我想补充一下。
> 
> 他还撰写了一篇[非常不错的概述](http://tradeblotter.files.wordpress.com/2012/08/pa-bacon.pdf) ，介绍了从 Bacon（2008）开发的函数，这些函数包括在 PerformanceAnalytics 中，这对理解 Bacon 作品的读者或教师应该很有帮助。Mathieu 的总结文件也将作为包中的一个示例文档分发，使用`vignette('PA-Bacon')`可以访问。每个函数的文档中还包括更多详细信息。我将在稍后的帖子中突出介绍一些这些函数..."

尽管 Bacon vignette 非常有帮助，但我强烈建议 also reading the book. 对于那些在 O'Reilly 的 Safari 上的读者，你可以把这本书添加到你的书架上。

预览

![](http://my.safaribooksonline.com/9781119995470/firstsection?portal=oreilly&uicode=&__hideTop=true&__readerfullscreen=1&__readerleftmenu=1&flashzoom=0&cid=shareWidgetUse "Practical Portfolio Performance Measurement and Attribution, Second Edition")

或者从亚马逊购买。

当我看到这个公告时（一直耐心等待），我还在阅读这篇非常好的文章[《番茄和低波动效应》](http://advisorperspectives.com/commentaries/research_82812.php)（由 Research Affiliates 撰写），我已经开始用 R 做一些探索，研究 S&P 500 的买入/持有和 10 个月移动平均策略之间的 Sharpe 和信息比率。当你看代码时，你可能会喜欢一些其他图表和方法，但我决定改变研究方向，并整合一个新的 PerformanceAnalytics 函数，并继续推动另一个优秀的 Google 夏季代码 2012 添加[xtsExtra plot.xts](http://timelyportfolio.blogspot.com/search/label/plot.xts)的极限。我没有太挑剔，选择了 ProspectRatio，因为它是一个我不常听到的公式。在第 20 页，Bacon vignette 将 ProspectRatio 描述为

以下是![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgZWbKTTf7KmpkkDxnB9A-5McLd3oEhCK9SRp7uI6CiJr3ChiAgzzCIIEt1kQUcRPpxClpb0KQ3FozwRWSci0wFsOUV8D9meukXq3y5mI9e52EBsAd3ZSAWqpRbzE3wUtGMazQXKM-JZA/s1600-h/image%25255B3%25255D.png)的图片。

我基本上试图在这张图表中包含尽可能多的内容（散乱、覆盖、涂抹、块状和切碎）来自[xtsExtra plot.xts](http://timelyportfolio.blogspot.com/search/label/plot.xts)。这张图表包括标普 500 的累积增长买入/持有和 10 个月移动平均线在上部面板，展示了回调情况在中部，然后增加了针对 ma 策略的展望比率水平图——买入/持有的展望比率。由于 plot.xts 也允许块状结构，我认为当 ma 策略的 36 个月滚动夏普比率表现优于买入/持有时，涂暗这些时期也会有所帮助。虽然这可能在单一图表中显得有些过多，但我认为它清楚地展示了这些工具的力量。

以下是[R 代码来自 GIST (用于复制/粘贴请选择原始格式)](https://gist.github.com/3529477)。
