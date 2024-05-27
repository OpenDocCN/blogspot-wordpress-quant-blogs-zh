<!--yml

类别：未分类

日期：2024 年 05 月 18 日 06:31:20

-->

# Fastbook - HTML 面对 Facebook | 交易台的故事

> 来源：[`mdavey.wordpress.com/2013/01/07/fastbook-html-in-the-face-of-facebook/#0001-01-01`](https://mdavey.wordpress.com/2013/01/07/fastbook-html-in-the-face-of-facebook/#0001-01-01)

## Fastbook - HTML 面对 Facebook

在 Sencha 的[博客](http://www.sencha.com/blog/the-making-of-fastbook-an-html5-love-story)上读到的有趣的内容 - Mark Zuckerberg 的 HTML5 视图与 Sencha 的 HTML5 视图。关于 Sencha Fastbook PoC 的好处是产生的视频：

> 四分钟的视频可以让你快速了解 Sencha Fastbook，并向你展示我们的 HTML5 应用在性能上与 iOS 和安卓原生 Facebook 应用进行对比。

阅读博客文章时，发现“应用程序的大部分部分仍然是原始的 HTML 页面”令人担忧 - Facebook 是否忘记阅读 HTML/JS 最佳实践指南了？Fastbook 的解决方案之一是利用沙箱容器，允许对 DOM 树进行分区，将分区渲染在单独的 iFrames 中。但是，沙箱容器并非万能良药，在父窗口和沙箱之间的代理调用需要被适当地使用。

另一个令人惊讶的是 Sencha 发现从 Facebook 获取的大量新闻数据::

> 平均每 10 个项目传输 15KB 到 20KB 的经过压缩的 JSON 数据，其中许多不需要用于渲染实际视图。

Web Workers 也在网络和序列化领域出现了。

作者 mdavey 于 2013 年 1 月 7 日。

发表在[JavaScript](https://mdavey.wordpress.com/category/languages/javascript/)
