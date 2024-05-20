<!--yml
category: 未分类
date: 2024-05-18 05:29:38
-->

# Deploying an Analytical Database | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/09/16/deploying-an-analytical-database/#0001-01-01](https://mdavey.wordpress.com/2016/09/16/deploying-an-analytical-database/#0001-01-01)

## Deploying an Analytical Database

O’Reilly has a short but interesting [article](https://www.oreilly.com/ideas/5-mistakes-to-avoid-when-deploying-an-analytical-database) on “5 mistakes to avoid when deploying an analytical database”.

Point one is pretty much the case of the engineer in the sweet shop.  Stop and think before you decide on the technology stack, and if its really going to help. 🙂

Point four is critical from my perspective.  The best [TLA](https://en.wikipedia.org/wiki/Three-letter_acronym) to describe this is the [ELT](https://en.wikipedia.org/wiki/Extract,_load,_transform) paradigm compared to the old ETL world.  Extract all data element from the source systems, and store in your analytical database.  Zero information loss.

~ by mdavey on September 16, 2016.

Posted in [HPC](https://mdavey.wordpress.com/category/hpc/)
Tags: [BigData](https://mdavey.wordpress.com/tag/bigdata/), [MachineLearning](https://mdavey.wordpress.com/tag/machinelearning/)