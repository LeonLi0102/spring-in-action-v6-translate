## 13.1 使用 R2DBC

响应式关系型数据库连接（通常称为 R2DBC）是一种使用响应类型处理关系数据新选择。它实际上是一个 JDBC 的响应式替代方案，支持针对传统关系型数据库，如 MySQL、PostgreSQL、H2 和 Oracle 的非阻塞持久化。因为它是建立在响应式基础上的，与 JDBC 有很大不同，是一个独立的规范，与 Java SE 无关。

Spring Data R2DBC 是 Spring Data 的一个子项目。它支持 R2DBC，与我们在第 3 章中看到的 Spring Data JDBC 非常相似。与 Spring Data JDBC 不同的是，Spring Data R2DBC 并不要求严格遵守领域驱动设计概念。事实上，您很快就会看到，使用 Spring Data R2DBC 通过聚合根持久化数据，需要比使用 Spring Data JDBC 要多做一些工作。

要使用 Spring Data R2DBC，您需要在项目的构建中添加一个 starter 依赖项。对于 Maven 构建的项目，依赖项如下所示：

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-data-r2dbc</artifactId>
</dependency>
```

或者，如果您使用 Initializr 配置工程，请在创建项目时勾选“Spring Data R2DBC”选择框。

您还需要一个关系数据库以便进行数据持久化，以及相应的 R2DBC 驱动。我们将使用内存数据库 H2。因此，我们需要增加两个依赖项：H2 数据库库和 H2 R2DBC 驱动。依赖项如下所示：

```xml
<dependency>
  <groupId>com.h2database</groupId>
  <artifactId>h2</artifactId>
  <scope>runtime</scope>
</dependency>
<dependency>
  <groupId>io.r2dbc</groupId>
  <artifactId>r2dbc-h2</artifactId>
  <scope>runtime</scope>
</dependency>
```

如果您使用不同的数据库，则需要配置相关依赖项以添加相应的 R2BDC 驱动程序。

现在，依赖项已经就位，让我们看看 Spring Data R2DBC 是如何工作的。让我们从定义实体类开始。
