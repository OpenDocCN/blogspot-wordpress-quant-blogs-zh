<!--yml
category: 未分类
date: 2024-05-18 05:50:06
-->

# Think Services | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2014/05/16/services/#0001-01-01](https://mdavey.wordpress.com/2014/05/16/services/#0001-01-01)

## Think Services

[Twitter](https://blog.twitter.com/2012/incubating-apache-mesos) provides some interesting reading on Apache Mesos.  Apache Aurora offers:

> a service scheduler that runs on top of Mesos, enabling you to run long-running services that take advantage of Mesos’ scalability, fault-tolerance, and resource isolation

[Vagrant](http://tepid.org/tech/01-aurora-mesos-cluster/) offers a quick [way](https://www.exoscale.ch/syslog/2014/03/01/discovering-mesos/) to get [started](http://java.dzone.com/articles/getting-started-apache-mesos) with Mesos and Aurora.

O’Reilly’s “Learning Apache [Moses](http://gigaom.com/2013/07/29/airbnb-is-engineering-itself-into-a-data-driven-company/)” offers a list of a few companies that have [Mesos](http://nerds.airbnb.com/distributed-computing-at-airbnb/) in production: Twitter, Airbnb, HubSpot, MediaCrossing, Sharethrough, Ooyala, Devicescape, iQiyi, OpenTable, CloudPhysics, Xogito, Vimeo.

mesosphere offers a number of [tutorials](http://mesosphere.io/learn/#tutorials), of interested [Play](http://typesafe.com/blog/play-framework-grid-deployment-with-mesos) and [Storm](http://mesosphere.io/learn/run-storm-on-mesos/) 😉

But Mesos gets more interesting when one considered deployment of services via [Docker](http://mesosphere.io/2013/09/26/docker-on-mesos/):

> Docker containers provide a consistent, compact and flexible means of packaging application builds. Delivering applications with Docker on Mesos promises a truly elastic, efficient and consistent platform for delivering a range of applications on premises or in the cloud.

During development you could run [Jenkins](http://developer-blog.cloudbees.com/2014/04/apache-mesos-and-jenkins-elastic-build.html) on Mesos 🙂 , allowing Mesos to be used not only in development, but also for deployment of you application (as a set of [services](http://en.wikipedia.org/wiki/Service-oriented_architecture) in docker containers).

~ by mdavey on May 16, 2014.

Posted in [Languages](https://mdavey.wordpress.com/category/languages/)