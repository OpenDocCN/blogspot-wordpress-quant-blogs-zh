<!--yml

分类：未分类

日期：2024-05-18 05:18:11

-->

# Magmasystems 博客：GemFire

> 来源：[`magmasystems.blogspot.com/2006/09/gemfire.html#0001-01-01`](http://magmasystems.blogspot.com/2006/09/gemfire.html#0001-01-01)

我正在开始对对象缓存技术的评估，从

[GemFire](http://www.gemstone.com/products/)

。目标应用程序是一个遗留的 C++应用程序，因此 Gemstone 拥有 GemFire 的 C++版本是一个很大的优势。他们还有.NET 绑定，我也会查看那些内容。

一个小陷阱 ... GemFire 不支持 Windows 2000，因为其底层依赖关系 29West 的 LBM 消息代理。这对于想在公司的工作站上进行评估的人来说是一个真正的恶心，但是公司仍然在使用 Windows 2000。因此，我不得不在运行 XP Pro 的家庭笔记本上安装 GemFire，并在笔记本上进行评估。

计划是使用对象缓存作为“数据布匹”，以加速我们的计算引擎。像 GigaSpaces 这样的对象缓存已经在许多华尔街投资银行中用于此目的。我听说一些前同事关于 GigaSpace 实现有一些小小的骚动，所以我们希望 GemFire 能够无忧无虑。到目前为止，我对他们的技术支持团队印象深刻（感谢 Mike 和 Santiago 的及时回应）。

我对任何评估过或在自己的金融应用程序中使用对象缓存的各位人士的评论感兴趣，尤其是 C++或 C#应用程序。请随意在此评论或私下给我发邮件。

©2006 Marc Adler - 版权所有
