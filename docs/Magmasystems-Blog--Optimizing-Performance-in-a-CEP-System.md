<!--yml

类别：未分类

Tibco

-->

# Magmasystems 博客：优化 CEP 系统的性能

> 来源：[`magmasystems.blogspot.com/2008/09/optimizing-performance-in-cep-system.html#0001-01-01`](http://magmasystems.blogspot.com/2008/09/optimizing-performance-in-cep-system.html#0001-01-01)

以下是我们减少来自我们的消息备份的一些经验教训

Tibco

EMS 代理到我们的

CEP

输入服务器。

1) 确保你在

Tibco

继电器和你的服务器。

我们碰巧发现硬件工程师给了我们遗留的 100MB 连接

2) 可能有帮助将“

EMS 代理和我们的

CEP

输入服务器。我们要求他们升级我们到

GigE

立即。除非你亲自安装了你的硬件，在你的基础设施中绝不要假设任何东西。

，按股票代码

自动确认

关于每条 FIX 消息的所有权放在

Tibco

会话之间。

为了做到这一点，改变

this.m_connection.CreateSession(false, SessionMode.AutoAcknowledge);

到

this.m_connection.CreateSession(false, SessionMode.NoAcknowledge);

日期：2024-05-18 04:59:17

确认

。这对你的影响是什么

CEP

系统如果你碰巧丢失了一条消息？

3) 在

Tibco

到你的输入服务器，并从你的输入服务器到

供应商。

系统。

如果你需要更好的性能，改变从

Tibco

CEP

负载均衡器

可以按

到一个负载均衡的多个队列，每个队列都有自己的线程。负载

主题消息之前在你的输入服务器中对消息进行一些

订单 ID

。

当然，你也可以使用来自你的

CEP

供应商。但这可能会额外增加成本，所以请向你的

CEP

供应商，看看某个输入适配器是否免费。另外，越多

CEP

你使用的供应商基础设施越多，就越容易与之捆绑在一起

CEP

要小心使用无

4) 试着在传递给

Tibco

- 过滤在传递给

CEP

引擎。

最近，我们成功将 Coral8 的 CPU 使用率减少了约 50%（根据我们的 Coral8 专家），通过过滤我们知道 Coral8 不感兴趣的 FIX 消息。

5) 持续优化你的代码。就在今天早上，我审查了输入服务器的代码，并提出了一项更改，减少了一个

hashtable 查找

的网络连接快速。

6) 使用服务器垃圾收集器

©2008 Marc Adler - 版权所有。

这里的所有意见都是个人意见，与我的雇主无关。
