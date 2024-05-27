<!--yml

分类：未分类

date: 2024-05-18 05:45:20

-->

# OpenStack，Mesos 和 Docker – PaaS | 交易桌面故事

> 来源：[`mdavey.wordpress.com/2014/11/05/openstack-mesos-and-docker-paas/#0001-01-01`](https://mdavey.wordpress.com/2014/11/05/openstack-mesos-and-docker-paas/#0001-01-01)

## OpenStack，Mesos 和 Docker – PaaS

eBay 在 2014 年的[文章](http://www.ebaytechblog.com/2014/04/04/delivering-ebays-ci-solution-with-apache-mesos-part-i/#.VFo_9WTF-Q0)“使用 Apache Mesos 为 eBay 的 CI 解决方案提供支持”暗示了我们应该在云计算方面推向何处：

> 我们的新的 Mesos 集群建立在现有的 OpenStack 部署之上。
> 
> 我们的集群建立在 OpenStack 环境中的虚拟服务器上。具体来说，该集群包括运行 Apache Zookeeper，Apache Mesos（主节点和从节点）和 Marathon 服务的虚拟服务器。这种服务组合被选中以提供容错和高可用性（HA）的冗余解决方案。我们的集群至少由三个运行上述每项服务的服务器组成。

最近的 Velocity 会议有一个关于 Mesos 和[Docker](https://mesosphere.github.io/marathon/docs/native-docker.html)的有趣[环节](http://velocityconf.com/velocityny2014/public/schedule/detail/35614)。这引出了一个概念：在 OpenStack 上的[Mesos](https://mesosphere.com/2013/09/26/docker-on-mesos/)上的 Docker 是一个有趣的[PaaS](http://en.wikipedia.org/wiki/Platform_as_a_service)。

~ mdavey 于 2014 年 11 月 5 日。

发布在[云](https://mdavey.wordpress.com/category/hpc/cloud/)，[HPC](https://mdavey.wordpress.com/category/hpc/)
