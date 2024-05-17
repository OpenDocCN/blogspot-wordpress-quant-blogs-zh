<!--yml
category: 未分类
date: 2024-05-18 05:31:50
-->

# Docker Toolbox and MySQL | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/05/19/docker-toolbox-and-mysql/#0001-01-01](https://mdavey.wordpress.com/2016/05/19/docker-toolbox-and-mysql/#0001-01-01)

## Docker Toolbox and MySQL

The install of Docker [Toolbox](https://docs.docker.com/mac/step_one/) is simple 🙂  Unfortunately, either due to late nights, or other, its not clear that you appear to need to start a network to access the Docker instance of [MySQL](https://hub.docker.com/_/mysql/) by a Java process running outside of the docker environment.  Hence I found the following from web search solved by project:

*   docker network create mysqlapp_net
*   docker run –name mysqldb –net mysqlapp_net -p 3306:3306 -e MYSQL_USER=mysql -e MYSQL_PASSWORD=mysql -e MYSQL_DATABASE=sample -e MYSQL_ROOT_PASSWORD=supersecret -d mysql

~ by mdavey on May 19, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/)