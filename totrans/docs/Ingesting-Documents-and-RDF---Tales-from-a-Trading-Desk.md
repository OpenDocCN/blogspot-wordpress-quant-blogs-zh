<!--yml
category: 未分类
date: 2024-05-18 05:31:04
-->

# Ingesting Documents and RDF | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/06/10/ingesting-documents-and-rdf/#0001-01-01](https://mdavey.wordpress.com/2016/06/10/ingesting-documents-and-rdf/#0001-01-01)

## Ingesting Documents and RDF

Strangle, [MarkLogic](http://www.marklogic.com/) appears to have some best documentation of dealing with documents and RDF in a single data hub, even though the concept isn’t unique to MarkLogic.  As I’ve blogged about before, there are a number of other products, and its conceivable to build your own using various open source frameworks and libraries (Apache [Jena](https://jena.apache.org/index.html) etc)

The BBC [News](https://developer.marklogic.com/learn/semantics-exercises/loading-data) sample is probably the best I’ve found so far.

> We started with each article as a single XHTML document. We then used OpenCalais to analyze the articles and find the entities (real-world things) within them. OpenCalais spotted entities like people, their roles, places (cities and countries) and organizations. On top of this it linked individuals with their role(s) and also determined the subject headings (categories) of the documents. For example, for one news article, OpenCalais generated triples for us that indicated the item was about war, identified the places mentioned in the article, and provided geo-location information for those places

The results can be seen in the downloadable zip, which provides a directory for the source (XHTML articles), and a directory wih the generated RDF file from [OpenCalais](http://www.opencalais.com/).  The RDF file uses rdf:Description to reference to the original BBC URL of the article.  Both the XHTML and the RDF files are then ingested into MarkLogic – as expected.

Finally, “SPARQL and XQuery [Together](https://developer.marklogic.com/learn/semantics-exercises/sparql-and-xquery)” shows how to leverage both content structures.

Interested in anyones experience of MarkLogic, as the documents hints at a cool product.

~ by mdavey on June 10, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/)
Tags: [Ontology](https://mdavey.wordpress.com/tag/ontology/)