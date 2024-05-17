<!--yml
category: 未分类
date: 2024-05-13 00:04:46
-->

# hacking NASDAQ @ 500 FPS: the opening spam

> 来源：[http://hackingnasdaq.blogspot.com/2011/08/opening-spam.html#0001-01-01](http://hackingnasdaq.blogspot.com/2011/08/opening-spam.html#0001-01-01)

Been poking around looking at how the market moves and thought would share a "how to spam the open" session.

First the plots, where everything is in "tick time" e.g one X unit is 1 tick. .. we have the best bid

.. and best ask

Next up is how far away from the best bid the tick is (zero if tick is a sell)

.. and the other side

finally the time delta between ticks (in nanosecconds)

As you can see the closer it gets to the opening bell the harder it bursts, and the further away from the best bid/ask it bursts. But... is it adding or removing shares at that price level?

Above is the share delta for ticks on the buy side, where positive is adding shares to the book at that price level - clearly its adding.

... and the same for the sell side, also clearly adding (positive share delta).

So whats it doing? clearly its layering orders vertically across the entire book, presumably at prices that would be very attractive should they get matched - e.g. highly passive strategy. But... why so close to the opening bell? Guessing theres also a spamming component to this. Where if theres 50K ticks in the queue to process, all at different price levels your orderbook has no choice but to update everything and thus, quite possibly, delay your snapshot of the world by 100`s of ticks after the first execution. 

Fantasy? not sure but there`s a very clear and distinct pattern/strategy going on here.