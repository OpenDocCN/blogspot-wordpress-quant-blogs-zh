<!--yml

分类：未分类

日期：2024-05-18 05:38:22

-->

# 微服务模式 | 交易台的故事

> 来源：[`mdavey.wordpress.com/2015/11/03/microservies-patterns/#0001-01-01`](https://mdavey.wordpress.com/2015/11/03/microservies-patterns/#0001-01-01)

微服务设计模式[文章](https://dzone.com/articles/microservice-design-patterns)提供了一个关于可能用于构建微服务的软件模式的视角。显然，代理和聚合器模式在避免从用户界面角度对 REST 微服务的过载方面提供了一些结构。

这很自然地引出了 Ray Nicholus 的“Web 开发的未来——React, Falcor, 和 ES6”[文章](http://engineering.widen.com/blog/future-of-the-web-react-falcor/)，特别是强调保持事物“简单”的重要性，避免不必要的请求开销、大量的请求和没有必要的大型响应载荷，这在交易应用中可能会杀死性能/延迟/用户体验，从而杀死客户。你不会从我这里得到太多关于 React 的争论，同样，我觉得 Falcor 是合理的，因为我曾在很久以前的项目中使用过这样的概念(太久以前了)。Webpack——再次同意。总的来说，这是一篇好文章。

转向“Do Good Microservices Architectures Spell the Death of the Enterprise Service Bus?”这篇文章，它提供了一个很好的高级挑战列表，关于微服务的。很高兴看到[Swagger](http://swagger.io/)在合约方面的提及。同样，对内存数据[网格](https://www.voxxed.com/blog/2015/01/good-microservices-architectures-death-enterprise-service-bus-part-one/)的提及也很棒，不只是传统的数据缓存。

> 微服务是独立的、可扩展的服务。现代架构使用可扩展的平台，允许独立自动部署不同的技术/服务/应用程序。使用您选择的工具定义服务合约，实现(微)服务和服务发现，自动化独立和可扩展的部署。协调不同的(微)服务，实时主动对事件进行事件相关联处理。这就是创建良好微服务架构的方法。

从软件堆栈的角度来看，需要解决的一个棘手问题就是微服务将采用哪种编程语言实现。如果我们假设在这个讨论中使用 REST+JSON 来定义微服务合同，那么有些人可能会倾向于使用 JavaScript 堆栈，以便微服务能够利用 JSON。其他人可能会选择 Java 道路，并承担 DTO 开销。是时候再次考虑 Falcor 了吗？另一个选择是避免走寻常路，考虑使用 Clojure。在[Clojure](http://blog.juxt.pro/posts/why-clojurescript-matters.html)道路上，您可以利用[Prismatics Schema](https://github.com/Prismatic/schema)和[compojure-api](https://github.com/metosin/compojure-api)（swagger’d）来声明轻量级数据合同——代码即数据，数据即代码。最终，Clojure 仍然运行在著名的两个虚拟机世界（JavaScript 和 JVM）上，与 Node.js 作为服务器软件堆栈的论点类似，为开发者提供了从客户端到服务器的连贯体验，而不是要求不同的技能集/团队。

作者：mdavey，发布日期：2015 年 11 月 3 日。

发布在[语言](https://mdavey.wordpress.com/category/languages/)分类下。
