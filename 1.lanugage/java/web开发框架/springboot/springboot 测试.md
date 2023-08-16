在 Spring Boot 中，测试是非常重要的，因为它可以帮助你验证应用程序的正确性、稳定性和性能。Spring Boot 提供了丰富的测试支持，包括单元测试和集成测试。以下是如何编写单元测试和集成测试，以及如何使用 Spring Boot 的测试支持的示例：

**单元测试示例：**

1. **创建测试类：**
   在测试源代码目录（通常是 `src/test/java`）中创建测试类。

2. **编写测试方法：**
   在测试类中，编写测试方法，并使用 JUnit 或其他测试框架执行测试。

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.assertEquals;

class MyServiceTest {

    @Test
    void testAddNumbers() {
        MyService service = new MyService();
        int result = service.addNumbers(2, 3);
        assertEquals(5, result);
    }
}
```

**集成测试示例：**

1. **创建测试类：**
   在测试源代码目录（通常是 `src/test/java`）中创建测试类。

2. **使用 Spring Boot 测试注解：**
   使用 Spring Boot 提供的测试注解，如 `@SpringBootTest`、`@RunWith(SpringRunner.class)`。

```java
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import static org.junit.jupiter.api.Assertions.assertEquals;

@SpringBootTest
class MyIntegrationTest {

    @Autowired
    private MyService myService;

    @Test
    void testAddNumbers() {
        int result = myService.addNumbers(2, 3);
        assertEquals(5, result);
    }
}
```

**使用 Spring Boot 的测试支持：**

1. **内嵌容器测试：**
   Spring Boot 允许在测试中使用内嵌的 Web 服务器（如 Tomcat、Jetty）来运行应用程序。

2. **自动配置：**
   Spring Boot 自动配置测试环境，使得测试变得更加简单。例如，你可以通过 `@Autowired` 注入 Bean，而不需要手动配置。

3. **属性替换：**
   Spring Boot 的测试支持可以自动替换测试环境中的属性，以适应测试需要。

总之，Spring Boot 提供了丰富的测试支持，使得编写单元测试和集成测试变得更加容易。你可以使用 Spring Boot 提供的注解、自动配置和内嵌容器来编写和执行测试，从而确保应用程序的正确性和稳定性。