<!--yml
category: 未分类
date: 2024-05-13 00:04:52
-->

# hacking NASDAQ @ 500 FPS: bid zappper

> 来源：[http://hackingnasdaq.blogspot.com/2011/08/bid-zappper.html#0001-01-01](http://hackingnasdaq.blogspot.com/2011/08/bid-zappper.html#0001-01-01)

been watching the nasdaq crop circles of the day for a while now

[http://www.nanex.net/FlashCrash/CCircleDay.html](http://www.nanex.net/FlashCrash/CCircleDay.html)

which is pretty cool, but whats more cooler is seeing it in your own app. What the nanex guys call repeaters which just toggle the best bid constantly for a bit is clearly visible in the following plot

This is the qty of shares open on the best bid, where someone is sending new/delete/new/delete repeatedly in a quite a short time span as can see in the next plot that shows the time delta between price level ticks (this ignores any tick not at the best bid)

Where its averaging around 100usec per change, certainly not the fastest you can do that but still thats alot of ticks a sw feedhandler to decode/process/update then analyze etc etc. Whats interesting is it seems to stop after it gets an execution at the offer.

... trying to rattle some change loose? its possible some less sophisticated algo would count the number of ticks or changes in best price/qty as an input signal to the short term direction of the market? as such they burst a bunch of activity that fools the other trade algo the bid/ask will move in an unfavorable direction thus, it grabs some qty at the bid/ask. How plausible is it? not sure but possible i guess.