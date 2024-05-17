<!--yml
category: 未分类
date: 2024-05-18 05:07:35
-->

# Magmasystems Blog: Thoughts about CEP Patterns

> 来源：[http://magmasystems.blogspot.com/2007/09/thoughts-about-cep-patterns.html#0001-01-01](http://magmasystems.blogspot.com/2007/09/thoughts-about-cep-patterns.html#0001-01-01)

One of the things that I have been wondering about:

How do you do transactions in the context of event processing? For example, if I get an event, we might trigger some units-of-work and generate some more derived events from this initial event. These derived events might be put into the event cloud.

If one of the units-of-work fail, how do we rollback the "transaction"? Do we need to define compensating events? Do we need to suck the derived events out of the event cloud? Do we need to attach "state" to the derived events which signal whether they are part of a transaction?

We run into a lot of the same issues here that DBMS vendors have run into. How can the transactions patterns in the DBMS world be applied to CEP?

Another thing I have been interested in is the generation of recursive events. If I get an event and generate a derived event, how do I know that this derived event will not result in recursion? Again, DBMS vendors have run into the same situation with database triggers, and some lessons can be learned.

So, does this mean that we are better off considering a CEP vendor who has roots in the DBMS world?

(As you can see, I am just using the blog as scatchpad for some thoughts .... but it gives you an idea about the things that any of you who are implementing CEP might have to consider...)

©2007 Marc Adler - All Rights Reserved