<!--yml
category: 未分类
date: 2024-05-18 04:57:18
-->

# Magmasystems Blog: Followup to "Do you need a Commercial CEP System?"

> 来源：[http://magmasystems.blogspot.com/2008/11/followup-to-do-you-need-commercial-cep.html#0001-01-01](http://magmasystems.blogspot.com/2008/11/followup-to-do-you-need-commercial-cep.html#0001-01-01)

Richard Bentley of

Apama

has a

[great post](http://apama.typepad.com/my_weblog/2008/11/fx-a-cep-succes.html)

in which he details the various uses of

Apama

in a number of financial companies. Richard's post and Tim Bass's

[companion post](http://www.thecepblog.com/2008/11/15/will-commercial-cep-engines-replace-algorithmic-trading-platforms/)

are two additional ways of thinking about the viability of commercial

CEP

engines.

My previous post concluded that

1) If I had a large team of developers, AND I had a number of

pre

-written frameworks that provided input and output adapters, AND I had a relatively easy use case (

ie

: simple aggregations, simple pricing, etc), AND if there was no existing vendor solution, then I would prefer to write everything ourselves. (All four conditions need to be satisfied.) I would choose this path because it gives us the maximum amount of control over the engine.

2) If I had a small team of developers, and money was no object, and if there was no existing vendor solution, then I would purchase a

CEP

engine from a vendor. If money was tight, I would probably opt for

Esper

. I would have to balance my budget with the lost opportunity cost. If the opportunity cost was a lot greater, then I might go for a vertical

CEP

application, if one existed.

If I needed an

algo

trading application and a

generc CEPengine

, why not use

Apama

?

Apama

has been in a sweet spot for a long time, and Richard Bentley has seen the fruits of this. They have offered a generic

CEP

solution for a while, but their claim to fame is that people like John Bates and Mark Palmer helped to create a trading-solution-in-a-box. When I hear people at my firm talk about

Apama

, they talk about it as if it were its own class of applications, much in the way people refer to Ketchup now instead of

Catsup

. They don't even know that

Apama

is related to

CEP

.

Where do I think the future of

CEP

lies? In building blocks that you can choose from in order to create applications. A risk management block, an

algo

trading block, a pricing block, a FIX processing block, a market surveillance block. These might be sold like

Legos

. You choose an

algo

trading block, which comes with the engine,

pre

-written code, a market data adapter of your choice, and a FIX adapter. You can snap in a risk management block. You can snap in a P&L block. All of these blocks come with source code so that you can tune them.

These

pre

-written blocks will have been written, tuned, and verified by the vendor. There would be less of a chance of a developer struggling with Streaming

SQL

.

This is something that I always thought would be done by an enterprising third party. However, the vendors themselves are moving in this direction. They are all trying to catch up to

Apama

in the financial arena, while trying to maintain their excellence in their offering of a general purpose

CEP

engine.

So far, I have selfishly focused on financial applications. However, there are many

CEP

applications in other industries, like gaming, transportation, and defense. All of them share the same characteristics. Monitor a bunch of real-time actions and warn when a certain condition is true. So, a generic surveillance block would be great. The surveillance block might come with a choice of adapters for the most popular sensors . (Tim Bass can tell me if I have been smoking crack here.)

It may be very difficult to come up with an "application block" that will solve all facets of a domain correctly. Can you come up with a risk management app block that can be used right out of the box? Probably not. However, a thoughtful architecture, combined with lots of market research, and combined with lot of extensibility points in the application block, will probably go a long way. In that sense, the vendors should look at how Microsoft

architected

their

[Enterprise Application Blocks](http://msdn.microsoft.com/en-us/library/cc467894.aspx)

.

©2008 Marc Adler - All Rights Reserved.

All opinions here are personal, and have no relation to my employer.