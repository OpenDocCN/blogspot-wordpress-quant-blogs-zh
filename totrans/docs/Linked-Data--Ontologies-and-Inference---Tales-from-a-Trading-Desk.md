<!--yml
category: 未分类
date: 2024-05-18 05:31:55
-->

# Linked Data, Ontologies and Inference | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/05/17/linked-data-ontologies-and-inference/#0001-01-01](https://mdavey.wordpress.com/2016/05/17/linked-data-ontologies-and-inference/#0001-01-01)

## Linked Data, Ontologies and Inference

Although a few years old, this presentation from a development manager at the British Museum provide some interesting [reading](http://www.slideshare.net/BarryNorton/linked-data-ontologies-and-inference).

Which nicely leads to [ModelD2RQ](http://d2rq.org/jena):

> The [ModelD2RQ](http://d2rq.org/javadoc/de/fuberlin/wiwiss/d2rq/jena/ModelD2RQ.html) class provides a Jena Model view on the data in a D2RQ-mapped database.

A nice example of a SPARQL query using the ModelD2RQ engine is shown [here](http://d2rq.org/jena#sparql).  A quick search of the web leads to an interesting discuss using similar [code](https://sourceforge.net/p/d2rq-map/mailman/message/22543261/), but around D2RQ and entailment (somewhat dated), showing the usage of ModelFactory.createOntologyModel()

[ModelFactory](https://jena.apache.org/documentation/javadoc/jena/org/apache/jena/rdf/model/ModelFactory.html) looks like we now have the option to add [Reasoner’s](https://jena.apache.org/documentation/javadoc/jena/org/apache/jena/reasoner/Reasoner.html) between the underlying data source, and the requesting SPARQL.  Interesting.  I’m guessing the following code would achieve some interesting results:

```
&lt;pre&gt;final ModelD2RQ m = new ModelD2RQ(&lt;path to mapping.ttl&gt;);
final Reasoner reasoner = &lt;some reasoner&gt;;
final InfModel ontModel = ModelFactory.createInfModel(reasoner, m);

final String sparql = &lt;query&gt;

final Query q = QueryFactory.create(sparql);
final ResultSet rs = QueryExecutionFactory.create(q, ontModel).execSelect();

```

Some code on the web is available [here](http://www.programcreek.com/java-api-examples/com.hp.hpl.jena.rdf.model.ModelFactory), [here](http://massapi.com/class/in/InfModel.html), and a FOAF example with reasoner and rule [here](https://github.com/agastheswar/Semantic-Web-application/blob/master/HelloSemanticWeb/src/org/semweb/assign6/HelloSemanticWeb.java).

Finally, a more recent [blog](https://blog.talentica.com/2014/08/16/semantic-web-a-technical-introduction/) posting on the topic, and also a reminder that the d2rq language is powerful, and offer the ability to join to yourself – [d2rq:alias](http://d2rq.org/d2rq-language#example-alias)

~ by mdavey on May 17, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/)
Tags: [DataLake](https://mdavey.wordpress.com/tag/datalake/), [Ontology](https://mdavey.wordpress.com/tag/ontology/)