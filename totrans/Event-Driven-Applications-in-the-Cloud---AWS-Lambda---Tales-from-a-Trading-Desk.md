<!--yml
category: 未分类
date: 2024-05-18 05:44:15
-->

# Event-Driven Applications in the Cloud – AWS Lambda | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2015/02/03/event-driven-applications-in-the-cloud-aws-lambda/#0001-01-01](https://mdavey.wordpress.com/2015/02/03/event-driven-applications-in-the-cloud-aws-lambda/#0001-01-01)

## Event-Driven Applications in the Cloud – AWS Lambda

Since the recent AWS Lambda launch, there have been numerous [articles](http://research.gigaom.com/2015/01/why-aws-lambda-is-a-masterstroke-from-amazon/) providing [insight](http://thenewstack.io/aws-lambda-is-a-step-towards-creating-a-new-normal/) into the service.  What’s key from my perspective is that Amazon have enabled event from other services, thus making AWS Lambda a glue service for event-driven applications:

> Lambda is [launching](https://mdavey.wordpress.com/2014/12/20/innovation-back-in-financial-services/ "Innovation back in Financial Services?") in conjunction with a new Amazon S3 feature called event notifications the generates events whenever objects are added or changed in a bucket, and our recently announced Amazon DynamoDB Streams feature that generates events when a table is updated. Now developers can attach code to Amazon S3 buckets and Amazon DynamoDB tables, and it will automatically run whenever changes occur to those buckets or tables. Developers don’t have to poll, proxy, or worry about being over or under capacity – Lambda functions scale to match the event rate and execute only when needed, keeping your costs low.

Tapir’s Tale offer an [example](http://anders.janmyr.com/2014/12/lambda-javascript-micro-services-on-aws.html) of what can be done with AWS Lambda’s.

What’s probably more interesting if the triggering of lambda from Kinesis streams – an example of such can be seen [here](http://docs.aws.amazon.com/lambda/latest/dg/walkthrough-kinesis-events-adminuser.html) – clearly some interesting opportunities to process large quantities of data.

There are a few challenges which will take time to [evolve](http://www.gregarnette.com/blog/2014/12/why-i-am-excited-about-aws-lambda/) e.g. security model

Finally, StackStorm offers a [view](http://stackstorm.com/2014/11/20/stackstorm-vs-aws-lambda-event-driven-computing-vs-event-driven-operations/) on AWS Lambda, and itself.

~ by mdavey on February 3, 2015.

Posted in [Cloud](https://mdavey.wordpress.com/category/hpc/cloud/), [Data](https://mdavey.wordpress.com/category/data/)