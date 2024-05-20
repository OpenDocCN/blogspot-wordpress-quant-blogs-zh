<!--yml
category: 未分类
date: 2024-05-13 00:04:56
-->

# hacking NASDAQ @ 500 FPS: the bb fuzzzzz

> 来源：[http://hackingnasdaq.blogspot.com/2011/08/bb-fuzzzzz.html#0001-01-01](http://hackingnasdaq.blogspot.com/2011/08/bb-fuzzzzz.html#0001-01-01)

Previously, we did a highlevel overview of market data burst rates, which is kinda cool but how does that translate to bids/offers/price/blah? the answer... it depends but does give an general feel for how fast the market moves.

First up an overview of my symbol for the day.. MSFT... so bring it on.

First up best bid over the day (yeah.. dont think its trading at $38.. got some sort of bug there)

Time delta between new best bids

And cumulative time over the trading session, which isnt so intuitive - horizontal axis is change in best bid, vertical axis is time since midnight in nanosecconds

Its kind of interesting as can see the general shape of the level ticks, the constant fuzzz on the best bid. Probably the most interesting thing at this level is the clearly visible steps and curve of the cumulative time. With the pre open step, few steps towards market open, the long flat string of activity at the open then slowing down during the middle, where as you can see the slight curve near the end. What i find interesting is the bursting near the close is quite different than the open - seems theres less changes in the best bid/offer but needs further investigation.

At the micro level it gets far more interesting, as can start to see micro structure algos at play,, how fascinating! Lets zoom in on some fuzzzzzzz

(note, these are all aligned horizontally in time, eg left bars are all the same tick for all 3 plots)

Where its pretty obvious the best bid is oscillating by 1cent

...and the time delta between price level changes.

where can see the fuzz in the middle has new price levels every ~50usec (vertical axis is in nanoseconds), which is pretty dam quick. Remember these are *new* best bid on the horizontal axis and not the raw ticks. e.g. when a new better price level is seen, or an existing price level is destroyed.

.. and to give it a bit more color heres the cumualtive time which puts it more into perspective.

...the fuzzzzz plateu is clearly visible - remember vertical axis is time.

So whats the fuzz doing? either generating noise on the best bid/offer in an attempt to fool other algos theres a new price level? possibly. Or could be the famous iceburg/pegged orders where you only display a fraction of shares, then replenish the bid/offer when someone grabs em. My guess is the latter here, easy test is add executed quantity but..fun for some other  day.

.. and dam need to fix those axis bugz.