<!--yml
category: 未分类
date: 2024-05-18 06:26:29
-->

# Sloppy Counters: Analysis of Linux Scalability to Many Cores | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2013/04/23/sloppy-counters-analysis-of-linux-scalability-to-many-cores/#0001-01-01](https://mdavey.wordpress.com/2013/04/23/sloppy-counters-analysis-of-linux-scalability-to-many-cores/#0001-01-01)

## Sloppy Counters: Analysis of Linux Scalability to Many Cores

From page 7 of the [paper](http://pdos.csail.mit.edu/papers/linux:osdi10.pdf):

> Our solution, which we call sloppy counters, builds on the intuition that each core can hold a few spare references to an object, in hopes that it can give ownership of these references to threads running on that core, without having to modify the global reference count. More concretely, a sloppy counter represents one logical counter as a single shared central counter and a set of per-core counts of spare references. When a core increments a sloppy counter by V , it ﬁrst tries to acquire a spare reference by decrementing its per-core counter by V . If the percore counter is greater than or equal to V , meaning there are sufﬁcient local references, the decrement succeeds.  Otherwise the core must acquire the references from the central counter, so it increments the shared counter by V . When a core decrements a sloppy counter by V , it releases these references as local spare references, incrementing its per-core counter by V.

The conclusion states that most kernel performance bottlenecks can be removed by changing the application code (or kernel) – as long as you know what to modify, and you are familiar with standard parallel programming techniques 🙂

~ by mdavey on April 23, 2013.

Posted in [Languages](https://mdavey.wordpress.com/category/languages/)