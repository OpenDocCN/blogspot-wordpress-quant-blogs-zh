<!--yml

分类：未分类

日期：2024 年 05 月 18 日 15:04:57

-->

# 及时投资组合：关于地平线图的更多信息

> 来源：[`timelyportfolio.blogspot.com/2012/08/more-on-horizon-charts.html#0001-01-01`](http://timelyportfolio.blogspot.com/2012/08/more-on-horizon-charts.html#0001-01-01)

*背景请参阅以前的帖子[地平线图的应用](http://timelyportfolio.blogspot.com/2012/07/application-of-horizon-plots.html)，* [*已有的地平线图*](http://timelyportfolio.blogspot.com/2012/06/horizon-plot-already-available.html)，*以及* [*R 中的立体地平线图*](http://timelyportfolio.blogspot.com/2012/06/cubism-horizon-charts-in-r.html)

一些反馈让我觉得在[我上一篇关于地平线图的文章](http://timelyportfolio.blogspot.com/2012/07/application-of-horizon-plots.html)中可能有点雄心勃勃。我认为快速提供地平线图概述可能会有所帮助。由于我不是可视化专家，我会尽量整理我找到的最好的例子和教程。最后，我将逐步介绍如何在 R 中构建地平线图。

下面是迈克·博斯托克的一个完整的精彩演讲。有关地平线图的讨论，请跳到 11:20 处。

[Mike Bostock @ Square 谈论时间序列可视化](http://vimeo.com/42176902) 来自 [Librato](http://vimeo.com/librato) 在 [Vimeo](http://vimeo.com).

幸运的是，迈克还提供了一个交互式示例视频，演示了如何从面积图构建地平线图。我在下面嵌入了它（请参阅[`bl.ocks.org/1483226`](https://gist.github.com/1483226 "https://gist.github.com/1483226")获取来自原始来源的完整示例）。

这个来自 2009 年 Panopticon 的快速 YouTube 剪辑也很好地解释了构建过程。如果你更喜欢阅读，Panopticon Software 的汉斯·雷纳（Hannes Reijner）撰写的一篇[简短论文](http://www.stonesc.com/Vis08_Workshop/DVD/Reijner_submission.pdf)涵盖了相同的内容。

[`www.youtube.com/embed/M53dYUcQbCs`](http://www.youtube.com/embed/M53dYUcQbCs)

视频

斯坦福大学的杰弗里·希尔（Jeffrey Heer）与加州大学伯克利分校的尼古拉斯·孔（Nicholas Kong）和曼尼什·阿格拉沃拉（Maneesh Agrawala）[调查了地平线图的有效性并提出了一些使用建议。](http://vis.stanford.edu/files/2009-TimeSeries-CHI.pdf) 下面的图表也提供了地平线图建立步骤的另一种解释。

![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjL1PlbyUmNnphrAe_wugnYZxdfcG5OuW5tXFU-kTD7Np_6MYELaQdu8YzWNFOdDJzpdUFORPORHWw3PTFe7ZMLai6DMOjGiYw44gY6u235aUDML30i86PUn-khofueg2IflMf4tKlQUw/s1600-h/image%25255B3%25255D.png)

他们建议并得出结论

> **分层条带随着图表尺寸的减小而受益**
> 
> 我们发现，将图表分成分层频段可以可靠地增加估计时间和增加估计误差，在保持图表高度不变的情况下。然而，我们还发现，对于小于 24 像素（在我们显示器上 6.8 毫米）的图表高度，双频段镜像图表可以提高估计精度。对于更大的图表尺寸，我们建议缩放单频段镜像图表。对于更小的尺寸，我们建议添加分层频段。

将视野扩展到医疗领域，这里有一个有趣的[项目，使用地平线图来可视化糖尿病护理](http://ieg.ifs.tuwien.ac.at/projects/HorizonVis/)。

> ### 地平线图
> ### 
> #### 糖尿病护理中多变量医疗测量的交互式视觉探索
> #### 
> ![HorizonVis](img/21f21cf09795ff4b3ff64ab1886e2f20.png)
> 
> 负责人/联系人
> 
> **沃尔夫冈·艾 IGNER**（http://ieg.ifs.tuwien.ac.at/%7Eaigner/）
> 
> 团队
> 
> **沃尔夫冈·艾 IGNER**（http://ieg.ifs.tuwien.ac.at/%7Eaigner/），维也纳技术大学
> 
> 迈克尔·阿塔纳索夫，HTBL 克雷姆斯
> 
> **亚历山大·林德**（http://www.ifs.tuwien.ac.at/%7Erind/），维也纳技术大学
> 
> 菲利普·辛德勒，HTBL 克雷姆斯
> 
> 雷纳特·温茨纳，HTBL 克雷姆斯
> 
> 合作伙伴
> 
> **维也纳技术大学，软件技术及交互式系统研究所**（http://ieg.ifs.tuwien.ac.at/）
> 
> **HTBL 克雷姆斯，信息技术系**（http://www.htlkrems.ac.at/）

**现在让我来尝试解释一下**

如果我们使用昨天的例子，一个 200 天移动平均系统，在移动平均线之上进入，在之下退出，我们可能会喜欢看到这样一个标准的时间序列图。

在一个简单的世界里，只有一个资产或股票，这可能就足够了。然而，我们可能会有多个想要监控的仪器，为每个仪器分配这么多高度将需要很多空间。理想情况下，我们可以压缩每个这些图表，这样我们就可以一次看到很多。

在缩减的第一步，我们可以提取最有意义的信息，我认为这是移动平均线之上或之下的百分比。

我们可能会尝试使用面积图来更好地描绘正或负 0。

我相信你们会想知道我们何时开始减少高度和节省空间。我们可以先将所有负值改为正值，并添加颜色来表示正或负。这意味着我们的图表高度可以减少约 1/2。

然而，我们需要更多的效率，所以让我们将这些图表分成频段。

有没有潜在的方法将这些频段分开，然后再将它们重组以节省空间呢？让我们分别看看每个频段。

频段 1（0 到 10%）

频段 2（10%到 20%）

频段 3（20%到 30%）

频段 4（30%到 40%）超过 3 个频段不推荐

注意，与热力图类似，频段的颜色随着值的增加而变得更加鲜艳和不透明。如果我们把每个频段叠加在一起，我们就能得到一个地平线图，而且在不丢失信息太多的情况下，我们可以将原始图表减少 1/6 甚至更多。

我希望这能解释为什么我们可能会使用地平线图以及如何制作它们。无论如何，也许你学会了 R 中的某些 lattice 技术。

[R 代码在 GIST 中（为了复制/粘贴，请选择原始格式）：](https://gist.github.com/3230354)
