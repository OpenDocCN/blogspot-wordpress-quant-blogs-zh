<!--yml
category: 未分类
date: 2024-05-18 05:48:57
-->

# Skill Cloud – Part 3 | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2014/06/03/skill-cloud-part-3/#0001-01-01](https://mdavey.wordpress.com/2014/06/03/skill-cloud-part-3/#0001-01-01)

## Skill Cloud – Part 3

One of the obvious way to store a skill cloud is through a graph database.  [Neo4j](http://www.neo4j.org/) or [Titan](http://thinkaurelius.github.io/titan/) are two possible choices.  For no reason in particular, I’ll go with Neo4j, and use the [embedded](http://docs.neo4j.org/chunked/milestone/tutorials-java-embedded.html) version with Java simple for a way to get up and running quickly.  Adding the Maven [dependencies](http://docs.neo4j.org/chunked/milestone/tutorials-java-embedded-setup.html) into my pom.xml is the easiest way to get started.  The Neo4j [HelloWorld](https://github.com/neo4j/neo4j/blob/2.1.1/community/embedded-examples/src/main/java/org/neo4j/examples/EmbeddedNeo4j.java) sample is probably the easiest thing to borrow as a skeleton for a quick start.

[Modelling](http://docs.neo4j.org/chunked/milestone/data-modeling-examples.html) a person, their skills and their team is obvious an important part of this proof of concept (PoC).  Skill’s and team members would be modelled as Node’s (obviously), with appropriate relationships to capture linkage to a persons skills cloud (node’s) coupled with who working with who in a team – team is clearly a node in itself.

This nicely leads to “Representing time dependent graphs in Neo4j ” on [GitHub](https://github.com/SocioPatterns/neo4j-dynagraph/wiki/Representing-time-dependent-graphs-in-Neo4j).  What’s possibly interesting is that ideally you want a bi-temporal view of the nodes and relationships, since people, and teams change over time.

~ by mdavey on June 3, 2014.

Posted in [Data](https://mdavey.wordpress.com/category/data/)