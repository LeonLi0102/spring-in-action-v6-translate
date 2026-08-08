# 第 4 章 处理非关系型数据

本章内容：

* 将数据持久化到 Cassandra
* Cassandra 中的数据建模
* 在 MongoDB 中使用文档数据

丰富多彩的生活才充满乐趣。

您可能有最喜欢的一种冰淇淋口味。选择它通常是因为它比其他口味更合您的心意。但大多数人尽管有自己偏爱的口味，也会不时尝试其他不同的口味。

数据库就像冰淇淋。几十年来，关系型数据库一直是用户最喜欢的类型。但是现在比以往任何时候都有更多的选择。所谓的“NoSQL”数据库提供了不同的概念和结构。尽管选择可能仍然取决于您的个人喜好，但有些数据库更适合存储特定类型的数据。

幸运的是，Spring Data 支持了许多 NoSQL 数据库，包括 MongoDB、Cassandra、Couchbase、Neo4j、Redis 等等。而且幸运的是，
无论选择哪个数据库，编程模型几乎是相同的。

本章没有足够的篇幅涵盖 Spring Data 支持的所有数据库类型。但为了让您了解 Spring Data 的其他“风味”，我们将研究两种流行的 NoSQL 数据库，Cassandra 和 MongoDB，并了解如何创建 Repository 进行数据持久化。让我们先看看如何使用 Spring Data 创建Cassandra Repository。



