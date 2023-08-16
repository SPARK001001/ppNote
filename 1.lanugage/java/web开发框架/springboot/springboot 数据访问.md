**Spring Boot 数据访问：** 了解如何使用 Spring Boot 进行数据访问，包括使用 Spring Data JPA、Spring Data JDBC 等。

- 使用 Spring Boot 进行数据访问非常方便，它提供了多种数据访问方式，包括 Spring Data JPA、Spring Data JDBC 等。以下是使用 Spring Boot 进行数据访问的基本步骤和示例：

  **使用 Spring Data JPA 进行数据访问：**

  1. **添加起步依赖：**
     在项目的 `pom.xml` 文件中添加 `spring-boot-starter-data-jpa` 起步依赖，它包含了 Spring Data JPA 和 JPA 实现（如 Hibernate）等组件。

  ```xml
  <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-data-jpa</artifactId>
  </dependency>
  ```

  2. **创建实体类：**
     创建一个 JPA 实体类，使用注解标记实体的属性和关系。

  ```java
  import javax.persistence.Entity;
  import javax.persistence.GeneratedValue;
  import javax.persistence.GenerationType;
  import javax.persistence.Id;
  
  @Entity
  public class User {
  
      @Id
      @GeneratedValue(strategy = GenerationType.IDENTITY)
      private Long id;
      private String username;
      private String email;
  
      // Getters and setters
  }
  ```

  3. **创建 JPA Repository：**
     创建一个继承自 `JpaRepository` 的接口，这将自动提供基本的 CRUD 操作和查询方法。

  ```java
  import org.springframework.data.jpa.repository.JpaRepository;
  
  public interface UserRepository extends JpaRepository<User, Long> {
  }
  ```

  4. **使用 Repository 进行操作：**
     在服务类中使用 `UserRepository` 来进行数据库操作。

  ```java
  import org.springframework.beans.factory.annotation.Autowired;
  import org.springframework.stereotype.Service;
  
  @Service
  public class UserService {
  
      private final UserRepository userRepository;
  
      @Autowired
      public UserService(UserRepository userRepository) {
          this.userRepository = userRepository;
      }
  
      public User createUser(User user) {
          return userRepository.save(user);
      }
  
      public User getUserById(Long id) {
          return userRepository.findById(id).orElse(null);
      }
  }
  ```

  **使用 Spring Data JDBC 进行数据访问：**

  1. **添加起步依赖：**
     在项目的 `pom.xml` 文件中添加 `spring-boot-starter-data-jpa` 起步依赖，它包含了 Spring Data JDBC 和 Spring Data JPA 等组件。

  ```xml
  <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-data-jdbc</artifactId>
  </dependency>
  ```

  2. **创建实体类：**
     创建一个简单的 Java 类来表示实体。

  ```java
  import org.springframework.data.annotation.Id;
  
  public class User {
  
      @Id
      private Long id;
      private String username;
      private String email;
  
      // Getters and setters
  }
  ```

  3. **使用 Repository 进行操作：**
     创建一个继承自 `CrudRepository` 的接口，使用 Spring Data JDBC 提供的方法来进行数据库操作。

  ```java
  import org.springframework.data.repository.CrudRepository;
  
  public interface UserRepository extends CrudRepository<User, Long> {
  }
  ```

  4. **使用 Repository 进行操作：**
     在服务类中使用 `UserRepository` 来进行数据库操作，与之前的示例类似。

  总结起来，Spring Boot 提供了多种数据访问方式，如 Spring Data JPA 和 Spring Data JDBC。你只需添加相应的起步依赖，定义实体类和 Repository 接口，就可以方便地进行数据访问操作。