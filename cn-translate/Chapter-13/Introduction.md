# 第 13 章 响应式持久化数据

本章内容

* 响应式持久化关系型数据库 R2DBC
* 编写适用于 Cassandra 和 MongoDB 的响应式 Repository 
* 测试响应式 Repository 

如果说我们从科幻小说中学到了什么，那就是如果想改变过去，所需要做的只是进行一次时间旅行。这在《回到未来》中有过，在《星际迷航》中也有好几集，《复仇者联盟4：终局之战》以及《斯蒂芬·金作品系列：11 22 63》都起过作用。（好吧，也许最后一个并没有变得更好，但您应该明白了。）

在这一章中，我们将回到第 3 章和第 4 章，重温我们为关系数据库、MongoDB 和 Cassandra 创建的 Repository 。这一次，我们要利用 Spring Data 的一些响应式 Repository 支持改进它们，我们能够以非阻塞方式使用这些 Repository 。

让我们先看看 Spring Data R2DBC，它是 Spring Data JDBC 持久化到关系数据库的一种响应式替代方案。
