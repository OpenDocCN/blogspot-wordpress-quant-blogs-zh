<!--yml
category: 未分类
date: 2024-05-18 05:37:56
-->

# Adopting Microservices – Part 2 | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2015/11/17/adopting-microservices-part-2/#0001-01-01](https://mdavey.wordpress.com/2015/11/17/adopting-microservices-part-2/#0001-01-01)

## Adopting Microservices – Part 2

I’ve been meaning to get around to reading [Building Microservices](http://www.amazon.co.uk/Building-Microservices-Sam-Newman/dp/1491950358) for sometime.  After carrying the book on too many flights, and not having the time to actually open the cover, I can finally provide my notes:

*   Page 2 – “Small, and Focused on Doing One Thing Well” – great description of what is important.  However, I fear that “small” will be over played 😦
*   Page 17 – Coding Architect – could not agree more
*   Page 22 – [DropWizard](http://www.dropwizard.io/0.9.1/docs/) and [Karyon](https://github.com/Netflix/karyon) – Netflix rules these days 🙂
*   Page 31 – Nice to see Eric Evan’s Domain-Drive Design referenced.  Not enough people are aware of this pattern in my view.
*   Page 33 – Be conscious of splitting out microservices too quickly!
*   Page 45 – Choreographed and events
*   Page 51 – [HATEOAS](https://en.wikipedia.org/wiki/HATEOAS)
*   Page 57 – “Back to 2006”  😉 Long time.  Think we were both there at that very bank
*   Page 59 – Client Library – Netflix likes the ideas, others may not.
*   Page 62 – Versioning.  A topic that will always generate a lot of discussion, and can lead to a lot of pain if the strategy is wrong
*   Page 79 – “Splitting the Monolith”.   I suspect there are a large number of software engineers/architects today looking for direction on splitting their monolith applications into microservices.  Always a hot topic 🙂
*   Page 111 – Deployment, and the usual suspects – Chef, Puppet and Ansible.
*   Page 126 – Docker – almost mandated in any book these days.
*   Page 131 – Testing.  Did I miss a BDD reference in this chapter?
*   Page 151 – Non-functional.  Agreed, Cross-functional requirements (CFR) is sharper.
*   Page 162 – Correlation IDS – all to often forgotten until the functionality hits production, and support.
*   Page 240 – Eureka

~ by mdavey on November 17, 2015.

Posted in [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)
Tags: [Microservices](https://mdavey.wordpress.com/tag/microservices/)