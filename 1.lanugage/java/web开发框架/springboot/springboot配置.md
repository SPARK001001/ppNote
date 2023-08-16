**Spring Boot 配置：** 了解 Spring Boot 的配置方式，包括使用 `application.properties` 或 `application.yml` 进行配置，以及优先级和覆盖规则。

- Spring Boot 提供了多种配置方式，其中最常用的是使用 `application.properties` 或 `application.yml` 文件进行配置。这些配置文件可以用于配置应用程序的属性、Bean、连接池等各种设置。以下是关于 Spring Boot 配置的一些重要概念和使用方法：

  **使用 `application.properties` 或 `application.yml`：**

  1. **`application.properties`：** 这是一个文本文件，使用简单的 `key=value` 形式来配置属性。例如：

     ```properties
     spring.datasource.url=jdbc:mysql://localhost:3306/mydb
     server.port=8080
     ```

  2. **`application.yml`：** 这是一个更为人类可读的 YAML 格式配置文件，使用缩进和冒号表示层级。例如：

     ```yaml
     spring:
       datasource:
         url: jdbc:mysql://localhost:3306/mydb
       server:
         port: 8080
     ```

  **优先级和覆盖规则：**

  Spring Boot 的配置遵循一定的优先级和覆盖规则，确保了不同配置来源的正确处理：

  1. **命令行参数：** 通过命令行参数可以覆盖配置文件中的属性值。例如：`java -jar myapp.jar --server.port=9090`。

  2. **`application.properties` 或 `application.yml` 文件：** 配置文件中的属性会被读取，但命令行参数可以覆盖它们。

  3. **环境变量：** 环境变量中的属性可以覆盖配置文件和命令行参数中的属性。

  4. **配置属性文件：** Spring Boot 支持将配置属性单独存放在 `.properties` 或 `.yml` 文件中，然后通过 `@PropertySource` 注解引入。这些属性会被添加到应用的配置中。

  5. **默认值：** 如果属性没有被设置，可以使用 `@Value` 注解的默认值来设置默认属性值。

  **多环境配置：**

  Spring Boot 还支持多环境配置，例如针对不同的开发、测试和生产环境。可以通过创建不同的配置文件，如 `application-dev.properties`、`application-test.properties`，然后在启动应用时通过 `spring.profiles.active` 属性指定当前活动的环境。

  **使用示例：**

  假设你要配置一个连接到 MySQL 数据库的应用。你可以在 `application.properties` 或 `application.yml` 中配置数据库相关属性：

  ```properties
  # 使用 properties 配置
  spring.datasource.url=jdbc:mysql://localhost:3306/mydb
  spring.datasource.username=root
  spring.datasource.password=secret
  
  # 使用 YAML 配置
  spring:
    datasource:
      url: jdbc:mysql://localhost:3306/mydb
      username: root
      password: secret
  ```

  总结起来，Spring Boot 配置可以使用 `application.properties` 或 `application.yml` 文件，并遵循一定的优先级和覆盖规则，以及多环境配置支持，使得应用程序的配置变得灵活、可维护和易于管理。



- 在 Spring Boot 中，可以使用不同环境下的配置文件来管理应用程序的配置。Spring Boot 支持多种格式的配置文件，如 `.properties` 和 `.yml`。通过为不同环境创建不同的配置文件，可以在不同的部署环境中轻松管理配置参数。

  以下是如何使用不同环境下的配置文件的示例：

  1. **创建配置文件：**
     首先，创建默认的配置文件 `application.properties` 或 `application.yml`。这是默认的配置文件，适用于所有环境。

  2. **为不同环境创建配置文件：**
     创建针对不同环境的配置文件。命名规则是 `application-{profile}.properties` 或 `application-{profile}.yml`，其中 `{profile}` 是环境名称（如 `dev`、`prod` 等）。

     例如，创建一个针对开发环境的配置文件 `application-dev.properties` 或 `application-dev.yml`。

  3. **定义环境变量：**
     在应用启动时，可以通过设置环境变量来指定当前的环境。例如，在启动命令中使用 `-Dspring.profiles.active=dev` 来指定使用开发环境。

  **示例：**

  假设你有一个使用 `.properties` 配置文件的 Spring Boot 应用程序，以下是示例配置文件的结构：

  - `application.properties`：默认的配置文件，适用于所有环境。

  ```properties
  spring.datasource.url=jdbc:mysql://localhost:3306/mydb
  spring.datasource.username=root
  spring.datasource.password=secret
  ```

  - `application-dev.properties`：用于开发环境的配置文件。

  ```properties
  # 开发环境下的数据库配置
  spring.datasource.url=jdbc:mysql://localhost:3306/devdb
  ```

  - `application-prod.properties`：用于生产环境的配置文件。

  ```properties
  # 生产环境下的数据库配置
  spring.datasource.url=jdbc:mysql://production-server:3306/proddb
  ```

  在上面的示例中，应用程序启动时，如果设置了环境变量 `spring.profiles.active=dev`，则应用程序将使用 `application-dev.properties` 中的配置。

  类似地，你也可以使用 `.yml` 格式的配置文件，只需将示例中的 `.properties` 文件改为 `.yml` 文件，并使用相应的 YAML 格式。

  总之，通过在 Spring Boot 应用程序中使用不同环境下的配置文件，你可以方便地管理不同环境的配置参数，从而适应不同的部署环境。