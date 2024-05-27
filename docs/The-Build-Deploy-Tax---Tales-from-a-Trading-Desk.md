```yaml

分类：未分类

日期：2024-05-18 05:28:47

```

# The Build/Deploy Tax | Tales from a Trading Desk

> 来源：[`mdavey.wordpress.com/2016/10/27/the-builddeploy-tax/#0001-01-01`](https://mdavey.wordpress.com/2016/10/27/the-builddeploy-tax/#0001-01-01)

## 构建/部署税

项目经常会忘记关于构建/部署的“税”。如今，它被归入 DevOps 的范畴，通常留给指定的 DevOps 人员去处理，而团队的其他成员则继续向产品添加新功能。

不幸的是，与在项目开始时决定测试策略类似，随着项目的推进，构建/部署也应该在相同的情境下考虑。

具体来说，“构建/部署税”是指从“git 提交”到将应用程序部署到环境（例如开发、UAT、集成、生产）所需的时间（浪费）。这个“税”通常以“等待构建/部署过程完成”的时间浪费来衡量。

影响构建/部署税的因素有很多，其中一些如下：

+   [Jenkins](https://jenkins.io/)（CD 服务器）硬件

+   构建资产的邻近性，例如源代码仓库、Nexus、npm、Docker 仓库、测试/生产环境的位置

+   源代码仓库和资产部署的结构

通常，上述问题会被团队、IT 支持和财务部门热烈讨论。例如：

+   源代码应位于单个仓库或多个（例如微服务）

+   单体部署，或基于已更改的服务进行部署

+   利用云服务，例如 DockerHub，或者在单独的环境中运行所有内容，例如 AWS

不幸的是，对于这些问题往往没有一个简单的解决方案。AWS 也许在运行所有的构建/部署基础设施方面是正确的，但是由于生产环境不在 AWS，最后的“一英里”可能仍然“痛苦”。也许这是可以接受的成本？

~ mdavey 于 2016 年 10 月 27 日。

发布在[敏捷](https://mdavey.wordpress.com/category/agile/)、[未分类](https://mdavey.wordpress.com/category/uncategorized/)

标签：[持续交付](https://mdavey.wordpress.com/tag/continuousdelivery/)
