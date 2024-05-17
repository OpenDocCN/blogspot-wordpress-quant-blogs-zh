<!--yml
category: 未分类
date: 2024-05-12 19:35:31
-->

# Lock free: the new C++ frontier | Coding the markets

> 来源：[https://etrading.wordpress.com/2011/02/09/lock-free-the-new-c-frontier/#0001-01-01](https://etrading.wordpress.com/2011/02/09/lock-free-the-new-c-frontier/#0001-01-01)

## Lock free: the new C++ frontier

### February 9, 2011

One of the joys of C++ is the way the state of the art in the language periodically renews itself. I started coding in C++ in 1992 (!?!). I spent a couple of years away in 2001 & 2, and when I came back to C++ in 2003 the generic programming movement led by the likes of Stepanov and Alexandrescu had renewed the language. _1 indeed ! And now it feels like it’s happening again. [LMAX](https://etrading.wordpress.com/2011/01/21/lmax-disrupter/) put me onto the lock free meme a couple of weeks back. There’s a [Herb Sutter article on lock free queues](http://www.drdobbs.com/high-performance-computing/210604448) out there, folks on stackoverflow say [it’s difficult](http://stackoverflow.com/questions/92455/how-can-i-write-a-lock-free-structure), Hack the Market has [blogged about FastFlow](http://www.puppetmastertrading.com/blog/2010/02/16/lock-free/), and there’s a “Boost” [lock free lib](http://tim.klingt.org/git?p=boost_lockfree.git).