**Spring Boot Web：** 学会使用 Spring Boot 创建 Web 应用程序，包括使用 Spring MVC 进行 Web 开发、处理请求和响应等。

- 使用 Spring Boot 创建 Web 应用程序非常简单，Spring Boot 提供了集成的 Spring MVC 框架来帮助你进行 Web 开发。以下是使用 Spring Boot 创建 Web 应用程序的基本步骤和示例：

  **步骤：**

  1. **创建一个 Spring Boot 项目：**
     使用 Spring Initializr（https://start.spring.io/）或 Spring Tool Suite 等工具创建一个新的 Spring Boot 项目。

  2. **添加起步依赖：**
     在项目的 `pom.xml` 文件中添加 `spring-boot-starter-web` 起步依赖，它包含了 Spring MVC 和内嵌的 Tomcat 服务器等组件。

  ```xml
  <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-web</artifactId>
  </dependency>
  ```

  3. **创建一个控制器：**
     创建一个控制器类来处理请求和响应。这可以是一个简单的类，使用 Spring MVC 的注解进行标记。

  ```java
  import org.springframework.stereotype.Controller;
  import org.springframework.web.bind.annotation.GetMapping;
  import org.springframework.web.bind.annotation.ResponseBody;
  
  @Controller
  public class HelloController {
  
      @GetMapping("/hello")
      @ResponseBody
      public String hello() {
          return "Hello, Spring Boot!";
      }
  }
  ```

  4. **运行应用程序：**
     启动应用程序，Spring Boot 会自动扫描并注册控制器。你可以在浏览器中访问 `http://localhost:8080/hello` 来查看响应。

  **示例：**

  下面是一个简单的 Spring Boot Web 应用程序示例，演示了如何使用 Spring MVC 处理请求和响应。

  ```java
  import org.springframework.boot.SpringApplication;
  import org.springframework.boot.autoconfigure.SpringBootApplication;
  import org.springframework.stereotype.Controller;
  import org.springframework.web.bind.annotation.GetMapping;
  import org.springframework.web.bind.annotation.ResponseBody;
  
  @SpringBootApplication
  public class WebAppApplication {
  
      public static void main(String[] args) {
          SpringApplication.run(WebAppApplication.class, args);
      }
  }
  
  @Controller
  public class HelloController {
  
      @GetMapping("/hello")
      @ResponseBody
      public String hello() {
          return "Hello, Spring Boot!";
      }
  }
  ```

  在浏览器中访问 `http://localhost:8080/hello`，你将看到 "Hello, Spring Boot!" 的响应。

  总之，使用 Spring Boot 创建 Web 应用程序非常简单，你只需添加起步依赖，编写控制器类，并运行应用程序，就可以轻松处理请求和响应。