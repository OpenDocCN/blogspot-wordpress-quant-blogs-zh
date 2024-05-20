<!--yml
category: 未分类
date: 2024-05-12 19:42:57
-->

# std::replace_if & boost::bind | Coding the markets

> 来源：[https://etrading.wordpress.com/2008/05/07/stdreplace_if-boostbind/#0001-01-01](https://etrading.wordpress.com/2008/05/07/stdreplace_if-boostbind/#0001-01-01)

## std::replace_if & boost::bind

### May 7, 2008

I wanted to use [std::replace_if](http://www.sgi.com/tech/stl/replace_if.html)( ) to substitute spaces for the tilde symbol (~) in a string. The [STL docs](http://www.sgi.com/tech/stl/replace_if.html) give an example that uses [std::bind2nd](http://www.sgi.com/tech/stl/binder2nd.html). MS has a [similar example](http://msdn.microsoft.com/en-us/library/te5sdkcs(VS.80).aspx) in their knowledge base. This is what I came up with to do the job using [boost::bind](http://www.boost.org/doc/libs/1_35_0/libs/bind/bind.html)…

`std::string rep("one~two");
std::replace_if( rep.begin( ), rep.end( ), boost::bind( std::equal_to<char>( ), _1, '~'), ' ');`