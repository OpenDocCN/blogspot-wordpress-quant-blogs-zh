<!--yml
category: 未分类
date: 2024-05-13 00:01:50
-->

# hacking NASDAQ @ 500 FPS: fpga paper

> 来源：[http://hackingnasdaq.blogspot.com/2012/10/fpga-paper.html#0001-01-01](http://hackingnasdaq.blogspot.com/2012/10/fpga-paper.html#0001-01-01)

Ran into this advertisement^H^H^H^H^H peer reviewed IEEE paper today

Its quite well written and covers alot of ground yet contains some pretty bad assumptions. Lets deconstruct

In the abstract:

"The application sustains 10Gb/s Ethernet line rate with a fixed end-toend latency of 1µs  – up to two orders of magnitude lower than comparable software implementations."

What they are saying is software latency for a brain dead strategy is 100usec? This is complete and utter bullshit, yes if you write shitty code your wire-wire latency will be 100usec +/- 25usec jitter. If you write tight code using standard hardware and know what your doing... can get under 10usec wire-to-wire no problem.

Next point:

"An initial line handling stage uses redundancy in the streams to replace any information temporarily missed due to packet losses in order to reconstruct the necessary parts of the  order book of the exchange."

This is pure magic, have nfi what their talking about here. How is it possible when you drop a market data packet you can reconstruct its symbol/price/side/qty/operation, in less than 1usec, in RTL on an fpga. Will concede given say 100msec or more AND significant delay in the stream e.g. you dropped a new quote X, but received the cancel quote X msg, its possible to take a good guess what was in the packet.... maybe they are talking about using the *cough cough* market data recovery channels.

Next point:

"Prices for all 8000 securities traded on U.S. Exchanges fit within the FPGA’s on-chip memory. The table size is scalable to support more symbols as required."

This is great but wtf? Guessing they are talking about a 8000 * 4bytes(32bit fixed point price only) * 2 (bid/ask) * number of venues to store the best bid/offer for a symbol. That easily fits in the block ram of a Xilinx V5 240T (note: block ram is memory on the die of the fpga and not to be confused with external memory e.g. DDR/QDR/SRAM)

Great but... how do they calculate what the BBO is? You need to store the entire book, which has to be stored in external memory because the working set is atleast 1GB. 

Why store the entire book? 

1) When you get an quote cancel message exchanges rarely have the price/qty/side/symbol in the cancel message. Typically its just the order id and/or quantity canceled, so you need to keep price/qty/side/symbol/orderid and more around to correctly process e.g. what qty is currently open for this order after Y quote cancel messages.

2) when a quote is deleted you need to remove it from the book, then iterate through the book to find the best price - read you need to keep the book in memory somewhere. The trick here is being smart in how and when you iterate to find the best price, e.g. sorting a mostly sorted list can be pretty dam fast.

3) .... and more but wasted too much time on this today.

... so are saying, we can store 8000 bid/ask prices ondie in the fpga for the rtl coded algo to use? hmm..

Its a great well written technical paper, probably one of the best papers on the subject however glosses over some more important details... as doe all academic papers on the subject.. aka yes just sit and hold that 30% draw down for 3 months and the pnl is beautiful.

/rant