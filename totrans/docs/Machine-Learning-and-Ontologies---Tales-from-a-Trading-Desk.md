<!--yml
category: 未分类
date: 2024-05-18 05:35:02
-->

# Machine Learning and Ontologies | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/03/23/machine-learning-and-ontologies/#0001-01-01](https://mdavey.wordpress.com/2016/03/23/machine-learning-and-ontologies/#0001-01-01)

## Machine Learning and Ontologies

Whilst considering the benefits of ontology based data sources to ingest into [H2O](http://www.h2o.ai/) and the machine learning world, I came across two interesting papers:

*   Ontology [Matching](http://homes.cs.washington.edu/~pedrod/papers/hois.pdf): A Machine Learning Approach
*   Using Machine Learning to Support [Continuous](http://wortschatz.uni-leipzig.de/~fwitschel/papers/ekaw10.pdf) Ontology Development

I’m not sure if either have helped me with my thought process, but they are still interesting.  In many ways, I’m wondering if Ontologies would aid in model/algorithm usage, or I end up with data overload 🙂

Its also worth having a look at “How Goldman Sachs is Using Knowledge to Create an Information [Edge](http://conferences.oreilly.com/strata/stratany2014/public/schedule/detail/37837)“.  Although the slide deck isn’t full of detail, slide 5 does at least off a high level architecture, and provide some detail on ontology usage. Looks like the same presentation was delivered [again](http://conferences.oreilly.com/strata/big-data-conference-uk-2015/public/schedule/detail/39810) last year – unfortunately this time there isn’t any slide deck available.

> In the Goldman approach, authoritative raw data sources are stored in an enterprise data lake in Hadoop, stored in HDFS. To represent our knowledge domains, Goldman Sachs has developed an enterprise ontology representing its business concepts. The upper ontology is represented in OWL format and describes class structures and data transformation rules. These rules are then leveraged in a custom-developed Hadoop process to transform data into semantically consistent information in RDF format. The assertions and higher-order concepts from the lower ontology are leveraged to generate the rule set on the transformed data, creating “Big Graphs” consisting of, in some cases, billions of nodes and edges

~ by mdavey on March 23, 2016.

Posted in [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)