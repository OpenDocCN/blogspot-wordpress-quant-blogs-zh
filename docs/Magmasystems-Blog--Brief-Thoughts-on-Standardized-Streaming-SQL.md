<!--yml

category: 未分类

date: 2024-05-18 04:59:45

-->

# Magmasystems Blog: Brief Thoughts on Standardized Streaming SQL

> 来源：[`magmasystems.blogspot.com/2008/08/brief-thoughts-on-standardized.html#0001-01-01`](http://magmasystems.blogspot.com/2008/08/brief-thoughts-on-standardized.html#0001-01-01)

我已经有几个星期没有写博客了，因为我度假了两个星期（旧金山，温哥华，惠斯勒，

Banff

) and in between that, I have been bogged down with all of the paperwork at my job, including doing budget planning for 2009\. Let me tell you that, in this current economic environment, budget planning is a very interesting and challenging exercise. (The best strategy for dealing with budget time is to take your favorite managing director on the business side out to

[The Brandy Library](http://www.brandylibrary.com/)

, make sure he gets all liquored-up, and make him sign off on your budget after his 5th

[Highland Cooler](http://brandylibrary.com/sections2007/menus/wcocktailsmenu.pdf)

.)

Also, I have been a bit turned off by all of the recent in-fighting that has been occurring on the

CEP

-相关博客。似乎有人发表意见，然后两三位知名评论家在自己的博客上开始反驳，这导致一系列（有时是友好的）争吵。就像最近在美国的民主党和共和党大会一样，我希望

Gartner CEP

Summit in two weeks will be a big love fest, and that the pundits will make peace with each other for a week or two.

I read with great amusement the recent announcement of Oracle and

Streambase

getting together and attempting to define a new standard for Streaming

SQL

. Some things that immediately crossed my mind were:

1)

Streambase

and Oracle are presenting their paper at the

VLDB

conference. The

[list of presentations](https://www.cs.auckland.ac.nz/research/conferences/vldb08/index.php/Accepted_Papers)

is very impressive. Notice the number of papers that Microsoft is presenting, which leads me to hope that some very interesting stuff will be coming down the pike from

MSFT

. I wish that I could attend the tutorial on "Detecting Clusters in Moderate-to-High Dimensional Data: Subspace Clustering, Pattern-based Clustering, and Correlation Clustering".

2) Mark Palmer, who railed against Streaming

SQL

for such a long time in favor of

Apama's

more procedural language, now has to publically support the effort to standardize Streaming

SQL

. I wonder how much of

Apama's

language will appear in the standardized language.

3) There are other efforts at standardization underway.

Opher Etzion

is involved in one of them. I am not sure if

Opher's

efforts are aimed at solely defining a meta-language for events, or if what he is working on is in direct competition to the

Streambase

/oracle effort.

4) How willing will

Aleri

，

Apama

, and Coral8 be in adopting this effort? In particular,

Aleri

由于他们的过程式

FlexStream

语言为开发者提供了一个过程式的“出口”，从

SQL

基于语言的程序。

Apama

他们为自己的类似 Java 的语言感到自豪。

5) 如果微软有一天也加入其中，会有什么后果呢？你知道微软会把任何在该领域的努力与

LINQ

联系起来。

Aleri

也正在转向一个更

LINQ

以一种类似的方式做事。当然，人们可以编写一个

LINQ

流式数据提供商

SQL

，但有人会被激励去这样做吗？

（更新：感谢一位不愿透露姓名的读者... Streambase/Oracle 论文位于

[在这里](http://www.cs.brown.edu/%7Eugur/streamsql.pdf)

）

----------------------

另而言之，祝 Colin Clark 好运，他已经离开了

Streambase

像他加入一样快地离开。Colin 看起来他正在独自一人作为独立顾问出去闯荡。Colin 刚刚有了他的第一个孩子，所以这对他来说一定是一个特别有趣的时候。这让我想起我自己的故事，在 1988 年，我正在等待我的抵押贷款申请时，为了独自出去闯荡而辞去了高盛的咨询工作。当你得到创业的热情时，没有什么能阻止你....

©2008 Marc Adler - 版权所有。

这里的所有观点都是个人的，与我的雇主无关。
