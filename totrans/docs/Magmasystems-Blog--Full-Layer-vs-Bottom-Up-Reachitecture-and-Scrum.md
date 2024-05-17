<!--yml
category: 未分类
date: 2024-05-18 05:22:41
-->

# Magmasystems Blog: Full-Layer vs Bottom-Up Reachitecture and Scrum

> 来源：[http://magmasystems.blogspot.com/2005/11/full-layer-vs-bottom-up-reachitecture.html#0001-01-01](http://magmasystems.blogspot.com/2005/11/full-layer-vs-bottom-up-reachitecture.html#0001-01-01)

**Mission**

To reengineer a credit derivates trading system using Scrum. (30-day sprints)

**Findings**

The existing application is somewhat monolithic, with direct database access from the UI layer, and business rules embedded in the UI.

**Things to consider** 

1) The users want to see

***visible***

functionality after each sprint. We need to rearchitect, but our refactoring must not affect the current UI.

2) We need to implement new structured products after the 3rd sprint.

**Question***Would you rearchitect from the bottom up and devote each sprint to deliver a fully-tested foundation layer, working your way up until you hit the UI layer? Or, would each sprint consist of implementing the entire stack with ever-increasing functionality?*

I would love to hear your opinions.

©2005 Marc Adler - All Rights Reserved