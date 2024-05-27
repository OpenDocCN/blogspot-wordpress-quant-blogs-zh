<!--yml

类别：未分类

日期：2024-05-18 05:50:06

-->

# Think Services | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2014/05/16/services/#0001-01-01`](https://mdavey.wordpress.com/2014/05/16/services/#0001-01-01)

## Think Services

[Twitter](https://blog.twitter.com/2012/incubating-apache-mesos) 提供了一些关于 Apache Mesos 有趣的阅读材料。Apache Aurora 提供：

> 一个在 Mesos 之上运行的服务调度程序，使你能够运行利用 Mesos 的可扩展性、容错性和资源隔离性的长期服务。

[Vagrant](http://tepid.org/tech/01-aurora-mesos-cluster/) 提供了一个快速[方式](https://www.exoscale.ch/syslog/2014/03/01/discovering-mesos/)来开始使用 Mesos 和 Aurora。

O’Reilly 的“学习 Apache [Moses](http://gigaom.com/2013/07/29/airbnb-is-engineering-itself-into-a-data-driven-company/)”列出了几家使用[Mesos](http://nerds.airbnb.com/distributed-computing-at-airbnb/)在生产环境中的公司：Twitter、Airbnb、HubSpot、MediaCrossing、Sharethrough、Ooyala、Devicescape、iQiyi、OpenTable、CloudPhysics、Xogito、Vimeo。

mesosphere 提供了一系列[教程](http://mesosphere.io/learn/#tutorials)，感兴趣的可以看看[Play](http://typesafe.com/blog/play-framework-grid-deployment-with-mesos)和[Storm](http://mesosphere.io/learn/run-storm-on-mesos/) 😉

但当考虑通过[Docker](http://mesosphere.io/2013/09/26/docker-on-mesos/)部署服务时，Mesos 变得更加有趣：

> Docker 容器提供了一种一致的、紧凑的且灵活的应用程序构建打包方式。使用 Docker 在 Mesos 上交付应用程序承诺了一个真正弹性、高效和一致的平台，以便在本地或云端交付各种应用程序。

在开发过程中，你可以在 Mesos 上运行[Jenkins](http://developer-blog.cloudbees.com/2014/04/apache-mesos-and-jenkins-elastic-build.html)，让 Mesos 不仅用于开发，还用于你应用程序的部署（作为一系列[服务](http://en.wikipedia.org/wiki/Service-oriented_architecture)的 Docker 容器）。

~ mdavey 于 2014 年 5 月 16 日。

发布在[Languages](https://mdavey.wordpress.com/category/languages/)
