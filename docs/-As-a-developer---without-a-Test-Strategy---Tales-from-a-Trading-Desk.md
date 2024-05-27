<!--yml

类别：未分类

日期：2024-05-18 05:39:21

-->

# “作为一名开发者……”没有测试策略 | 来自交易桌的故事

> 来源：[`mdavey.wordpress.com/2015/10/14/as-a-developer-without-a-test-strategy/#0001-01-01`](https://mdavey.wordpress.com/2015/10/14/as-a-developer-without-a-test-strategy/#0001-01-01)

## “作为一名开发者……”没有测试策略

对我来说，测试在任何项目中都是至关重要的——显而易见，但值得强调。我不理解的是那些乐于编码而不进行测试的团队，尤其是考虑到多年来关于测试——TDD 和 BDD——的大量文献。就我个人而言，我是 BDD 的支持者。BDD 允许我在编写任何代码之前明确我希望软件如何工作——在我看来，其他任何做法都是“黑客”行为。我们都可以“黑”。BDD 迫使大脑在编写代码之前明确应用程序的行为（从而明确代码），迫使在编写任何代码之前进行更好的设计，而不是在编写前几行代码后立即进行重构。

这导致了一系列我不太理解为什么人们似乎愿意在项目中接受的问题：

+   对测试[金字塔](http://martinfowler.com/bliki/TestPyramid.html)缺乏认识

+   没有完成的定义——测试通过的绿色条等

+   缺乏[集成](http://jamescrisp.org/2011/05/30/automated-testing-and-the-test-pyramid/)测试，特别是有效载荷的验证

+   认为性能框架应该测试一组在其他地方未测试的行为。性能框架不应该测试应用程序设计展示的整体行为集中的不同行为频率吗？

+   接受[纸杯蛋糕](https://www.thoughtworks.com/insights/blog/introducing-software-testing-cupcake-anti-pattern)反模式

+   在持续[交付](https://en.wikipedia.org/wiki/Continuous_delivery)过程中，对保持自动化测试通过的绿色状态毫不在意。

+   质量（保证）与软件工程之间的脱节，这导致测试的重复，或者更令人担忧的是，反模式“分裂脑”测试策略——各方对应用程序应遵守的行为有不同的看法。

+   缺乏任何测试结果数据库以供分析

我不喜欢“质量保证（QA）”这个词。我更喜欢“质量工程”，原因很简单，如果质量不是从软件工程代码库开始的，那么真正的质量就没有希望。整个团队必须拥抱质量才能使应用程序成功。

~ 由 mdavey 于 2015 年 10 月 14 日发布。

发布于[敏捷](https://mdavey.wordpress.com/category/agile/)
