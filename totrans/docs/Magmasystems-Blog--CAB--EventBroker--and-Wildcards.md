<!--yml
category: 未分类
date: 2024-05-18 05:13:59
-->

# Magmasystems Blog: CAB, EventBroker, and Wildcards

> 来源：[http://magmasystems.blogspot.com/2006/12/cab-eventbroker-and-wildcards.html#0001-01-01](http://magmasystems.blogspot.com/2006/12/cab-eventbroker-and-wildcards.html#0001-01-01)

I will be blogging about the CAB EventBroker soon. But, I think that I like mine (previously published here) better. I would like to see wildcard support in the EventBroker's subscription strings.

In CAB, you can define an event to be published like this:

[EventPublication("event://Trade/Update", PublicationScope.Global)]public event EventHandler <instrumentupdatedeventargs>TradeUpdated;</instrumentupdatedeventargs>........public void TradeIsUpdated(Trade trade){ if (this.TradeUpdated != null) { this.TradeUpdated(this, new InstrumentUpdatedEventArgs(trade)); }}

In some other module, you can subscribe to an event like this:

[EventSubscription("event://Trade/Update")public void OnTradeUpdated(object sender, InstrumentUpdatedEventArgs e){}

I need wildcards. I might like to have a function that gets called when any operation happens to a Trade object. So, I would like to see subscription topics like these:

"event://Trade/*"

or

"event://Trade

Both of these would cover the case when any operation happens to a trade. The subscription string would catch the following topic:

event://Trade/Updatedevent://Trade/Deletedevent://Trade/Created

I need Tibco-lite as my internal message bus.

©2006 Marc Adler - All Rights Reserved