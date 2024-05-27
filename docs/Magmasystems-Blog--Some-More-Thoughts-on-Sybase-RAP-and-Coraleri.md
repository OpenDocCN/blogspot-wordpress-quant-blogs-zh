<!--yml

类别：未分类

日期：2024 年 05 月 18 日 04:54:56

-->

# Magmasystems 博客：关于 Sybase RAP 和 Coraleri 的一些更多思考

> 来源：[`magmasystems.blogspot.com/2009/03/some-more-thoughts-on-sybase-rap-and.html#0001-01-01`](http://magmasystems.blogspot.com/2009/03/some-more-thoughts-on-sybase-rap-and.html#0001-01-01)

首先，一些简要的消息...

祝贺 Terry Cunningham，前 Coral8 CEO。看起来他现在是 Seagate 旗下 i365 公司的高级副总裁。我猜 Terry 将会兼任两个职务，因为他还是 Aleri 的董事长。人们不禁思考 Seagate 是否最终会进入 CEP（事件处理）业务 :-)

同时，祝福 Mark Tsimelzon。一些 Coral8 的人提到 Mark 已经不再与合并后的实体一起了。鉴于 Mark 的履历，我相信他肯定会参与一些新的、有趣的事情。

看起来 Coraleri 已经选择 Coral8 的 CCL 作为开发 Coraleri 应用程序的基于 SQL 的首选语言。这是第一个落实的部分，对我来说是个好消息。现在，我们必须等待 Splash 整合的发生，然后拼图的第二部分就会解决。

最新的 Coral8 5.6.1 符合其主要性能增强的宣称。我的 CEP 团队报告称，在我们最复杂的查询测试中，CPU 使用量显著减少。

随着 Coral8 在性能方面取得重大进展，保留 Aleri CEP 引擎的理由正在减弱。Don DeLoach 坚决表示，他们的任何客户都不需要重写一行代码，甚至 Aleri 已经书面承诺。我知道 Don 从内心深处相信这一点，但我还是有点怀疑。但只要这不影响我们对 Coral8 的工作，我愿意给予他们大量的支持。我们继续按照一切照旧进行，并且我相信 Don 和 Coraleri 团队能够使过渡对我们完全透明。

这就引出了我下一个主题…… Sybase RAP 和 Coral8。

对于这个主题，我戴上了另一个帽子，那就是我担任的职位之一，即 Equities 的首席架构师。架构师的一项工作是及时了解我们使用的当前技术，以查看它们是否会接近“寿命尽头”。首席架构师需要确保公司不会投资于任何可能存在风险的技术。

几乎每家大型投资银行都有每一种技术。当我说我们有许多应用程序使用 Sybase ASE 作为数据库时，我并没有透露我们的任何机密。所以，当 Sybase 来敲我的门，问我是否对他们的新 CEP 产品感兴趣时，我会怎么想呢？

首先，我觉得 Sybase 没有公开提到使用 Coral8 作为他们的 CEP 引擎有点奇怪。我现在可以理解为什么了。我猜测 Sybase 知道 Coral8 即将被 Aleri 收购，想要避免这种合并带来的混乱。如果我知道一个公司的产品是基于另一个供应商的产品，而那个供应商刚刚被另一家公司收购，我会需要绝对确定所有的部件都会有长久的生命力，我们不会面临生命周期结束的情况。当 Coral8 表示他们要卖给 Aleri 时，我敢想象 Sybase 那边一定有不少人急得头上冒汗。我敢肯定 Sybase 不希望这种担忧泄露给他们的潜在客户。所以，最好不要提及 Coral8 和 Sybase RAP 之间的联系。如果这是沉默的主要原因，那么我完全可以理解。

上，但作为架构师，我还想知道 Sybase 对 Coral8 引擎未来的计划。Sybase 购买了 Coral8 的源代码。Sybase 计划从 Coral8 获得连续的改进，随着 Coral8 引擎和语言的发展吗？Sybase 计划对源代码进行单独的分叉，以至于最终 Coral8 引擎和语言以及 Sybase RAP 引擎和语言成为两回事吗？Sybase RAP 最终会整合 Aleri 的 Splash 语言吗？这些都是对我们来说非常重要的事情。我们需要看到 Sybase 的路线图以及 Coraleri 的路线图。

在

[Marco 的博客上的一篇帖子](http://rulecore.com/CEPblog/?p=213)

，Era 提出了非常重要的问题：

这个交易的还有其他细节吗？这是一次性的源代码树分叉吗？Sybase 会从 Aleri 获得新版本吗？有趣的是，如果 Sybase 他们会自己进一步开发，或者 bug 修复、补丁和新功能会来自 Aleri 的开发人员？

John Morrell 从 Coraleri 回应说：

抱歉，我们不会发布关于交易条款的更多细节。这些都是 Sybase 和 Aleri 之间的商业条款。

这有点令人不安。我可以理解财务条款没有公布（尽管有趣的是，如果 Coraleri 从每笔 Sybase RAP 销售中获得一部分收入，这将有助于改善 Coraleri 的财务状况）。但不透露 Sybase 的计划透明度对 Sybase 来说不是好消息，尽管这对 Coraleri 来说是个积极的因素。我无法了解 Sybase 是否会根据 Coraleri 即将进行的工作升级他们的引擎，这让我感到不安。

Sybase RAP 可以不使用 CEP 部分。然而，我不知道 RAP 的其他部分是否依赖于其他第三方供应商，以及这些其他部分是否面临任何风险。而且，它看起来与 KDB+和 Vhayu 有一些重叠。（我想知道是否有第三方对这三者进行了比较。）

在这些问题没有得到解答之前，我不会推荐 Sybase RAP 进行考虑。当前的情况留下了太多未解答的问题。我期待 Sybase 能提供更多的透明度。

©2009 马克·阿德勒 - 版权所有。

这里的所有观点都是个人的，与我的雇主无关。
