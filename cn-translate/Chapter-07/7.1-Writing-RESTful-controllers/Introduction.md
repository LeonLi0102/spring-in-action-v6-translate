## 7.1 编写 RESTful 控制器

简而言之，REST API 与网站没有太大区别。两者都涉及对 HTTP 请求的响应。但关键的区别在于，网站是用 HTML 响应这些请求，而REST API通常以面向数据的格式（如 JSON 或 XML）响应。

在第 2 章中，使用 `@GetMapping` 和 `@PostMapping` 注解来获取和发送数据到服务器。在定义 REST API 时，这些相同的注释仍然很有用。此外，Spring MVC 还为各种类型的 HTTP 请求支持少量其他注解，如表 7.1 所示。

**表 7.1 Spring MVC HTTP 请求处理注解**

| 注解 | HTTP 方法 | 典型用法 |
| :--- | :--- | :--- |
| @GetMapping | HTTP GET 请求 | 读取资源数据 |
| @PostMapping | HTTP POST 请求 | 创建资源 |
| @PutMapping | HTTP PUT 请求 | 更新资源 |
| @PatchMapping | HTTP PATCH 请求 | 更新资源 |
| @DeleteMapping | HTTP DELETE 请求 | 删除资源 |
| @RequestMapping | 通用请求处理 |  |

要查看这些注释的实际效果，将首先创建一个简单的 REST 端点，该端点获取一些最近创建的 taco。


