**HTTP 方法**：

- 解释 GET、POST、PUT、DELETE 等 HTTP 方法在 Flask 中的作用。

  - 在 Flask 中，HTTP 方法（GET、POST、PUT、DELETE 等）用于定义不同类型的客户端请求，从而告诉服务器执行特定的操作。每个 HTTP 方法都具有不同的语义和用途，Flask 提供了相应的机制来处理这些方法。

    以下是这些常见的 HTTP 方法在 Flask 中的作用：

    1. **GET**：
       - 用途：用于从服务器获取资源的信息，通常用于读取操作。
       - Flask 中的处理：在 Flask 中，通过为视图函数添加 `@app.route` 装饰器并指定 GET 方法，可以处理来自客户端的 GET 请求。
       - 示例：
         ```python
         @app.route('/user/<int:user_id>', methods=['GET'])
         def get_user(user_id):
             # 获取用户信息并返回
             pass
         ```

    2. **POST**：
       - 用途：用于向服务器提交数据，通常用于创建新资源。
       - Flask 中的处理：通过为视图函数添加 `@app.route` 装饰器并指定 POST 方法，可以处理来自客户端的 POST 请求。
       - 示例：
         ```python
         @app.route('/user', methods=['POST'])
         def create_user():
             # 创建新用户并返回结果
             pass
         ```

    3. **PUT**：
       - 用途：用于更新服务器上的资源，通常用于修改资源的全部属性。
       - Flask 中的处理：通过为视图函数添加 `@app.route` 装饰器并指定 PUT 方法，可以处理来自客户端的 PUT 请求。
       - 示例：
         ```python
         @app.route('/user/<int:user_id>', methods=['PUT'])
         def update_user(user_id):
             # 更新用户信息并返回结果
             pass
         ```

    4. **DELETE**：
       
       - 用途：用于从服务器删除资源，通常用于删除指定资源。
       - Flask 中的处理：通过为视图函数添加 `@app.route` 装饰器并指定 DELETE 方法，可以处理来自客户端的 DELETE 请求。
       - 示例：
         ```python
         @app.route('/user/<int:user_id>', methods=['DELETE'])
         def delete_user(user_id):
             # 删除用户并返回结果
             pass
         ```

    在每个示例中，`methods` 参数用于指定所处理的 HTTP 方法。根据客户端请求的方法，Flask 会自动将请求分发到相应的视图函数。这种方式使得开发者可以轻松地处理不同类型的请求，执行适当的操作，并返回相应的结果。

- 如何使用装饰器限制视图函数接受的请求方法。

  - 在 Flask 中，您可以使用 `methods` 参数来限制视图函数可以接受的请求方法。通过将所允许的请求方法作为列表传递给 `methods` 参数，您可以确保只有特定的 HTTP 方法能够触发该视图函数。以下是如何使用装饰器限制视图函数接受的请求方法：

    ```python
    from flask import Flask
    
    app = Flask(__name__)
    
    @app.route('/example', methods=['GET', 'POST'])
    def example():
        if request.method == 'GET':
            # 处理 GET 请求
            pass
        elif request.method == 'POST':
            # 处理 POST 请求
            pass
    
    if __name__ == '__main__':
        app.run()
    ```

    在上述示例中，`@app.route('/example', methods=['GET', 'POST'])` 告诉 Flask 将 `example` 视图函数映射到 `/example` 路径，并限制该视图函数只能接受 GET 和 POST 请求。通过检查 `request.method`，您可以在视图函数内部根据请求方法执行不同的操作。

    请注意，如果不指定 `methods` 参数，视图函数默认会接受所有类型的请求方法。限制请求方法可以提高应用的安全性，确保视图函数只能被设计用来处理的特定类型的请求所触发。