<!--yml
category: 未分类
date: 2024-05-18 05:48:44
-->

# Skill Cloud – Part 4 – Spring Data and Neo4j | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2014/06/13/skill-cloud-part-4-spring-data-and-neo4j/#0001-01-01](https://mdavey.wordpress.com/2014/06/13/skill-cloud-part-4-spring-data-and-neo4j/#0001-01-01)

## Skill Cloud – Part 4 – Spring Data and Neo4j

Spent the last flight banging my head against [Spring Data](http://projects.spring.io/spring-data-neo4j/) and Neo4j.  I was hoping Spring Data would save me some code writing, but the pain of Maven dependency hell, coupled with exceptions that are meaningless in many way, has almost driven the will to live out of me.  At the moment I’m in the world of:

> Exception in thread “main” org.springframework.beans.factory.BeanCreationException: Error creating bean with name ‘entityFetchHandler’ defined in class path resource [org/springframework/data/neo4j/aspects/config/Neo4jAspectConfiguration.class]: Instantiation of bean failed; nested exception is org.springframework.beans.factory.BeanDefinitionStoreException: Factory method [public org.springframework.data.neo4j.support.mapping.Neo4jEntityFetchHandler org.springframework.data.neo4j.config.Neo4jConfiguration.entityFetchHandler() throws java.lang.Exception] threw exception; nested exception is org.springframework.beans.factory.BeanCreationException: Error creating bean with name ‘nodeStateTransmitter’ defined in class path resource [org/springframework/data/neo4j/aspects/config/Neo4jAspectConfiguration.class]: Initialization of bean failed; nested exception is java.lang.reflect.MalformedParameterizedTypeException

Which even after a number of google’s is still not resolved.  I did walk into [LockException](https://jira.spring.io/browse/DATAGRAPH-478) compatibility issues with Neo4j 2.1.1, and then the Spring Data [3.0.1](http://forum.spring.io/forum/spring-projects/data/nosql/746297-spring-data-neo4j-fails-on-upgrade-to-3-0-1) issue 😦  Here’s my pom.xml, which could be the root of the issue, who knows:

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

~ by mdavey on June 13, 2014.

Posted in [Data](https://mdavey.wordpress.com/category/data/), [Java](https://mdavey.wordpress.com/category/languages/java/)