<!--yml
category: 未分类
date: 2024-05-13 00:04:21
-->

# hacking NASDAQ @ 500 FPS: stuffing the turkey

> 来源：[http://hackingnasdaq.blogspot.com/2011/09/stuffing-turkey.html#0001-01-01](http://hackingnasdaq.blogspot.com/2011/09/stuffing-turkey.html#0001-01-01)

Been a bit crazy busy of late so not so many posts, but keeping in the spirit of things here is an interesting POV on quote stuffing and some of the basic microstructure games that get played.

Assume the following plots

Best Ask (Above)

Best Bid (Above)

Open Qty @ Best Bid (above)

As you can see(hilighted in red) what looks like a neat pristinely manicured bit of astroturf among the wild grass, weeds and occasional dead spot. What someone is doing is adding to the BB qty, then immediately canceling it all in rapid fire.

Above is the time delta between changes, where its toggling it every say 100usec. Clearly some algo messing with the BBO. Now what happens if you use a ~~dumb ass~~  simple moving average of say the last 1024 open qty levels of the BB - plot below.

Above between the yellow lines is the average open qty @ BB when on the astroturf.. and that is how you can exploit ~~stupidity~~weakness in someones algo. Here it is again with a more aggressive vertical scaling

Again, a beautiful manipulation of a simple moving average. So whats worse? Spaming the market with a bit of noise OR using a simple moving average as a signal? Personally Id say the latter as we`re no longer in the school yard where there`s no "special needs play area"... However the former is far easier to bitch and complain about.