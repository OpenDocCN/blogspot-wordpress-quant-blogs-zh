<!--yml

分类：未分类

日期：2024 年 05 月 12 日 19:42:47

-->

# boost::cref | 编码市场

> 来源：[`etrading.wordpress.com/2008/05/21/boostcref/#0001-01-01`](https://etrading.wordpress.com/2008/05/21/boostcref/#0001-01-01)

## boost::cref

### 2008 年 5 月 21 日

我正在继续发现 boost 的奇妙之处。昨天是 [boost::lexical_cast()](http://www.boost.org/doc/libs/1_35_0/libs/conversion/lexical_cast.htm)，一个非常巧妙的方式来进行整数到字符串的转换。今天，是 [boost::cref()](http://www.boost.org/doc/libs/1_35_0/doc/html/ref.html)。我为什么需要它呢？我正在使用 [boost::bind()](http://www.boost.org/doc/libs/1_35_0/libs/bind/bind.html) 来为跨线程边界的调度参数进行编组。一切都很顺利，直到有一个参数继承自 boost::noncopyable。将不可复制的对象包装在 [boost::cref()](http://www.boost.org/doc/libs/1_35_0/doc/html/ref.html) 调用中，一切又恢复正常。

显然，boost::cref 在内部将引用转换为指针。讽刺，不是吗？
