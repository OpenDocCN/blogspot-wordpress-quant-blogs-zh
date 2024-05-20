<!--yml
category: 未分类
date: 2024-05-13 00:07:29
-->

# hacking NASDAQ @ 500 FPS: The life and Times of a Tx Packet

> 来源：[http://hackingnasdaq.blogspot.com/2010/01/life-and-times-of-tx-packet.html#0001-01-01](http://hackingnasdaq.blogspot.com/2010/01/life-and-times-of-tx-packet.html#0001-01-01)

Finally.. got some time to spend on this. We got a rough high level view last time on where all the time went, so lets dig a bit deeper into the SW stack to find out what is going on. So.... lets get started using a stock kernel 2.6.30.10, build it, install it, run it  and boom the first plot.

[![](img/bf54b7ed757c87a197dd31db2d2b7918.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiPuVzSCZitEgZPy9EOC8AGrnx4nlhaWNAW2QbrAciLkscR49PFg7TQhq8rJ7Qa3Tuq9AN9ojhWy6PElbaphir3nYmk3_Pg4ap8A5KiRNSe-hYUZ-mTGYSyN0vDlQZp1EgfAqZVi_bdDg/s1600-h/send_latency_base.png)

Machine A sendto() -> Tx desc

Which is our toplevel latency reference, of around 1500ns or so from the userlevel function call, to the NIC driver incrementing the Tx Descriptor ring. Not bad, and surprisingly quite a bit faster than our previous tests(2000-3000ns). Why this is, I've no idea, but likely slightly different kernel version and build parameters. Other strange thing is the "shadow graph"**,** possible due to increasing the resolution of our histogram bin size (100ns -> 10ns) **all timing is based on an old 2.6Ghz Xeon**.

Hacking the networking core is a royal pain in the ass, theres no easy module to build, which means rebuilding the kernel and rebooting each time... paaaaaainfully slow dev cycle. But lets start by looking at glibc code, for sendto(), which does basically nothing - invoke a kernel command so first plot is kernel call overhead.

[![](img/14b7254fc3cc9bdbc82336f55a824f22.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgQnWn2Et2rloBvepk8lE3zh_VkdYu-Jsc6ezJivhK2LVosOUhpyWOxqGY61wdDZsy6fjs2Gc88mgfcGK1oFh_-9AGLWRTjr92qxYqAogtSliQm-XC8KjQ2aP9QhtZwrN5FdW3jPWRDvg/s1600-h/send_latency_kernel.png)

userland -> kernel overhead

Looks around 250ns on average. The double peeks are most likely due to the 2 hardware threads on the machine, so around 700cycles. One side note thats not evident in the plot is, the kernel overhead time drops from about 1200cycles at the start to averaging 700cycles quickly ~ 1000 calls.

The packet then arrives at udp_sendmsg() in the ipv4 udp code, where it does some misc packet header/buffer allocation and a few checks, finds the cached route and acquires a lock on the socket. General house keeping stuff.

[![](img/118e823a30cc7effecadbdbaf257598a.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhStcK0WHBz6zDqmCXEnetHhS99_BtJHi9hW9e5rQ6jt4ljqvR7GFZIa7hyphenhyphen6lfAlDgr7vncXLgGRPcuqjzVHBNY_IMpVlafX0DIh8Tm6kb4D6nrYLIV6Fqo4QjbgTykQ99mdSN6buy-cg/s1600-h/send_latency_prep.png)

kernel socket/packet house keeping

Housekeeping clocks in around the same as the kernel switch, 6-700cycles or about 250ns. After the packets has been checked, its copied into the sockets send buffer - this is what ppl generally think of when discussing socket buffers. Where it it memcpys the packet from userland into kernel space and enbales/maps PCI/DMA access from the NIC.

Userspace -> Kernelspace Packet copy

Histogram is a bit prickly for some reason, possibly due to PCI dma map commands, as the amount of data we:re copying is tiny - 128B and it should be in the L1 and definitely in L2 cache so not sure whats going on there. Its possible the combo of old hardware and un-aligned writes means the CPU is read-modify-write the destination mem cache line, instead of a driect write (no read) thus we pay the latency cost of an uncached memory fetch. Or... its just kernel dma/pci mapping code, not sure.

IP/UDP header write

After the payload is copied, the stack adds the appropriate IP/UDP headers(above) Nothing too interesting here, but is surprising how long it takes, ~150ns which.. is alot. Packet checksums are all offloaded onto the hardware, so its doing something else here.

Now it gets interesting, almost all stock kernel builds have netfilter enabled, to allow packet filter / routing  / firewalls / vpns etc etc - very core usecases for linux. Theres a ton of books and documents on how to use netfilter/ipchains but in our case its entirely pass thru, in fact we should disable netfilter to reduce latency.

[![](img/969d12ca655297680d8740f2ba5c680a.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiEuTCMD0KX-14MwVZvmkdCWUieSBDPM-Tqo3SyPJL7aHoxfGArBs2u39GRDK6myDjWJP8ThJJm6jy_Pe1iJMLSJEO_r2PSVX3JB3K5XUokM6PojI6pv3szKxLIlvaSnTRT48MfNOXjdg/s1600-h/send_latency_nf_local.png)

netfilter LOCAL passthru

[![](img/6a53947ebd17dd64b89306edebd5915f.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgEMk-X93c2i01d4F9shAsaj7SwB3deU8OhqVX2r6lD2JBhG7NuYBH8npHvSIV0lLwJcLV1CMvxOpTOBxOemiaNMcmj5t7QHWNTCpzsLLsY6GDaKosWCBXDqG0VCI8d8WkHIyRnzaaG2g/s1600-h/send_latency_nf_post.png)

netfilter POST pass thru

As you can see(above) its still quite fast, 80ns or so all up, but think its safe to assume the exchange isnt trying to h4x0r your machine and its all quite un-necessary.

After netfilter approves the packet, its sent to the NIC driver, using another buffering system, qdisc - queuing disciplines. This is MAC level now, typically a single fast priority FIFO per MAC but its completely configurable using the "tc" traffic control command and probably other tools. Qdisc is a powerful system, enabling various buffering, scheduling and filters to be applied but they all add latency, - not particularity helpful  for low latency systems. In fact I intend to completely disable qdisc to reduce latency.

 qdisc packet enqueue

Queing is fairly fast (above) around 130ns or so, the 2nd hump in the histogram is interesting.Guessing its wait time for a atomic lock. Now that our packet is on the queue for eth0, all that's left is for the net scheduler to issue it to the NIC driver. However, there's a nice optimization that after the packet is queued, it immediately attempts to send the packet to the driver, and in this case  usually succeeds The only reason it can fail to immediately send is, if another hardware thread is running the net scheduler thus pushing data to the driver, e.g. we have a small fifo here to avoid dropping packets, but it does add another source of latency.

[![](img/d967d81247c451b6fd4051677efe3e91.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjv5s23fNho5WhHGVIWeOkxFoRqkFygqeOv67oav_iAlmSVHDbLaumUcQr0tpMA5oofVPYDnvpXj1nY0yIS5v8anY09oKznN2sLTcVb3nsebcerH8Qg1se5hOYFycijxGwRrE1mLRewtw/s1600-h/send_latency_soft.png)

qdisc queue -> driver xmit

As expected (above), the latency from qdisc queue, to issuing a driver call is  small 100ns or so. Whats interesting is the double spikes, assuming it misses the initial scheduling pass, and hits on the 2nd try.

[![](img/620e4d410a05953b7a41eb785b6e9a47.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgnCeUreqhYUu4u2w3eltrdVjR1nW0Sd_Rkil9zJHjg3T14pczX0BU8d-i8k8jAFM1F4S1kbwGS8PlJgRUJ-ptv-4k8yA1ufnlkqneRVHI8vksqYxbY1Adz80gxPtK9N9lK-CmE_Q6jVA/s1600-h/send_latency_driver.png)

 NIC driver 1 Tx packet process time

And finally(above) our trusty e1000e NIC driver processing cost, which fills our the Tx descriptor and moves the ring buffer forward. Then frees the packet and is fairly quick to process 400ns. Note, this is the time from driver entry point, to exit point, which is longer than driver entry -> Tx update(below)/hardware hand off, due to cleanup code.

[![](img/a25e6be8fa324f26d020bbd780b22bb0.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjyZUtnz_nqpmkRLzT_QdO8OKLS6W5Xve75ARnyi-wOAGUOn1GBi9b32DFCWjUsjcICL8Xh28YTrTnrFL2Hw3Vm17yR513LTwuzlfb0GxRUiQjQUQI71jjW2141U1uEMWAjh8Yel1D-vw/s1600-h/send_latency_qdq_tx.png)

qdisc enqueue -> NIC Tx descriptor write

The question is, if the NIC driver is only taking 3-400ns to kick a Tx descriptor, then the rest of the time must be spent in the  linux kernels networking stack?

 sendto() -> the start of NIC driver handoff

Answer -> yes, most of the time is spent in the kernel.. Plot above shows the entire SW latency excluding the NIC driver where the shape matches the first high level plot (green one) except shifted slightly to the left.  This is good as we have quite a few options to reduce the kernels processing time, to make that packet hit the MAC in < 1,000ns!

[![](img/7b644150585cf91c67d1411ab73fe20b.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEinv_rWdWtW4EZDmmtqD_iRZ8IudjSisRWOgi-idK62xQI5erVZNRvRA_n4Mf4x024pcAe4V9SK2kSkLmETuNZIt2XfjGyCbMdWjdoWxwO1a7NBLkHXK7P14bczf32x5v_vEn5FQCqcOg/s1600-h/tx_send_highlevel.png)

typical high level Tx hw/sw flow @ 2.6Ghz old Xeon machine

In summary, the above flow chart shows our current latency estimates. We can only guesstimate the hardware latency due to lack of tools but you can clearly see the HW latency is far greater than the software. As  we are using a typical (old) consumer/server hardware layout thats designed for high throughput NOT ultra low latency. Which is why anyone serious about  ultra low latency... has a very different hardware topology :)