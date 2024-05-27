<!--yml

类别：未分类

日期：2024-05-18 05:21:14

-->

# Magmasystems Blog: C#/.NET 的轻量级内 app 事件代理

> 来源：[`magmasystems.blogspot.com/2006/04/lightweight-intraapp-event-broker-for.html#0001-01-01`](http://magmasystems.blogspot.com/2006/04/lightweight-intraapp-event-broker-for.html#0001-01-01)

多年来，我设法编写了一系列有趣的类库，这些类库帮助我在系统架构和开发中。在接下来的几个月里，有时间的话，我会提交一些这些类库供您使用。

大约两年前，我为具有 Tibco 连接的交易系统编写了一个事件代理，该系统将报价发布到消息总线。我希望从后端到前端，以及在前端内部的对称处理模型。因此，我编写了一个基于.NET/C#的轻量级事件代理，类似于 GUI 内的 min-Tibco。

Microsoft CAB 有类似的东西，出来的时候，我从它那里拿了一些想法（比如弱引用处理）并整合到我的事件代理中。CAB 与我不同之处在于几个方面......也就是说，它有事件范围的概念，而且它装饰代码的方式也不同（它装饰事件声明，而我不装饰方法）。

然而，这个事件代理已经在几个交易系统中使用，并且似乎运行良好。

在接下来的几篇帖子中，我将发布事件代理的代码。您可以自由使用它，只要保持我的版权并给予适当的认可。另外，我很想听听您可能对我在这里发布的任何类所做的任何改进、增强和错误修复。您可以通过以下方式随时联系我：

*magmasystems at yahoo dot com*

.

**事件代理**

应用程序使用轻量级发布/订阅（PubSub）模型内部通知控制器或 UI 层有趣的事件。一个典型有趣的事件是底层数据模型的变化。

实现应用程序内 PubSub 的机制称为事件代理。事件发布者和事件订阅者将通过使用自定义的.NET 属性自动注册到事件管理器。

使用事件管理器绝不妨碍应用程序用自己的.NET 事件/委托机制进行事件管理。

**在类中使用 EventBroker**

任何想要使用 EventBroker 的发布/订阅功能的类应该做两件事。

1) 添加对 EventBroker 程序集的引用。同样，在您的类内部引用命名空间：

using Magmasystems.TradingSystem.EventManager;

2) 使用 EventBroker 注册类。这样做的一个好地方是在类的构造函数中。要注册类以使用事件代理，只需插入以下代码行：

EventBroker.Register(this);

There are several .NET attributes that can be used to decorate functions in order to define them as either Event Publishers or Event Subscribers. When one of these attributes is constructed, the EventTopic parameter is examined. The EventTopic is added to the EventManager's internal Dictionary. A Dictionary collection is used in order to provide fast access to a particular Topic/Event pairing.

[EventPublisher(string EventTopic)]

This registers a function or class to be an event publisher. The class will publish an event with a specific name. Any subscribers to that topic will be notified.

[EventSubscriber(string EventTopic, options)]

This registers a subscriber to an event. The attribute should be placed directly above the function that will be used as the event handler. The options can be one of the following:

*

**Background**

- the handler is called asynchronously

The string-based topic name can be the actual name of a published topic, or it can be a

**wildcarded**

topic like

"Magmasystems.TradingSystem.Trade.*"

.

To fire an event, the static method EventManager.Fire() is called

EventManager.Fire(object obj, string eventTopic, EventArgs args);

Event handlers have the signature:

public delegate bool EventManagerEventHandler(object sender,

string topicName, EventArgs e);

Here is a piece of code that publishes an event (The recipient could be a controller that processes events from views and from the models):

[EventPublisher("Magmasystems.TradingSystem.Controller.Action.GetTrades")]

private void GetTrades()

{

GetTradeArgs args = new GetTradeArgs();args.CUSIP = "12345";EventBroker.Fire(this, "Barcap.Gcdit.Odc.Controller.Action.GetTrades", args);

}

Here is a piece of code from a controller that subscribes to an event

[EventSubscriber("Magmasystems.TradingSystem.Controller.Action.GetTrades")]

public void GetTrades(object sender, string topicName, System.EventArgs e)

{

GetTradesUnitOfWork.GetTradesArgs args = e as GetTradesUnitOfWork.GetTradesArgs;

if (e == null)

return;

ExecuteAction(new GetTradesUnitOfWork(this._context.UIApplicationContext, args));

}

There is a .Net event associated with every topic that is registered. Events are really Multicast Delegates. Every subscriber to an event adds an event handler to the list of delegates. When an event is fired, the delegate list is traversed and each delegate will be invoked either synchronously or asynchronously. The options can include the Background flag. This tells the event firing mechanism that the underlying delegate should be invoked asynchronously. If the

*Background*

flag is not present in the attribute declaration, then the underlying delegate will be invoked synchronously.

**Guidelines for Usage**

Any class can publish an event, and any class can subscribe to that event.

The line of code that registers a class with the EventBroker is best put in the constructor of the Base Class.

在我们采纳了命名空间约定之后，我们也采纳了一项通用的事件命名约定。这项约定是：

公司名.部门.应用.领域对象.动作

©2006 马克·阿德勒 - 版权所有
