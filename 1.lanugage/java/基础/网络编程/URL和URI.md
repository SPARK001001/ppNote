熟悉 `java.net.URL` 和 `java.net.URI` 类，了解如何处理统一资源定位符和统一资源标识符。

- `java.net.URL`（统一资源定位符）和 `java.net.URI`（统一资源标识符）是 Java 中用于处理和表示统一资源定位的类。它们用于解析和操作 URLs（网址）和 URIs（标识符），允许你在应用程序中处理网络资源。

  **`java.net.URL` 类：**
  `URL` 类表示一个统一资源定位符，它可以用于定位到网络上的资源。`URL` 类提供了方法来访问 URL 的各个组成部分（协议、主机、端口、路径等），以及打开连接来获取资源的输入流。

  基本使用示例：
  ```java
  import java.net.*;
  
  public class URLExample {
      public static void main(String[] args) {
          try {
              URL url = new URL("https://www.example.com");
              System.out.println("Protocol: " + url.getProtocol());
              System.out.println("Host: " + url.getHost());
              System.out.println("Port: " + url.getPort());
              System.out.println("Path: " + url.getPath());
              
              InputStream inputStream = url.openStream();
              // Read data from the input stream...
          } catch (MalformedURLException e) {
              e.printStackTrace();
          } catch (Exception e) {
              e.printStackTrace();
          }
      }
  }
  ```

  **`java.net.URI` 类：**
  `URI` 类用于表示统一资源标识符，它与 `URL` 类类似，但不限于网络资源。`URI` 主要用于表示一个标识符，可以是网络上的资源或本地文件系统中的资源。

  基本使用示例：
  ```java
  import java.net.*;
  
  public class URIExample {
      public static void main(String[] args) {
          try {
              URI uri = new URI("https://www.example.com/page.html");
              System.out.println("Scheme: " + uri.getScheme());
              System.out.println("Host: " + uri.getHost());
              System.out.println("Path: " + uri.getPath());
              
              // You can also create a URI from a string without worrying about checked exceptions.
              URI newURI = URI.create("https://www.example.com");
          } catch (URISyntaxException e) {
              e.printStackTrace();
          } catch (Exception e) {
              e.printStackTrace();
          }
      }
  }
  ```

  总结：
  - `URL` 用于表示网络上的资源的统一资源定位符，提供了与网络资源相关的方法。
  - `URI` 用于表示任何类型的统一资源标识符，不仅限于网络资源，也适用于本地资源。

  在实际应用中，你可以使用 `URL` 和 `URI` 类来解析和操作不同类型的统一资源标识符，以便在程序中访问网络资源或其他资源。

