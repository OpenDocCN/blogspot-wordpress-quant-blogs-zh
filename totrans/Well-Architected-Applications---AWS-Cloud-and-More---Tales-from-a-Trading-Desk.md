<!--yml
category: 未分类
date: 2024-05-18 05:34:15
-->

# Well-Architected Applications – AWS Cloud and More | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/04/13/well-architected-applications-aws-cloud-and-more/#0001-01-01](https://mdavey.wordpress.com/2016/04/13/well-architected-applications-aws-cloud-and-more/#0001-01-01)

## Well-Architected Applications – AWS Cloud and More

Although “AWS [Well-Architected](https://d0.awsstatic.com/whitepapers/architecture/AWS_Well-Architected_Framework.pdf) Framework” is clearly cloud focused, it has in my view a lot of relevant material for non-cloud applications.  AWS Well-Architected Framework is based on four pillars—security, reliability, performance efficiency, and cost optimization.  Clearly all four pillars are relevant to non-cloud applications, with cost optimization being high up due to budgets, hardware purchases, and data centre space.

Cloud does have a number of benefits, one of which is “Lower the risk of architecture change” – something that all of us have probably experienced, testing in an environment which has a considerable delta to production.  Cloud offers “automate the creation of test environments that emulate your production configurations, you can carry out testing easily.”

Similarly, data protection these days is often an important topic, especially in light of the EU’s General Data Protection [Regulation](http://www.computerweekly.com/news/450281144/European-Parliament-set-to-approve-EU-data-protection-law).

Under the Reliability Pillar, its worth calling out “Test recovery procedures”.  Unfortunately this test is all to often never attempted, leaving to chance the risk that when recovery is needed, its not going to work as expected 😦

~ by mdavey on April 13, 2016.

Posted in [Cloud](https://mdavey.wordpress.com/category/hpc/cloud/)
Tags: [AWS](https://mdavey.wordpress.com/tag/aws/)