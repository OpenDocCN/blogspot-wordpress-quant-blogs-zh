<!--yml

类别：未分类

日期：2024-05-18 04:48:51

-->

# Magmasystems Blog：在您的 PC 上安装 RabbitMQ

> 来源：[`magmasystems.blogspot.com/2011/11/installing-rabbitmq-on-your-pc.html#0001-01-01`](http://magmasystems.blogspot.com/2011/11/installing-rabbitmq-on-your-pc.html#0001-01-01)

在过去的 7 年里，我一直在我的笔记本上运行 Tibco EMS 的旧版本，每当我需要做一些原型设计和开发新的基于消息的应用时，我就会使用它。但在这些成本意识的年代，我的许多客户都在寻找低成本的解决方案。所以，是时候认真考虑 RabbitMQ 了。

这是一份我写的快速指南，以便在准备一些.NET 开发时，在本地 PC 上安装并运行 RabbitMQ。

1) RabbitMQ 需要 Erlang 运行时。您可以从

您需要在下载并安装 RabbitMQ 服务器之前安装 Erlang。

2a) 安装 RabbitMQ。它会安装一个 Windows 服务，并自动启动它。

并验证 RabbitMQ 服务是否已启动。

3a) 下载.NET 3.0 版本的 RabbitMQ 客户端库和示例。这个文件叫做 rabbitmq-dotnet-client-2.6.1-

3b) 将 ZIP 文件提取到 C:\Program Files\RabbitMQDotNetClient（您可以选择您想要的任何位置）。

3c) 在 C:\Program Files\RabbitMQDotNetClient\

<wbr>

bin 中，有一个名为

**RabbitMQ.Client.dll**

在同一目录中，有一个名为

**RabbitMQ.ServiceModel.dll**

.

4) 从 Windows 开始菜单，找到 RabbitMQ 服务器项，然后运行 RabbitMQ 命令提示符

4a) rabbitmqctl.bat 是让您控制 RabbitMQ 并列表各种对象的命令行工具。一个用于列出 RabbitMQ 交换的示例命令是

rabbitmqctl list_exchanges

然而，我们将使用管理控制台，而不是命令行。

5) 从

[`www.rabbitmq.com/plugins.html`](http://www.rabbitmq.com/plugins.html)

5a) 下载与 rabbitmq_management_visualiser 相关的所有 EZ 文件

5b) 将这些文件拖放到我的系统上的 C:\Program Files (x86)\RabbitMQ Server\rabbitmq_server-2.6.1\

<wbr>

插件

5c) 重新启动 RabbitMQ 服务器。您可以通过在您的 Windows 机器上的 Services.msc 小程序来完成此操作。

**使用管理控制台测试**

现在我们将通过将消息发送到交换区并让通配符订阅者读取该消息来测试 RabbitMQ。

6) 为了测试 RabbitMQ 管理控制台，请在您的浏览器中尝试这个 URL：

[`localhost:55672/mgmt/`](http://localhost:55672/mgmt/)

使用用户 ID“guest”和密码“guest”

7) 转到

*交换区*

标签并添加一个名为

*CalcExchange*

这是一个非持久（临时）主题。填写名称、类型和持久性，如下所示：

**名称：**

CalcExchange

**类型：**

主题

**持久性：**

临时

8) 转到

*队列*

标签并添加一个名为

*Calc.Queue.1*

9) 留在

*队列*

标签页。在队列表中，点击

*Calc.Queue.1*

9a) 添加一个绑定。在交换和路由键字段中，添加以下内容：

**交换:**

CalcExchange

**路由键:**

Calc.Data.*.1

这将绑定任何具有路由键

*Calc.Data.*.1*

到

*Calc.Queue.1*

消息队列。所以，如果你使用键

*Calc.Data.Foobaz.1*

，它将被路由到此队列，订阅者将从此队列中获取消息进行处理。

现在我们将尝试使用管理控制台发送一个示例消息。

10) 返回“交换”标签页，点击 CalcExchange 项

10a) 向下滚动到

*发布消息*

部分。

10b) 为路由键和载荷字段输入以下内容：

**路由键:**

Calc.Data.ABC123.1,

**载荷:**

这是一个给 Calc Node 1 的测试消息

10c) 点击

*发布*

按钮。当状态消息弹出时，只需关闭它。状态消息应该有一个绿色背景，表示成功。

11) 返回

*队列*

标签页，点击 Calc.Queue.1

11a) 向下滚动到

*获取消息*

部分并点击“获取消息(s)”按钮。你应该看到你刚刚发送的消息。

12) 你也可以访问管理页面最后的标签页，应该是

*可视化器*

标签页，查看拓扑结构。

顺带一提，随.NET 客户端提供的示例程序需要在加载到 Visual Studio 2010 之前进行大量修改。

©2011 Marc Adler - 版权所有。此处所有观点均为个人观点，与我的雇主无关。
