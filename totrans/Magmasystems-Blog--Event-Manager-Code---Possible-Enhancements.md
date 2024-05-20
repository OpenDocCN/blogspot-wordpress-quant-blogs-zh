<!--yml
category: 未分类
date: 2024-05-18 05:20:54
-->

# Magmasystems Blog: Event Manager Code - Possible Enhancements

> 来源：[http://magmasystems.blogspot.com/2006/04/event-manager-code-possible.html#0001-01-01](http://magmasystems.blogspot.com/2006/04/event-manager-code-possible.html#0001-01-01)

Now that I have posted the code for the Event Manager that I have used in several projects, I would like to list some possible enhancements that I have considered:

**Precompile regular expressions**

The Event Manager supports wildcards. The .NET RegularExpression classes are used to perform matching of a published topic with a wildcarded subscription. Howver, I do not pre-compile the regexps. This is a very simple change to make.

**Enhanced regular expressions**

We can expand the regular expressions that wildcarded subscriptions will accept. For example, to subscribe to an insert or delete action for a trade, we should be able to have a wildcard topic that looks like this:

Magmasystems.TradingSystem.Trade.[InsertedDeleted] **Stronger typing of args for event declarations**

The third argument of EventManager.Fire() is anything that derives from EventManagerArgs. We can add more type safety by specifying the subclass of EventManagerArgs that a publisher expects to send and that the corresponding subscribers expect to receive.

**Scoping**

Microsoft's CAB has the notion of event scoping. We can limit a published event to subscribers that run in the same thread (or a certain thread) as the publisher. We can limit the scope to a named "applet". Otherwise, by default, the event is published globally.

**EventManager.Register(this)**

I am not totally thrilled with the fact that, for every object that publishes or subscribes, a call to EventManager.Register(this) is called. The Register() function will examine the passed class, using reflection on the class to build up a dictionary of publishers and subscribers to a topic.

**Dynamically register the publisher and subscriber**

Instead of using the static way of decorating a method, we may want to add publications and subscriptions dynamically. For instance, we should be able to say something liek this:

EventManager.Subscribe("Magmasystems.TradingSystem.Trade.*", this.OnTradeEvent);**Sinks for event publishing**

Implement Sinks so a class can have a crack at an event args before it is sent to the subscribers.

©2006 Marc Adler - All Rights Reserved