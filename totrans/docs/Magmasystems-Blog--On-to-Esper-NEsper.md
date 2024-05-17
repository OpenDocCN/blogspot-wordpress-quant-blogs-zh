<!--yml
category: 未分类
date: 2024-05-18 05:06:02
-->

# Magmasystems Blog: On to Esper/NEsper

> 来源：[http://magmasystems.blogspot.com/2007/12/on-to-espernesper.html#0001-01-01](http://magmasystems.blogspot.com/2007/12/on-to-espernesper.html#0001-01-01)

I have had to expand the CEP evaluation process. I am going to start looking at NEsper, and maybe, Apama (after some recommendations by some of our Asia folks who seemed pleased at Apama's performance over heavy loads).

I just downloaded NEsper and I am starting to go over some of the docs. I am sure that Thomas and Aaron will correct me if I say anything incorrect about Esper. Two things stand out about the Esper offering:

1) No GUI Builder or visual tools, probably because .....

2) Esper/Nesper is a component designed to be incorporated into your application ... in other words, it is treated as a third-party .NET assembly, just like things like Syncfusion, Log4Net, etc.

So, unlike Coral8, where you run a separate Coral8 server process, you need to write an application that "contains" Esper/NEsper. While this solution does not favor quick, out-of-the-box prototyping as Coral8 does, it gives you more control over the CEP actions. Everything with Esper/Nesper is "in-process" to your application.

Also, Esper/Nesper is Open Source. I downloaded it, and I have the full source code sitting on my hard drive. I have to talk to the financial guys at my company, but I don't think that we would have to do the amount of financial due dilligence with an Open Source effort as we would with a company who does not follow the Open Source model. Maybe we will have to count the number of moths that fly out of Thomas' wallet.

©2007 Marc Adler - All Rights Reserved