<!--yml
category: 未分类
date: 2024-05-18 04:59:17
-->

# Magmasystems Blog: Optimizing Performance in a CEP System

> 来源：[http://magmasystems.blogspot.com/2008/09/optimizing-performance-in-cep-system.html#0001-01-01](http://magmasystems.blogspot.com/2008/09/optimizing-performance-in-cep-system.html#0001-01-01)

Here are some lessons learned that helped us reduce message backup from our

Tibco

EMS broker into our

CEP

Input Server.

1) Make sure that you have fast networking between the

Tibco

broker and your servers.

We just happened to find out that the hardware folks gave us legacy 100MB connections between our

Tibco

EMS broker and our

CEP

Input Server. We asked them to upgrade us to

GigE

immediately. Unless you have personally installed your hardware, never assume anything in your infrastructure.

2) It might be helpful to turn the "

AutoAcknowledge

" flag off in your

Tibco

session.

To do this, change

this.m_connection.CreateSession(false, SessionMode.AutoAcknowledge);

to

this.m_connection.CreateSession(false, SessionMode.NoAcknowledge);

Be careful about using No

Acks

. What is the impact to your

CEP

system if you happen to drop a message?

3) Implement threaded queues on the input from

Tibco

to your input server, and on the output from your input server to the

CEP

system.

If you need more performance, change the single threaded queue that reads messages from

Tibco

to a load-balanced multiple queues, each with its own thread. The load

balancer

can partition by

Tibco

topic, by ticker, or by

OrderId

.

Of course, you can always use the built-in adapters from your

CEP

vendor. But that may come at an extra monetary cost, so check with your

CEP

vendor to see if a certain input adapter comes free of charge. Also, the more of the

CEP

vendor's infrastructure you use, the more it ties you into the

CEP

vendor.

4) Try to do some

pre

-filtering of messages in your input server before passing them on to the

CEP

engine.

Recently, we were able to reduce the CPU usage of Coral8 by about 50% (according to our Coral8 guy) by filtering out FIX messages that we knew that Coral8 was not interested in.

5) Continually optimize your code. Just this morning, I did a code review of the input server, and I was able to suggest a change which reduced one

hashtable lookup

on each FIX message. I know that there are tons of other places in our code that can do with some optimization. If you need to parse FIX messages into C# objects, then do some investigation and benchmarking of FIX engines.

6) Use the Server Garbage collector

©2008 Marc Adler - All Rights Reserved.

All opinions here are personal, and have no relation to my employer.