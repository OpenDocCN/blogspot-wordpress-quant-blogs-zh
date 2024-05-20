<!--yml
category: 未分类
date: 2024-05-13 00:03:19
-->

# hacking NASDAQ @ 500 FPS: HFT Strategy

> 来源：[http://hackingnasdaq.blogspot.com/2012/04/hft-strategy.html#0001-01-01](http://hackingnasdaq.blogspot.com/2012/04/hft-strategy.html#0001-01-01)

Two posts in one day... yes, have too much free time. Colo box is heading back, lost this round but just one of many to come. Decided to target pure FPGA strategies as it plays to my strengths  - hardcore tech (yes can code verilog) & need team up for that,  but more on that later.

So what does the return on a HFT strategy look like? Somethings like this.

Above is March 2012 worth of accumulated PnL, horizontal axis is # trades, vertical axis is accumulated dollars. In this case it makes about $4K / month on a single symbol on roughly 4M shares / month of volume, which is about $80MM/month of trades. On the day-to-day basis 90% of the time the PnL is flat or positive doing about 100-200 trades per day - keep in mind this is only 1 symbol out of many. Its simulated with full trade & quote data + liquidity rebates, commissions and latency discussed later.

How real is it? Its not live thus 100% BS :) In reality my model of the nasdaq queue is fairly simple and there`s some weirdness in the matching engine I haven`t worked out thus isn`t modeled. The only way to know is trade it for real... which I dont have the infra for.

The theory goes $4K/month for 1 symbol,  find 10 symbols makes it $40K/month, 20 symbols $80K/month etc all is good. Thus go out, signup for an eTrade/IB account and trade your way to $100M return in a year... or NOT.

HFT strategies are either highly sensitive to latency, commissions or both, so lets explore. First up latency.

The above plots show the monthly PnL with a -1.25 commission at various levels of simulated latency. From top to bottom its, 0usec, 100usec, 250usec, 500usec, 1msec, 2msec, 5msec, 10msec, 100msec. Thats a pretty broad spectrum. Whats clear is the variance dramatically changes from a 100usec latency to a 100msec latency aka the return gets very "lumpy" something you really don`t want.

In pure dollar terms, 0usec latency returns $3,942 with 100usec $3,179, 1msec $2,341, 100msec $1,978.

Or put another way, 

100usec  $3942 - $3179 =  $763/mo @ 10 symbols thats  $7,630/mo

+900usec $3942 - $2341 = $1601/mo @ 10 symbols thats $16,010/mo

+90msec  $3942 - $1978 = $1964/mo @ 10 symbols thats $19,640/mo

... 90msec costs $20,000/mo. Which can be interpreted in a variety of ways. e.g. dont trade on 100msec of latency!

If you look closely the number of trades slightly decreases then increases with the higher latency, the reason? Its a passive strategy thus if your too slow when the world moves you get hit by a bus because your sleeping in the middle of the road... instead of running to the other side. Resulting in a alot of unfavorable trades. In tennis I guess this is called "unforced errors".

So even @ 100msec latency its profitable making a hypothetical Tech setup of IB account hooked up to say Amazon EC2 & even if the everything is Java(.. ducks..) we should be well under 100msec tick to trade.. all good.

The other axis is per trade commission's as discussed in a previous post. Whats the PnL look like? ......

... and there`s alot of red ink on the plot. The above plot has commission's from top to bottom of 0, -1, -5, -10, -15, -20 per share. As you can see @ -1 myri / share its a solid green, -5 its a bit shaky yet still firmly in the green.  At -10 myri/share its in trouble and it just goes down hill from there.

So whats a reasonable commission/latency estimate? It depends at what level of the game your playing. For IB something like 100msec & -20myri / share which gives...

... a really red and nasty picture.. it loses about -$10,000/month. Same strategy just different latency & commissions.

Whats do you need and what is realistic ? 100usec & -1.25myri/share if you have $250K - $1MM to invest and doing alot of volume every day... which looks like.

... a nice picture indeed.

As has been said by many people before HFT is half strategies, half technology, you need both or you will lose.