<!--yml
category: 未分类
date: 2024-05-12 19:35:36
-->

# Limit Order Book implementation | Coding the markets

> 来源：[https://etrading.wordpress.com/2011/02/02/limit-order-book-implementation/#0001-01-01](https://etrading.wordpress.com/2011/02/02/limit-order-book-implementation/#0001-01-01)

## Limit Order Book implementation

### February 2, 2011

[Fascinating blog](http://howtohft.blogspot.com/2011/02/how-to-build-fast-limit-order-book.html) on HFT implementation from WK. He commnts “a variation on this structure is to store the Limits in a sparse array instead of a tree. ”  More detail on the implications for L1 and L2 cache behaviour of trees versus arrays for limits would be welcome. I’m assuming C++ implementation here of course, though WK points out you can make Java go fast if you avoid GC, which chimes with the experience of the LMAX guys. I ask because I interviewed with a big HFT firm last year: they gave me a programming exercise based on L1/2 cache behaviour.