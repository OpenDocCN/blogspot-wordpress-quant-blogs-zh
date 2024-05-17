<!--yml
category: 未分类
date: 2024-05-18 05:21:14
-->

# Magmasystems Blog: A Lightweight IntraApp Event Broker for C#/.NET

> 来源：[http://magmasystems.blogspot.com/2006/04/lightweight-intraapp-event-broker-for.html#0001-01-01](http://magmasystems.blogspot.com/2006/04/lightweight-intraapp-event-broker-for.html#0001-01-01)

Over the years, I have managed to write a repository of interesting classes that has helped me in architecting and developing systems. Over the coming months, and as time allows, I will submit some of these classes for your use.

I wrote the EventBroker about two years ago for a trading system that had Tibco connectivity to a message bus that published quotes. I wanted a symmetrical processing model from the back end to the front end, and also, within the front end. So, I wrote a .NET/C#-based lightweight event broker that was like a min-Tibco within the GUI.

The Microsoft CAB has something similar, and when it came out, I took a few ideas from it (such as the handling of WeakReferences) and integrated it into my own Event Broker. CAB differs from mine in several respects .... namely, it has the concept of Event Scope, and it also has a different way of decorating code (it decorates event declarations, while mine decorates methods).

However, this event broker has been used in several trading systems and seems to function well.

In the next several posts, I will post the code of the Event Broker. You are free to use it as long as my copyright is maintained and proper acknowledgement is given. Also, I am anxious to hear of any improvments, enhancements and bug fixes you might make to any of the classes that I publish here. You can always reach me at

*magmasystems at yahoo dot com*

.

**The Event Broker** 

The application uses a lightweight Publish/Subscribe (PubSub) model internally in order to notify the controller or UI layer of interesting events. A typical interesting event is a change in the underlying data model.

The mechanism that implements PubSub within the application is called the Event Broker. Event publishers and event subscribers will be automatically registered with the Event Manager by the use of customized .NET attributes.

The use of the Event Manager in no way precludes the application from doing its own event management using the standard .NET event/delegate mechanism.

**Using the EventBroker in a class**

Any class that wants to use the Pub/Sub capabilities of the EventBroker should do two thing.

1) Include a reference to the EventBroker's assembly. Also, reference the namespace within your class:

using Magmasystems.TradingSystem.EventManager; 

2) Register the class with the EventBroker. A good place to do this is in the class' constructor. To register the class with the Event Broker, all that needs to be done is to put in the following line of code:

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

Any class can publish an event, and any class can subscribe to that event. The event bus is global to the entire application.

The line of code that registers a class with the EventBroker is best put in the constructor of the Base Class.

Following our adoption of a namespace convention, we have also adopted a general naming convention for events. This convention is:

companyname.department.application.domainobject.action 

©2006 Marc Adler - All Rights Reserved