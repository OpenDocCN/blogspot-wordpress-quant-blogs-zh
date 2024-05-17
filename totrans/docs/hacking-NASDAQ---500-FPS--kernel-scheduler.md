<!--yml
category: 未分类
date: 2024-05-13 00:06:59
-->

# hacking NASDAQ @ 500 FPS: kernel scheduler

> 来源：[http://hackingnasdaq.blogspot.com/2010/01/kernel-scheduler.html#0001-01-01](http://hackingnasdaq.blogspot.com/2010/01/kernel-scheduler.html#0001-01-01)

The double peek in the Rx -> recvfrom() specifically the kernel -> userland switch looked suspiciously like some sort of core/hardware interaction. So, what happens if we change the # cores. Its really simple to do, just add maxcpus=0 to the kernel boot command. And thus the following plots are generated

 [![](img/b759052c957861576d07e54f7a8a86e1.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj_y8QiV_4GJCXfUQpXuiw1Rexij9F-eXyHKFAx0YYe4wFBZE61zqGJoG0O-mVG_-gCyWNkX_O84_YrYidD1JiLTUnto7cSPYRMCDZNVkW4SScSZbeNwv-tPwjFBpojGWjbkEL_MWTQVA/s1600-h/cpu2_2_send.png)

2 Core sendto() -> Tx Desc

 [![](img/b48e0c319427e16546d8820bb29caa6b.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjf6c2RM_fMKYNT5DrPZD9d-2aQlnfZfWSLTBGUY-xgww6XTYoCA-XboC_9LKBlyZmzH9a6cT2c4eD9VYFlAMdDZEpT6P2Uoj3v7ClochHRb-NaluKys5vFKOj9d0WNPrdEAPjvJphvbQ/s1600-h/cpu1_2_send.png)

1 Core sendto() -> Tx Desc

Which is kind of interesting, not sure how/why the 1 Core sendto() has quite a few sample points < 1,000ns where the 2 Core version has none, other than that nothing too exciting.

 [![](img/7ee75350d0bbdfaca5bf82ad464ac66c.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg9aTngKHtLqtcMoY0LLR9AT2yDX3uwQe9H4-fcSG4HHJwpyzfCGGpd_JDEeG5Xg6dh2zHOmtwzJKeh6KkafPDWgoWQmjHYqITMMTIXrY8eGruJ0nTDLlGKY_gcTi9i2DC5r_uWrkdIFQ/s1600-h/cpu2_3_recv.png)

2 Core Rx Intr -> recvfrom()

 [![](img/fb9492270db332d7003a46c949c13364.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgY0LzPCCxW11uHj5RtgFYGzTNBTdM6QWbm7BfABAYpW4zqisagIhqtkOzzH-No6rxamCwhTuVNkIbof__62j_ZFS_YVBnJz9wldlts1_7YgCuOgLPMsmfUZQ1BVmD2_i1MUSbaEhWAlA/s1600-h/cpu1_2_recv.png)

1 Core Rx Intr -> recvfrom()

OTOH receive shows quite a substantial change and as we suspected, it goes from a double peek, to a single peek assumed to be kernel -> userland signaling behaviour.  And ...

[![](img/f5a80f812dbfc93ce916bcb9e14ccd6d.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEinoDiuMGFZP8tD7ai03fmrUkc9ej4eDYrHa7kuB9PiTSjZ9h1pGZp-8PcwO4at2G8JoLXMSkp9p240Vw7lXmkL0UrbZnrpzcPAf-a9X2pQrcB4Y6V3Ha80tONlLS7qiNCHq4itFMr3dA/s1600-h/recv_2core.png)

2 Core udp finish kernel space -> userspace recvfrom()

 [![](img/62a1ad5a1fe97f7082b5c30b2923f79d.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiZTx-0auRPLn1p1P_kJAnlhpNZrvSlqUmzvPgaQVRU7XKztMdGI2staWqSXxEOCnJ90ntH5IuuYJps7N8_CqBFRXXrRUfnVefWhZRaiJg7CMhCmGKuOND5qSuG4-VImAWYFlw6UfxoHw/s1600-h/recv_1core.png)

1 Core udp finish kernel space -> userspace recvfrom()

... the plots speak for them self. Strangely, adding cores in some cases increases latency (the 2nd peek),. No idea whats going on, but keep in mind this is a blocking recvfrom() call so its obviously related to how linux scheduler deals with signals.