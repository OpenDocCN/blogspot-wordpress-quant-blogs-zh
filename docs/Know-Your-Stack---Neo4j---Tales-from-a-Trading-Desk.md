<!--yml

类别：未分类

日期：2024-05-18 05:28:18

-->

# 了解你的堆栈——Neo4j | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2017/02/22/know-your-stack-neo4j/#0001-01-01`](https://mdavey.wordpress.com/2017/02/22/know-your-stack-neo4j/#0001-01-01)

## 了解你的堆栈——Neo4j

有时生产环境中的事情会变得很糟糕。通常这是因为一系列事件共同作用，形成了一场完美的风暴。这场风暴指的是由于对应用堆栈、工具和知识理解不足，导致生产故障难以诊断。

在尝试诊断问题时，重要的是要通过证据——日志文件、监控工具等来拼凑情况。您的代码库往往可以通过适当的日志记录和包含监控工具/UI 来改进。问题往往源于现成的产品和对如何理解内部工作原理的知识不足。在 Neo4j 中有一个例子。以下是一些希望有帮助的建议，以了解您的应用堆栈中正在发生的事情：

+   Neo4j 有一个 query.log，在查看正在运行的查询和每个查询的执行时间方面非常有用。

+   Neo4j 浏览器（默认端口 7474）有一个“:play sysinfo”，其中有一些基本信息可能会有所帮助，例如事务瓦片，特别是“当前”。如果“当前”持续大于 0，而您期望它是 0，您可能有长时间运行的事务😦

+   Neo4j 3.1+改进了查询管理。特别是现在可以查看哪些查询[正在运行](https://neo4j.com/docs/operations-manual/current/monitoring/query-management/procedures/?_ga=1.17453689.1953165753.1485254392#query-management-list-queries)，并在需要时终止查询

+   在使用产品之前阅读文档是关键。记得 Neo4j 的[打开文件](https://support.neo4j.com/hc/en-us/articles/222587167-How-do-I-set-max-open-files-for-Debian-installs)。

~ mdavey 于 2017 年 2 月 22 日发表。

发布于[语言](https://mdavey.wordpress.com/category/languages/)，[未分类](https://mdavey.wordpress.com/category/uncategorized/)
