<!--yml
category: 未分类
date: 2024-05-13 00:04:26
-->

# hacking NASDAQ @ 500 FPS: "The Wall"

> 来源：[http://hackingnasdaq.blogspot.com/2011/08/wall.html#0001-01-01](http://hackingnasdaq.blogspot.com/2011/08/wall.html#0001-01-01)

Found a just classic example of the problem currently fighting with, an uptick which all signals says GO but has the crap beaten out of it by some freight train.

Below is the best bid

Red circle is where the strategy correctly predicts an uptick, but as you can see it promptly gets hammered down. So lets look at the qty open at the best bid, first thing you notice is this massive bid qty spike, kind of like a train heading towards a brick wall. 

Above is the open qty at the best bid, where its clearly visible at the previous valley(hmm whats the lingo for this?) someone adds another 10K shares at that price level adding a nice amount of support. Then as expected market uses that support level pushing the price up again.

Above is open bid at levels 1, 2, 3 away from the best bid. As the best bid price moves up can clearly see "The Wall" moving away then returning until it becomes the best bid again.

At this point would expect the price to bounce back up as there`s support, but what actually happens is this.

Above plots are 4 signals, best bid price(one close + really closeup) with red circle where expect the price to bounce back up. 2nd is the open quantity at the best bid, and 3rd is the cumulative execution qty at that price level.

This is whats frustrating, whats happening is "The Wall" returns (in red), price jumps 1 tick then.. someone decides to hit the entire best bid, knocking the price down again, then continues to eat chunks of 10K shares at that price level (red, blue purple) - the price I thought no one was interested in... Probably the most interesting thing is not that someone hit the bid, but whoever is buying continues to replenish with 10k shares! And thus the reason half my orders just beat the spread, with gross PnL 0/net PnL neagtive hmm...

If you read all the trading books and what not, the less technical ones really push "whos on the other side of your trade" e.g. who are you trading against and whats their psychology/motives/brand of coffee/star sign/phase of the moon or whatever. So with that said, probably the most important question here is, is it man or machine? e.g. is this some crazy ass trader thumping 10k shares buy/sell button on a workstation? or is this algos at play.

Above is the delta time between quotes for the above sequence, where vertical axis is time in nanosecconds. As you can see theres this huge chunk of black in the middle with some fairly high peeks, one  goes all the way to around 500msec. But this whole sequence is on the order of 1seccond or so. I guess its possible the seller is human but would have to be really quick to pull this off, i mean *really* fast, which is possible but I think unlikely seller is clicking some GUI button here. The buyer on the otherhand is clearly an algo.

Above is zommed in time delta between quotes/trades in the same time series as the above, 100K on vertical is 100usec. Where we can see the bid qty for "The Wall Part2 & Part3" happens within in a few MSec of the executed order... which has to be a machine. 

... hmm so how to model this...