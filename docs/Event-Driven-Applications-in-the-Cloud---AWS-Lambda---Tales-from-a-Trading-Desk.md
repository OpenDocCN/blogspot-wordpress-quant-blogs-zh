<!--yml

类别：未分类

日期：2024 年 5 月 18 日 05:44:15

-->

# [云中的事件驱动应用 - AWS Lambda | 一个交易台的故事](https://mdavey.wordpress.com/2015/02/03/event-driven-applications-in-the-cloud-aws-lambda/#0001-01-01)

> 来源：[`mdavey.wordpress.com/2015/02/03/event-driven-applications-in-the-cloud-aws-lambda/#0001-01-01`](https://mdavey.wordpress.com/2015/02/03/event-driven-applications-in-the-cloud-aws-lambda/#0001-01-01)

## 云中的事件驱动应用 - AWS Lambda

自最近 AWS Lambda 推出以来，已经有许多[文章](http://research.gigaom.com/2015/01/why-aws-lambda-is-a-masterstroke-from-amazon/)提供了[见解](http://thenewstack.io/aws-lambda-is-a-step-towards-creating-a-new-normal/)。 从我的角度来看，关键是亚马逊使其他服务的事件能够触发，从而使 AWS Lambda 成为面向事件驱动应用程序的胶水服务：

> Lambda [与新的 Amazon S3 功能一起推出](https://mdavey.wordpress.com/2014/12/20/innovation-back-in-financial-services/ "金融服务中的创新？")，称为事件通知，每当向存储桶添加或更改对象时生成事件，并且我们最近宣布的 Amazon DynamoDB Streams 功能在表更新时生成事件。 现在开发人员可以将代码附加到 Amazon S3 存储桶和 Amazon DynamoDB 表，并且每当对这些存储桶或表进行更改时，它将自动运行。 开发人员不必轮询、代理或担心容量过多或过少 - Lambda 函数会根据事件速率进行扩展，并且仅在需要时执行，从而使您的成本降低。

Tapir’s Tale 提供了一个[示例](http://anders.janmyr.com/2014/12/lambda-javascript-micro-services-on-aws.html)，展示了 AWS Lambda 的功能。

如果从 Kinesis 流触发 Lambda，可能更有趣 - 可以在[这里](http://docs.aws.amazon.com/lambda/latest/dg/walkthrough-kinesis-events-adminuser.html)看到这样的示例 - 显然有一些有趣的机会来处理大量数据。

有一些挑战需要时间来[演变](http://www.gregarnette.com/blog/2014/12/why-i-am-excited-about-aws-lambda/)，例如安全模型。

最后，StackStorm 提供了对 AWS Lambda 和其自身的[观点](http://stackstorm.com/2014/11/20/stackstorm-vs-aws-lambda-event-driven-computing-vs-event-driven-operations/)。

~ 由 mdavey 于 2015 年 2 月 3 日发布。

发表在[云](https://mdavey.wordpress.com/category/hpc/cloud/)，[数据](https://mdavey.wordpress.com/category/data/)中。
