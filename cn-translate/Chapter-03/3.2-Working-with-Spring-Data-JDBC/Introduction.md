### 3.2 使用 Spring Data JDBC

Spring Data 项目是一个相当大的一揽子项目，由几个子项目组成，其中大多数是聚焦在对各种不同数据库类型进行持久化。一些最流行的 Spring Data 项目包括：

* Spring Data JDBC —— 针对关系数据库的 JDBC 持久化
* Spring Data JPA —— 针对关系数据库的 JPA 持久化
* Spring Data MongoDB —— Mongo 文档数据库的持久化
* Spring Data Neo4j —— 持久化到 Neo4j 图形数据库
* Spring Data Redis —— 持久化到 Redis 键值存储数据库
* Spring Data Cassandra —— 持久化到 Cassandra 列存储数据库

Spring Data 为所有这些项目提供的最有趣、最有用的特性之一是，基于 Repository 规范接口自动创建 Repository 的能力。因此，Spring Data 项目的持久化几乎没有持久化逻辑，只涉及编写一个或多个 Repository 接口。

让我们看看如何将 Spring Data JDBC 应用到我们的项目中，以简化 JDBC 的数据持久化。首先，需要将 Spring Data JDBC 添加到项目构建中。