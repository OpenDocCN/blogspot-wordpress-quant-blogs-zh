<!--yml

分类：未分类

日期：2024-05-12 19:35:51

-->

# LNK2019 | Coding the markets

> 来源：[`etrading.wordpress.com/2011/01/30/lnk2019/#0001-01-01`](https://etrading.wordpress.com/2011/01/30/lnk2019/#0001-01-01)

## LNK2019

### 2011 年 1 月 30 日

每个 C++开发者时不时都会在构建过程中遇到未解析的符号问题。你可能会盯着代码看好几个小时，确信你的库定义了一个符号。我刚刚解决了一个这样的问题。当我构建 exe 时，一个库中的三个方法显示为未解析。这个[stackoverflow 条目](http://stackoverflow.com/questions/261377/lnk2001-error-when-compiling-apps-referencing-stlport-5-1-4-with-vc-2008)很有帮助，尤其是 Raymond Chen 的博客文章，它让我注意到了 undname 工具。我对 dumpbin 已经了解了好几年，但 undname 对我来说是个新工具。问题最后被发现是因为我的一个库在没有 STLport 头文件的包含路径下构建的。Visual Studio 默默地带上了它自己的 STL。然后链接器抱怨它无法解析返回 std::string 的方法。所有未解析的引用在签名中都有 stlp_。当然，在我用 dumpbin /linkmembers:2 和 undname 与链接器未解析的方法进行比较后，我才看出来这一点。
