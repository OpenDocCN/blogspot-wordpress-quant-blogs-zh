<!--yml

category: 未分类

date: 2024-05-12 19:38:45

-->

# Visual Studio 2005 属性加粗 | Coding the markets

> 来源：[`etrading.wordpress.com/2009/10/05/visual-studio-2005-property-bolding/#0001-01-01`](https://etrading.wordpress.com/2009/10/05/visual-studio-2005-property-bolding/#0001-01-01)

## Visual Studio 2005 属性加粗

### October 5, 2009

VS 开发小知识：如果你的 C++ 项目属性页中的条目显示为加粗，这意味着它们在 .vcproj XML 中被赋予了显式覆盖。这今天破坏了我的构建，因为覆盖阻止了从 .rules 和 .vsprops 文件中继承的值被引入。
