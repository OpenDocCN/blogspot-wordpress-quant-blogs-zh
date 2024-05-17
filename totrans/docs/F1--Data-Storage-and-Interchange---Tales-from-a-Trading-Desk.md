<!--yml
category: 未分类
date: 2024-05-18 06:02:12
-->

# F1: Data Storage and Interchange | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2013/09/07/f1-data-storage-and-interchange/#0001-01-01](https://mdavey.wordpress.com/2013/09/07/f1-data-storage-and-interchange/#0001-01-01)

## F1: Data Storage and Interchange

Google Research F1 [paper](http://static.googleusercontent.com/external_content/untrusted_dlcp/research.google.com/en//pubs/archive/41344.pdf) offers an interesting read.  Of particular [interest](http://static.googleusercontent.com/external_content/untrusted_dlcp/research.google.com/en//pubs/archive/38125.pdf), and worth a call out is the usage of Protocol Buffers:

> At Google, Protocol Buffers are ubiquitous for data storage and interchange between applications. When we still had a MySQL schema, users often had to write tedious and error-prone transformations between database rows and in-memory data structures. Putting protocol buers in the schema removes this impedance mismatch and gives users a universal data structure they can use both in the database and in application code.

[BSON](http://bsonspec.org/) is another alternative in the data storage and interchange space, with [MongoDB](http://blog.mongodb.org/post/114440717/bson) benefiting from BSON in a similar way to F1 benefiting from Protocol Buffers.  The F1 usage of protocol buffers as column types, and the query ability is extremely nice.

~ by mdavey on September 7, 2013.

Posted in [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)
Tags: [BSON](https://mdavey.wordpress.com/tag/bson/), [Google](https://mdavey.wordpress.com/tag/google/), [ProtocolBuffers](https://mdavey.wordpress.com/tag/protocolbuffers/)