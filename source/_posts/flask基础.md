---
title: flask基础
date: 2019-09-07 21:56:31
categories: 技术
tags: 基础

---


### flask优点：轻巧、可扩展性

###### flask依赖

flask的基础从它三个依赖说起。第一个是路由，调试和WSGI（web服务器网关接口）子系统，由[Werkzeug](https://werkzeug-docs-cn.readthedocs.io/zh_CN/latest/)提供；第二个是模版系统由[Jinja2](http://docs.jinkan.org/docs/jinja2/)提供；第三个是命令行集成，由[Click](https://click-docs-zh-cn.readthedocs.io/zh/latest/)提供。这些依赖，是Flask开发者Armin Ronacher开发的。Flask原生不支持数据库访问、Web表单验证、用户身份验证等高级功能。这些功能以及其他大多数Web应用需要的核心服务都以扩展的形式实现，然后再与核心包集成。

###### 一个完整的应用（路由的定义）

```
from flask import Flask
app = Flask(__name__)
@app.route('/')   #装饰器定义路由
def index():      #视图函数
    return '<h1>Hello world</h1>'  #函数返回值为响应
    
@app.route('/user/<name>')   #动态路由
def user(name):
    return '<h1>Hello,{}!</h1>'.format(name) #动态参数
```

###### 调试模式

flask应用可以在调试模式中运行。在这个模式下会加载重载器和调试器。启用重载器后，Flask会监视项目的所有源码文件，发生变动时自动重启服务器，每次修改并保存源码文件后，服务器会自动重启，让改动生效。

调试器是一个基于Web的工具，当应用抛出来未处理的异常时，它会出现在浏览器中，这时Web浏览器变成一个交互式栈跟踪，可以在里面审查源码，在调用栈的任何位置计算表达式。

###### 启用服务器

```
export FLASK_APP=hello.py
export FLASK_DEBUG=1
flask run --host 0.0.0.0 --port 1234  
# 任何计算机能通过http://a.b.c.d:5000访问Web服务器，其中a.b.c.d是运行服务器的计算机的IP地址。
```

###### 请求-响应循环

Flask从客户端收到请求，要让视图函数能访问一些对象，这样才能处理请求。<u>请求对象</u>封装了客户端发送的HTTP请求。为避免大量参数把视图函数弄得混乱，Flask用上下文临时把某些对象变成全局可访问。

上下文全局变量

| 变量名      | 上下文     | 说明                                                   |
| :---------- | ---------- | ------------------------------------------------------ |
| current_app | 应用上下文 | 当前应用的应用实例                                     |
| g           | 应用上下文 | 处理请求时用作临时存储的对象，每次请求都会重设这个变量 |
| request     | 请求上下文 | 请求对象，封装了客户端发出的HTTP请求中的内容           |
| session     | 请求上下文 | 用户会话，值为一个字典，存储请求之间需要"记住"的值     |

Flask在分派请求之前激活（或推送）应用和请求上下文，请求处理完成后再将其删除。如果使用这些变量时没有激活上下文，会导致错误。获取应用上下文的方法是在应用实例上调用app.app_context()

```
from hello import app
from flask import current_app
app_ctx = app.app_context()
app_ctx.push()
name = current_app.name  #'hello'
app_ctx.pop()
```

###### 请求钩子

有时在处理请求之前或之后执行代码。例如在请求开始时，需要创建数据库连接或者验证发起请求的用户身份。为了避免在每个视图函数中都重复编写代码，Flask提供了注册通用函数的功能。

请求钩子通过装饰器实现。Flask支持4种钩子。

- before_request   注册一个函数，在每次请求之前运行。
- before_first_request  注册一个函数，只在处理第一个请求之前运行，可以用来添加服务器初始化任务。
- after_request  注册一个函数，如果没有未处理的异常抛出，在每次请求之后运行。
- teardown_request 注册一个函数，即使有未处理的异常抛出，也在每次请求之后运行。

###### 响应

响应就是一个简单的字符串，作为HTML页面回送客户端。但是HTTP响应中一个很重要的部分时状态码，Flask默认设为200，表面请求已被成功处理。如果视图函数返回的响应需要使用不同的状态码，可以把数字代码作为第二个返回值，添加到响应文本之后。如返回400状态码，表示请求无效。

```
@app.route('/')
def index():
    return '<h1>Bad Request</h1>', 400
```

响应有个特殊的类型，称为重定向。重定向的状态码通常是302。Flask提供redirect()用于生成这样响应。还有种特殊的响应由abort()函数生成，用于处理错误。状态码是404。

```
from flask import redirect,abort
@app.route('/')
def index():
return redirect('http://www.example.com')

@app.route('/user/<id>')
def get_user(id):
    user = load_user(id)
    if not user:
        abort(404) # 注意，abort()不会把控制权交还给调用它的函数，而是抛出异常。
       return '<h1>Hello, {}</h1>'.format(user.name）      
```

