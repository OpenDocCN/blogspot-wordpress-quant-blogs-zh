<!--yml
category: 未分类
date: 2024-05-13 00:03:38
-->

# hacking NASDAQ @ 500 FPS: Under the hood of a Black Box

> 来源：[http://hackingnasdaq.blogspot.com/2012/04/under-hood-of-black-box.html#0001-01-01](http://hackingnasdaq.blogspot.com/2012/04/under-hood-of-black-box.html#0001-01-01)

Building Mid-freq strategies is alot more involved than HF/UHF strategies, atleast so far. With HF/UHF your looking for a simple pattern with a simple data transform that`s consistent enough you can build a strategy to exploit. With the mid-freq strategies its still a simple pattern the difference is the abstraction level and greeks to the trade are more complicated - at least thats what it seems. e.g no longer looking at the very short term micro inventory/information/latency arbitrage opportunities and instead stationary patterns in highly abstracted and transformed data sets.

My mid freq strategies are not going well, it takes alot of time and I put a hard deadline of end-of-the-month to have something... which gets closer each day. Thus its almost certain will be pulling the machine from colo, to regroup, lick my wounds, get some sleep and then march forward with a modified approach... just cant do this alone starting from 0.

So less ranting about my (lack of) PnL and more on the tech side. Here`s a logical block diagram of my system.

Pretty simple eh?

First up NIC`s

NIC0 -> ssh / management interface

NIC1 -> Order Enter

NIC2 -> not used

NIC3 -> Market Data

Next is HWT`s

Conventional wisdom says you should disable hyper threading as it has significant impact on the performance of the other HWT for the core, which can be true. Hyper threading works by having separate "contexts" e.g. register block & program counter in hardware but sharing the same execution pipeline. Similar in concept to a time sliced operating system where each process/thread has its own copy of all user-land registers which are swapped in at the start of the threads time slice, the thread executes for a set period of time, the registers are copied back into memory, and a new thread is swapped in. This allows multiple programs to share a single CPU and maximize the utilization of the CPU. HW threads work in a similar way but at the ISA (instruction set architecture) level ontop of a processors micro architecture.

The theory for both time sliced OS and hyper threading is, for a significant % of time the execution units are idle as the program is blocked waiting for IO. Thus some other program can utilize the hw resource while waiting for the blocked IO to complete and you get higher execution occupancy & more throughput... but at the cost of increased latency.

OS Example:

while a thread is blocked waiting for Keyboard/Disk/Network input, some other thread runs

HW Example:

a memory read missed L1/L2/L3 and has to be fetched from DDR (100cycles), some other program runs for those cycles.

Have been coding for 8 core asynchronous systems since 2001 so designing for wide processing is quite natural these days - have suffered that transition pain. Thus have plenty of process/threads but not enough cores, so have to eat the latency cost and enable hyperthreading.

Short description of each HWT. All processes/threads are locked to their respective HWT.

HWT0

This is the general purpose, everything runs on this. To linux the system looks like a 1 HWT machine. bash sshd etc etc.

HWT1:

nothing pre-defined. depends what im doing with the machine for what is assigned to this. e.g. live strategies, back testing, backup/crunching.

HWT2:

FIFO scheduled (e.g. not time sliced) for all strategies to run. Processing is setup so 1 cycle of a strategy is run, the round robbin(via linux scheduler) to the next strategy and so. Can be dangerous as the strategies can effect each other but the core strategy logic is usually very simple and light.

HWT3:

For HF/UHF the amount of brute force number crunching is not so high, thus a single HWT is sufficient. The thread has a job queue where anyone can submit something to be crunched.

HWT4:

Market Data Feed handler. You might ask why only 1 HWT for this? The answer is the more queue`s you add the higher the latency. My system only has 1 Queue and thats the Socket`s Rx Buffer which is massive. The 2nd answer is, i`m not keeping a book for all ~6.5K symbols on nasdaq thus dont need the additional throughput. As mentioned way back in 2010, the key here is extremely fast trivial reject`s to filter out all the crap you dont need.

HWT5:

This is the disk io core who`s sole purpose in life is to copy blocks of shared memory to the SSD.

HWT6:

The Gateway + Active Risk checks. This translates internal order requests (new/mod/can/exe) into native protocol versions and performs basic risk check / position management / fat finger checks before sending it into the market. Gateway or OMS as some call it has hooks to external programs which can enable/disable the sending of orders. The risk checks are minimal as its on the critical latency path, thus the more elaborate checks are done passively post trade.

HWT7:

Networking utils / passive risk checking. Part one of this HWT is capture and logs everything on the wire in all directions going everywhere, think NSA style layer2 snooping - yes I see you knocking on the door 192.168.42.1\. The other part is to digest and analyze the captured data pseudo realtime. There are soft latency limits here, ideally all these functions would be running on an independent machine but... didnt want to spend the cash for that.

.. and so the quest continues as digging thru terrabytes of data, racing a 500HP golf cart on the screaming edge of technology down some sketchy back alleyway in Hong Kong... is so my thing :P