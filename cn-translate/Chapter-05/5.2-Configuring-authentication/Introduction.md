## 5.2 配置身份验证

多年来，有几种配置 Spring Security 的方法，包括冗长的基于 xml 的配置。幸运的是，Spring Security 的几个最新版本都支持基于 Java 的配置，这种配置更容易读写。

在本章结束之前，已经在基于 Java 的 Spring Security 配置中配置了所有 Taco Cloud 安全需求。但是在开始之前，可以通过编写下面清单中所示的基本配置类来简化它。

**清单 5.1 Spring Security 的基本配置类**
```java
package tacos.security;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;

@Configuration
public class SecurityConfig {

  @Bean
  public PasswordEncoder passwordEncoder() {
  return new BCryptPasswordEncoder();
  }

}
```

这个基本的安全配置做了什么？嗯，不是很多，但是它确实离需要的安全功能更近了一步。其实不多。主要的事情它只是声明了一个 PasswordEncoder bean，我们将在创建新用户和登录验证用户身份时使用。在本例中，我们使用的是 BCryptPasswordEncoder，它是
Spring Security 提供的密码编码器之一，包括：

* BCryptPasswordEncoder —— 应用 bcrypt 加强哈希加密
* NoOpPasswordEncoder —— 不应用任何编码
* Pbkdf2PasswordEncoder —— 应用 PBKDF2 加密
* SCryptPasswordEncoder —— 应用 scrypt 哈希加密
* StandardPasswordEncoder —— 应用 SHA-256 哈希加密

无论您使用哪种密码编码器，重要的是要密码在数据库中永远不会被解密。相反，用户在登录时输入的密码使用相同的算法加密，然后将其与数据库中的编码密码进行比较。比较在 PasswordEncoder 的 `matches()` 方法中执行。

除了密码编码器之外，我们还将在这个配置类中填充更多的 bean 以定义应用程序的安全性细节。我们将首先配置用户存储，可以处理多个用户身份验证。

为了配置用于身份验证的用户存储，您需要声明 UserDetailsService bean。UserDetailsService 接口相对简单，只有一个方法必须实现。以下是 UserDetailsService 接口：

```java
public interface UserDetailsService {

  UserDetails loadUserByUsername(String username) throws UsernameNotFoundException;

}

```

`loadUserByUsername()` 方法接受用户名并使用它查找 UserDetails 对象，如果找不到给定用户名的用户，则会抛出UsernameNotFoundException。

事实证明，Spring Security 提供了几个 UserDetailsService 实现，可以开箱即用。包括：

* 一个内存用户存储
* 基于 JDBC 的用户存储
* 由 LDAP 支持的用户存储

或者，您可以定制自己的实现，以满足特殊安全需求。

现在，让我们先尝试 UserDetailsService 的内存用户存储。


