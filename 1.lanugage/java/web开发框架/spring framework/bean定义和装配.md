**Bean 定义和装配：** 理解 Spring 中 Bean 的概念，学会通过 XML 配置、Java 注解或 Java 配置类来定义和装配 Bean。

- 在 Spring 框架中，Bean 是指被 Spring 容器管理的对象。通过 Bean 的定义和装配，我们可以告诉 Spring 如何创建、配置和管理这些对象。Bean 定义包括对象的类型、属性、依赖关系等信息，而 Bean 装配指的是将这些定义好的 Bean 放入 Spring 容器中并建立它们之间的关联。

  有多种方式可以进行 Bean 的定义和装配，以下是常见的方式：

  1. **XML 配置：** 通过编写 XML 配置文件来定义和装配 Bean。在 XML 文件中，可以使用 `<bean>` 元素来声明 Bean 的定义，包括类名、属性、构造函数参数等信息。XML 配置方式在 Spring 的早期版本中很常见。

  ```xml
  <bean id="userService" class="com.example.UserService">
      <property name="userRepository" ref="userRepository"/>
  </bean>
  ```

  2. **Java 注解：** 使用 Java 注解来定义 Bean。通过在类上标注 `@Component` 或其衍生注解（如 `@Service`、`@Repository`、`@Controller`）来表示该类是一个 Bean，并由 Spring 自动扫描并管理。

  ```java
  @Component
  public class UserService {
      @Autowired
      private UserRepository userRepository;
  }
  ```

  3. **Java 配置类：** 使用 Java 配置类来定义 Bean，取代了传统的 XML 配置。在配置类中，使用 `@Configuration` 注解标记类，并使用 `@Bean` 注解来定义 Bean。

  ```java
  @Configuration
  public class AppConfig {
      @Bean
      public UserService userService() {
          return new UserService(userRepository());
      }
  
      @Bean
      public UserRepository userRepository() {
          return new UserRepository();
      }
  }
  ```

  以上方式可以单独使用，也可以结合使用。通过配置文件、注解或配置类，我们可以定义 Bean 的各种属性和依赖关系。Spring 容器会根据这些定义来创建 Bean，并将它们放入容器中，以供其他组件使用。

  总之，Bean 定义和装配是 Spring 框架中的核心概念，通过合适的方式将对象定义和装配到 Spring 容器中，能够实现依赖注入、控制反转等特性，使应用程序更加模块化、灵活和可维护。