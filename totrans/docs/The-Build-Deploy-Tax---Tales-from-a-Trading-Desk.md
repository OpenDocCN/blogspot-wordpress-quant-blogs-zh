<!--yml
category: 未分类
date: 2024-05-18 05:28:47
-->

# The Build/Deploy Tax | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/10/27/the-builddeploy-tax/#0001-01-01](https://mdavey.wordpress.com/2016/10/27/the-builddeploy-tax/#0001-01-01)

## The Build/Deploy Tax

Projects often forget about the build/deploy tax.   These days its thrown under the DevOps banner, and often being left to the appointed DevOps individual to wade though and resolve whilst the rest of the team stream ahead with adding new features to the product.

Unfortunately, similar to deciding a testing strategy at the start of a project, and evolving the strategy along the road, build/deployment should be consider in the same context.

Specifically, the build/deploy tax is the duration of time (waste) that it costs the team, from “git commit” to deployment of application to an environment e.g. development, UAT, Integration, Production.  This tax is often measured in terms of time wasted “waiting for the build/deployment process to complete”.

There are many factors that influence the build/deploy tax, a few of which are listed below:

*   [Jenkins](https://jenkins.io/) (CD server) hardware
*   Proximity of build assets e.g. locations of source code repository, nexus, npm, docker registry,  test/prod environments
*   Structure of source code repository and asset deployment

Often the above issues are hotly debated by both the team, IT support and finance.  Examples being:

*   Source code be in a single repository or multiple (e.g by micro service)
*   Monolithic deployment, or deployment based on services that have changed
*   Leverage cloud services e.g. DockerHub or run everything within a separate environment e.g. AWS

Unfortunately, there often isn’t a simple solution to many of these problems.  AWS maybe right to running all your build/deployment infrastructure, but the last mile to Prod may still be “painful” due to Prod not being in AWS.  Maybe this is an acceptable cost?

~ by mdavey on October 27, 2016.

Posted in [Agile](https://mdavey.wordpress.com/category/agile/), [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)
Tags: [ContinuousDelivery](https://mdavey.wordpress.com/tag/continuousdelivery/)