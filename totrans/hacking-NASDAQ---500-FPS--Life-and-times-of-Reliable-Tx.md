<!--yml
category: 未分类
date: 2024-05-13 00:06:45
-->

# hacking NASDAQ @ 500 FPS: Life and times of Reliable Tx

> 来源：[http://hackingnasdaq.blogspot.com/2010/01/life-and-times-of-reliable-tx.html#0001-01-01](http://hackingnasdaq.blogspot.com/2010/01/life-and-times-of-reliable-tx.html#0001-01-01)

For our on-going investigation into the bowels of the networking stack, we looked at the w latency of  the UDP stack, thus the next logical step is TCP. Alot of people turn their nose up at TCP for low latency connections, saying it buffers too much, the latency is too high, your better off using UDP which is great for a certain class of communications, say lossy network game physics. However in finance dropping a few updates is death, and not an option.

Theres  2 general approachs:

1) build a shitty version of TCP ontop of UDP. This is the classic "not invented here" syndrome many developers fall into.

2) use TCP and optimize it for the situation.

In graphics, OpenGL / Direct3D theres a "fast path" for the operations/state/driver that's typically the application bottleneck, which the driver/stack engineers aggressively optimize for. If you change the state such that its no longer on the fast path, it goes though the slower generic code path, produces correct results, but is significantly slower. This approach is to have the best of both worlds, a nice feature rich API but has lightning fast performance for specific use cases.

If we take this philosophy and apply it to the network stack, theres no reason you cant get UDP or better level performance for a specific use case, say short 128B low latency sends but fall back to the more generic/slower code path when it occasionally drops a packet. Resulting in a dam fast, low latency protocol, thats reliable, in-order and most importantly the de-facto standard. And with that...lets put on the rubber gloves and delve into the TCP stack.

First up, lets take a high level view and compare the round trip latency of 128B message of UDP vs TCP. Keep in mind this is all on an un-loaded system, the UDP numbers arent exactly 128B messages but close, so is more a guide than absolute comparison. The trick here, is assuming a 0% packet loss, and an already established TCP connection, then each send() will generate its own TCP segment and thus we can poke data into the payload. Hacky ... yes but easy and does the job for now.

round trip UDP A->B->A

[![](img/0a08e1ff33b4f2e828d0063ad82732f1.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj7o0d1hzX7hglSwggdFH98dcfy-OF2tlyZUdKL2sVjBNoxKky4H6hdstWK95cy2eZy_e0CXQhzeiVG264hKh59pwUeZlmsEaKtAdd8cq0Wnrcyl4RMZ_2AlcuDJN-0O6OjngyNNjsrzA/s1600-h/tcp_round_default.png)

round trip TCP A->B->A

Keep in mind the TCP time scale is x2 the UDP plot and it clocks in around say 35,000ns vs 50,000ns with TCP significantly slower - proving conventional wisdom. Where does the time go? First step is look at the time from application -> NIC on both Tx and Rx sides for Machine A.

UDP sendto() -> Tx descriptor

 [![](img/83f3992d50cce20540bed96a8d68d4d6.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg5hyGFl4s31Tascn7w5QhT1uf6243XLXjVEu1OJgf6nA5fgC5FOOPc-dZxCcdDqOjSPfpDguHAxHKR4uKvIEpHM893-LyvkWyz9OwasjGQgWRUQTq0cVOuBfaYwYKh57e2FpYdcc86kA/s1600-h/tcp_a_user2tx.png)

TCP send() -> Tx descriptor

Above plots are on the Tx side of the equation, which is pretty good, not a huge difference considering the UDP vs TCP delta in round trip. So it must be in the Rx logic where TCP has problems?

UDP Rx Intr -> recvfrom()

 [![](img/18034acf5647030db08492078b38fa06.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiCnqXvQnCvGL_lgYofCl2wCLLPr_ll1ZTaX_KP-CHopdoYOVGeV_9TeWkjUFesS_g_gBH6iBZzTcGF_JZeOb6gXlWx9Otm8X_vaWeWDNMTxppzYSFash2Y27Lj9Bh7cTLD7VzQdgRh0A/s1600-h/tcp_a_rx2user.png)

TCP Rx Intr -> recv()

... and we see the Rx is about x2 slower in TCP than UDP, around 2,500ns vs 1,200ns. Not sure whats going on there, obviously related to ACKing each TCP segment its received, but x2 slower ? we can do better for this use case.

Comparing the round trip latency, we are missing about 15,000ns. Machine A is say, a generous 3,000ns so where did 12,000ns go? Onto Machine B. Remember Machine A NIC is directly wired to the SouthBridge vs Machine B has to go via PCIexpress,  thus the latency differences between the machines.

UDP Machine B Rx Intr -> recvfrom()

Machine B TCP Rx Intr -> recv()

On the Rx side its kind of interesting, having a peek almost exactly on 5,000ns is a bit suspicious, yet its slightly faster than UDP - which is ... a little strange. Then a large chunk, over half the transfers around 8,000ns, so another say 3,000ns or so just for Machine B Rx.

[![](img/a757b2a09c12516e075c667116dc49fd.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjhrJm1iviPf-dk0MoG4qgKSeguLraGWmj24czezMJvvkq2OwFIylChj8m7p_YC2LYbD2nD50gDWjEMDueY7Sep5Yx9KpJl4maCOX7p6y12tsDlipS_sSPkWJpDXnT5b0j2mVLB-x1lWw/s1600-h/bapp2tx_latency_stock.png)

Machine B UDP sendto() -> Tx descriptor

Machine B send() -> Tx Descriptor

As with Machine A, the Tx side is fairly consistent with UDP, even to the point of peeks roughly of the same pitch, if slightly translated. Its interesting TCP is somehow slightly faster to hit the NIC -likely differences in datasize.

So we have accounted for a bit over half of the time delta between TCP vs UDP, but where did the rest of the time go? hardware ? seems unlikely. More likely is the UDP vs TCP test data is different enough? Or maybe after many kernel and driver rebuilds the settings are slightly different?

In anycase its surprusing how close the performance is for small sends. Next task is to look into TCP Rx side and see why its not competitive with UDP.