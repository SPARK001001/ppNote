SSE（Server-Sent Events）在JavaScript中使用EventSource API来与服务器建立连接并监听实时事件流。以下是EventSource API的基本用法：

1. **创建EventSource实例：** 使用`EventSource`构造函数创建一个SSE连接。

```javascript
const eventSource = new EventSource('url');
```

替换 `'url'` 为服务器提供SSE事件流的URL。

2. **监听事件：** 使用`addEventListener`方法监听不同类型的事件。

```javascript
eventSource.addEventListener('event-name', (event) => {
  const eventData = event.data;
  // 处理事件数据
});
```

替换 `'event-name'` 为你服务器上定义的事件名称。

3. **处理连接状态：** `EventSource`对象有一些属性来处理连接状态。

```javascript
eventSource.onopen = (event) => {
  // 连接成功时的处理
};

eventSource.onerror = (event) => {
  // 连接出错时的处理
};

eventSource.onclose = (event) => {
  // 连接关闭时的处理
};
```

4. **关闭连接：** 当你不再需要连接时，应该手动关闭它。

```javascript
eventSource.close();
```

这就是基本的SSE JavaScript API用法。通过这些API，你可以建立到服务器的持久连接，监听实时事件，处理事件数据，并在需要时关闭连接。SSE在客户端-服务器之间提供了一种轻量级的实时通信方式，特别适用于需要实时数据推送的场景。