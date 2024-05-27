<!--yml

分类：未分类

日期：2024-05-18 06:02:37

-->

# RXJava 飞机编程 | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2013/08/19/rxjava-airplane-coding/#0001-01-01`](https://mdavey.wordpress.com/2013/08/19/rxjava-airplane-coding/#0001-01-01)

## RXJava 飞机编程

在从悉尼返回伦敦的漫长飞行中，我设法找到了几小时的时间进行编程。大部分的编程工作是围绕增强[场景](http://cukes.info/)测试以及重构底层代码库，以便进一步利用[RxJava](https://github.com/Netflix/RxJava)。遇到了一个奇怪的“箱型”Cucumber 错误，由于在飞行前没有下载完整的文档，幸运的是在.feature 文件中进行了拼写更正后解决了。

使用 Observable.[Zip](https://github.com/Netflix/RxJava/wiki/Combining-Observables#zip) 允许我将两个可观察对象组合在一起，但我现在意识到这并不是我真正想做的。我真正想要的是两个 Observables 之间的“选择”——我仍在思考这个问题。

~ mdavey 于 2013 年 8 月 19 日。

发表于 [Java](https://mdavey.wordpress.com/category/languages/java/)
