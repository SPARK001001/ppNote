解释HTTP/2和WebSocket是什么，以及Nginx如何支持它们。

- **HTTP/2：**
  HTTP/2是一种用于在Web浏览器和服务器之间传输数据的协议，它是HTTP/1.1的升级版本。HTTP/2的目标是提供更快、更高效的Web性能，通过多路复用、头部压缩、服务器推送等特性来优化数据传输。HTTP/2可以在不修改应用程序代码的情况下提供更快的页面加载速度和更好的用户体验。

  **WebSocket：**
  WebSocket是一种用于在浏览器和服务器之间实现全双工通信的协议。与HTTP不同，WebSocket在连接建立后，允许双方在一个持久连接上发送消息，而无需频繁建立和关闭连接。WebSocket适用于实时通信、即时聊天、实时数据传输等场景。

  **Nginx对HTTP/2和WebSocket的支持：**
  Nginx从版本1.9.5开始支持HTTP/2协议，使Web应用能够充分利用HTTP/2的性能优势。要启用HTTP/2，只需在Nginx配置中使用`http2`关键字，如下所示：

  ```nginx
  server {
      listen 443 ssl http2;
      server_name example.com;
      # SSL配置
  }
  ```

  至于WebSocket，Nginx也可以支持它，但需要特定的配置来实现。WebSocket的支持需要在Nginx配置中进行如下设置：

  ```nginx
  server {
      listen 80;
      server_name example.com;
  
      location /ws {
          proxy_pass http://backend;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection "Upgrade";
      }
  }
  ```

  在上面的配置中，`proxy_pass`将WebSocket连接代理到后端服务器，而`proxy_set_header`指令用于设置协议升级头部，使Nginx知道连接需要升级到WebSocket协议。

  需要注意的是，虽然Nginx可以支持HTTP/2和WebSocket，但配置和特性可能会根据具体版本而有所不同。在使用Nginx支持这些协议时，请查阅官方文档以获取详细的配置和使用说明。