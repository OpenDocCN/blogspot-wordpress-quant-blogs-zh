<!--yml
category: 未分类
date: 2024-05-13 00:09:18
-->

# hacking NASDAQ @ 500 FPS: interesting activity

> 来源：[http://hackingnasdaq.blogspot.com/2009/12/interesting-activity.html#0001-01-01](http://hackingnasdaq.blogspot.com/2009/12/interesting-activity.html#0001-01-01)

the last post was randomly selected snippets of the market which was sometimes interesting, sometimes not. Was curious at what is going on at the highest order rate in the day which turns out to be.... just after the first 30secconds of market open. Around 10k (mostly add) orders are put on the books in a very interesting pattern.

[![](img/7be322d8a5db92bd3e647b9775fb6b41.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjNUQb4wnZ78rAeEy0-f9wAhELFbIR-d8lPYGhQcpLPgBkoLSoEpu-8JkVOy9IUtJ83Uu6PmYDcEy6rpFOY2ySJE4P9xzC87CpXKVkoPdwLQZOJ9zf1jj21JvBp8-kNCVXqDAVSxsA09w/s1600-h/msft_stack1ms_marketopen.png)

As you can see theres this cresendo of orders which suddently flatlines. Its quite bizzare the # orders in every 1ms slice never exceeds 100 - double checked the data as its a highly artifical pattern. So whats going on here? my guess, as its almost entirely add orders, is this is an artifiact of the exchanges software. e.g. at exchange open time all particpants send their orders at the same time, which get queued at the exchange, and processed at a rate limited speed of 100 orders / 1ms, or 100k / sec (assumely per symbol). Once everyones initial orders are placed everything settles down and its business as usual. Whats the takeaway? probably if you flood the exchange with > 100 orders / 1ms its going to get severly clogged up, so maybe you can slow down your compeitors orders.

The seccond interesting point is a bit of an anti-climax, portion of the session with the highest number of executed orders, which turns out to be just after the 6H mark.

1 horz = 1ms

Nothing too interesting here. 2 huge spikes, followed by a chunk of activity. Remember, this is # orders executed not share volume executed. So its a lot of activity for 1ms slice maybe some big dumb algo snapping up a chunk of the book? followed by watcher algos thinking something bigger is going to happen. But... just guesses at this point.