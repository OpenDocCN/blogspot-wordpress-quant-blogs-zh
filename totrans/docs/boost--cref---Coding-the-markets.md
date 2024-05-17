<!--yml
category: 未分类
date: 2024-05-12 19:42:47
-->

# boost::cref | Coding the markets

> 来源：[https://etrading.wordpress.com/2008/05/21/boostcref/#0001-01-01](https://etrading.wordpress.com/2008/05/21/boostcref/#0001-01-01)

## boost::cref

### May 21, 2008

I’m continuing to discover the wonder of boost. Yesterday it was [boost::lexical_cast()](http://www.boost.org/doc/libs/1_35_0/libs/conversion/lexical_cast.htm), a very neat way to do those peskly int to string conversions. Today, it’s [boost::cref()](http://www.boost.org/doc/libs/1_35_0/doc/html/ref.html). Why did I need it ?  I’m using [boost::bind()](http://www.boost.org/doc/libs/1_35_0/libs/bind/bind.html) to marshall parameters for dispatch across a thread boundary. All well and good til one of the parameters inherited from boost::noncopyable. Wrap the noncopyable in a [boost::cref()](http://www.boost.org/doc/libs/1_35_0/doc/html/ref.html) invocation, and all is well again.

Apparently, boost::cref converts the reference to a pointer under the covers. Ironic, non ?