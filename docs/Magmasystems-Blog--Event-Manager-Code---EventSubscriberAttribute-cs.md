<!--yml

分类：未分类

日期：2024-05-18 05:21:06

-->

# 磁码系统博客：事件管理器代码 - EventSubscriberAttribute.cs

> 来源：[`magmasystems.blogspot.com/2006/04/event-manager-code-eventsubscriberattr.html#0001-01-01`](http://magmasystems.blogspot.com/2006/04/event-manager-code-eventsubscriberattr.html#0001-01-01)

EventSubscriberAttribute 用于装饰 C#函数，该函数是我们事件管理器订阅的事件的接收者。主题名称可以是通配符字符串，就像 Tibco 一样。例如，要订阅所有关于交易发生的事件，你可以订阅主题"TradingSystem.Trade.*"。

请注意，该属性已声明 AllowMultiple=true。这使得一个函数可以有多个订阅声明。

需要注意的最后一点是 IsBackground 标志。如果一个订阅者声明为 IsBackground=true，那么事件将被调度到一个工作线程（内部使用 Begin/EndInvoke）。

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

©2006 Marc Adler - 版权所有
