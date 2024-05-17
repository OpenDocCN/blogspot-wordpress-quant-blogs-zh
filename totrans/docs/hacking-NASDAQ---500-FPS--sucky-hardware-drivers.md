<!--yml
category: 未分类
date: 2024-05-13 00:08:08
-->

# hacking NASDAQ @ 500 FPS: sucky hardware+drivers

> 来源：[http://hackingnasdaq.blogspot.com/2009/12/all-software-isnt-equal.html#0001-01-01](http://hackingnasdaq.blogspot.com/2009/12/all-software-isnt-equal.html#0001-01-01)

What`s up with the bizzare latency? Turns out its a combination of hardware + driver, most likely a shitty driver. Previous tests used a Send(Intel 823573L) and Recv(Realtek RTL811/6168B) thus the logical question is, what happens if we switch send and receive?

First up is Send(Realtek) (above) which is still a little troubling, as It looks a bit like the Send(Intel) throttle @ 1msg/10us in the previous post. Two double spikes, one where you`d expect, and a second off out in the woods having a tea party or something. As we see this on 2 different machiines, it llooks suspiciously like something in the IP stack or NAPI... somewhere between the NIC and sendto().

Next is receive(intel) and....  

...... tight, real tight. None of this bullshit spread we saw with Recv(Realtek). Very low number and a very tight spread, this is good.

And a nice closeup. As we can see, its peeking around 900ns, 2400 cycles @ 2.66Ghz(recv`s machine clock) which is pretty good considering this is a user program+socket user lib+network stack+driver. This however is just the time between packets, its **NOT the latency  between machines,** its the latency from one message to the next on a single machine - a very different but related number.

Machine to machine latency requires both machines send and receive, so will have to wait until a less sucky network card+driver is put in the other box.