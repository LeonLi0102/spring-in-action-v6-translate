# 5.3 保护 web 请求

Taco Cloud 的安全需求应该要求用户在设计 tacos 或下订单之前进行身份验证。但是主页、登录页面和注册页面应该对未经身份验证的用户可用。

要配置这些安全规则，需要声明一个 SecurityFilterChain bean。下面的方法添加了 `@Bean` 注解，这是一个最简化的 （不太实用） SecurityFilterChain 类：

```java
@Bean
public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
  return http.build();
}
```

这个 `filterChain()` 方法接受 HttpSecurity 对象，充当的生成器，用于 web 级别安全配置。一旦安全配置通过 HttpSecurity 对象完成设置，调用 `build()` 方法将创建并返回一个 SecurityFilterChain 对象。

可以配置 HttpSecurity 的属性包括：

* 在允许服务请求之前，需要满足特定的安全条件
* 配置自定义登录页面
* 使用户能够退出应用程序
* 配置跨站请求伪造保护

拦截请求以确保用户拥有适当的权限是配置 HttpSecurity 要做的最常见的事情之一。让我们确保 Taco Cloud 的客户满足这些要求。


