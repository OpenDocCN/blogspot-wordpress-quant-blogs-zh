```yaml

分类：未分类

日期：2024-05-18 05:21:10

→

# Magmasystems 博客：事件管理器代码 - `EventPublisherAttribute.cs`

> 来源：[`magmasystems.blogspot.com/2006/04/event-manager-code-eventpublisherattri.html#0001-01-01`](http://magmasystems.blogspot.com/2006/04/event-manager-code-eventpublisherattri.html#0001-01-01)

`EventPublisherAttribute`是一个 C#属性，它装饰了一个发布内部事件的函数。任何发布事件到我们这个小事件代理的函数都应该用这个属性来装饰自己。例如：

````
 [EventPublisher("Brokerage.TradingSystem.Trade.ReceivedFromBackend")]
public void OnTradeReceived(Trade trade)
{
  .......
  EventManager.Fire(this, "Brokerage.TradingSystem.Trade.ReceivedFromBackend", 
                    tradeArgs);
} 
````

以下是代码：

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

©2006 Marc Adler - 版权所有
