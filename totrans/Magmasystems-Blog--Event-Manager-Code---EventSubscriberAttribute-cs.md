<!--yml
category: 未分类
date: 2024-05-18 05:21:06
-->

# Magmasystems Blog: Event Manager Code - EventSubscriberAttribute.cs

> 来源：[http://magmasystems.blogspot.com/2006/04/event-manager-code-eventsubscriberattr.html#0001-01-01](http://magmasystems.blogspot.com/2006/04/event-manager-code-eventsubscriberattr.html#0001-01-01)

The EventSubscriberAttribute is used to decorate a C# function that is the recipient of a subscribed event from our event manager. The topic name can be a wildcard string, just like Tibco. For instance, to subscribe to all actions that happen to a trade, you can subscribe to topic "TradingSystem.Trade.*".

Notice that the attribute is declared with AllowMultiple=true. This lets a function have multiple subscription declarations.

The final thing to notice is the IsBackground flag. If a subscriber is declared with IsBackground=true, then the event will be dispatched to the subscriber on a worker thread (internally, Begin/EndInvoke is used).

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
 /// <summary>/// EventSubscriberAttribute
 ///</summary> 
 [AttributeUsage(AttributeTargets.Method, AllowMultiple=true)]
 public class EventSubscriberAttribute : System.Attribute
 {
  private string _topicName;
  private bool   _isBackground;

  public EventSubscriberAttribute()
  {
  }

  /// <summary>/// EventSubscriberAttribute
  ///</summary> 
  /// <param name="topicName">The name of the event
  public EventSubscriberAttribute(string topicName)
  {
   this._topicName    = topicName;
   this._isBackground = false;
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

  public bool IsBackground
  {
   get
   {
    return this._isBackground;
   }
   set
   {
    this._isBackground = value;
   }
  }
 }
} 
```` 

©2006 Marc Adler - All Rights Reserved