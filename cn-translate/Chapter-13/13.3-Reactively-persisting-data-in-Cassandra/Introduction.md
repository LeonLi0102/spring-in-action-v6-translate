## 13.3 使用 Cassandra 响应式保存数据

针对 Cassandra 数据库的响应式持久化，您需要添加以下 starter 依赖项到项目中：

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-data-cassandra-reactive</artifactId>
</dependency>
```

此依赖项替代了我们前面使用的任何 Mongo 或 R2DBC 依赖项。

然后，您需要声明有关 Cassandra 键空间的一些细节，以及 schema 的管理方式。在 application.yml 文件中，添加以下行：

```yaml
spring:
  data:
    rest:
      base-path: /data-api
    cassandra:
      keyspace-name: tacocloud
      schema-action: recreate
      local-datacenter: datacenter1
```

这与我们在第 4 章中使用非响应式 Cassandra Repository 时使用的 YAML 配置完全相同。需要注意的是 keyspace-name，需要在 Cassandra 集群中创建具有该名称的键空间。

您还需要在本地计算机上运行 Cassandra 群集，侦听端口 9042，最简单的方法是使用 Docker：

```bash
$ docker network create cassandra-net
$ docker run --name my-cassandra --network cassandra-net \
        -p 9042:9042 -d cassandra:latest
```

如果您的 Cassandra 群集位于另一台计算机或其他端口上，则需要在 application.yml 中指定接连接信息，如第 4 章所示。

要创建键空间，请运行 CQL shell 并使用如下 create keyspace 命令：

```bash
$ docker run -it --network cassandra-net --rm cassandra cqlsh my-cassandra
cqlsh> create keyspace tacocloud
WITH replication = {'class': ’SimpleStrategy', 'replication_factor' : 1};
```

现在您有了一个 Cassandra 集群、一个新的“tacocloud”键空间和 Spring Data Cassandra Reactive starter 在您的项目中，您已经准备好开始定义领域实体类了。


