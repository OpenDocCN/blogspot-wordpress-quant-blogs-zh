<!--yml
category: 未分类
date: 2024-05-13 00:03:46
-->

# hacking NASDAQ @ 500 FPS: Work Life Balance

> 来源：[http://hackingnasdaq.blogspot.com/2012/03/work-life-balance.html#0001-01-01](http://hackingnasdaq.blogspot.com/2012/03/work-life-balance.html#0001-01-01)

Another week finished and still unprofitable.. haven`t really traded much last week or two as busy in research/quant mode. My edge gets better by the day, but sadly the comission`s and latency do not. Current problem is I keep building profitable strategies but for some reason always make them passive ... which require extremely good queue positions which means... it wont work with my setup... meaning wasting more time.

To have an excellent queue position on say SPY requires a direct feed from nasdaq, 10Gb, ultra low latency pre trade risk checks and fpga/extremely tight code for market data processing. e.g. the ability to filter out all the crap when your about to get hit by a bus. Unfortunately this is really expensive (for myself atleast) so dont have it and thus have finally made the conscious decision to absolutely under no situation build a passive strategy.

For those who dont know, I`m based out of Tokyo which means really weird and utterly brutal hours. All the movies of dudes sitting on Yachts in the Bahamas spending 10min/day adjusting their positions via laptop over a satilite connection? ... is well ... not my case and certainly not the life of anyone I know who trades.

Imagine this schedule

  Mon:  5:00 - 18:30 :  Mon: 30min - 1H siesta Mon: 19:30 - 00:00 : Market Open 9:30 EST (22:30 Tokyo) Tue:  0:00 -  7:00 : Market close 16:00 EST (5:00 Tokyo) --- sleep --- Tue: 11:00-   0:00 Wed:  0:00 -  7:00 -- sleep --- Wed: 11:00 -  0:00 Thu:  0:00 -  7:00 -- sleep -- Thu: 11:00 -  0:00 Fri:  0:00 -  7:00 -- sleep -- Fri: 11:00 -  0:00 Sun:  0:00 -  7:00  <--- now! -- sleep -- Sun: 13:00 -  0:00 -- sleep -- 

And yes Monday is a 24H work day. All up think its easier to use 24H * 7 - SleepTime... which is

24*7 - (6 * 4 + 1 * 5) = 168 - 19 = 149H week

Obviously this aint sustainable long term and pile onto that 6days/week * 12-16H/day for 6months and you get some sort of idea on how many hours its taken me to get to this point.. and still not profitable (holy fark!) For those lucky enough that are in the right location and can learn from co-workers/existing code bases it makes a *huge* difference... ive wasted so much time on the wrong things, but on the plus side what I do understand is burned into my cortex forever as have paid the price via trial & error.

.....dont try this at home kids :P