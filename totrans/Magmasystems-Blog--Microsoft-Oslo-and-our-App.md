<!--yml
category: 未分类
date: 2024-05-18 04:58:28
-->

# Magmasystems Blog: Microsoft Oslo and our App

> 来源：[http://magmasystems.blogspot.com/2008/10/microsoft-oslo-and-our-app.html#0001-01-01](http://magmasystems.blogspot.com/2008/10/microsoft-oslo-and-our-app.html#0001-01-01)

For some reason, Microsoft seems to think that I am an "

influencer

" in Wall Street, and that plying me with large steaks and bottles of wine will make me happy (they are certainly correct in the second assumption).

Last night, I had a very nice dinner with Robert

Wahbe

and Steven Martin of Microsoft. They are large in the Connected Systems Division, which is the group that is overseeing the development of the mysterious Microsoft Oslo product/framework. We had a happy group that included the famous

DonXML

, Ambrose from

Infragistics

, Bill Zack, and a charming lady from Waggoner

Edstrom

whose job it was to make sure that Robert and Steven did not disclose too many of Microsoft's secrets (although I ended up telling them a few little ditties about Microsoft that they were not aware of!).

I have been sworn to secrecy, so I am going to regurgitate what little known facts about Oslo has been leaked out through various blogs. Oslo contains three things:

1) A new language that enables you to create your own Domain-Specific Languages (

DSL

).

2) A visual modeling tool.

3) A repository for models that you build.

What would we do with Oslo in our

CEP

system?

We would like our traders to be able to eventually build their own queries/models, and "inject" them into our

CEP

system. We do not want the traders coding in Coral8's

CCL

or any other streaming

SQL

language for that matter. And, we want the traders to play in our "sandbox" without hurting themselves or the other users of the system.

If we could create a high-level

DSL

that, through the use of some sort of "adapter", was translated into Streaming

SQL

, then we could give that to the traders. A visual modeling tool would allow them to easily

construct

models (remember how enthusiastic I was

about

Yahoo Pipes a few months ago?).

Let's see what Microsoft comes up with, and how soon it will be until Oslo is ready to use on a trading floor.

©2008 Marc Adler - All Rights Reserved.

All opinions here are personal, and have no relation to my employer.