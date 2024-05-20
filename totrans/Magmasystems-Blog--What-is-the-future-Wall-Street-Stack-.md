<!--yml
category: 未分类
date: 2024-05-18 05:01:41
-->

# Magmasystems Blog: What is the future Wall Street Stack?

> 来源：[http://magmasystems.blogspot.com/2008/06/what-is-future-wall-street-stack.html#0001-01-01](http://magmasystems.blogspot.com/2008/06/what-is-future-wall-street-stack.html#0001-01-01)

Can Microsoft eventually work its way to producing the future Wall Street Stack? A series of components that are tightly integrated and supported. Here is what I imagine:

High speed intelligent message bus (not related to any

Biztalk

technologies) that can transform data directly into .NET objects. The message bus might have some

SQL

-like filtering built into it.

The bus delivers data directly to the Velocity object cache.

Velocity is directly integrated with a

CEP

engine.

When events are detected, some Windows

Workflow

is triggered and monitored.

Velocity and the message bus has built-in, in-process adapters for market data and FIX messages.

Velocity can be hooked into apps through

WCF

for push notifications.

WCF

-based services are available so apps and users can query the state of the cache.

A Service Broker so apps can find out

about

what kind of data is available in the cache.

A monitoring stack is available right out of the box that will monitor the entire stack and alert when abnormal conditions are detected.

How far off can this be, given Microsoft's current and future directions?

©2008 Marc Adler - All Rights Reserved