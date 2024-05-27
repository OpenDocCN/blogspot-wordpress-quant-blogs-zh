<!--yml

分类：未分类

date: 2024-05-18 05:48:44

-->

# 技能云 – 第四部分 – Spring Data 和 Neo4j | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2014/06/13/skill-cloud-part-4-spring-data-and-neo4j/#0001-01-01`](https://mdavey.wordpress.com/2014/06/13/skill-cloud-part-4-spring-data-and-neo4j/#0001-01-01)

## 技能云 – 第四部分 – Spring Data 和 Neo4j

在最近的航班上，我一直在头疼如何使用[Spring Data](http://projects.spring.io/spring-data-neo4j/)和 Neo4j。我希望 Spring Data 能帮我减少一些代码编写工作，但是 Maven 依赖地狱的痛苦，以及许多情况下毫无意义的异常，几乎让我失去了生存的意志。此刻我正处在这样的环境中：

> 线程“main”中的异常 org.springframework.beans.factory.BeanCreationException：在类路径资源[org/springframework/data/neo4j/aspects/config/Neo4jAspectConfiguration.class]中定义的名为“entityFetchHandler”的 bean 创建失败；内部异常是 org.springframework.beans.factory.BeanDefinitionStoreException：工厂方法[public org.springframework.data.neo4j.support.mapping.Neo4jEntityFetchHandler org.springframework.data.neo4j.config.Neo4jConfiguration.entityFetchHandler() throws java.lang.Exception]抛出异常；内部异常是 org.springframework.beans.factory.BeanCreationException：在类路径资源[org/springframework/data/neo4j/aspects/config/Neo4jAspectConfiguration.class]中定义的名为“nodeStateTransmitter”的 bean 初始化失败；内部异常是 java.lang.reflect.MalformedParameterizedTypeException

即使在进行了许多次谷歌搜索之后仍未解决。我确实遇到了与 Neo4j 2.1.1 不兼容的[LockException](https://jira.spring.io/browse/DATAGRAPH-478)问题，然后又遇到了 Spring Data [3.0.1](http://forum.spring.io/forum/spring-projects/data/nosql/746297-spring-data-neo4j-fails-on-upgrade-to-3-0-1)的问题😦  以下是我的 pom.xml，可能是问题的根源，谁知道呢：

```

<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
<modelVersion>4.0.0</modelVersion>

<groupId>teams</groupId>
<artifactId>teams</artifactId>
<version>1.0-SNAPSHOT</version>
<properties>
<neo4j.version>2.0.0</neo4j.version>
<spring.data.version>3.0.1.RELEASE</spring.data.version>
<aspect.version>1.7.4</aspect.version>
<java.version>1.8</java.version>
</properties>

<parent>
<groupId>org.springframework.boot</groupId>
<artifactId>spring-boot-starter-parent</artifactId>
<version>1.1.1.RELEASE</version>
</parent>

<dependencies>

<dependency>
<groupId>org.springframework.boot</groupId>
<artifactId>spring-boot-starter-web</artifactId>
</dependency>

<dependency>
<groupId>org.springframework.data</groupId>
<artifactId>spring-data-neo4j</artifactId>
<version>${spring.data.version}</version>
</dependency>

<dependency>
<groupId>org.springframework.data</groupId>
<artifactId>spring-data-neo4j-aspects</artifactId>
<version>${spring.data.version}</version>
</dependency>

<dependency>
<groupId>org.neo4j</groupId>
<artifactId>neo4j</artifactId>
<version>${neo4j.version}</version>
</dependency>
<dependency>
<groupId>org.neo4j</groupId>
<artifactId>neo4j-kernel</artifactId>
<version>${neo4j.version}</version>
</dependency>
<dependency>
<groupId>org.neo4j</groupId>
<artifactId>neo4j-community</artifactId>
<version>${neo4j.version}</version>
</dependency>
<dependency>
<groupId>org.neo4j</groupId>
<artifactId>neo4j-advanced</artifactId>
<version>${neo4j.version}</version>
</dependency>

<dependency>
<groupId>org.aspectj</groupId>
<artifactId>aspectjrt</artifactId>
<version>${aspect.version}</version>
</dependency>
</dependencies>

<build>
<plugins>
<plugin>
<groupId>org.springframework.boot</groupId>
<artifactId>spring-boot-maven-plugin</artifactId>
</plugin>

<plugin>
<groupId>org.codehaus.mojo</groupId>
<artifactId>aspectj-maven-plugin</artifactId>
<version>1.4</version>
<dependencies>
<!-- NB: You must use Maven 2.0.9 or above or these are ignored (see MNG-2972) -->
<dependency>
<groupId>org.aspectj</groupId>
<artifactId>aspectjrt</artifactId>
<version>${aspect.version}</version>
</dependency>
<dependency>
<groupId>org.aspectj</groupId>
<artifactId>aspectjtools</artifactId>
<version>${aspect.version}</version>
</dependency>
</dependencies>
<executions>
<execution>
<goals>
<goal>compile</goal>
<goal>test-compile</goal>
</goals>
</execution>
</executions>
<configuration>
<outxml>true</outxml>
<aspectLibraries>
<aspectLibrary>
<groupId>org.springframework</groupId>
<artifactId>spring-aspects</artifactId>
</aspectLibrary>
<aspectLibrary>
<groupId>org.springframework.data</groupId>
<artifactId>spring-data-neo4j-aspects</artifactId> </aspectLibrary>
</aspectLibraries>
<source>1.8</source>
<target>1.8</target>
</configuration>
</plugin>
</plugins>

</build>
</project>

```

~ mdavey 于 2014 年 6 月 13 日发表。

发布在[数据](https://mdavey.wordpress.com/category/data/)、[Java](https://mdavey.wordpress.com/category/languages/java/)分类
