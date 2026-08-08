# 第 16 章 管理 Spring

本章内容

* 设置 Spring Boot Admin
* 注册客户端应用程序
* 使用 Actuator 端点
* 保护 Admin 服务器的安全

俗话说，一图胜千言。对于众多的应用使用者来说，一个对用户友好的 Web 界面抵得上一千次 API 调用。别误会，我是命令行爱好者，非常喜欢使用 curl 和 HTTPie 来进行 REST API 调用。但是，有时手动键入命令行以调用 REST，然后目视检查返回结果，效率可能不如单击链接在浏览器中查看结果。

在上一章中，我们讨论了 Spring Boot Actuator。这些 HTTP 端点返回 JSON 响应数据，可以根据需要使用。在本章中，我们将了解如何创建基于 Actuator 的前端界面（UI）。让 Actuator 更易于使用，并能实时捕获难以直接从 Actuator 获取的数据。
