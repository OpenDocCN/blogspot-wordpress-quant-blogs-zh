<!--yml

分类：未分类

日期：2024-05-12 19:35:36

-->

# Limit Order Book 实现 | Coding the markets

> 来源：[`etrading.wordpress.com/2011/02/02/limit-order-book-implementation/#0001-01-01`](https://etrading.wordpress.com/2011/02/02/limit-order-book-implementation/#0001-01-01)

## Limit Order Book 实现

### 2011 年 2 月 2 日

[有趣的博客](http://howtohft.blogspot.com/2011/02/how-to-build-fast-limit-order-book.html)来自 WK，关于高频交易实现的细节。他评论说：“这个结构的变种是使用稀疏数组而不是树来存储限价单。”关于树和数组对于限价单 L1 和 L2 缓存行为的影响，有更多细节将会很受欢迎。我当然假设这里是用 C++ 实现的，尽管 WK 指出如果你避免垃圾回收（GC），你也可以让 Java 运行得很快，这与 LMAX 团队的体验相符。我问这个问题是因为我去年面试了一家大型高频交易公司：他们给我一个基于 L1/2 缓存行为的编程练习。
