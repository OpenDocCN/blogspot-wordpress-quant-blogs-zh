<!--yml

类别：未分类

日期：2024-05-18 06:22:46

-->

# 浏览器性能 – 10 年回顾 | 来自交易台的故事

> 来源：[`mdavey.wordpress.com/2013/07/05/browser-performance-10-year-recall/#0001-01-01`](https://mdavey.wordpress.com/2013/07/05/browser-performance-10-year-recall/#0001-01-01)

随着围绕浏览器性能的博客/文章/论坛条目的显着增加，再加上 JavaScript VM 领域的不断提升的性能改进，有趣的是回顾一些从用户角度实现期望性能结果的“旧”应用/框架思想。

如果我没记错的话，在 Microsoft Foundation Classes (MFC)/.NET WinForm 时期，使用 [BeginUpdate()](http://msdn.microsoft.com/en-us/library/system.windows.forms.listbox.beginupdate.aspx) 和 EndUpdate() 批量更新可视控件的能力，使软件工程师在对可视控件进行大量更改时避免了某些渲染成本。显然，可视控件批量方法并非万能的解决方案，无法让所有的可视性能问题消失。在进行适当的代码编写之前，软件工程师仍然需要适当地对更改进行批处理，然后调用适当的函数到可视化小部件上。

我注意到在优化 web 应用程序时，考虑到 websocket 和数据流时并没有太多数据。一般的 web 应用程序性能文章，以及 Google I/O 的视频演示集中在 JavaScript 和 [CSS](https://developers.google.com/events/io/sessions/324511365) 优化上，以及利用优化的 [VM](https://developers.google.com/events/io/sessions/324908972) 功能进行编码。显然，这对大多数应用程序来说是最合适的。随着 V8 VM 的不断进步，浏览器 web 应用程序世界比几年前好多了。

回到 websocket 和性能问题。目前似乎很少有数据展示了对 websocket 的传入事件消耗的观点，以及将事件与可视小部件结合的情况。毫不奇怪，这再次让我想起了历史上为了性能而设计的 Java Swing/MFC/WinForm/WPF 桌面应用程序的方式。特别是，在提供线程访问的情况下，大量处理传入的流数据由非 UI 线程处理。更进一步，通常会发现对数据流有效载荷进行限流/批处理以避免淹没用户界面。

在我看来，节流和批处理提供了解决整体目标的不同解决方案 - 避免 UI 被淹没。节流通常与限制每秒更新的数量相关联，例如每秒 5 次。节流通常会丢弃施加节流之外的某些更新，但仍旧旨在确保从服务器发送到客户端的数据是最新的数据。因此，节流只提供了网络应用程序仅接收受限制数量的更新的净值，这些更新应用于

批处理是与从服务器发送数据到客户端相关的进一步优化。具体来说，如果您有 10 个小部件，每个小部件每秒更新 3-7 次，这可能意味着每 100 毫秒左右将为每个小部件流式传输一个数据负载，并进行适当的 DOM 更新。也许更好的考虑是将所有可用的小部件更新批处理为从服务器发送到客户端的单个有效负载，每 200 毫秒一次。

明显的是，网络应用程序的开发在浏览器空间继续向前发展，从开发工具（[Canary](https://www.google.com/intl/en/chrome/browser/canary.html)）到 JavaScript VM。Firefox 的 [OdinMonkey](http://www.extremetech.com/computing/151403-firefox-sticks-it-to-google-with-odinmonkey-which-can-boost-javascript-performance-by-1000-or-more) 和 Google 的 V8 在 JS VM 空间继续前进，忽略了即将发生的布局引擎 [Blink](http://blog.chromium.org/2013/04/blink-rendering-engine-for-chromium.html) vs WebKit 的差异。然后是 IE11，推动 [touch](http://www.windows81.com/2013/06/microsoft-says-ie-11-offers-the-best-touch-performance-on-the-market/) 性能，其对世界的主要好处可能是通过自动更新选项（遵循 Google）帮助消除旧的 IE。

网页开发的缺点仍然是 IE，如《计算机世界》所总结的：

> IE10 仅支持 Windows 8 和 Windows 7，使得 Windows Vista 被困在 IE9 上，就像 Windows XP 被冻结在 IE8 上一样。

如果企业能够放弃 Windows XP，世界将会变得更美好！

最后的想法：尽管人们似乎喜欢具有大量行的 [tables](https://github.com/new-proimage/insanely-big-tables)，但我们真的需要评估所呈现数据的投资回报率，以及是否所有数据都需要一直存在于网络应用程序中 - 分页？

~ 由 mdavey 于 2013 年 7 月 5 日发布。

发布在 [Languages](https://mdavey.wordpress.com/category/languages/)
