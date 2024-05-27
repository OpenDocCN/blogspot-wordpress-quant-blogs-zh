<!--yml

分类：未分类

日期：2024-05-12 19:49:13

-->

# MFC & Win32 GUI 重写？| Coding the markets

> 来源：[`etrading.wordpress.com/2006/10/07/mfc-win32-gui-rewrite/#0001-01-01`](https://etrading.wordpress.com/2006/10/07/mfc-win32-gui-rewrite/#0001-01-01)

## MFC & Win32 GUI 重写？

### 2006 年 10 月 7 日

[Marc 询问](http://magmasystems.blogspot.com/2006/10/what-are-you-doing-with-your-mfc-apps.html)银行计划如何处理他们的 MFC 应用。我们电子交易系统的代码库是 600KLOC 的 C++，有一些 Java 和 C#。GUI 层主要是 C++ MFC/Win32。一些新东西是 C#。我们没有计划花费一年时间将 C++ MFC 代码重写为 C# Winforms。

让我们假设你在 97 年编写了一个 MFC GUI。如果你买了自那时以来每一波新 GUI 技术的说法，你会重写多少次？一次为了 Java AWT、Java Swing、C# WinForms？现在你会追求 AJAX、Flash 还是 Vista。任何购买 vendor 声称到如此程度以至于要重写生产应用 just to be on whatever platform the vendors are hyping this week 的技术经理都需要检查他们的头脑。或者需要解雇。

也许我太忙于在前台战壕里埋头工作，但我不知道微软是否已经宣布停止对 MFC 的支持。即使他们这样做了，我也要等到微软发布一个基于除 C++ MFC & Win32 之外的东西的 Office 版本后才会担心。正如在电子交易中始终如一，低延迟和高吞吐量是关键。我们的定价清单在许多桌面上运行，并且必须跟上每秒跳动几次的大量债券和掉期——每次都更新价格、收益率、DV01、久期、凸度等。因此，我们将继续使用 C++ MFC Win32 一段时间。我毫不怀疑微软也将会在他们的桌面应用中保持这种方法一段时间。
