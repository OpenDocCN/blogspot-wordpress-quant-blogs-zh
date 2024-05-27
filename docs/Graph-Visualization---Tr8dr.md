<!--yml

类别：未分类

日期：2024 年 5 月 18 日 15:31:25

-->

# 图表可视化 | Tr8dr

> 来源：[`tr8dr.wordpress.com/2010/09/12/graph-visualization/#0001-01-01`](https://tr8dr.wordpress.com/2010/09/12/graph-visualization/#0001-01-01)

2010 年 9 月 12 日 9:19 am

我正在寻找一个用于网络可视化的优秀应用程序或库，需要能够可视化非常大的图表，所以静态图表渲染方法行不通。希望有一个动态的东西，可以在浏览图表时专注于局部环境。比如，一些比[这个](http://www.neuroproductions.be/twitter_friends_network_browser/)更复杂的东西。我想要图表上的权重和方向的概念。理想情况下，应该能够以 graphml 格式输入。

碰到一些可视化库：

1.  [Protoviz](http://vis.stanford.edu/protovis/ex/)（漂亮的渲染和图形构思）

    看起来需要花费一些时间，但通过一些代码，可能可以使用这个库作为交互式探索的基础。对我来说可能是太忙了的工作。有一些例子给我了其他可视化的想法。

1.  [JUNG](http://jung.sourceforge.net/)（我已经在使用这个进行图表分析，但没有进行可视化）

    可视化效果不是非常漂亮，但是功能齐全。不是动态定位的。

1.  [ThinkMap](http://www.thinkmap.com/)

    这些家伙是我在网上看到的最早的之一（大概 10 年前），使用了动态图形技术。那时是基于 Flash 的。现在看起来他们正在使用 Java。奇怪的是，他们的 Java 界面远远不如他们以前的 Flash API。

1.  [Flare](http://flare.prefuse.org/) (基于 Flex / Flash 的 API)

    图表布局似乎是动态的，但需要相当多的代码。代码是基于 ActionScript 的。嗯，不想去那里。

我确信还有其他的。只是偶然碰见的一些...

**附录

Shane Conway 指引我去看他的[Rwebvis](http://code.google.com/p/rwebvis/)包，提供了一个与 Protoviz（以及其他基于 Web 的渲染器）渲染有关的 R 接口。看起来正是我需要的（谢谢）！但是 Protoviz 需要一些编程，但是这种抽象程度似乎是适合这种灵活性的。
