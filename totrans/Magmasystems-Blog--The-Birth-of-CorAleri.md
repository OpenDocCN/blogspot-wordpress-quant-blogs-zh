<!--yml
category: 未分类
date: 2024-05-18 04:55:20
-->

# Magmasystems Blog: The Birth of CorAleri

> 来源：[http://magmasystems.blogspot.com/2009/03/birth-of-coraleri.html#0001-01-01](http://magmasystems.blogspot.com/2009/03/birth-of-coraleri.html#0001-01-01)

 <smarttagtype namespaceuri="urn:schemas-microsoft-com:office:smarttags" name="PlaceType"><smarttagtype namespaceuri="urn:schemas-microsoft-com:office:smarttags" name="PlaceName"><smarttagtype namespaceuri="urn:schemas-microsoft-com:office:smarttags" name="country-region"><smarttagtype namespaceuri="urn:schemas-microsoft-com:office:smarttags" name="place"><smarttagtype namespaceuri="urn:schemas-microsoft-com:office:smarttags" name="State"><smarttagtype namespaceuri="urn:schemas-microsoft-com:office:smarttags" name="City"><smarttagtype namespaceuri="urn:schemas-microsoft-com:office:smarttags" name="address"><smarttagtype namespaceuri="urn:schemas-microsoft-com:office:smarttags" name="Street">It is now March 9^(th), 2009 somewhere in the world. And, the atomic bomb news that I have been mysteriously referring to for the past two weeks is ….

ALERI BUYS CORAL8

Not quaking in your boots? Well, this IS earth-shattering news in the small community of Complex Event Processing. But, you guys were good guessers. No, I am not leaving my company (yet). No, I did not take the CTO position at a Complex Event Processing vendor (none has been offered yet). No, I did not get escorted out off of the trading floor by a gaggle of security guards (yet). No, I didn’t run off to play marimba with Magma.

However, it confirms the predictions of many people in the blogosphere that the consolidation amongst CEP vendors is starting to happen. And, I am sure that this consolidation is not over, both in the CEP space and in the infrastructure space. Already, I am hearing of financial troubles among several of the infrastructure players, and it would be really wise of everyone out there to re-engage your vendors in a little bit of financial due diligence. Make sure that their source code is in escrow …. not that you would ever do anything with it.

I had been predicting that Coral8 would be acquired for quite some time. Terry Cunningham had been personally bank-rolling the company since its inception, and unless Terry went short on the market, I am sure that his portfolio has suffered like the rest of ours. I can only speculate whether financial considerations inspired Terry to sell the company, or whether Terry just got the itch to move on to his next adventure (although he did take the role of Chairman of the new company). To be honest, when I heard that a large database company had purchased a source code license for Coral8, I thought that the end was near for our intrepid band of CEP’ers from <city st="on"><place st="on">Mountain View</place></city>.

My curiosity was aroused when I received a dinner invitation from Terry about two weeks ago. Since I have been burning the midnight oil due to my new role and responsibilities, I politely declined, saying that I was just two exhausted to go out at night and play. However, Terry knew how to appeal to the closet “foodie” in me, and picked a very nice restaurant at

Columbus Circlethat I have only been able to dream about. Imagine my surprise when I got to the restaurant, and found Terry locked arm-in-arm with my other favorite CEO, Don DeLoach of Aleri. I thought that they had united to jointly serve me with the lawsuit that I deserved for publicly taking their products to task on my blog.

(I am taking a bit of literary license here … I actually found out about the merger the night before from another source, so I was not too surprised to see Don there.)

Why did they single me out for such attention? I guess that having a big mouth and a title pays off sometimes. But as a customer of the newly combined company, they wanted to know how a typical customer would react, and what effect the merger might have on us. Would we continue to buy licenses, or would we go running to a competitor? Or, did they want me to give them love and kisses on my blog?

So, in between lot of glasses of wine and a lot of arm-waving on my part, I expressed a number of concerns. But, also, there is lots of goodness in this merger.

There have always been some issues with Coral8\. First and foremost, they had no financial domain expertise. They had attempted to rectify that recently by hiring Colin Clark, but I had my doubts whether that strategy would result in anything concrete. Second, they had no true presence in <state st="on">New York</state>, and if you are going to market to the financial services industry, you have to at least have an office in <city st="on"><place st="on">New York City</place></city>. Third, they had no European penetration<place st="on">, and I could imagine that Apama, Streambase and Aleri were cleaning Coral8’s clock in EMEA. Fourth, they were one of the only CEP vendors who did not have a vertical product for trading or risk, and they really had no intentions of writing one.</place>

Here was this nice 40-person company, sitting in their nice, sunny offices in <city st="on"><place st="on">Mountain View</place></city>, 3000 miles away from their main customer base, without a clue of what the capital markets companies really needed. However, Coral8 is an extremely nice company, very friendly to developers, writing lots of nice white papers, and putting out a good product that was less expensive than all of the other products (except Esper).

Then, there was Aleri. Lots of financial domain expertise, with a few products that were geared towards trading firms. Good European presence. Ex-Bell Labs rocket scientists working in a basement office in Mountainside, right across the street from their old Bell Labs haunts. Not a very developer-friendly company. Very hard to configure the product. Documentation that was not as good as Coral8's (although my last experience with their docs was the old 2.4 version). A better IDE than Coral8, but that’s not saying much as Coral8 has a minimalist IDE. Not very good at testing and QA (based on 2.4 experiences, and some recent feedback from some customers in London). Some sort of real-time OLAP strategy. More adapters geared towards financial services companies.

Now, Aleri has bought all of the assets of Coral8\. What does the combined company have to offer us? It has a European presence, it has financial expertise, it has a good documentation writer, it has a person who knows .NET, it has people who are concerned about compelling visualizations, it has a procedural language called Splash, and it has two engines and two SQL-ish languages. And it has two pricing models, with Coral8 coming in at $15K per core and Aleri costing about $27K per core.

What did you say? Did you say two engines and two languages? What’s a customer to think?

First, let’s tackle the issues of the engineers. You have two very smart teams located on different sides of the <country-region st="on"><place st="on">USA</place></country-region>. Each team is justifiably proud of the CEP engines that they wrote. One engine came out of a <place st="on"><placename st="on">Stanford</placename> <placetype st="on">University</placetype></place> research group, and the other engine came out of a commercial effort from Bell Labs. (Correction: the engine is not the same one that they developed at Bell Labs.) Eventually, the combined CorAleri is going to have to choose one language and one engine. So, you will have two sets of development teams positioning themselves as the winner of the language and engine competition.

Every customer of Coral8 MUST program the engine in CCL, which is Coral8’s SQL-like language. However, even though Aleri supports an SQL language, almost nobody uses it, as the Aleri IDE does not support it. (The Aleri IDE likes to generate XML-based code.) Let’s assume that Coral8 wins the language and engine competition. However, in my vision, Aleri gets their licks in when CCL is supplemented with the Splash language.

So, in my ideal world, the language of CorAleri would be CCL with some Splash. And, since the language and the engine are linked tightly, Coral8 keeps the engine as well. However, Aleri would help the Coral8 engine team to make their engine even faster.

At first, CorAleri will have to support two engines and two languages. But, the longer you postpone the single-engine strategy, the more time you give the Coral8 and Aleri engineers to improve their individual engines in order to win the engine competition. Then, it becomes more difficult to have a single-engine strategy.

Don and Terry talked about a single product that includes BOTH engines. The Aleri engine would be the “performance engine” and the Coral8 engine would be the “deterministic engine”. If you check a certain checkbox, “stuff” would be sent to the Coral8 engine and if you check another checkbox, “stuff” would be sent to the Aleri engine.

You cannot have two engines running simultaneously on a single server. They would be competing for resources. We have to worry about administering another process on our servers. We wouldn’t be sure which engine was handling what. It makes monitoring more difficult.

If you give a customer too many choices, then the customer might get confused. Customers want transparency and simplicity. If you confuse a customer, then that customer might change over to a CEP vendor who offers a simpler solution. This means that a confused customer might run over to Apama or Streambase.

CorAleri must come up with a solid roadmap about the merging of the languages and engines, and they must make this roadmap available to customers.

We do not want to take 25% of each sprint to play catch-up on a moving target. The worst thing for us is to be surprised. With each release of the new CorAleri engine and language, we want the migration effort to be painless. We want to change as little of our existing CCL scripts as possible, and we don’t want to find that queries that previously worked do not work anymore.

To me, this is the greatest challenge to CorAleri and the greatest risk to us.

I would like to see the engine and language and the documentation stay with the <city st="on"><place st="on">Mountain View</place></city> folks. What would the Aleri folks do? They could concentrate on writing more adapters, work on integration with other partners (ie: Netezza, Gemfire, RTI, etc), come up with a better IDE with debugging a monitoring support, come up with more Jack Rusher-type visualizations, real-time OLAP and analytics, and develop some more financial apps. This would give a clear line of separation of duties between the two development teams.

In summation, there is a lot to be excited about, but there is also risk that is associated with confusion.

I wish CorAleri good luck. They have some really good people. They have a sense of integrity. They have a new sense of purpose. And, if they could come up with a unified roadmap that makes sense, then it would be a company to be reckoned with in the CEP marketplace.</smarttagtype></smarttagtype></smarttagtype></smarttagtype></smarttagtype></smarttagtype></smarttagtype></smarttagtype>