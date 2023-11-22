Spring Boot 是基于 Spring 框架的快速开发框架，提供了很多用于简化 Spring 应用程序开发的注解。

**以下是常见的 Spring Boot @ 相关的注解：**

1. **@SpringBootApplication：**

   Spring Boot 应用程序的入口注解，标注在启动类上，表示该类为 Spring Boot 应用程序的主配置类，包括自动配置、组件扫描和提供 Bean 等等。

2. **@RestController：**
   Spring MVC 控制器注解，用于声明一个 REST 风格的控制器类，该类中的所有方法的返回值都会直接以 JSON 或 XML 形式返回给客户端。

3. **@RequestMapping：**
   处理 HTTP 请求的注解，为 Spring MVC 控制器中的方法提供 URL 映射信息，可以指定请求方式、路劲、参数、响应类型等信息。

4. **@Autowired：**
   自动注入依赖对象的注解，用于将依赖对象自动注入到相关类中。

5. **@Component：**
   把普通实例化的类标识为 Spring 中的 Bean，可以被 @Autowired 注解自动注入。

6. **@Configuration：**
   Spring Boot 应用程序配置类的注解，用于声明该类为 Spring 配置类，含有 @Bean 注解的方法都将被 Spring 容器管理，可用于替代 XML 配置文件。

7. **@EnableAutoConfiguration：**
   能够自动配置 Spring 应用程序的注解，其目的是在 Spring 应用程序启动时，根据应用程序的依赖关系、类路径和其他属性等信息，自动引入所需的 Spring 配置，简化 Spring 应用程序的配置。

8. **@Value：**
   注入配置文件中属性值的注解，用于将属性值自动注入到类中，可以指定默认值或从配置文件中获取对应属性值。

9. **@Transactional：**
   声明对数据库事务的支持，实现事务管理。

这些注解大大简化了 Spring Boot 应用程序的开发，减少了程序员进行繁琐的配置和管理，提高了开发的效率。
