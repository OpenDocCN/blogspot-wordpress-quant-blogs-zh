<!--yml

分类：未分类

日期：2024-05-18 05:43:49

-->

# 是时候使用 React.js 了吗？| 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2015/02/18/time-to-react-js/#0001-01-01`](https://mdavey.wordpress.com/2015/02/18/time-to-react-js/#0001-01-01)

Eric Florenzano 提供了一个有趣的[阅读](https://medium.com/@ericflo/facebook-just-taught-us-all-how-to-build-websites-51f1e7e996f2)关于“Facebook 刚刚教会了我们如何构建网站”。本质上他在谈论 React.js。考虑到网络上关于 React.js 的噪音水平，加上最近 React.js [会议](http://conf.reactjs.com/)，如果读者还没有对 React.js 有一个看法，并且没有看到他们的同事/同事观看各种[演讲](https://www.youtube.com/watch?v=KVZ-P-ZI6W4)，我会感到惊讶。

BBC 最近的一篇[博客](http://www.bbc.co.uk/blogs/internet/entries/47a96d23-ae04-444e-808f-678e6809765d)提供了他们更新 BBC 首页道路的洞察。不出所料，BBC 选择了 React.js：

> 在前端，我们采用了像 isomorphic Javascript 这样的新技术，使用 ReactJS。这允许我们在服务器和客户端执行我们的 JavaScript 模板，这意味着没有 JavaScript 的用户仍然可以加载页面的基本版本。该技术还将允许我们快速开发可以定期从 BBC 周围的实时数据更新自己的模块。所有脚本都使用 Browserify 捆绑在一起，它允许我们混合 AMD 和 CommonJS 模块加载系统。利用这两种加载系统的混合意味着我们不会因为特定模块中实现的机制而受到限制，从而可以选择各种开源库。
> 
> 我们使用 Sass 构建我们的样式表，并使用 BEM 结构化我们的 CSS 选择器，以确保良好的性能。在自动化构建过程中，Sass 样式表被编译成 CSS，该过程使用 Gulp，我们的构建系统，在本地和 Jenkins 持续集成服务器上运行。
> 
> Gulp 还运行我们的自动化单元和验收测试，这些测试是用 Mocha 编写的，

关于客户端服务器渲染，Tom Dale [提出了](http://tomdale.net/2015/02/youre-missing-the-point-of-server-side-rendered-javascript-apps/)一些想法。也许还应该阅读有关 ember [FastBook](http://emberjs.com/blog/2014/12/22/inside-fastboot-the-road-to-server-side-rendering.html) 的文章，考虑到 2012 年 Twitter 上有关[性能](https://blog.twitter.com/2012/improving-performance-on-twittercom)改进的旧帖子。One Big Fluke 还就客户端 [模板化](http://www.onebigfluke.com/2015/01/experimentally-verified-why-client-side.html) 提供了一些测试数据来支持他的观点。

> 如果你关心首次绘制时间，服务器端渲染是赢家。如果你的应用程序需要在页面上显示所有数据才能执行任何操作，客户端渲染是赢家。

顺便说一下，QuirksMode 提供了一个关于[Angular 的问题](http://www.quirksmode.org/blog/archives/2015/01/the_problem_wit.html)的观点，以及 2.0 版本变更的原因，从而导致了 Angular.js 的死亡：

> 采用 Angular 2.0 可能需要他们将大量预算用于重写已经能工作的代码。此外，我很好奇具有 Java 背景的人会喜欢新的编程风格吗？
> 
> 出于这些原因，我认为许多企业用户将坚持使用 1.x 并忽略 2.0。当然，谷歌最终会停止支持 1.x。因此，我认为谷歌试图用 Angular 破解前端企业难题的努力在未来两到三年内将会失败。
> 
> 尽管企业 IT 叛逃可能被前端工程师的涌入所抵消，但 Angular 在他们中间已经获得了不好的声誉。此外，现在前端世界并不需要另一个 MVC 框架。
> 
> 尽管 Angular 1.x 存在严重技术问题，但在具有 Java 背景的企业开发者中尤其成功。2.0 重写针对的是前端开发者，但可能无法达到他们，此外还会让 Angular 的当前追随者望而却步。我认为 Angular 无法在重写中幸存下来。

无论如何，让我们回到 React.js。值得注意的是 Atlassian 发布的关于[Hipchat](https://developer.atlassian.com/blog/2015/02/rebuilding-hipchat-with-react/)重建的文章。Atlassian 是一家很酷的公司。如果他们决定转向 React.js，那么其他人可能需要注意了。

最后，有 React [Native](http://jlongster.com/First-Impressions-using-React-Native)。Facebook 为我们提供了一种构建浏览器和原生应用的统一方式吗？“一次学习，到处编写”。

~ mdavey 于 2015 年 2 月 18 日。

发布在[JavaScript](https://mdavey.wordpress.com/category/languages/javascript/)分类下。
