# 3.3 使用 Spring Data JPA 持久化数据

虽然 Spring Data JDBC 可以轻松地持久化数据，但 Java Persistence API（JPA）也是在关系数据库中处理数据的另一个常用选项。Spring Data JPA 提供了一个类似 JDBC 的 JPA 方式来持久化数据。

为了了解 Spring Data 是如何工作的，需要将本章前面介绍的基于 jdbc 的存储库替换为 Spring Data JPA 创建的存储库。但是首先，需要将 Spring Data JPA 添加到项目构建中。

