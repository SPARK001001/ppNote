pipenv  install *** 安装依赖的包到虚拟环境

pipenv shell  进入虚拟环境

flask run 启动程序

​	FLASK_RUN_HOST  

​	FLASK_RUN_PORT  

​	FLASK_APP  

flask. url_for(index)  根据函数名显示路由相对路径

flask routes 查看路由、端点映射

@app.before_request   after_request...   函数执行前后执行，类型aop

flask.jsonify(name='Grey Li', gender='male')  返回json数据
