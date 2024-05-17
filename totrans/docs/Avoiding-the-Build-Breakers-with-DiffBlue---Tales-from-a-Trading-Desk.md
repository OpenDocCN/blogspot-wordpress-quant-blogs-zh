<!--yml
category: 未分类
date: 2024-05-18 05:26:44
-->

# Avoiding the Build Breakers with DiffBlue | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2019/02/13/avoiding-the-build-breakers-with-diffblue/#0001-01-01](https://mdavey.wordpress.com/2019/02/13/avoiding-the-build-breakers-with-diffblue/#0001-01-01)

## Avoiding the Build Breakers with DiffBlue

ABN Amro provides insight into its Continuous Integration Continuous Delivery (CICD), tooling, software quality and security via this [posting](https://medium.com/abn-amro-developer/improved-software-delivery-within-abn-amro-by-continuous-integration-continuous-delivery-1e317f7fb8cc).  Of interest is how they have partly improved quality via “Build Breakers”.  The issue with these breakers is that its fine for new projects who are clear on the bar, but older projects have somewhat of a hurdle to jump before they can adhere to the break.

Solution?  [DiffBlue](https://www.diffblue.com/)

How?  If you added DiffBlue to the CI/CD pipeline, in the event that your project drops below the % code coverage breaker, DiffBlue could create the Unit Tests, bringing you quickly back above the breaker.

Moving aged projects/products into your nice shiny CI/CD pipeline could also be aided by DiffBlue.  Generate a “[full regression suite](https://www.diffblue.com/datasheet)” before migrating into the CI/CD pipeline.  Problem solved.  Migration is now part of the build breaker quality solution without the need to hire personnel 🙂

Finally, [Accelerate](https://www.amazon.co.uk/dp/B07B9F83WM) provides a view on the capabilities required to 2x team/product delivery.  DiffBlue is part of the solution for [Capacity 4, Test Automation](https://devops-research.com/assets/accelerate-book-excerpt.pdf).  [DORA State of DevOps](https://cloudplatformonline.com/rs/248-TPC-286/images/DORA-State%20of%20DevOps.pdf) also play to DiffBlue, with regards to Elite/Higher performers undertaking considerably less manual testing than Medium/Low performers.

~ by mdavey on February 13, 2019.

Posted in [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)