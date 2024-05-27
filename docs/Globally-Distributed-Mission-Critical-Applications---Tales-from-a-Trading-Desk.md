<!--yml

category: 未分类

日期：2024-05-18 05:39:46

-->

# 全球分布式关键任务应用 | 从交易台的故事

> 来源：[`mdavey.wordpress.com/2015/09/23/globally-distributed-mission-critical-applications/#0001-01-01`](https://mdavey.wordpress.com/2015/09/23/globally-distributed-mission-critical-applications/#0001-01-01)

## 全球分布式关键任务 应用

Kris Beevers 在 [NSONE](https://nsone.net/) 上通过一系列关于构建全球分布式关键任务应用的见解提供了一些很棒的[洞察](http://highscalability.com/blog/2015/9/2/building-globally-distributed-mission-critical-applications.html)。 几个值得注意的点：

+   “单元测试并不足够。测试子系统之间的交互。” 对此我非常赞同。 许多项目过分关注单元测试覆盖率，并忽略了子系统之间的边界测试。 同样，有多少系统失败了测试传送的预期有效载荷数量？

+   “自动化部署和配置管理–要非常小心”。没有免费的午餐！

+   “我们按设施进行部署，从流量最低到最高。在一个设施内，我们按服务器进行部署，甚至按核心进行部署，在每一步都运行全面的功能测试套件。” 大爆炸式的部署会有影响。 NSONE 的部署听起来与

+   “在问题发生之前模拟坏事情。Netflix 的混沌猴就是一个著名的例子” – 你有多少次听到 IT 提出没有容错/灾备概念，因为他们相信没有预算，只能在一段时间后被烧伤？

+   “锁定系统，并最小化暴露给互联网的攻击面。” – 在我看来这是 101 的安全知识。 同样，“你的架构中的每个角色应该只向需要访问这些服务的系统集提供它所提供的服务”

~ 由 mdavey 于 2015 年 9 月 23 日发布。

发表在[敏捷](https://mdavey.wordpress.com/category/agile/)
