<!--yml

category: 未分类

date: 2024-05-18 05:06:17

-->

# Magmasystems Blog: Coral8 Update

> 来源：[`magmasystems.blogspot.com/2007/11/coral8-update.html#0001-01-01`](http://magmasystems.blogspot.com/2007/11/coral8-update.html#0001-01-01)

我们正在完成 Coral8 评估的第一阶段。这周，我和 Terry Cunningham（他驾驶他的 Falcon 10 飞过来与我们见面）见面了，我和他们的高级工程师 Henry 进行了一次很好的会话。

pre

-销售工程师。Terry 是 Crystal Reports 的创建者，后来成为

Seagate

软件编写的。我心中总有一个对飞行员情有独钟的位置……即使他的飞机比我快，飞得比我高！

我们验证了 Coral8 输出的结果与我们的自定义应用程序相同，并且我对 Coral8 的一些功能有了更深入的了解，这些功能在他们的文档中并不容易找到。虽然 Coral8 有很多优点，但也有一些需要注意的地方。

- 文档需要稍微整合一下。有很多单独的手册和技术文章。需要有一个关于他们的

CCL

language.

- 没有编写中间流，你无法测试一个简单的用户定义函数。没有简单的方法将变量输出到控制台。换句话说，我想做这样一件简单的事情：

CREATE VARIABLE commission; SET commission = CalculateCommission(); -- 这是我的用户定义函数 CONSOLE.WRITE(commission);

- 我们设法让 Coral8 工作室稳定下来。幸运的是，没有丢失任何工作。Coral8 工作室是用

wxWidgets

，所以我很好奇他们如何在工作室中进行单元测试。

我的看法是，虽然拥有高级功能很好，但仍然需要注意开发人员需要做的日常小事。Henry 告诉我，将来 Coral8 将转向更类似于 Visual Studio 的基于文件的开发方式。我当然欢迎这种方式。Henry 花了 8 个小时观察我驾驶。当我遇到问题时，我会口头描述问题，这样 Henry 就能看到我所经历的情况，并将问题反馈给他的管理层。

优点：

- 我一直在阅读有关 Coral8 的模式匹配能力的资料。我们肯定会探索这个。

- Coral8 的入门门槛相对较低。如果我们有生产、开发和 COB 服务器（都是双核或四核机器），那么它不会超出我们的预算。

- 他们的软件在评估版本上没有任何时间限制。我不喜欢的是一个只能使用 30 天的许可证密钥。考虑到金融公司的性质，我们经常被拉入很多边缘项目。我不想我的时间花在“ thick of things”中，结果发现许可证密钥已经过期。Coral8 对评估者非常友好。

现在，让我们转向

Aleri

. 我将使用他们的新 2.4 版本。

©2007 Marc Adler - 版权所有
