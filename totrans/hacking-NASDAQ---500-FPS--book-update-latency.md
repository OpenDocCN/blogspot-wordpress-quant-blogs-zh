<!--yml
category: 未分类
date: 2024-05-13 00:08:34
-->

# hacking NASDAQ @ 500 FPS: book update latency

> 来源：[http://hackingnasdaq.blogspot.com/2009/12/rejection.html#0001-01-01](http://hackingnasdaq.blogspot.com/2009/12/rejection.html#0001-01-01)

The code for updating the book is quite simple, the interesting question is how fast can this be done as it adds latency to the trading algo, and this space is all about latency. My initial thoughts is you want to update the book for every symbol for every order operation on a single machine, thus need a throughput of around 100k msg / second which translates to around 10,000ns or 41000 cycles @4.1ghz per message... which it a huge chunk of time and no problem to process. What makes it interesting is optimizing for latency.

[![](img/1d2d5f9a0497c3977755c1c9adb28740.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiRug6conN-A3nYyVXAKoOizf3idGKJ79zx_BL3iGT7uYioUzBO03W1QK0kYGSjcEga9MdC6AMoakhDDlo6ZZ1KNXVACRSAJH8OX-HovgGfjW7g1yg2_K07g_yZcduHXSVeJ5OoO59LIg/s1600-h/highlevel_latency.jpg)

Why is latency so important? because the response time from when the exchange sends out the order operation, to the time the exchange receives your order request is what matters. So from the exchange, over ethernet to your servers NIC, through the linux network stack, into your black box trading algos, then back through the linux networking stack, to the ethernet card, over the wire and back to the exchange. Building the book is part of the "black box" thus the time it takes to update the book is important. How important? not so sure at this point but if your dumb arse code is taking 10,000 nanosec to just update the book, your going to get your ass kicked in the market.

How to minimize the book update latency? pretty simple really - keep 1 symbols`s book per cpu, or just a few books per cpu if your say, pair trading. And duplicate machines for however many symbols your trading on. Why does it help? because on say an intel i7 processor, you hve 32KB x2 (instruction/data) L1 cache, 256KB L2 per core, and a shared 8MB L3\. When execution latency is paramount, the L1 cache is god, L2 cache is close to god, L3 cache is your preist and DDR is death. Translation - because the memory access patterns are fairly random keep the working data set as small as possible, thus only process a few symbols on a single core/cpu socket so all the data stays on chip, in the cache.

What are the numbers? an L1 miss is reportedly 10cycles(2.44ns @ 4.1Ghz), L2 miss is 30-40 cycles(9.76ns @ 4.1Ghz) and if you miss the L3 and go to DDR your in the 100`s of cycles say 400 cycles(97.6ns @ 4.1Ghz). However the intel engineers have been hard at work making shitty code run fast on their hardware, so its more complicated as data can be pre-fetched, hardware can schedule hit under miss, there`s TLB miss costs or god forbid... hitting the virtual page file. Moral of the story is to keep the memory footprint as small as possible, and access order as predictable as possible - this is x86 optimization 101.

So thats err... cool but how is it relevant? Simple. If your code is busy spending 1000ns processing the book for symbol X, and your trading on symbol Y, then you`ve just pissed away 1000ns of latency while symbol Y`s message is sitting in a buffer waiting to be processed! By that time your competitors already have an order on the wire en-route to the exchange and you - FAIL. Thus the problem can be re-stated as "*the fastest way to reject messages*" and only process what your interested in.

My first thought was, great just do a 64b compare on the stock symbol for all messages and we`re done, cool.. too easy. However its not that simple as everything revolves around a unique OrderID, meaning you only have the symbol on the order add message, and all other order types you need to work backwards from the orderid to decide if its a relevant message - a nice fun problem.