<!--yml
category: 未分类
date: 2024-05-18 05:35:41
-->

# Error Model Reading | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/03/14/error-model-thoughts/#0001-01-01](https://mdavey.wordpress.com/2016/03/14/error-model-thoughts/#0001-01-01)

## Error Model Reading

It’s taken me a while to get round to reading Joe Duffy’s Error Model [article](http://joeduffyblog.com/2016/02/07/the-error-model/) – mainly due to the length of the article 🙂  However, like most things Joe write, its full of useful information.

Principles at the beginning of the article appropriately sets the stage for the reminder of the article.  A number of people could learn a lot from Joe’s writing style and format.  Context is key.

Its nice to see a lot of references to the Go language through the article.  Also, the “Let it crash” and Netflix’s Chaos Monkey references 🙂 in the Reliability, Fault-tolerance, and Isolation section 🙂

The “lightweight nature of Midori processes” seems to have been a key design decisions.  In many ways its sad that Midori never saw the light of day outside of Microsoft

> Despite us beginning with Singularity, which used Sing#, a variant of Spec#, we quickly moved away to vanilla C# and had to rediscover what we wanted. We ultimately ended up in a very different place after living with the model for years.

If you don’t have time to read the full article, then at least read the Retrospective and Conclusions 🙂  Microsoft Edge took advantage of abandonment in a few areas based on the Midori work, coupled with consideration to bring contracts to C++.

~ by mdavey on March 14, 2016.

Posted in [Languages](https://mdavey.wordpress.com/category/languages/)