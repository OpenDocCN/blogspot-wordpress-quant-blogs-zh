<!--yml
category: 未分类
date: 2024-05-18 05:03:00
-->

# Magmasystems Blog: More Cloudy Thoughts

> 来源：[http://magmasystems.blogspot.com/2008/04/more-cloudy-thoughts.html#0001-01-01](http://magmasystems.blogspot.com/2008/04/more-cloudy-thoughts.html#0001-01-01)

It seems that my inelegance in describing my idea of the event cloud has spurred some debate between Greg and Hans. I am going to try to clarify my thoughts around the event cloud, and see if it makes more sense.

I don’t want to give any of our “secret sauce” away in my postings, so I will try to map my thinking from the Equities Trading domain to another domain that I am not familiar with …. The domain of building security. (Apologies in advance to all of the sleuths who are reading this. My use cases will probably malign your esteemed field of study.)

Let’s say that we are writing an enterprise-wide CEP application for our MegaBank that will monitor our security system so that those nosey parkers from StanLehGoldBar Inc don’t break into our building and steal our secrets.

We are going to make the distinction between

**Atomic Events**

and

**Derived Events**

. A Derived Event is generated when something interesting is detected from the monitoring of one or more atomic events.

An atomic event may be saved in our CEP engine, depending on the use case. A derived event will be definitely be saved by our CEP system. Since a derived event represents an “interesting” condition, we may want to do reporting and analysis on derived events. We may also want to do some sophisticated searching of our derived events. In my mind, the persisted atomic and derived events form our event cloud.

Two or more derived events can be combined to form a new derived event. A derived event can be combined with an atomic event to form a new derived event. Let me illustrate this.

We have a lot of atomic events that come through our CEP system. Every person that passes through MegaBank’s doors generates a

**PersonEnteredBuilding**

atomic event. (This is analogous to a market data event.) We have a static database of all of MegaBank’s employees, and when the person in a

**PersonEnteredBuilding**

event does not match an entry in our employee database, the CEP system generates a

**NonEmployeeEntered**

derived event. This derived event will be persisted in our CEP engine.

We also have a derived

**PersonLeftBuilding**

event generated whenever a person leaves the building. This event is generated

(Let’s fantasize a bit, and assume we do a retina scan of everyone entering the building. Let’s stretch our imaginations a bit and say that we have a retina scan of all StanLehGoldBar Inc employees)

Let’s say that we do a join between a

**NonEmployeeEntered**

event and the static source of StanLehGoldBar employees. We can generate a

**CompetitorInBuilding**

derived event. This derived event will be saved in the CEP engine too.

We monitor all doors to our building. Whenever someone goes through the doors of the Equities trading floor, we generate a

**TradingFloorEntered**

atomic event. If someone goes through the trading floor doors for the first time of the day after 6:00 PM, we might want to consider that action to be a suspicious activity, and we want to generate a

**PossibleIntruderOnTradingFloor**

derived event.

Now, some smart security guard who is a user of our CEP system wants to create a new derived event. He wants to see if we have a competitor roaming around our Trading Floor at night. So, the security guard goes into our CEP GUI and creates a new, custom derived event called CompetitorOnTradingFloorAfterHours that gets generated 1) if we have a

**CompetitorInBuilding**

derived event 2) that does not have a “cancelling”

**PersonLeftBuilding**

event, 3) combined with a

**PossibleIntruderOnTradingFloor**

event. The fact that various events are “floating” around our event cloud makes it possible to easily create new derived events on the fly.

The security guard might also want to do a query of our event cloud to see if the competitor was “casing the joint” prior to the intrusion into the trading floor at night. The security guard might want to see how many times that particular competitor visited MegaBank over the past month. He might want to see how many times the competitor visited the trading floor during normal business hours. This sounds like the kind of query that you would do with a Data Warehouse, not a CEP engine.

So, we need to be able to represent the event cloud in an efficient way in the CEP engine. We need to be able to create new derived events dynamically, while the CEP engine is running. We need to be able to do ad-hoc analysis of the event cloud to improve our situational awareness. We need to be able to create new and interesting visualizations that let the user peek into what is going on inside the cloud.

Interesting stuff, right?

Tim Bass gives a list of techniques that can be used to perform analysis of events. These techniques include:

*   Rule-Based Inference

*   Bayesian Belief Networks (Bayes Nets)

*   Dempster-Shafer’s Method

*   Adaptive Neural Networks

*   Cluster Analysis

*   State-Vector Estimation

I have to admit that I have not delved into these areas before. However, we just hired someone with a BioInformatics background who we hope could do this stuff in his sleep. Who would have thought that, working for MegaBank, I would be exposed to such interesting areas of study?

©2008 Marc Adler - All Rights Reserved