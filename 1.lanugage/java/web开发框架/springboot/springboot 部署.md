**Spring Boot 部署：** 学会将 Spring Boot 应用程序打包成可执行的 JAR 或 WAR 文件，以及如何部署到不同的容器中。

- 将 Spring Boot 应用程序部署到不同的容器中是相对简单的，Spring Boot 提供了多种打包方式（JAR 或 WAR）以及内嵌的容器，使部署过程变得更加方便。以下是将 Spring Boot 应用程序打包和部署的基本步骤和示例：

  **将 Spring Boot 应用程序打包成可执行的 JAR 文件：**

  1. **创建可执行 JAR 文件：**
     在项目的 `pom.xml` 文件中，使用 `spring-boot-maven-plugin` 插件来创建可执行 JAR 文件。

  ```xml
  <build>
      <plugins>
          <plugin>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-maven-plugin</artifactId>
          </plugin>
      </plugins>
  </build>
  ```

  2. **使用 Maven 打包：**
     运行以下命令来使用 Maven 打包应用程序。

  ```sh
  mvn package
  ```

  3. **运行可执行 JAR 文件：**
     使用以下命令来运行可执行 JAR 文件。

  ```sh
  java -jar target/myapp.jar
  ```

  **将 Spring Boot 应用程序部署到外部容器（如 Tomcat）：**

  1. **将 Spring Boot 应用程序打包成 WAR 文件：**
     在项目的 `pom.xml` 文件中，将 `<packaging>` 设置为 `war`，并确保排除 Spring Boot 内嵌的容器依赖。

  ```xml
  <packaging>war</packaging>
  ```

  2. **配置 Spring Boot 启动类：**
     在 Spring Boot 启动类中继承 `SpringBootServletInitializer` 类，并重写 `configure` 方法。

  ```java
  import org.springframework.boot.builder.SpringApplicationBuilder;
  import org.springframework.boot.web.servlet.support.SpringBootServletInitializer;
  
  public class ServletInitializer extends SpringBootServletInitializer {
  
      @Override
      protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
          return application.sources(MyApplication.class);
      }
  }
  ```

  3. **部署 WAR 文件到外部容器：**
     将打包生成的 WAR 文件部署到外部容器（如 Tomcat）的 webapps 目录下，然后启动容器即可。

  总结起来，Spring Boot 提供了便捷的方式将应用程序打包成可执行的 JAR 或 WAR 文件，并且可以选择将 WAR 文件部署到外部容器中。这使得部署过程变得非常简单，不需要过多的配置和步骤。