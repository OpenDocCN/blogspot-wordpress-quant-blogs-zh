<!--yml

类别：未分类

日期：2024 年 05 月 18 日 06:02:12

-->

# F1：数据存储和交换 | 交易台的故事

> 来源：[`mdavey.wordpress.com/2013/09/07/f1-data-storage-and-interchange/#0001-01-01`](https://mdavey.wordpress.com/2013/09/07/f1-data-storage-and-interchange/#0001-01-01)

## F1：数据存储和交换

Google Research F1 [论文](http://static.googleusercontent.com/external_content/untrusted_dlcp/research.google.com/en//pubs/archive/41344.pdf) 值得一读。特别值得关注的是协议缓冲区的使用：

> 在 Google，协议缓冲区在应用程序之间的数据存储和交换中无处不在。当我们还有 MySQL 架构时，用户经常需要在数据库行和内存数据结构之间编写冗长且容易出错的转换。将协议缓冲区放入架构中消除了这种阻抗不匹配，并为用户提供了一种通用数据结构，他们既可以在数据库中使用，也可以在应用程序代码中使用。

[BSON](http://bsonspec.org/) 是数据存储和交换领域的另一种选择，[MongoDB](http://blog.mongodb.org/post/114440717/bson) 从 BSON 中获益，类似于 F1 从 Protocol Buffers 中获益一样。F1 使用协议缓冲区作为列类型，并且查询功能非常好。

~ 由 mdavey 于 2013 年 9 月 7 日发表。

发表在[未分类](https://mdavey.wordpress.com/category/uncategorized/)

标签：[BSON](https://mdavey.wordpress.com/tag/bson/)，[Google](https://mdavey.wordpress.com/tag/google/)，[ProtocolBuffers](https://mdavey.wordpress.com/tag/protocolbuffers/)
