# 第 17 章 使用 JMX 监控 Spring

本章内容

* 使用 Actuator 端点 MBean
* 将 Spring Bean 公开为 MBean
* 发布通知

十多年来，Java 管理扩展（JMX）一直是监视和管理 Java 应用程序的标准方法。通过公开托管组件即 MBean（托管 bean），外部 JMX 客户端可以执行调用、检查属性和监视来自 MBeans 的事件。

我们开始探索 Spring 和 JMX，先看看 Actuator 端点是如何暴露为 MBean 的。


