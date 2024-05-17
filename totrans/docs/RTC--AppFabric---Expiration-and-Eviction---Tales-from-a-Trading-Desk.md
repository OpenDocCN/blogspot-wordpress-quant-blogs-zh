<!--yml
category: 未分类
date: 2024-05-18 06:13:15
-->

# RTC: AppFabric – Expiration and Eviction | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2010/04/16/rtc-appfabric-expiration-and-eviction/#0001-01-01](https://mdavey.wordpress.com/2010/04/16/rtc-appfabric-expiration-and-eviction/#0001-01-01)

## RTC: AppFabric – Expiration and Eviction

Progress on the Real-Time Cube (RTC) leveraging [Windows AppFabric Caching](http://msdn.microsoft.com/en-us/windowsserver/ee695849.aspx) is going well. I should have more to say on this in the next few days. If you are using AppFabric, it’s worth [reading](http://msdn.microsoft.com/en-us/library/ee790981.aspx) the “Expiration and Eviction” documentation, otherwise you may find your objects disappearing 🙂 Here are the [defaults](http://msdn.microsoft.com/en-us/library/ee790935(v=MSDN.10).aspx) I have for the RTC:

> PS C:\Windows\system32> Get-CacheConfig
> 
> cmdlet Get-CacheConfig at command pipeline position 1
> Supply values for the following parameters:
> CacheName: default
> 
> CacheName : default
> TimeToLive : 10 mins
> CacheType : Partitioned
> Secondaries : 0
> IsExpirable : True
> EvictionType : LRU
> NotificationsEnabled : True

You can easily spot the obvious issues with the above 🙂 – TTL will cause problems

Finally, anyone got an idea of when AppFabric will RC? Beta 2 has been out for some time now.

~ by mdavey on April 16, 2010.

Posted in [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)
Tags: [Microsoft](https://mdavey.wordpress.com/tag/microsoft/), [RealTimeOLAP](https://mdavey.wordpress.com/tag/realtimeolap/)