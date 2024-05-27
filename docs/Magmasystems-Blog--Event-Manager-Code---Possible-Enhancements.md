```yaml

分类：未分类

日期：2024-05-18 05:20:54

```

# Magmasystems Blog: Event Manager Code - Possible Enhancements

> 来源：[`magmasystems.blogspot.com/2006/04/event-manager-code-possible.html#0001-01-01`](http://magmasystems.blogspot.com/2006/04/event-manager-code-possible.html#0001-01-01)

现在我已经发布了我在几个项目中使用的 Event Manager 的代码，我想列出一些我已经考虑过的可能的改进：

**预编译正则表达式**

事件管理器支持通配符。.NET 正则表达式类用于匹配带有通配符的发布主题和订阅。然而，我没有预编译正则表达式。这是一个非常简单的更改。

**增强的正则表达式**

我们可以扩展通配符订阅将接受的正则表达式。例如，为了订阅交易的插入或删除操作，我们应该能够有一个像这样的通配符主题：

Magmasystems.TradingSystem.Trade.[InsertedDeleted] **事件声明中 args 的更强类型**

EventManager.Fire()的第三个参数是继承自 EventManagerArgs 的任何东西。我们可以通过指定发布者期望发送和相应订阅者期望接收的 EventManagerArgs 的子类来增加类型安全性。

**作用域**

微软的 CAB 有事件作用域的概念。我们可以限制一个发布事件仅限于在同一个线程（或特定的线程）中运行的订阅者。我们可以将作用域限制在一个名为“applet”的命名空间中。否则，默认情况下，事件是全局发布的。

**EventManager.Register(this)**

我并不是特别兴奋，因为对于每个发布或订阅的对象，都会调用 EventManager.Register(this)。注册函数将检查传递的类，使用类反射来构建发布者和订阅者到主题的字典。

**动态注册发布者和订阅者**

instead of using the static way of decorating a method, we may want to add publications and subscriptions dynamically. For instance, we should be able to say something liek this:

EventManager.Subscribe("Magmasystems.TradingSystem.Trade.*", this.OnTradeEvent);**事件发布的水槽**

实现水槽，以便类在事件参数被发送给订阅者之前有机会处理事件参数。

©2006 Marc Adler - 版权所有
