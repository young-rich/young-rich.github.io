# 简介

    **Spring Security** 是 Spring 家族中的一个安全管理框架。相比与另外一个安全框架**Shiro**，它提供了更丰富的功能，社区资源也比Shiro丰富。

    一般来说中大型的项目都是使用**SpringSecurity** 来做安全框架。小项目有Shiro的比较多，因为相比与SpringSecurity，Shiro的上手更加的简单。

    一般Web应用的需要进行**认证**和**授权**。

    **认证：验证当前访问系统的是不是本系统的用户，并且要确认具体是哪个用户**

    **授权：经过认证后判断当前用户是否有权限进行某个操作**

    而认证和授权也是SpringSecurity作为安全框架的核心功能。

# 认证

## 登陆校验流程

![image-20211215094003288](https://file+.vscode-resource.vscode-webview.net/d%3A/DATA/%E5%8D%9A%E5%AE%A2/young-rich.github.io/_posts/Spring/image/image-20211215094003288.png)

SpringSecurity的原理其实就是一个过滤器链，内部包含了提供各种功能的过滤器。这里我们可以看看入门案例中的过滤器。

![image-20211214144425527](https://file+.vscode-resource.vscode-webview.net/d%3A/DATA/%E5%8D%9A%E5%AE%A2/young-rich.github.io/_posts/Spring/image/image-20211214144425527.png)

**UsernamePasswordAuthenticationFilter**:负责处理我们在登陆页面填写了用户名密码后的登陆请求。入门案例的认证工作主要有它负责。

**ExceptionTranslationFilter：**处理过滤器链中抛出的任何AccessDeniedException和AuthenticationException 。

**FilterSecurityInterceptor：**负责权限校验的过滤器。

## **认证流程**

![image-20211214151515385](https://file+.vscode-resource.vscode-webview.net/d%3A/DATA/%E5%8D%9A%E5%AE%A2/young-rich.github.io/_posts/Spring/image/image-20211214151515385.png)

Authentication接口: 它的实现类，表示当前访问系统的用户，封装了用户相关信息。

AuthenticationManager接口：定义了认证Authentication的方法

UserDetailsService接口：加载用户特定数据的核心接口。里面定义了一个根据用户名查询用户信息的方法。

UserDetails接口：提供核心用户信息。通过UserDetailsService根据用户名获取处理的用户信息要封装成UserDetails对象返回。然后将这些信息封装到Authentication对象中。

## 密码加密存储

实际项目中我们不会把密码明文存储在数据库中。

    默认使用的PasswordEncoder要求数据库中的密码格式为：{id}password 。它会根据id去判断密码的加密方式。但是我们一般不会采用这种方式。所以就需要替换PasswordEncoder。

    我们一般使用SpringSecurity为我们提供的BCryptPasswordEncoder。

    我们只需要使用把BCryptPasswordEncoder对象注入Spring容器中，SpringSecurity就会使用该PasswordEncoder来进行密码校验。

    我们可以定义一个SpringSecurity的配置类，SpringSecurity要求这个配置类要继承WebSecurityConfigurerAdapter。

## 思路

登录

    ①自定义登录接口

    调用ProviderManager的方法进行认证 如果认证通过生成jwt

    把用户信息存入redis中

    ②自定义UserDetailsService

    在这个实现类中去查询数据库

校验：

    ①定义Jwt认证过滤器

    获取token

    解析token获取其中的userid

    从redis中获取用户信息

    存入SecurityContextHolder

创建一个类实现UserDetailsService接口，重写其中的方法。更加用户名从数据库中查询用户信息
