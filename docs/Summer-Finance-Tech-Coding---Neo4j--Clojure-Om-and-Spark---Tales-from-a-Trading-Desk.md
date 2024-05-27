<!--yml

分类：未分类

日期：2024-05-18 05:40:54

-->

# 夏日金融技术编程——Neo4j、Clojure/Om 和 Spark | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2015/07/15/summer-finance-tech-coding-neo4j-clojureom-and-spark/#0001-01-01`](https://mdavey.wordpress.com/2015/07/15/summer-finance-tech-coding-neo4j-clojureom-and-spark/#0001-01-01)

## 夏日金融技术编程——Neo4j、Clojure/Om 和 Spark

我现在正在尝试多种不同的技术。大多数是之前我在博客上提到过的想法的扩展。

+   时间线和 Neo4j

    +   具体来说，我对在 Neo4j 中建模交易生命周期感兴趣（如这里讨论：[`mdavey.wordpress.com/2011/12/07/bitemporal-model-lifecycle-events-and-operational-risk-part-2/`](https://mdavey.wordpress.com/2011/12/07/bitemporal-model-lifecycle-events-and-operational-risk-part-2/)）以及对 Skill Cloud（如这里：[`mdavey.wordpress.com/2014/06/03/skill-cloud-part-3/`](https://mdavey.wordpress.com/2014/06/03/skill-cloud-part-3/)）的探讨，并避免大多数应用程序/示例使用的“当前”视图图。主要使用 ES6 代码与 Seraph 一起，因为我不关心这个原型的性能。

    +   以下是一些值得一读的有趣参考文档：

        +   在 Neo4j 中表示[依赖时间](https://github.com/SocioPatterns/neo4j-dynagraph/wiki/Representing-time-dependent-graphs-in-Neo4j)的图。

        +   基于时间的[版本化](http://iansrobinson.com/2014/05/13/time-based-versioned-graphs/)图——Ian 的解决方案主要利用关系上的属性：

> 每个关系都有一个表示 2014 年 1 月 1 日的长毫秒值属性（from），以及一个非常大的长值属性（to，即 End-Of-Time，或 EOT，这是一个魔法数字——在这个案例中是 Long.MAX_VALUE），这实际上意味着与关系关联的时期没有当前的上限。

+   Spark

+   Clojure

    +   Om [Next](https://www.youtube.com/watch?v=ByNs9TG30E8&) —— David Nolen 的演讲重新点燃了我对[ClojureScript](https://www.niwi.nz/cljs-workshop/#_let_s_start_with_2)的兴趣。Push Technologies 提供了一个简单的但偏向 FX 的[演示](http://www.pushtechnology.com/2015/02/26/dynamic-pages-clojurescript/)，展示了 ClojureScript 流式价格——虽然这个演示并不复杂，但它确实提供了一些关于[Clojure](http://www.infoq.com/interviews/stuart_holloway_clojure)在电子交易领域的思考。“Brandon Bloom – 使用 Om 构建 CircleCI 的前端”提供了一些关于 Om 项目的[挑战](https://www.youtube.com/watch?v=LNtQPSUi1iQ)的见解。部署到生产环境由[lein-ring](https://github.com/weavejester/lein-ring)提供，IDE 首选是[Cursive](https://cursiveclojure.com/)。Clojure 编译到 JVM 应该避免企业环境中的一些问题。

~ mdavey 于 2015 年 7 月 15 日。

发布在[语言](https://mdavey.wordpress.com/category/languages/)分类下。
