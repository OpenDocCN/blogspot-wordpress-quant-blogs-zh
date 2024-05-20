<!--yml
category: 未分类
date: 2024-05-18 05:06:17
-->

# Magmasystems Blog: Coral8 Update

> 来源：[http://magmasystems.blogspot.com/2007/11/coral8-update.html#0001-01-01](http://magmasystems.blogspot.com/2007/11/coral8-update.html#0001-01-01)

We are finishing up the first phase of the Coral8 evaluation. This week, I met with Terry Cunningham (who flew his Falcon 10 out to meet us), and I had a great session with Henry, their

pre

-sales engineer. Terry was the creator of Crystal Reports, and later, the head of

Seagate

Software. I always have a soft spot in my heart for a fellow pilot .... even if his plane can go faster and higher than mine!

We validated that Coral8 was putting out the same output as our custom app, and I was enlightened on some of Coral8's capabilities that were not so easy to find in their wads of documentation. Although there is much good in Coral8, there were also some gotchas.

- Documentation needs to be consolidated a bit. There are a lot of separate manuals plus technical articles. There needs to be a "cookbook" on their

CCL

language.

- You cannot test a simple user-defined function without writing an intermediate stream. There is no simple way to dump a variable to the console. In other words, I would like to do this simple thing:

CREATE VARIABLE commission; SET commission = CalculateCommission(); -- this is my user-defined function CONSOLE.WRITE(commission);

- We managed to get the Coral8 Studio to freeze consistently. Luckily, no work was lost. The Coral8 Studio is written using

wxWidgets

, so I wonder how they do unit-testing on the studio.

My opinion is that, although it is great to have the advanced features, you still need to pay attention on the everyday, little tasks that developers need to do. Henry tells me that, in the future, Coral8 will move to a more Visual Studio, file-based way of developing. I certainly welcome this. Henry spent 8 hours watching me drive. When I was having problems, I verbalized the issues so that Henry could see what I was going through and he could bring the issues back to his management.

On the plus side :

- I have been reading about Coral8's pattern matching capabilities. We will definitely be exploring this.

- Coral8 has a relatively inexpensive barrier to entry. If we have a production, development, and COB servers (all dual or quad-core machines), then it won't break our budget.

- Their software does have any time limits on the evaluation versions. One thing that I do not like is a license key that is only good for 30 days. Given the nature of financial companies, we often get pulled into a lot of side projects. I don't want my time to be in the "thick of things", only to find out that the license key elapsed. Coral8 is very friendly to the evaluator.

Now, on to

Aleri

. I will be using their new 2.4 release.

©2007 Marc Adler - All Rights Reserved