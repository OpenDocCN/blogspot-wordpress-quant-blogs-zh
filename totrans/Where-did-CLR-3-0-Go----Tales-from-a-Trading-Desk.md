<!--yml
category: 未分类
date: 2024-05-18 06:08:30
-->

# Where did CLR 3.0 Go? | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2008/11/12/where-did-clr-30-go/#0001-01-01](https://mdavey.wordpress.com/2008/11/12/where-did-clr-30-go/#0001-01-01)

## Where did CLR 3.0 Go?

The [PDC](http://coolthingoftheday.blogspot.com/2008/10/pdc2008-quick-video-link-list.html) provide us with [CLR 4.0](http://channel9.msdn.com/pdc2008/PC49/) – a push for an environment that works together, faster with less bugs. It’s clear from the presentation that .NET just seems to be accelerating away from what Sun is doing in the Java JVM space. Here are a few highlights:

*   [Contracts](http://channel9.msdn.com/pdc2008/tl51/) – [Contracts](http://blogs.msdn.com/bclteam/archive/2008/11/11/introduction-to-code-contracts-melitta-andersen.aspx) was bound to turn up at some point in .NET given the MSR [Spec#](http://research.microsoft.com/SpecSharp/) project
*   Tuple support – This should keep the Python [fans](http://etrading.wordpress.com/) happy 🙂
*   GC Enhancements – workstation has a new background collection feature, server has Gen 2 notification
*   Corrupted State Exception
*   Threading, Parallel, Core enhancements – Parallel Extensions and ThreadPool
*   [Profiling](http://blogs.msdn.com/davbr/archive/2008/11/10/new-stuff-in-profiling-api-for-upcoming-clr-4-0.aspx)

Off topic:

*   Silverlight [Testing](http://www.jeff.wilcox.name/2008/11/04/test-framework-source/) Framework
*   If you still don’t get Oslo, [this](http://blogs.msdn.com/mllopis/archive/2008/11/07/pdc-2008-sessions-about-oslo.aspx) maybe a worthwhile read.
*   [Oslo](http://www.betanews.com/article/Microsofts_Burley_Kawasaki_How_modeling_will_change_programming/1226357640) Tutorials – [here](http://blog.devarchive.net/2008/11/generating-code-using-ms-codename-t4.html) and [here](http://blog.codeslower.com/2008/11/Exploring-Oslo-Using-Mg-to-Define-a-To-Do-Language)
*   CCR & DSS Case [Studies](http://www.microsoft.com/ccrdss/#CaseStudies) – what $399.95 USD gets you
*   Microsoft has [two](http://www.infoworld.com/article/08/10/31/microsoft-azure-cloud-qa_1.html) hypervisors
*   [F#](http://www.ffconsultancy.com/products/fsharp_for_scientists/?fsb) @ [PDC](http://channel9.msdn.com/pdc2008/TL11/)
*   [Prism 2.x](http://blogs.msdn.com/blaine/archive/2008/11/10/prism-2-0-drop-available-on-codeplex.aspx) to support Silverlight?
*   With the improvements in [WF4](http://channel9.msdn.com/pdc2008/TL17/), should I now consider it for a trade ticket UI with workflow dependencies between UI components?
*   Covariance and [Contravariance](http://blogs.msdn.com/charlie/archive/2008/10/28/linq-farm-covariance-and-contravariance-in-visual-studio-2010.aspx) in C# 4.0
*   CEP [presentations](http://www.thecepblog.com/2008/11/03/twenty-two-cep-public-presentations-on-slideshare/) (24)

~ by mdavey on November 12, 2008.

Posted in [.NET](https://mdavey.wordpress.com/category/languages/net/)
Tags: [Microsoft](https://mdavey.wordpress.com/tag/microsoft/)