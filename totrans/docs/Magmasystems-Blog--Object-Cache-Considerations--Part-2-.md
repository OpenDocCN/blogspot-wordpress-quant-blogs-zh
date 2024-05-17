<!--yml
category: 未分类
date: 2024-05-18 05:15:25
-->

# Magmasystems Blog: Object Cache Considerations (Part 2)

> 来源：[http://magmasystems.blogspot.com/2006/11/object-cache-considerations-part-2.html#0001-01-01](http://magmasystems.blogspot.com/2006/11/object-cache-considerations-part-2.html#0001-01-01)

**Object Versioning** 

You can consider the ‘version’ of an object to be two different things.

In the first case, the ‘version’ of an object could represent the number of times a particular object has been written to. When an object is first created, its version number is set to 1, and then each time a client updates the object, the version number is increased. So, we can have an API call is our object cache that tests to see if we are holding on to the most recent version:

if (!ObjectCache.IsCurrent(object))
object = ObjectCache.Get(object.Key); 

or, if we are using a object that has a proxy to the cache, we can do something like this:

if (!object.IsCurrent())
object.Refresh(); 

In the second (and substantially more complex) case, the ‘version’ can represent the actual layout or shape of an object’s class. Consider a Trade object:

public class Trade : CachedObject
{
public int SecurityId;
public double Price;
} 

This would be version 1.0 of the class.

Let’s say that we have a trading system that has to run 24x7, as is the current rage. Systems that run 24x7 theoretically have no chance to be bounced. Even a system that runs 24x6.5 has a window for maintenance. Our trading system has version 1.0 of the Trade object.

Now let’s say that we have a request to add sales attribution to the trading system, so now we need to add the id of the sales trader that took the trade request.

public class Trade : CachedObject
{
public int SecurityId;
public double Price;
public int BrokerId;
} 

This is now version 1.1 of the class.

Our object cache holds version 1.0 objects, and all of our subscribers also hold version 1.0 objects. But, now let’s say that the system that writes new trades into the object cache now has to write version 1.1 objects. What do we do?

There are several things to consider here. How do we represent the object in the cache? Because we are using name/value pairs, all new objects will just have the BrokerId/

<id>field added. The old 1.0 objects that are in the cache do not have to change.

The object cache might want to broadcast a message to all subscribers, telling them that the version number of the Trade object has changed. Since the subscribers may be systems that must run 24x7, then the systems might not be able to be bounced in order to rebuild their trade caches. The systems must be able to read and write the new version 1.1 objects as well as continue to support the older 1.0 objects. But, we cannot reconfigure the layout of the objects dynamically, can we?

Instead of using C# objects, we might consider using dictionaries of dictionaries to represent an app’s object cache. But this is a different kind of programming model. Instead of coding:

Trade obj = ObjectCache.Get(“102374”);
int broker = obj.BrokerId; 
We might have to do the following (taking advantage of C# 2.0’s nullable types) :

TradeDictionaryObject obj = ObjectCache.Get(“1002374”);
int? broker = obj.GetInt(“BrokerId”); 
What a mess!

What does this tell us? When using an object cache for a 24x7 system, make sure you get your class definition right the first time, and avoid object versioning!

©2006 Marc Adler - All Rights Reserved</id>