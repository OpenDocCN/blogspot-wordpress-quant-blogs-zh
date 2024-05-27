```

分类：未分类

日期：2024-05-12 19:43:17

```

# Python: mutability is the key | Coding the markets

> 来源：[`etrading.wordpress.com/2008/04/28/python-mutability-is-the-key/#0001-01-01`](https://etrading.wordpress.com/2008/04/28/python-mutability-is-the-key/#0001-01-01)

## Python: 可变性是关键

### 2008 年 4 月 28 日

我从 2000 年开始使用 Python 编程，所以今天早上发现自己编程知识中的一个空白让我感到惊讶。阅读[关于集合的文档](http://www.python.org/doc/2.4.1/lib/types-set.html)时，我遇到了这样一段内容：“`set`类型是可变的——内容可以通过`add()`和`remove()`等方法进行更改。由于它是可变的，所以没有哈希值，不能作为字典键或另一个集合的元素使用。”

我从未意识到可变性决定了对象能否作为键。我猜我总是就这样编码，我的键通常都是整数或字符串，或者是它们的元组。
