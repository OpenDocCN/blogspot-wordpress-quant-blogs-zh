<!--yml
category: 未分类
date: 2024-05-13 00:01:43
-->

# hacking NASDAQ @ 500 FPS: Top 5 reasons my (your) backtest is bullshit

> 来源：[http://hackingnasdaq.blogspot.com/2012/12/top-5-reasons-my-your-backtest-is.html#0001-01-01](http://hackingnasdaq.blogspot.com/2012/12/top-5-reasons-my-your-backtest-is.html#0001-01-01)

Alot of the time when building/backtesting strategies you get a result thats just too-good-to-be-true. When this shows up the best way test your brand spanking new million *cough* dollar *cough* strategy a day is to

1) flip the sides/signals - if possible e..g not capturing bid/ask spread..

2) random() is your friend, replace random() with your secret sauce signal gen and see how it goes.

My preference is to use a random() strategy or an "always trade" strategy as its less intrusive. If it generates million dollar backtested profits... you know its complete and utter bullshit. 

So in dave letternman top 10 style..

## **top 5 reasons my (your) backtested results are bullshit**

number 5...  your cost structures are wrong

Part of the shock and horror of HF trading is the realization your being screwed on all angles in all holes by everyone. When ppl think about trading its all about the (sell price - buy price) == money in your bank account. Sadly because the gross margins are so low & with so many fees and taxs along the way, money in the bank isnt always that good..

Be sure to include

1) exchange fees / rebates

2) SEC fees/taxs

2) brokers fees

3) your (not) friendly capitial gains tax man

4) [optional] exchange rates

Got totally screwed by 4) this year - Japanese Yen / USD really hurt

number 4 ....   You have built a time machine, cool can I buy one?

Need to seriously change my trade idea scratchpad / research framework soon to completely eliminate this. For now using essentially arrays of data, with each index being a time/event sample. Problem is its all too easy to do a if (Price[t] > Price[t+1] ) kind of compare which, takes a peek into the future and can heavily bias your results. The more painful and subtle variation is using multiple datasets/signals that are not perfectly synchronized e.g. A signal is one time/event ahead of the others.

The only way around this is to make this impossible, say strategy has no access to the array/precalced data or be very very careful. My approach for the moment is the latter. When I started would make this mistake more often than I want to admit but rarely screw it up these days - too many hours lost chasing wtf is this random() strategy profitable

number 3.... EventSeries != TimeSeries

Most exchanges will pack multiple market data events into a single UDP packet making the market data event stream appear as a time series, when it is not. Simple passive example strategy would be, if BBO price level has less than X orders/qty then replace away/deeper into the book. If you equate the event stream for a time series then the backtest will always avoid deep, aggressive trades. Why? because when each order gets wacked by some massive aggressive trade, each and every passive order that gets filled, an individual market data update is generated.

Now. if you treat each of market data update as a discrete event, your strat/backtest can see each update individually until it reaches the minimum X level and you replace away. aka a perfect 0 latency system.

Whats wrong? In real-time all the orders get wacked at the same time including yours! with a group of market data events actually being an atomic operation.

number 2.... resetting position at start-of-day

when doing multi-day backtesting its easy to forget the strategy is still open at the end of the day. e.g. strategy exit condition has not triggered as its usually in a loss state. Simplest example of this is, for every 1minute buy SPY aggressively then recycle it passively at +X ticks and start the day with no position. What happens is you have 100% winning trades! Why? because when the market moves against you the strategy just sits there drifting away from the bbo. (in a 10ft pool of red) waiting for that passive exit. Then when the market closes, your backtest resets the strat for the next day that loss is simply ignored, disappeared and never existed. If there were a wizard of oz, would certainly ask for such a button.

Always update the position/pnl after every trade - not just at the exit, and never reset between days.

number 1.... aggressively buying at the bid and aggressively selling at the ask.

Its so easy.. just aggressively buy at the bid, and aggressively sell at the ask for every tick, on every instrument for every exchange in the world and you, yourself, can bail Greece, Spain and probably half of the world no worries.

the problem is, in real life your aggressively buying at the *ask* aka paying the spread to fill now. I still screw this up all the time when testing out an idea. Usually by fiddling with different styles to enter/exit a trade then forgetting to revert the code back and preso.... $1M / day in pnl.

--------

 By now your either shaking your head saying how badly I suck, or quietly nodding about those indiscretions you never told anyone, or laughing your ass off saying yeah been there done that, will never do again.

oh the shame... lol