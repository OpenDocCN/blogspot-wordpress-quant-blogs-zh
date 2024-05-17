<!--yml
category: 未分类
date: 2024-05-18 06:31:03
-->

# Book: Akka Essentials | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2013/01/14/book-akka-essentials/#0001-01-01](https://mdavey.wordpress.com/2013/01/14/book-akka-essentials/#0001-01-01)

## Book: Akka Essentials

Over the last few years the has been a renewed interested in the actor pattern.  In the Microsoft stack, both Microsoft and MSR have provide extensions to .NET to leverage the actor model.  Likewise, in the Java/Scala stack, [akka](http://akka.io/) and Typeseafe has gained some traction, with akka 2.1.0 recently release.  Within the financial version, the actor model is of considerable interested due to the complexity of the systems that are developed within both the sell-side and buy-side.  [Akka](http://www.amazon.co.uk/Akka-Essentials-Munish-Kumar-Gupta/dp/1849518289) [Essentials](http://www.packtpub.com/akka-java-applications-essentials/book) has therefore hit the shelves (for anyone who still buys a physical book) at the right time – especially if scroll down to the lower section of the akka home page, and view the list of “selection of production users” – UBS and Credit Suisse.

So to follow the historical format of book reviews used by this blog:

*   Jonas Boner was a reviewed 🙂
*   Page 10, “The JEE programming model of writing distributed applications is not the best fit for a scale-out application model”.  Classic statement.
*   Page 11, actor principles
*   Page 30 and 46.  Java and Scale version of the same sample application.  Although Scala is in my view the preference for development, so of us have to live in the Java world during our day jobs.  Is Java the Cobol of the 21st Century?
*   Page 74.  Ability to swap and actors message loop functionality at run-time
*   Page 90\. Supervisors strategy
*   Page 97.  Dispatchers via java.util.concurrent
*   Page 123.  Let it crash paradigm!  Its important to consider machine failure when deciding on supervision and monitoring.
*   Page 171.  The age old money account transfer problem, but using STM’s
*   Page 248.  Typesafe Console.  If you haven’t fired up the console, read this chapter, and then think again.

So to summaries, if you are looking to leverage akka in an up and coming projects, Akka Essentials is worth a read.  It should be noted that Akka 2.1.0 ([Coltrane](http://doc.akka.io/docs/akka/2.1.0/cluster/cluster-usage-java.html)) provides experimental cluster support, which is key to building production ready Akka solutions, and thus isn’t covered in Akka Essentials.

~ by mdavey on January 14, 2013.

Posted in [Java](https://mdavey.wordpress.com/category/languages/java/)