<!--yml

分类：未分类

日期：2024 年 5 月 12 日 19:35:41

-->

# 在 VC9 中构建 STL port 5.1.3 | 编码市场

> 来源：[`etrading.wordpress.com/2011/02/01/building-stl-port-5-1-3-in-vc9/#0001-01-01`](https://etrading.wordpress.com/2011/02/01/building-stl-port-5-1-3-in-vc9/#0001-01-01)

## 在 VC9 中构建 STL port 5.1.3

### 2011 年 2 月 1 日

使 STLport 5.1.3 与 VC9/Visual Studio 2008 构建有些费劲。我在[这里](http://blog.narahome.com/entry/STLPORT-VS2008)得到了一些提示，但还必须从 Makefile.inc 中删除.rc 依赖项，并调整 LIB 和 INCLUDE 环境变量以从与 Visual Studio 目录分开的 MS SDK 目录中获取头文件和库文件。然后用 nmake /fmsvc.mak dbg-shared 就搞定了。当然，我没有使用调试迭代器进行构建 - 我确实珍视我的理智！
