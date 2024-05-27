<!--yml

分类：未分类

日期：2024 年 5 月 18 日 05:31:50

-->

# Docker Toolbox 和 MySQL | 来自一个交易台的故事

> 来源：[`mdavey.wordpress.com/2016/05/19/docker-toolbox-and-mysql/#0001-01-01`](https://mdavey.wordpress.com/2016/05/19/docker-toolbox-and-mysql/#0001-01-01)

## Docker Toolbox 和 MySQL

安装 Docker [Toolbox](https://docs.docker.com/mac/step_one/) 很简单 🙂 不幸的是，可能由于熬夜或其他原因，目前似乎需要启动一个网络才能访问 [MySQL](https://hub.docker.com/_/mysql/) 的 Docker 实例，而这个访问是通过运行在 docker 环境之外的 Java 进程实现的。因此，我从网络搜索中找到了以下解决方案：

+   docker network create mysqlapp_net

+   docker run –name mysqldb –net mysqlapp_net -p 3306:3306 -e MYSQL_USER=mysql -e MYSQL_PASSWORD=mysql -e MYSQL_DATABASE=sample -e MYSQL_ROOT_PASSWORD=supersecret -d mysql

~ 作者 mdavey，发表于 2016 年 5 月 19 日。

发布于 [数据](https://mdavey.wordpress.com/category/data/) 分类。
