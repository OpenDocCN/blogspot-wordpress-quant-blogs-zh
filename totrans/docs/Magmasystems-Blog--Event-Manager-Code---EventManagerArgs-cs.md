<!--yml
category: 未分类
date: 2024-05-18 05:21:02
-->

# Magmasystems Blog: Event Manager Code - EventManagerArgs.cs

> 来源：[http://magmasystems.blogspot.com/2006/04/event-manager-code-eventmanagerargscs.html#0001-01-01](http://magmasystems.blogspot.com/2006/04/event-manager-code-eventmanagerargscs.html#0001-01-01)

These are two minor argument classes that are used to send information from the event publisher to the subscriber. The args are sent as the third parameter in the EventManager.Fire() function.

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

©2006 Marc Adler - All Rights Reserved