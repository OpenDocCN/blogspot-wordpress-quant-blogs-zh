<!--yml

分类：未分类

date: 2024-05-18 05:13:59

-->

# Magmasystems Blog: CAB, EventBroker, and Wildcards

> 来源：[`magmasystems.blogspot.com/2006/12/cab-eventbroker-and-wildcards.html#0001-01-01`](http://magmasystems.blogspot.com/2006/12/cab-eventbroker-and-wildcards.html#0001-01-01)

我很快就会写关于 CAB EventBroker 的博客。但是，我认为我更喜欢我的（之前在这里发布过）。我希望在 EventBroker 的订阅字符串中看到通配符支持。

在 CAB 中，您可以这样定义一个发布事件：

[事件发布("event://Trade/Update", 发布范围.全局)]public 事件处理<instrumentupdatedeventargs>TradeUpdated;</instrumentupdatedeventargs>........public void TradeIsUpdated(Trade trade){ if (this.TradeUpdated != null) { this.TradeUpdated(this, new InstrumentUpdatedEventArgs(trade)); }}

在其他模块中，您可以这样订阅一个事件：

[事件订阅("event://Trade/Update")public void OnTradeUpdated(object sender, InstrumentUpdatedEventArgs e){}

我需要通配符。我可能希望有一个函数，当对 Trade 对象执行任何操作时调用。因此，我希望看到这样的订阅主题：

"event://Trade/*"

或者

"event://Trade

这两个都会涵盖对交易对象执行任何操作的情况。订阅字符串将捕获以下主题：

event://Trade/Updatedevent://Trade/Deletedevent://Trade/Created

我需要 Tibco-lite 作为我的内部消息总线。

©2006 Marc Adler - 版权所有
