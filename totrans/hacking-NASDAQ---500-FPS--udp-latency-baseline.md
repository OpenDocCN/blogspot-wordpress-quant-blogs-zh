<!--yml
category: 未分类
date: 2024-05-13 00:07:49
-->

# hacking NASDAQ @ 500 FPS: udp latency baseline

> 来源：[http://hackingnasdaq.blogspot.com/2010/01/space-time-continum.html#0001-01-01](http://hackingnasdaq.blogspot.com/2010/01/space-time-continum.html#0001-01-01)

Now that the NIC`s are sorted, we can look into the round trip latency numbers. The guesstimate based on the previous post was around 3450ns, or 3.5us which is ... err.. "slightly" off..

First up we`ll go flat out so A sends as many packets to B, and B tries to relay them back to A. When A gets the packet, its got a send time stamp, so we can log the time delta into a histogram(below)

Sending at full rate

Yes, that{s 200

**microsecconds**

at the end, just a bit longer than 3500ns. What a mess.. Simplifying it down to a serial round trip latency histogram, translates to:

1) A Send

2) B recv

3) B Send back to A

4 A Recv

5) A Next message

So the system is on a minimum work loading thus, should get the minimum round trip latency. We get the following graph(below) which is alot cleaner, even if highly disturbing

Serial Round Trip

As you can see, it clocked in around 100,000ns ! that`s 96550ns longer than expected, and with a razor thin spread.

So whats going on? For one a razor thin profile centered almost exactly on 100,000ns is extremely suspicious of a timer at work. With a little bit of digging, lo and behold there is, called Interrupt Coalescing - in the Intel Network card drivers and generally part of the NAPI. Its purpose is to reduce CPU load by batching interrupts into groups, so there's only 1 interrupt per say 32 packets, thus all 32 packets *may* be processed in that single interrupt handler. Which is fine and great, improves network throughput and a good general all-purpose solution but is killing our low latency system.

On page 19 on Intels "Interrupt Moderation Using GbE Controllers" manual there`s a fantastic graph.

If you check the area circled, its the default parameter setting for intel drivers and looks... around 50,000ns which conveniently (round trip) adds up to what were seeing in our histogram 100,000ns. Thus lets mess with the parameter. First up is changing Machine B to InterruptThrottleRate=8000 (intels old default)

Machine B InterruptThrottleRate=8000

And great, our latency number moves (in the wrong direction) but none the less a very direct correlation. Thus lets disable all throttling on Machine B

Machine B Interrupt Throttle Rate = OFF

And bang, we just reduced the latency by half! Not bad for a one liner. The Spikes are still extremely tall and thin, suggesting theres still a timer element in there. Next up, disable throttling for Machine A too.

Machine A & B Interrupt Throttle Rate = OFF

And finally we have somthing that has a fairly small spread, but not so thin that it looks like a timer, and must be close to our baseline round trip number. App -> Lib -> Kernel -> NIC -> Wire -> Switch -> Wire -> NIC -> Kernel -> Lib -> Bapp and back.

Machine A & B, Interrupt Throttling Rate = OFF

And a close up of what kind of latency we`re getting, calling it at 40,000ns round trip which ... is alot. Yet from the previous experiments 3500ns of that is in the throughput, so where did the rest go?