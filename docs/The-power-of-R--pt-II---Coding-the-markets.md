<!--yml

类别：未分类

日期：2024-05-12 19:51:19

-->

# R 语言的力量，第二部分 | 编码市场

> 来源：[`etrading.wordpress.com/2006/08/07/the-power-of-r-pt-ii/#0001-01-01`](https://etrading.wordpress.com/2006/08/07/the-power-of-r-pt-ii/#0001-01-01)

## R 语言的力量，第二部分

### 2006 年 8 月 7 日

今天早上我一直在用 R 语言解析一个很大的 CSV 文件，直到我发现了[这个讲座](http://biostat.mc.vanderbilt.edu/twiki/pub/Main/TheresaScott/RLecture2.pdf)。里面有一些关于使用 read.table()的有用技巧，对于分隔符和引号有详细的说明。我手头有 350806 行数据，寻找导致“列名比列多”错误的那些行就像在干草堆里找针一样困难。讲座展示了如何使用 count.fields()和 table()快速识别问题。
