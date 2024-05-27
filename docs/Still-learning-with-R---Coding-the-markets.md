<!--yml

分类：未分类

日期：2024-05-12 19:50:07

-->

# 仍在使用 R 学习 | 编码市场

> 来源：[`etrading.wordpress.com/2006/09/20/still-learning-with-r/#0001-01-01`](https://etrading.wordpress.com/2006/09/20/still-learning-with-r/#0001-01-01)

## 仍在使用 R 学习

### 2006 年 9 月 20 日

在我迄今为止的所有 R 编程中，我一直使用 frame$list 语法来引用数据框（译：表格中的列）内的单个列表。这并不非常通用，特别是当我试图编写一个通用的、多维的桶函数时。所以， somewhat belatedly 我发现了 frame[[list]]语法，它允许我参数化我传递给桶代码的列引用。哇！
