<!--yml
category: 未分类
date: 2024-05-18 05:20:58
-->

# Magmasystems Blog: Event Manager Code - EventManager.cs

> 来源：[http://magmasystems.blogspot.com/2006/04/event-manager-code-eventmanagercs.html#0001-01-01](http://magmasystems.blogspot.com/2006/04/event-manager-code-eventmanagercs.html#0001-01-01)

Here is the code for the main EventManager class.

There are a number of ways that I would like to improve the code, but just never have had the time. When I get a few free moments, I will discuss some of the enhancements that I would like to put in the code eventually.

 ````
 // for MethodImplAttrbute
using System;
using System.Collections;
using System.ComponentModel;
using System.Reflection;
using System.Runtime.CompilerServices;
using System.Text.RegularExpressions;
// for ISynchronizer

// --------------------------------------------------------------------
//
// This code is (C) Copyright 2005 Marc Adler
//
// --------------------------------------------------------------------

namespace Magmasystems.EventManager
{
  public delegate bool EventManagerEventHandler(object sender, string topicName, EventArgs e);

  public class EventManager
  {
    #region Delegates

    // Internal delegate used to help us fire async events
    private delegate void AsyncFire(Delegate del, object[] args);

    #endregion

    #region Variables

    // The singleton EventManager
    private static EventBroker _theEventManager = null;

    // A Dictionary of EventManagerEventInfo classes, indexed by the topic name
    private Hashtable _theEventDictionary = null;

    private Hashtable _theWildcardSubscribers = null;

    // Used to disabled and re-enable the firing of events
    private bool _isEnabled = true;

    #endregion

    #region Constructors and Static Instance

    protected EventBroker()
    {
    }

    // This is the way that the EventManager singleton is accessed
    static public EventManager Instance
    {
      get
      {
        if(_theEventManager == null)
        {
          _theEventManager = new EventBroker();
          _theEventManager._theEventDictionary = new Hashtable();
          _theEventManager._theWildcardSubscribers = new Hashtable();
          _theEventManager._isEnabled = true;
        }
        return _theEventManager;
      }
    }

    #endregion

    #region Properties

    private Hashtable Dictionary
    {
      get
      {
        // make sure that the dictionary and event manager are instantiated
        return _theEventDictionary;
      }
    }

    private Hashtable WildcardDictionary
    {
      get
      {
        // make sure that the dictionary and event manager are instantiated
        return _theWildcardSubscribers;
      }
    }

    public bool Enabled
    {
      get { return this._isEnabled; }
      set { this._isEnabled = value; }
    }

    #endregion

    #region General Methods

    static public void Register(object o)
    {
      Type type = o.GetType();

      MethodInfo[] methods = type.GetMethods();
      foreach (MethodInfo mi in methods)
      {
//        if(mi.DeclaringType != type)
//          continue;
        object[] oAttrs = mi.GetCustomAttributes(true);
        foreach (object oAttr in oAttrs)
        {
          EventManagerEventInfo evInfo;
          if(oAttr is EventSubscriberAttribute)
          {
            EventSubscriberAttribute evSubAttr = oAttr as EventSubscriberAttribute;
            evInfo = FindTopicEntry(evSubAttr.Topic, true);
            if(evInfo != null)
            {
              EventSubscriberInfo subInfo = evInfo.AddSubscriber(evSubAttr.Topic, o, evSubAttr.IsBackground, mi);
              if(subInfo.HasWildcards)
              {
                EventBroker.Instance._theWildcardSubscribers[evSubAttr.Topic] = evInfo;
              }
            }
          }

          else if(oAttr is EventPublisherAttribute)
          {
            EventPublisherAttribute evPubAttr = oAttr as EventPublisherAttribute;
            evInfo = FindTopicEntry(evPubAttr.Topic, true);
            if(evInfo != null)
            {
              evInfo.AddPublisher(evPubAttr.Topic, o);
            }
          }
        }
      }
    }

    static private EventManagerEventInfo FindTopicEntry(string topicName, bool createIfEmpty)
    {
      EventManagerEventInfo evInfo  ;

      topicName = topicName.ToUpper();
      object oEventInfo = EventBroker.Instance._theEventDictionary[topicName];

      if(oEventInfo == null)
      {
        if(createIfEmpty)
        {
          // Allocate a new entry
          evInfo = new EventManagerEventInfo();
          EventBroker.Instance.Dictionary[topicName] = evInfo;
        }
        else
        {
          evInfo = null;
        }
      }
      else
      {
        // Use the existing entry
        evInfo = oEventInfo as EventManagerEventInfo;
      }

      return evInfo;
    }

    #endregion

    #region Ways to Fire and Event

    [MethodImpl(MethodImplOptions.NoInlining)]
    static public void Fire(object sender, string topicName, EventArgs args)
    {
      if (EventBroker.Instance.Enabled == false)
        return;

      EventManagerEventInfo evInfo = FindTopicEntry(topicName, false);
      if(evInfo != null)
      {
        evInfo.Fire(sender, topicName, args);
      }

      foreach (object oKey in EventBroker.Instance._theWildcardSubscribers.Keys)
      {
        string keyName = oKey as String;
        Regex regExp = new Regex(keyName, RegexOptions.IgnoreCase);
        if(regExp.IsMatch(topicName))
        {
          evInfo = EventBroker.Instance._theWildcardSubscribers[oKey] as EventManagerEventInfo;
          evInfo.Fire(sender, topicName, args);
        }
      }
    }

    #endregion

    #region Inner Class for EventManagerEventInfo

    /// <summary>/// EventManagerEventInfo
    /// This class represents information about a single event
    ///</summary> 
    public class EventManagerEventInfo
    {
      #region Variables

      // Multicast delegate of all subcribers to this event
      private event EventManagerEventHandler _eventHandler;

      // The list of classes that publish this event
      private ArrayList _publishers;
      // The list of classes that subscribe to this event
      private ArrayList _subscribers;

      #endregion

      #region Constructors

      public EventManagerEventInfo()
      {
        this._publishers = new ArrayList();
        this._subscribers = new ArrayList();
        this._eventHandler = null;
      }

      #endregion

      #region Events

      public event EventManagerEventHandler EventManagerEvent
      {
        add { this._eventHandler += value; }
        remove { this._eventHandler -= value; }
      }

      #endregion

      #region Properties

      public EventManagerEventHandler EventHandler
      {
        get { return this._eventHandler; }
      }

      public ArrayList Publishers
      {
        get { return this._publishers; }
      }

      public ArrayList Subscribers
      {
        get { return this._subscribers; }
      }

      #endregion

      #region Methods

      public EventSubscriberInfo AddSubscriber(string topicName, object objectRef, bool isBackground, MethodInfo mi)
      {
        EventSubscriberInfo subInfo = new EventSubscriberInfo(this, topicName, objectRef, isBackground, mi);
        this._eventHandler += new EventManagerEventHandler(subInfo.OnPublisherFired);
        this.Subscribers.Add(subInfo);
        return subInfo;
      }

      public EventPublisherInfo AddPublisher(string topicName, object objectRef)
      {
        EventPublisherInfo pubInfo = new EventPublisherInfo(this, topicName, objectRef);
        this.Publishers.Add(pubInfo);
        return pubInfo;
      }

      public void RemoveSubscriber(EventSubscriberInfo sub)
      {
        this.Subscribers.Remove(sub);
      }

      public void RemovePublisher(EventPublisherInfo pub)
      {
        this.Publishers.Remove(pub);
      }

      #endregion

      #region Event Firing

      public void Fire(object sender, string topicName, EventArgs args)
      {
        // This handles the event firing to the SubscriberInfo class. In turn, the
        // SubscriberInfo object will invoke the actual delegate. The SubscriberInfo
        // object will determine whether the delegate shoul dbe called synchronously
        // or asynchronously.
        if(this.EventHandler != null)
        {
          this.EventHandler(sender, topicName, args);
        }
      }

      #endregion
    }

    #endregion

    #region Inner class for EventPublisherInfo

    public class EventPublisherInfo
    {
      #region Variables

      private EventManagerEventInfo _evInfo;
      private WeakReference _objectRef;
      private string _topicName; // the upper-cased name
      private string _displayName; // used to generate context menus at runtime

      #endregion

      #region Constructors

      private EventPublisherInfo()
      {
        this._objectRef = null;
      }

      public EventPublisherInfo(EventManagerEventInfo evInfo, string topicName) : this()
      {
        this._evInfo = evInfo;
        this.DisplayName = topicName;
        this._topicName = topicName.ToUpper();
      }

      public EventPublisherInfo(EventManagerEventInfo evInfo, string topicName, object objectRef) : this(evInfo, topicName)
      {
        this._objectRef = new WeakReference(objectRef);
      }

      #endregion

      #region Properties

      public WeakReference Publisher
      {
        get { return (this._objectRef.IsAlive == true) ? this._objectRef : null; }
        set { this._objectRef = value; }
      }

      public string DisplayName
      {
        get { return this._displayName; }
        set { this._displayName = value; }
      }

      #endregion
    }

    #endregion

    #region Inner class for EventSubscriberInfo

    public class EventSubscriberInfo
    {
      #region Variables

      private EventManagerEventInfo _eventInfo; // ref back to the holding container
      private WeakReference _objectRef;
      private MethodInfo _methodInfo; // The method that the event firer should Invoke
      private bool _isBackground;
      private EventManagerEventHandler _delegateForAsync;

      private string _topicName; // we may have wildcards
      private bool _hasWildcards; // to help determine whether to use RegEx or not

      #endregion

      #region Constructors

      private EventSubscriberInfo()
      {
        this._objectRef = null;
        this._isBackground = false;
        this._hasWildcards = false;
      }

      public EventSubscriberInfo(EventManagerEventInfo evInfo, string topicName) : this()
      {
        this._eventInfo = evInfo;
        this.TopicName = topicName; // use the property so that formatting is done
      }

      public EventSubscriberInfo(EventManagerEventInfo evInfo, string topicName, object objectRef) : this(evInfo, topicName)
      {
        this._objectRef = new WeakReference(objectRef);
      }

      public EventSubscriberInfo(EventManagerEventInfo evInfo, string topicName, object objectRef, bool isBackground, MethodInfo mi) : this(evInfo, topicName, objectRef)
      {
        this._isBackground = isBackground;
        this._methodInfo = mi;

        if(isBackground)
        {
          this._delegateForAsync = (EventManagerEventHandler) Delegate.CreateDelegate(typeof (EventManagerEventHandler), objectRef, mi.Name);
        }

      }

      #endregion

      #region Properties

      public object Subscriber
      {
        get { return (this._objectRef.IsAlive) ? this._objectRef.Target : null; }
      }

      public bool IsBackground
      {
        get { return this._isBackground; }
        set { this._isBackground = value; }
      }

      public string TopicName
      {
        get { return this._topicName; }
        set { this._topicName = FormatTopicName(value); }
      }

      public bool HasWildcards
      {
        get { return this._hasWildcards; }
      }

      #endregion

      #region Methods

      private string FormatTopicName(string topic)
      {
        // We want to make things easy for matching publishers and sunscribers.
        // 1) We always use upper-case topic names.
        // 2) Replace the dots with slashes so that the dot is not taken as a regexp
        //    character by the pattern matcher.
        // 3) Let us know whether this topic has a wildcard in it so we know whether
        //    to use the slow regexp matcher or the faster Equals operator.
        if(topic.IndexOfAny(new char[] {'*'}) >= 0)
          this._hasWildcards = true;

        return topic.Replace('.', '/').ToUpper();
      }

      #endregion

      #region Event Firing

      /// <summary>/// This gets called whenever the event manager fires an event.
      /// This does the hard work in event firing. It eventually calls
      /// the subscriber's delegate in order to process the event. it also determines
      /// whether the delegate should be called synchronously or asynchronously.
      ///</summary> 
      /// <param name="sender">
      /// <param name="topicName">
      /// <param name="args">
      /// <returns>// 
      public bool OnPublisherFired(object sender, string topicName, EventArgs args)
      {
        // If the object that this subscriber is bound to has been garbage-collected, then
        // remove the subscriber from the EventInfo's subscriber list and return.
        if(this.Subscriber == null)
        {
          this._eventInfo.RemoveSubscriber(this);
          return true;
        }

        if(this.IsBackground)
        {
          AsyncFire asyncFire = new AsyncFire(InvokeDelegate);
          asyncFire.BeginInvoke(this._delegateForAsync, new object[] {sender, topicName, args}, new AsyncCallback(Cleanup), null);
        }
        else
        {
          object oRet = this._methodInfo.Invoke(this.Subscriber, new object[] {sender, topicName, args});
          if(oRet is Boolean)
            return (bool) oRet;
        }

        return true;
      }

      private void InvokeDelegate(Delegate del, object[] args)
      {
        ISynchronizeInvoke synchronizer = del.Target as ISynchronizeInvoke;
        if(synchronizer != null) // Requires thread affinity
        {
          if(synchronizer.InvokeRequired)
          {
            synchronizer.Invoke(del, args);
            return;
          }
        }

        // Not requiring thread afinity or invoke is not required
        del.DynamicInvoke(args);
      }

      private void Cleanup(IAsyncResult asyncResult)
      {
        asyncResult.AsyncWaitHandle.Close();
      }

      #endregion
    }

    #endregion
  }
}</returns> 
```` 

©2006 Marc Adler - All Rights Reserved