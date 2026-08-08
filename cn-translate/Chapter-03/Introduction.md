# 第 3 章 处理数据

本章内容：

* 使用 Spring JdbcTemplate
* 创建 Spring Data JDBC Repository
* 使用 Spring Data 声明 JPA Repository

大多数应用程序的价值不仅仅在于漂亮的界面。虽然用户界面提供了与应用程序的交互入口，但真正将应用程序与静态网站区分开来的，是它所呈现和存储的数据。

在 Taco Cloud 应用程序中，需要能够维护关于 ingredients、tacos 和 orders 的信息。如果没有一个数据库来存储这些信息，应用程序将无法比在第 2 章中开发的应用程序取得更大的进展。

在本章中，我们将为 Taco Cloud 应用添加数据持久化功能。首先使用 Spring 对 JDBC（Java Database Connectivity）的支持来消除样板代码，然后使用 JPA（Java Persistence API）进一步简化数据存储操作。


