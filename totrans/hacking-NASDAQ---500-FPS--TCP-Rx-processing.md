<!--yml
category: 未分类
date: 2024-05-13 00:06:22
-->

# hacking NASDAQ @ 500 FPS: TCP Rx processing

> 来源：[http://hackingnasdaq.blogspot.com/2010/01/tcp-rx-processing.html#0001-01-01](http://hackingnasdaq.blogspot.com/2010/01/tcp-rx-processing.html#0001-01-01)

Previous post looked at things in a more macro level so lets dig a bit deeper into the stack to find out whats going on. We break the plots up in driver / ip / tcp / user and we get the following

TCP 128B round trip total

[![](img/14cddf19c611dcec4447d7ba3013084a.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhZ37UGr46X26bvickQPyTTT1JFSXTm_2P3wuolxhwOp8evfZykRZigl8IpBOeKrdrWH26sVV_4vpw9U32WPgUmzk7RvcvWE1El-nWBvhe6K2jGY4hzSIaI13OsHT2lgPLvR_05hBheYQ/s1600-h/tcp_Rx.png)

NIC Driver time

IP processing time

[![](img/9c70a25d0749fbfcb241d59366c1f49f.png)](http://3.bp.blogspot.com/_wI0x7e0fUck/S1hzAPxgaMI/AAAAAAAAASk/nXr8cDOS-5s/s1600-h/tcp_TCP_Total.png)

TCP processing time

Kernel -> User switch

Which is the expected result, TCP processing time becomes the bottleneck, but what is it actually doing? Digging down a bit further we get:

[![](img/071c4d0d6cf25034eb6e47fb0f078fd9.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgcUoWR-k5TM0Psdbo3Xa_W7A3fvcSe0DXeCiVu5KpcwSJg2tC81r832AkIwywKIh891li0JeNpp1Z4N2QWnXLm5WXvy2YyldEv2ibJDvL_mKe8XcbipWZWhZBTYH3meOuyIfTD0iuNvQ/s1600-h/tcp_TCP_Top.png)

TCP top level processing + prequeue

[![](img/c6c57481e1d5052172956f4f1882dd5a.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEje8TlXa2BBOpLZTkm-9Ut4FRSzdbZR1IJwjo6vCurdqubXfOFFpfWfc53Ec54ptedH4iP0Xh0gxc5AaYc9XPRxGNsFXiMBRSkdwrUFDLGhXZWitzdu8Cxa8HvZ4yx7XRihv5zVj1S9OQ/s1600-h/tcp_TCP_Recv.png)

TCP tcp_rcv_established()

Which is rather surprising, it appears the top level processing in tcp_v4_rcv() is where the bulk of the time goes! Not what you expect when tcp_rcv_established() is the main work horse. However.. its gets stranger.

TCP  before prequeue -> tcp_rcv_establish()

Turns out most of the time goes somewhere between pushing the packet onto the tcp prequeue and actually processing it in tcp_rcv_established(). Not sure whats going on there, but surprisingly its where all the action is.