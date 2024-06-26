<!--yml

分类：未分类

日期：2024-05-12 19:18:05

-->

# 量化交易：Fios 和 EC2

> 来源：[`epchan.blogspot.com/2009/04/fios-and-ec2.html#0001-01-01`](http://epchan.blogspot.com/2009/04/fios-and-ec2.html#0001-01-01)

作为一个算法交易员，我一直在寻找更好的物理基础设施，这样我可以通过互联网以最高速度连接到我的执行经纪人，并且停电的可能性最小，成本合理。

为此，我想提一下

[Fios](http://www22.verizon.com/Residential/FiOSInternet/FiOSvsCable/FiOSvsCable.htm)

，来自 Verizon 的光纤服务，下载速度为 50 Mbps，上传速度为 20 Mbps，都比典型的 T-1 线路（1.5 Mbps）快。此外，它每月只需 45 美元。嘿，甚至

保罗·克鲁格曼[Paul Krugman](http://krugman.blogs.nytimes.com/2009/03/23/incommunicado-probably/)

在他的家里安装了！

（我自己还没有尝试过，很想听听你们那些尝试过的人的看法，看看是否该和 T-1 说再见了。）

而且，正如我之前

报道过[reported](http://epchan.blogspot.com/2009/01/algorithmic-trading-technology-update.html)

所提到的，我也在不断寻找一个好的云计算平台，这样我就可以运行更多的策略，而不会让我的办公室里堆满电脑。找到一个将消除在办公室进行任何大型互联网连接投资的必要性。

为此，我尝试了亚马逊的 EC2 几个月。我用它来运行我们的一种策略，我必须报告我的体验是喜忧参半的。

首先，如果你不是 IT 人士，那么花时间（8 个人小时？）来设置和启动是非常多的，特别是考虑到他们的安全预防措施。学习曲线是陡峭的。

第二点，更让人烦恼的是，实例有时无法正确启动，或者无法正确捆绑。（捆绑意味着保存软件配置以供将来使用。）我正在使用 Windows 实例。那些使用 Linux 实例的人有更好的体验吗？

第三点，也是最让人烦恼的，当一个新的实例被启动时，Windows 通常无法自动将其时钟与 time.windows.com 或其他任何互联网时钟同步。结果，时间经常是错误的。现在，这对一般的办公室工作可能不是什么大问题。但是，如果你的自动化交易策略严重依赖一天中的时间，它可能会对你的利润造成致命的影响。如果有人经历过 Windows 时钟的类似问题，并知道一个解决办法，请让我知道！

尽管所有这些烦恼，我仍然在 EC2 上运行策略，希望一旦 EC2 度过测试版发布，情况会变得更好。
