<!--yml
category: 未分类
date: 2024-05-18 04:59:45
-->

# Magmasystems Blog: Brief Thoughts on Standardized Streaming SQL

> 来源：[http://magmasystems.blogspot.com/2008/08/brief-thoughts-on-standardized.html#0001-01-01](http://magmasystems.blogspot.com/2008/08/brief-thoughts-on-standardized.html#0001-01-01)

I haven't blogged for a few weeks because I am been on vacation for two weeks (San Francisco, Vancouver, Whistler,

Banff

) and in between that, I have been bogged down with all of the paperwork at my job, including doing budget planning for 2009\. Let me tell you that, in this current economic environment, budget planning is a very interesting and challenging exercise. (The best strategy for dealing with budget time is to take your favorite managing director on the business side out to

[The Brandy Library](http://www.brandylibrary.com/)

, make sure he gets all liquored-up, and make him sign off on your budget after his 5th

[Highland Cooler](http://brandylibrary.com/sections2007/menus/wcocktailsmenu.pdf)

.)

Also, I have been a bit turned off by all of the recent in-fighting that has been occurring on the

CEP

-related blogs. It seems that one person posts an opinion, then two or three of the well-known pundits start a counter-argument on their own blogs, which leads to a spiral of (sometimes good-natured) venom. Just like the recent Democratic and Republican conventions in the United States, I am hoping that the

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

,

Apama

, and Coral8 be in adopting this effort? In particular,

Aleri

has a richer programming environment because of their procedural

FlexStream

language that gives developers a procedural "out" from the

SQL

-based language.

Apama

prides themselves on their Java-like language.

5) What happens if Microsoft ever weighs in with something of their own? You know that Microsoft will tie any effort in this area in with

LINQ

.

Aleri

is also moving to a more

LINQ

-like way of doing things. Of course, one can write a

LINQ

provider for Streaming

SQL

, but would anyone be motivated to do so?

(Update: Thanks to a reader who does not wish to be identified... the Streambase/Oracle paper is located

[here](http://www.cs.brown.edu/%7Eugur/streamsql.pdf)

)

----------------------

On another note, good luck to Colin Clark, who has left

Streambase

as quickly as he joined them. Colin looks like he is striking out on his own as an indie consultant. Colin just had his first child, so this must be an especially interesting time for him. It reminds me a bit of my own story when , in 1988, I quit consulting for Goldman Sachs while my mortgage application was pending in order to strike out on my own. When you get the entrepreneurial fever, nothing can stop you ....

©2008 Marc Adler - All Rights Reserved.

All opinions here are personal, and have no relation to my employer.