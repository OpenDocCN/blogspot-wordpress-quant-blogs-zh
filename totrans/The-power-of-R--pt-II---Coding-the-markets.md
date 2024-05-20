<!--yml
category: 未分类
date: 2024-05-12 19:51:19
-->

# The power of R, pt II | Coding the markets

> 来源：[https://etrading.wordpress.com/2006/08/07/the-power-of-r-pt-ii/#0001-01-01](https://etrading.wordpress.com/2006/08/07/the-power-of-r-pt-ii/#0001-01-01)

## The power of R, pt II

### August 7, 2006

I was struggling to parse a big CSV with R this morning, til I discovered [this lecture](http://biostat.mc.vanderbilt.edu/twiki/pub/Main/TheresaScott/RLecture2.pdf). There’s some useful tips in there on the use of read.table(), with good detail on separators and quotes. I’ve got 350806 lines of data, and hunting down the lines causing the “more columns than column names” error was like looking for a needle in a haystack. The lecture shows how to use count.fields() and table() to quickly identify the problem.