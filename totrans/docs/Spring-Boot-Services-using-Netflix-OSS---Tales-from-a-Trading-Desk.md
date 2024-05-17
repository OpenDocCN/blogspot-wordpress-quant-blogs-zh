<!--yml
category: 未分类
date: 2024-05-18 05:36:07
-->

# Spring Boot Services using Netflix OSS | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/02/25/spring-boot-services-using-netflix-oss/#0001-01-01](https://mdavey.wordpress.com/2016/02/25/spring-boot-services-using-netflix-oss/#0001-01-01)

## Spring Boot Services using Netflix OSS

Collection of articles that I found useful whilst playing around with the Netflix stack

*   Building microservices with Spring Cloud and [Netflix](http://callistaenterprise.se/blogg/teknik/2015/04/10/building-microservices-with-spring-cloud-and-netflix-oss-part-1/) OSS, part 1
*   Intro to Spring [Boot](http://www.infoq.com/presentations/spring-boot-web) for the Web Tier
*   Building an [Application](http://spring.io/guides/gs/spring-boot/) with Spring Boot
*   Spring IO [platform](http://platform.spring.io/platform/)
*   [Installing](https://docs.spring.io/spring-boot/docs/current/reference/html/deployment-install.html) Spring Boot applications
*   Spring Boot with [Docker](https://spring.io/guides/gs/spring-boot-docker/)
*   Deploying Spring Boot-based microservices with [Docker](http://plainoldobjects.com/2014/11/16/deploying-spring-boot-based-microservices-with-docker/)
*   Spring Netflix Zuul: [Authenticate](http://www.jhreview.com/tech-stack/questions/34449447/spring-netflix-zuul-authenticate-and-route-the-same-request) and Route the same request
*   Spring [Cloud](http://cloud.spring.io/spring-cloud-netflix/spring-cloud-netflix.html) Netflix
*   Building Cloud [Native](http://ryanjbaxter.com/2015/09/21/building-cloud-native-apps-with-spring-part-2/) Apps With Spring
*   Authenticating a [User](https://spring.io/guides/gs/authenticating-ldap/) with LDAP

Some of the Maven pain is resolve by using the following allowing dependencies to be added without the need for explicit versions, since Spring has provided a release version offering the correct versions of sub components for the entire [release](http://platform.spring.io/platform/) version.

```
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>io.spring.platform</groupId>
            <artifactId>platform-bom</artifactId>
            <version>2.0.2.RELEASE</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement></pre>

```

~ by mdavey on February 25, 2016.

Posted in [Cloud](https://mdavey.wordpress.com/category/hpc/cloud/), [Java](https://mdavey.wordpress.com/category/languages/java/), [Languages](https://mdavey.wordpress.com/category/languages/)