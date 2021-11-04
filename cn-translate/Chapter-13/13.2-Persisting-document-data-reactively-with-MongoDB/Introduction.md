## 13.2 使用 MongoDB 响应式保存文档

在第 4 章中，我们使用 Spring Data MongoDB 定义了基于 MongoDB 文档型数据库的文档数据持久化。在本节中，我们将使用 Spring Data 对 MongoDB 的响应式支持。

首先，您需要使用 Spring Data Reactive MongoDB starter 创建一个项目。实际上，这是使用 Initalizr 创建项目时要选择的复选框的名称。或者，您可以使用以下依赖项手动将其添加到 Maven 构建中：

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-data-mongodb-reactive</artifactId>
</dependency>
```

在第 4 章中，我们还借助于 Flapdoodle 嵌入式 MongoDB 数据库进行测试。不幸的是，以响应式持久化时，Flapdoodle 的表现不是很好。在运行测试时，您需要运行一个实际的 Mongo 数据库，并侦听端口 27017。

现在，我们已经准备好开始为响应式 MongoDB 持久化编写代码了。我们先从创建文档类型开始。
