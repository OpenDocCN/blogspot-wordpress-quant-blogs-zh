<!--yml
category: 未分类
date: 2024-05-18 05:21:10
-->

# Magmasystems Blog: Event Manager Code - EventPublisherAttribute.cs

> 来源：[http://magmasystems.blogspot.com/2006/04/event-manager-code-eventpublisherattri.html#0001-01-01](http://magmasystems.blogspot.com/2006/04/event-manager-code-eventpublisherattri.html#0001-01-01)

The EventPublisherAttribute is a C# attribute that decorates a function that publishes an internal event. Any function that publishes an event out to our little event broker should decorate itself with this attribute.For example:

 ````
 [EventPublisher("Brokerage.TradingSystem.Trade.ReceivedFromBackend")]
public void OnTradeReceived(Trade trade)
{
  .......
  EventManager.Fire(this, "Brokerage.TradingSystem.Trade.ReceivedFromBackend", 
                    tradeArgs);
} 
```` 

Here is the code:

 ````
 using System;
// --------------------------------------------------------------------
//
// This code is (C) Copyright 2005 Marc Adler
//
// --------------------------------------------------------------------

namespace Magmasystems.EventManager
{
 /// <summary>/// EventPublisherAttribute
 ///</summary> 
 public class EventPublisherAttribute : Attribute
 {
  private string _topicName;

  public EventPublisherAttribute()
  {
  }

  /// <summary>/// EventPublisherAttribute
  ///</summary> 
  /// <param name="topicName">The name of the event
  public EventPublisherAttribute(string topicName)
  {
   this._topicName = topicName;
  }

  public string Topic
  {
   get
   {
    return this._topicName;
   }
   set
   {
    this._topicName = value;
   }
  }
 }
} 
```` 

©2006 Marc Adler - All Rights Reserved