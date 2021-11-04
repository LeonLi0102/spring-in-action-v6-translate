## 2.3 验证表单输入

当设计一个新的 taco 产品时，如果用户没有选择任何食材或者没有为他们的产品指定名称，该怎么办？当提交订单时，如果他们没有填写所需的地址字段，该怎么办？或者，如果他们在信用卡字段中输入的值甚至不是有效的信用卡号，该怎么办？

按照目前的情况，没有什么能阻止用户创建一个没有任何配料或空空如也的送货地址的玉米饼，甚至提交他们最喜欢的歌曲的歌词作为信用卡号码。这是因为还没有指定应该如何验证这些字段。

执行表单验证的一种方法是在 `processDesign()` 和 `processOrder()` 方法中加入一堆 if/then 块，检查每个字段以确保它满足适当的验证规则。但是这样做会很麻烦，并且难于阅读和调试。

幸运的是，Spring 支持 Java's Bean Validation API（也称为 JSR-303；[https://jcp.org/en/jsr/detail?id=303](https://jcp.org/en/jsr/detail?id=303)）。这使得声明验证规则比在应用程序代码中显式地编写声明逻辑更容易。使用 Spring Boot，不需要做任何特殊的事情来将验证库添加到项目中，因为 Validation API 和 Validation API 的 Hibernate 实现作为Spring Boot web 启动程序的临时依赖项自动添加到了项目中。

要在 Spring MVC 中应用验证，需要这样做：

* 工程中添加 Spring 校验 starter。
* 对要验证的类声明验证规则：特别是 Taco 类。
* 指定验证应该在需要验证的控制器方法中执行，具体来说就是：DesignTacoController 的 `processDesign()` 方法和 OrderController 的 `processOrder()` 方法。
* 修改表单视图以显示验证错误。

Validation API 提供了几个可以放在域对象属性上声明验证规则的注解。Hibernate 的 Validation API 实现甚至添加了更多的验证注解。通过将 Spring 校验 starter 添加到项目中，可以将两者都添加到项目构建中。Spring Boot Starters 向导中，勾选 I/O 下的“Validation”复选框将完成这个工作。但是如果您更喜欢手动编辑，那么在 Maven 的 pom.xml 文件可以手工添加以下内容：

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```

或者，如果您使用的是 Gradle，那么这就是您需要的依赖项：

```text
implementation 'org.springframework.boot:spring-boot-starter-validation'
```

>注意：是否需要明确添加 Spring Validation starter？
>
>在 Spring Boot 的早期版本中，Spring Validation starter 是自动包含在 web statert 中的。从 Spring Boot 2.3.0 开始，
如果要应用验证，则需要显式地将其添加到项目构建中。

添加好了校验 starter 以后，让我们看看如何应用这些注解来验证提交的 Taco 或 TacoOrder


