<!--yml
category: 未分类
date: 2024-05-18 04:49:30
-->

# Magmasystems Blog: Excursions Back into the World of Java

> 来源：[http://magmasystems.blogspot.com/2011/08/excursions-back-into-world-of-java.html#0001-01-01](http://magmasystems.blogspot.com/2011/08/excursions-back-into-world-of-java.html#0001-01-01)

I did some Java development when it first came out. Honest I did. I even taught Java classes in the late 1990's at Bellcore, which was a division of AT&T.

I have managed teams that have Java-based systems. And, as part of the CEP system that I did, I had to go and write Java-based web services and deliver a Java API so that other groups could hook into the Notification Services.

Despite that, and because of my long history with Microsoft technologies, I am often viewed as "The Dot Net Guy".

So, this week, I broke out the Java manuals again, and I decided to write the Exchange Simulator portion of my little project in Java 1.6\. Writing the simulator was fairly easy, and in little time, I had FIX messages being passed back and forth between my Java-based Exchange Simulator and my .NET-based OMS.

Java is not that much different than C#. They even have Reflection, something that I sorely missed when I had to do C++ in the past year. I wish that Java supported C# auto properties and C# events (is this stuff coming in Java 1.8?), but other than that, it feels like programming in C# 1.0.

However, the Java language is only one small part about being a true Java developer and architect. There is an entire ecosystem that surrounds Java development. I got a list of tools and frameworks to learn from one of my friends, and there is a lot of stuff in there. This is a list of the basic tools that one needs:

*   JDK 1.6
*   Eclipse 3.6 (Java EE Edition)
*   JTA/JTS (transaction services)
*   Spring 3.0 or 3.1
*   Hibernate 3.6
*   Open JMS or ActiveMQ
*   JBoss, [Jetty](http://www.eclipse.org/jetty/), or Apache Geronimo
*   Subversion
*   [Jenkins](https://wiki.jenkins-ci.org/display/JENKINS/Meet+Jenkins) or Hudson

For the past year, I have been using Eclipse for my C++ development, editing on Windows and compiling on Linux. Editing, building and debugging Java apps using Eclipse seems to be a breeze. Eclipse has a lot of the real-time error detection built into it that I am used to with Resharper in Visual Studio. The incremental compilation helps, and it takes almost no time to go from editing to running an application.

I have experimented with Spring in various forms over the years (mostly Spring.Net), in addition to writing my own dependency injection framework. Plus, my recent experiences with Prism has gotten me back into the world of IOC (although I am annoyed that Prism/UnityContainer does not support any kind of "IDisposable" pattern when your modules are unloaded when an app closes). I cannot integrate Spring 3.1 into my app just yet because of some logging dependencies that are documented (QuickFix/J uses SLF4J, which is not compatible with Spring).

(N)Hibernate is also another ORM that I have looked at over the years.

As far as source control, I have always been a TFS/Perforce user. The past year and a half was spent in Clearcase, which seems a bit ancient, although it seems to work. Many people seem to prefer Subversion, so this is a good opportunity for me to learn it.

The same goes for Continuous Integration servers. I have been using Cruise Control .NET for all of my CI needs, and Hudson/Jenkins is something that I have heard mentioned for a while now.

The only piece of this stack that is

[totally alien to me](http://stackoverflow.com/questions/3954614/why-does-java-apps-need-an-application-server-and-net-just-iis-web-server)

is the Java Application Server. The whole concept of a Java Application Server is a bit new to me, as we really don't have an equivalent in the .NET world. I am not interested in the web server capability of these containers, so I need to find out the other capabilities that I can leverage. This morning, I am going to download JBoss as a first step.

(Update - It looks like you need to purchase a $99 subscription for JBoss. So, I will download Jetty, even though I am not sure that Jetty is a complete Java Application Server.)

(From the Stack Overflow post, where is a great summary of what a JAS is:

*A Java EE app server is a transaction monitor for distributed components. It provides a number of abstractions (e.g., naming, pooling, component lifecycle, persistence, messaging, etc.) to help accomplish this.* *Lots of these services are part of the Windows operating system. Java EE needs the abstraction because it's independent of operating system.)*

I will keep everyone posted on my progress.

©2011 Marc Adler - All Rights Reserved. All opinions here are personal, and have no relation to my employer.