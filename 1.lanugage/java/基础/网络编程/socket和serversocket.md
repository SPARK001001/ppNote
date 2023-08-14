理解 `Socket` 和 `ServerSocket` 类，以及它们在客户端和服务器之间建立连接的作用。

- `Socket` 和 `ServerSocket` 类是 Java 提供的用于实现网络通信的关键类，它们在客户端和服务器之间建立连接并进行数据传输。以下是它们的作用和基本概念：

  1. **Socket 类：**
     - `Socket` 类代表客户端套接字，用于建立与服务器的连接并进行数据通信。
     - 通过 `Socket` 类，客户端可以发起连接请求，发送数据给服务器，并接收来自服务器的响应。
     - 客户端通过 `Socket` 类的构造方法来指定服务器的 IP 地址和端口号，从而连接到服务器。
     - `Socket` 提供了用于获取输入流和输出流的方法，用于进行数据的读取和写入。

  2. **ServerSocket 类：**
     - `ServerSocket` 类代表服务器套接字，用于监听指定的端口，接受客户端的连接请求，并与客户端进行通信。
     - 服务器通过 `ServerSocket` 类创建一个监听的套接字，并通过 `accept()` 方法等待客户端的连接请求。
     - 一旦有客户端发起连接请求，`accept()` 方法会返回一个新的 `Socket` 实例，该实例用于与客户端进行通信。
     - 服务器可以通过监听多个端口来处理多个客户端的连接请求。

  基本使用示例：

  客户端：
  ```java
  import java.io.*;
  import java.net.*;
  
  public class Client {
      public static void main(String[] args) {
          try {
              Socket socket = new Socket("localhost", 12345);
  
              OutputStream outputStream = socket.getOutputStream();
              PrintWriter writer = new PrintWriter(outputStream, true);
              writer.println("Hello, Server!");
  
              InputStream inputStream = socket.getInputStream();
              BufferedReader reader = new BufferedReader(new InputStreamReader(inputStream));
              String response = reader.readLine();
              System.out.println("Server response: " + response);
  
              socket.close();
          } catch (IOException e) {
              e.printStackTrace();
          }
      }
  }
  ```

  服务器：
  ```java
  import java.io.*;
  import java.net.*;
  
  public class Server {
      public static void main(String[] args) {
          try {
              ServerSocket serverSocket = new ServerSocket(12345);
              System.out.println("Server is listening...");
  
              while (true) {
                  Socket socket = serverSocket.accept();
                  System.out.println("Client connected: " + socket.getInetAddress().getHostAddress());
  
                  InputStream inputStream = socket.getInputStream();
                  BufferedReader reader = new BufferedReader(new InputStreamReader(inputStream));
                  String message = reader.readLine();
                  System.out.println("Received message from client: " + message);
  
                  OutputStream outputStream = socket.getOutputStream();
                  PrintWriter writer = new PrintWriter(outputStream, true);
                  writer.println("Message received!");
  
                  socket.close();
              }
          } catch (IOException e) {
              e.printStackTrace();
          }
      }
  }
  ```

  在这个示例中，客户端通过 `Socket` 类连接到服务器的 IP 地址和端口号，发送一条消息，服务器接收并回复。通过 `ServerSocket` 类，服务器监听一个端口，等待客户端连接请求，并在连接建立后进行数据通信。

  需要注意，`Socket` 和 `ServerSocket` 类在网络编程中仅涉及到基本的连接和数据传输，实际项目中还需要考虑异常处理、并发处理、安全性等问题。