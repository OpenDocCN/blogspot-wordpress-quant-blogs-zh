<!--yml
category: 未分类
date: 2024-05-18 05:42:03
-->

# The Great Micro-services Debate | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2015/06/05/the-great-micro-services-debate/#0001-01-01](https://mdavey.wordpress.com/2015/06/05/the-great-micro-services-debate/#0001-01-01)

## The Great Micro-services Debate

A few people have picked up on the great Micro-services debate that is probably occurring in many companies.  Micro-services, like many other architectural options, are just another tool in the toolbox.  No single solution will solve all problems 🙂  Martin Fowler [offers](http://martinfowler.com/bliki/MonolithFirst.html) some recent views on micro-services architectures.  Sam [Newman](http://samnewman.io/blog/2015/04/07/microservices-for-greenfield/) offer a nice case study on brownfield/greenfield micro-services.  I think one of the key takeaways from Sam’s post is that domain knowledge of the problem is essential to the partitioning of services.

> Despite knowing the domain of continuous integration really well, their initial stab at coming up with service boundaries for their hosted-CI solution wasn’t quite right. This led to a high cost of change and high cost of ownership. After several months fighting this problem, the team decided to merge the services back into one big application. Later on, when the feature-set of the application had stabilized somewhat and the team had a firmer understanding of the domain, it was easier to find those stable boundaries.

Clean Code [blog](http://blog.cleancoder.com/uncle-bob/2014/09/19/MicroServicesAndJars.html) also offers sensible advice in the services area:

> Don’t leap into microservices just because it sounds cool. Segregate the system into jars using a plugin architecture first. If that’s not sufficient, then consider introducing service boundaries at strategic points.

~ by mdavey on June 5, 2015.

Posted in [Languages](https://mdavey.wordpress.com/category/languages/)