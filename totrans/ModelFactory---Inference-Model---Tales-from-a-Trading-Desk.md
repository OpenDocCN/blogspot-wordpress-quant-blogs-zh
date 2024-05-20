<!--yml
category: 未分类
date: 2024-05-18 05:31:59
-->

# ModelFactory – Inference Model | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/05/17/modelfactory-inference-model/#0001-01-01](https://mdavey.wordpress.com/2016/05/17/modelfactory-inference-model/#0001-01-01)

## ModelFactory – Inference Model

[ModelFactory](https://jena.apache.org/documentation/notes/model-factory.html) is the on stop shop for creating Model’s in Apache Jena.  ModelFactory is also the way to create Inference models, which offer different kinds of inference over RDF-based models (used for RDFS and OWL) – through reasoners.

One interesting example can be seen here on [stackoverflow](http://stackoverflow.com/questions/25055263/how-to-get-only-inferred-data-from-jena-ontology-model).

Which does lead back to section 2 and the OpenTox [article](http://opentox.org/data/documents/development/RDF%20files/JavaOnly/query-reasoning-with-jena-and-sparql).  Its a shame the article doesn’t go further to show effectively a SPARQL made against a D2RQ data source, but prior to the D2RQ data source being queried, a Reasoner is leveraged to effectively enhance the SPARQL.

Finally, probably worth having a look at these [samples](https://www.google.co.uk/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=0ahUKEwjK9dDBzeDMAhVmOMAKHRNtABgQFggjMAE&url=http%3A%2F%2Finfo.slis.indiana.edu%2F~dingying%2FTeaching%2FZ636%2FSlides%2FJenaExample.ppt&usg=AFQjCNEsWI18VrDHhP5mjTN2fG71yMAcgw&sig2=QVvUNXFYBbvFWFCXu9-0Gg&bvm=bv.122129774,d.ZGg) around Family Tree.

~ by mdavey on May 17, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/)
Tags: [Ontology](https://mdavey.wordpress.com/tag/ontology/)