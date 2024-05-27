<!--yml

分类：未分类

日期：2024-05-18 05:21:02

-->

# Magmasystems 博客：事件管理器代码 - EventManagerArgs.cs

> 来源：[`magmasystems.blogspot.com/2006/04/event-manager-code-eventmanagerargscs.html#0001-01-01`](http://magmasystems.blogspot.com/2006/04/event-manager-code-eventmanagerargscs.html#0001-01-01)

这些都是两个用于从事件发布者向订阅者发送信息的次要参数类。这些参数作为 EventManager.Fire()函数的第三个参数发送。

````
 using System;

namespace Magmasystems.EventManager
{
 /// <summary>/// Summary description for EventManagerArgs.
 ///</summary> 
 public class EventManagerArgs : EventArgs
 {
  public EventManagerArgs()
  {
  }
 }

        // This is used to pass string data between the publisher and subscriber
 public class EventManagerMessageArgs : EventManagerArgs
 {
  private string _message;

  public EventManagerMessageArgs(string msg)
  {
   this._message = msg;
  }

  public string Message
  {
   get { return this._message; }
  }
 }
} 
````

©2006 Marc Adler - 版权所有
