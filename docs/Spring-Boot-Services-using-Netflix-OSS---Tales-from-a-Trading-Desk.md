<!--yml

分类：未分类

日期：2024-05-18 05:36:07

-->

# 使用 Netflix OSS 的 Spring Boot 服务 | 交易桌面故事

> 来源：[`mdavey.wordpress.com/2016/02/25/spring-boot-services-using-netflix-oss/#0001-01-01`](https://mdavey.wordpress.com/2016/02/25/spring-boot-services-using-netflix-oss/#0001-01-01)

## 使用 Netflix OSS 的 Spring Boot 服务

在我探索 Netflix 堆栈时发现有用的文章集合

+   使用 Spring Cloud 和 Netflix [OSS](http://callistaenterprise.se/blogg/teknik/2015/04/10/building-microservices-with-spring-cloud-and-netflix-oss-part-1/) 构建微服务，第一部分

+   面向 Web 层的 Spring [Boot](http://www.infoq.com/presentations/spring-boot-web) 入门

+   使用 Spring Boot 构建 [应用程序](http://spring.io/guides/gs/spring-boot/)

+   Spring IO [平台](http://platform.spring.io/platform/)

+   [安装](https://docs.spring.io/spring-boot/docs/current/reference/html/deployment-install.html) Spring Boot 应用程序

+   Spring Boot 与 [Docker](https://spring.io/guides/gs/spring-boot-docker/)

+   使用 Docker 部署基于 Spring Boot 的微服务 [Docker](http://plainoldobjects.com/2014/11/16/deploying-spring-boot-based-microservices-with-docker/)

+   Spring Netflix Zuul: [认证](http://www.jhreview.com/tech-stack/questions/34449447/spring-netflix-zuul-authenticate-and-route-the-same-request) 并路由同一请求

+   Spring [Cloud](http://cloud.spring.io/spring-cloud-netflix/spring-cloud-netflix.html) Netflix

+   使用 Spring 构建 [云原生](http://ryanjbaxter.com/2015/09/21/building-cloud-native-apps-with-spring-part-2/) 应用

+   使用 LDAP [认证](https://spring.io/guides/gs/authenticating-ldap/) 用户

使用以下方法可以解决 Maven 的一些痛点，允许添加依赖而不需要显式版本，因为 Spring 提供了发行版本，为整个 [发行版](http://platform.spring.io/platform/) 版本提供了子组件的正确版本。

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

~ mdavey 于 2016 年 2 月 25 日。

发布于 [云](https://mdavey.wordpress.com/category/hpc/cloud/)、[Java](https://mdavey.wordpress.com/category/languages/java/)、[语言](https://mdavey.wordpress.com/category/languages/)
