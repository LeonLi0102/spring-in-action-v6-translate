# 14.2 创建一个简单的 RSocket 服务端和客户端

Spring 为 RSocket 的消息传递提供了非常好的支持，包括所有四种通信方式模型。要开始使用 RSocket，您需要将 Spring Boot RSocket starter 添加到项目构建中。在 Maven 的 POM 文件中，RSocket starter 依赖项如下所示：

**清单 14.1 Spring Boot 的 RSocket stater 依赖项**
```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-rsocket</artifactId>
</dependency>
```

RSocket 的服务器和客户端应用程序都需要添加这个依赖。

>使用 Spring Initializr 选择依赖项时，您可能会看到类似命名的 WebSocket 依赖项。虽然 RSocket 和 WebSocket 名称相似，且您可以使用 WebSocket 作为 RSocket 的底层（我们将在本章后面介绍），但您并不需要选择 WebSocket 依赖。

接下来，您需要决定哪种通信模型最适合您的应用程序。没有一种方式会适合所有情况，因此您需要依据期望的应用程序通信行为，来权衡选择。但是，正如您将在接下来的几节中看到的，每个通信模型的开发模型没有太大的不同，所以如果您选错了，很容易切换。

让我们看看如何在 Sprin 中使用每种通信创建 RSocket 服务器和客户端。因为每个 RSocket 的通信模型都不同，最适合在特定的用例场景中，我们将暂时搁置 Taco Cloud 应用程序，看看如何在不同的问题域上应用 RSocket。我们将从了解如何使用 `请求/响应` 通信模型开始。