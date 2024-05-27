<!--yml

category: 未分类

date: 2024-05-12 19:42:57

-->

# std::replace_if & boost::bind | Coding the markets

> 来源：[`etrading.wordpress.com/2008/05/07/stdreplace_if-boostbind/#0001-01-01`](https://etrading.wordpress.com/2008/05/07/stdreplace_if-boostbind/#0001-01-01)

## std::replace_if & boost::bind

### May 7, 2008

我想使用`[std::replace_if](http://www.sgi.com/tech/stl/replace_if.html)()`来将字符串中的波浪线符号（~）替换为空格。 [STL 文档](http://www.sgi.com/tech/stl/replace_if.html)提供了一个使用`[std::bind2nd](http://www.sgi.com/tech/stl/binder2nd.html)`的示例。MS 在他们的知识库中有一个[类似的示例](http://msdn.microsoft.com/en-us/library/te5sdkcs(VS.80).aspx)。这是我使用`[boost::bind](http://www.boost.org/doc/libs/1_35_0/libs/bind/bind.html)`来完成工作的方法…

`std::string rep("one~two");

std::replace_if( rep.begin( ), rep.end( ), boost::bind( std::equal_to<char>( ), _1, '~'), ' ');`
