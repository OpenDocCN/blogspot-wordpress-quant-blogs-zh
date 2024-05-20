<!--yml
category: 未分类
date: 2024-05-18 06:34:54
-->

# Scala IDE – Versions are Too Painful | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2012/09/27/scala-ide-versions-are-too-painful/#0001-01-01](https://mdavey.wordpress.com/2012/09/27/scala-ide-versions-are-too-painful/#0001-01-01)

## Scala IDE – Versions are Too Painful

During the last few evenings I’ve been doing some work with Scala.  Initially I started off with [Eclipse](http://scala-ide.org/docs/user/gettingstarted.html) as the IDE of choice.  But after remember how much I dislike Eclipse, I moved over to [IntelliJ](http://www.jetbrains.com/idea/).  I prefer IntelliJ’s refactoring support, but for some reason just found the run/debug particularly painful with Scala, so ended up reverting back to Eclipse.  With [ScalaIDE](http://scala-ide.org/docs/user/gettingstarted.html) installed, and thus Scala 2.9.2, I experienced the frustration of creating a [Maven](http://www.stupiphany.org/?p=10) Scala project, and finding the MySpec test failed to build.  It turned out, either rightly or wrongly, that the solution was to correct 😦 the pom.xml for the scala-library, junit and specs.  [Specs](http://code.google.com/p/specs/) probably being the key, and hence moving to [Specs2](http://etorreborre.github.com/specs2/).  Which leads me to the previously blogged view, IDE’s and versions are still to painful in 2012.  It just shouldn’t be this hard to get an environment running and start development. 😦

If anyone is mildly curious, I’m currently using Scala 2.9.2, JUnit 4.8.1 and Specs2 1.12.1

~ by mdavey on September 27, 2012.

Posted in [Java](https://mdavey.wordpress.com/category/languages/java/)