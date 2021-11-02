# 7.3 使用 REST 服务

您是否曾经去看电影，当电影开始的时候，您发现只有您一个人在电影院？从本质上说，这是一次私人观影的美妙经历。您可以选择任何您想要的座位，和屏幕上的人物交谈，甚至可以打开您的手机发推特谈论它，而不会有人因为破坏了他们的观影体验而生气。最棒的是，也没有其他人会为您毁了这部电影！

这种情况在我身上并不常见。但当它出现的时候，我在想如果我没有出现会发生什么。他们还会放映这部电影吗？英雄还会拯救世界吗？电影结束后，工作人员还会打扫影院吗？

没有观众的电影就像没有客户端的 API。它已经准备好接受和提供数据了，但是如果 API 从未被调用过，那么它真的是一个 API 吗？就像薛定谔的猫一样，在我们向它发出请求之前，我们无法知道 API 是活动的还是返回 HTTP 404 响应。

Spring 应用程序既提供 API，又向另一个应用程序的 API 发出请求，这种情况并不少见。事实上，在微服务的世界里，这正变得越来越普遍。因此，花点时间看看如何使用 Spring 与 REST API 交互是值得的。

Spring 应用程序可以通过以下方式使用 REST API：

* RestTemplate —— 一个由 Spring 核心框架提供的简单、同步 REST 客户端。
* _Traverson_ —— 可感知超链接的同步 REST 客户端，由 Spring HATEOAS 提供，灵感来自同名的 JavaScript 库。
* WebClient —— 一个响应式、异步 REST 客户端。

现在，我们将主要关注 RestTemplate。在第 12 章讨论 Spring 的响应式 web 框架之前，我将推迟讨论 WebClient。如果您有兴趣
编写支持超链接的客户端，请查看以下位置的 Traverson 文档：[https://docs.spring.io/spring-hateoas/docs/current/reference/html/#client](https://docs.spring.io/spring-hateoas/docs/current/reference/html/#client)。

从客户的角度来看，与 REST 资源进行交互需要做很多工作 —— 主要是单调乏味的样板文件。使用低级 HTTP 库，客户端需要创建一个客户端实例和一个请求对象，执行请求，解释响应，将响应映射到域对象，并处理过程中可能抛出的任何异常。不管发送什么 HTTP 请求，所有这些样板文件都会重复。

为了避免这样的样板代码，Spring 提供了 RestTemplate。正如 JDBCTemplate 处理使用 JDBC 糟糕的那部分一样，RestTemplate 使你不必为调用 REST 资源而做单调的工作。

RestTemplate 提供了 41 个与 REST 资源交互的方法。与其检查它提供的所有方法，不如只考虑 12 个惟一的操作，每个操作都有重载，以形成 41 个方法的完整集合。表 7.2 描述了 12 种操作。

**表 7.2 RestTemplate 定义的 12 个唯一操作，每一个都重载了，共提供41种方法（未完待续）**

| 方法 | 描述 |
| :--- | :--- |
| delete(...) | 对指定 URL 上的资源执行 HTTP DELETE请求 |
| exchange(...) | 对 URL 执行指定的 HTTP 方法，返回一个 ResponseEntity，其中包含从响应体映射的对象 |
| execute(...) | 对 URL 执行指定的 HTTP 方法，返回一个映射到响应体的对象 |
| getForEntity(...) | 发送 HTTP GET 请求，返回一个 ResponseEntity，其中包含从响应体映射的对象 |
| getForObject(...) | 发送 HTTP GET 请求，返回一个映射到响应体的对象 |
| headForHeaders(...) | 发送 HTTP HEAD 请求，返回指定资源 URL 的 HTTP 请求头 |
| optionsForAllow(...) | 发送 HTTP OPTIONS 请求，返回指定 URL 的 Allow 头信息 |
| patchForObject(...) | 发送 HTTP PATCH 请求，返回从响应主体映射的结果对象 |
| postForEntity(...) | 将数据 POST 到一个 URL，返回一个 ResponseEntity，其中包含从响应体映射而来的对象 |
| postForLocation(...) | 将数据 POST 到一个 URL，返回新创建资源的 URL |
| postForObject(...) | 将数据 POST 到一个 URL，返回从响应主体映射的对象 |
| put(...) | 将资源数据 PUT 到指定的URL |

除了 TRACE 之外，RestTemplate 对于每个标准 HTTP 方式至少有一个方法。此外，`execute()` 和 `exchange()` 为使用任何 HTTP 方式发送请求提供了低层的通用方法。

表 7.2 中的大多数方法都被重载为三种方法形式：

* 一种是接受一个 String 作为 URL 规范，在一个变量参数列表中指定 URL 参数。
* 一种是接受一个 String 作为 URL 规范，其中的 URL 参数在 `Map<String, String>`; 中指定。
* 一种是接受 java.net.URI 作为 URL 规范，不支持参数化 URL。

一旦了解了 RestTemplate 提供的 12 个操作以及每种变体的工作方式，就可以很好地编写调用资源的 REST 客户端了。

要使用 RestTemplate，需要创建一个实例：

```java
RestTemplate rest = new RestTemplate();
```

或是将它声明为一个 bean，在需要它的时候将其注入：

```java
@Bean
public RestTemplate restTemplate() {
  return new RestTemplate();
}
```

让我们通过查看支持四种主要 HTTP 方法（GET、PUT、DELETE 和 POST）的操作来探寻 RestTemplate 的操作。我们将从 `getForObject()` 和 `getForEntity()` —— GET 方法开始。