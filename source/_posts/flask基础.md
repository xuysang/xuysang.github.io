---
title: flask基础
date: 2019-09-07 21:56:31
categories: 技术
tags: 基础

---


### flask优点：轻巧、可扩展性

###### flask依赖

flask的基础从它三个依赖说起。第一个是路由，调试和WSGI（web服务器网关接口）子系统，由[Werkzeug](https://werkzeug-docs-cn.readthedocs.io/zh_CN/latest/)提供；第二个是模版系统由[Jinja2](http://docs.jinkan.org/docs/jinja2/)提供；第三个是命令行集成，由[Click](https://click-docs-zh-cn.readthedocs.io/zh/latest/)提供。这些依赖，是Flask开发者Armin Ronacher开发的。Flask原生不支持数据库访问、Web表单验证、用户身份验证等高级功能。这些功能以及其他大多数Web应用需要的核心服务都以扩展的形式实现，然后再与核心包集成。

###### 一个完整的应用

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

