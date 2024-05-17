<!--yml
category: 未分类
date: 2024-05-12 19:36:24
-->

# LMAX Disrupter | Coding the markets

> 来源：[https://etrading.wordpress.com/2011/01/21/lmax-disrupter/#0001-01-01](https://etrading.wordpress.com/2011/01/21/lmax-disrupter/#0001-01-01)

## LMAX Disrupter

### January 21, 2011

This [presentation](http://www.infoq.com/presentations/LMAX) from two LMAX guys was recommended to me by a couple of friends. I watched it last night, and was very impressed. The topic is high throughput, low latency server engineering. There’s a lot on what it takes to make Java go really quick, and how to work with the hardware in a sympathetic fashion. They recommend one thread for business logic, and dedicated threads for messaging and persistence. This runs counter to the conventional Java wisdom, which tends to involve pools of worker threads executing the same logic and using locking. It’s an approach I’ve had success with in hybrid C++ Python server processes: put all the biz logic on a single Python thread, and handle pub/sub messaging and persistence on C++ threads.

What I found really new and exciting about the LMAX Disrupter pattern they advocate was the use of ring buffers for lock free cross thread comms. I used queues for thread to thread comms in my C++ Python processes. As the LMAX guys point out, those queues use locking. LMAX Disrupter uses atomic CAS instructions for cross thread comms, so that the comms done with the ring buffer are lock free.

All in all it’s a brilliant and insightful presentation…