<!--yml
category: 未分类
date: 2024-05-18 04:55:52
-->

# Magmasystems Blog: Follow-ups to Some Comments

> 来源：[http://magmasystems.blogspot.com/2009/02/follow-ups-to-some-comments.html#0001-01-01](http://magmasystems.blogspot.com/2009/02/follow-ups-to-some-comments.html#0001-01-01)

Marco says:>> What do you mean by "Entitlements on output events"?

I have blogged about this here before. When our CEP engine generates alerts, we do not want everyone to see them. There might be very few people who can see alerts on orders. Prop traders should not see many of the the alerts that sales traders see. One trading desk might not be able to receive the alerts that another trading desk should see.

We have the concept of coarse-grained and fine-grained alerts. A coarse-grained alert might be filtered out by role. For example, a particular alert should only be seen by a North American Cash Trader, and not by derivative traders. In the case of fine-grained entitlements, we might have to filter by certain data that is within the alert's payload. For example, someone might not be able to see an alert if the symbol is IBM and the volume is greater that 1000 shares.

There is also the matter of entitlements on real-time aggregations, but that is another long topic.

Charlie Skelton from KX says:>> "don't make us code in Q" Please can you elaborate?

Charlie, I have written ad nauseum here about Kdb and Q. I actually started to learn Q a few months ago in order to be able to read some of the code that was thrown our way. I have a greater appreciation of Q than I did a few months ago, but I would not want to ask all of my developers to learn Q.

My opinion is that, if you have a facade (input adapter) to a database, then you should be able to code in some database-agnostic way and leave the db-specific language access to the drivers. Look what you can do with O/R frameworks like Hibernate and iBatis.

Hans asked about Unit Testing

When we first started to use Coral8, we actually wrote a C# application that did the exact same thing as our Coral8 application and we did reconciliations between the two. We had found an issue or two with Coral8, which they were able to fix fairly rapidly. We also found some issues with our Coral8 coding, which helped us learn Coral8 better.

Unit testing is still something that is not mature in our Coral8 processing, although we do have unit tests for our internal framework. We have fabricated data in flat files that we can pump into our C8 engine, and we can do regression testing against a known set of outputs. However, we know that we can do a better job.

I would like to hear more about Streambase's unit testing capabilities.

©2009 Marc Adler - All Rights Reserved.

All opinions here are personal, and have no relation to my employer.