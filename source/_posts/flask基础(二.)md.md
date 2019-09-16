---
title: flask基础(二)
date: 2019-09-13 21:35:25
categories: 技术
tags: 基础
---

**中秋快乐**

### flask扩展

这篇主要介绍三个扩展，在flask应用中，这三个扩展是非常具有实用性的。第一个是Web表单；第二个是数据库；第三个是电子邮件。

#### Web表单（FLASK-WTF）

信息除了从服务器流向用户，还需要把用户提供的数据交给服务器来处理。Flask-WTF扩展对独立的WTForms包进行了包装，方便集成到Flask应用中。

##### 配置

```
app = Flask(__name__)
app.config['SECRET_KEY'] = 'dan yuan ren chang jiu'
```

##### 定义表单类—>在视图函数中处理表单—>把表单渲染成HTML

```
#定义表单类
from flask_wtf import FlaskForm
from wtforms import StringField,SubmitField
from wtforms.validators import DataRequired

class NameForm(FlaskForm):
    name = StringField('what is your name?',validators=[DataRequired()])
    submit = SubmitField('Submit')
    
#在视图中处理表单
@app.route('/', method=['GET','POST'])
def index():
    name = None
    form = NameForm()
    if form.validate_on_submit():
        name = form.name.data
        form.name.data = ''
    return render_template('index.html',form=form,name=name)
‘’‘
首次访问应用时，服务器会收到一个没有表单数据的GET请求，所以if语句的内容会被跳过，会直接渲染模板，并将值为None的name变量作为参数。用户看到的浏览器显示了一个为空的表单。当用户提交表单后，服务器会收到一个包含数据的POST请求，if后面的不为空验证函数通过后，用户输入的名字可以通过字段的data属性获取，再把data属性设为空字符串，清空表单字段。再次渲染表单时，各字段没有内容。最后渲染模板，name参数的值为表单中输入的名字。
‘’‘

#把表单渲染成HTML
<form method='POST'>
    {{ form.hidden_tag() }}
    {{ form.name.label }} {{ form.name(id='my-text-field') }}
    {{ form.submit() }}
</form>
#表单的form.hidden_tag()元素生成一个隐藏的字段，供Flask-WTF的CSRF防护机制使用。
‘’‘
Flask-Bootstrap扩展提供了高层级的辅助函数，可以使用Bootstrap预定义的表单样式渲染整个Flask-WTF表单，只需调用一次即可。
’‘’
{% import "bootstrap/wtf.html" as wtf %}
{{ wtf.quick_form(form) }}
```

##### 重定向和用户会话

```
from flask import Flask,render_template,session,redirect,url_for

@app.route('/',methods=['GET','POST'])
def index():
    form = NameForm
    if form.validate_on_submit():
        session['name'] = form.name.data
        return redirect(url_for('index'))
    return render_template('index.html',form=form,name=session.get('name'))
#变量name保存在用户会话中，以便在请求间记住数据。用户会话时一种私有存储，每个连接到服务器的客户端都可以访问。
‘’‘
最后是使视图函数调用redirect()函数，这是Flask提供的辅助函数，用于生成HTTP重定向响应。它的参数是重定向的URL，这里使用的是应用的根URL，可以写成redirect('/')，不过上面使用了URL生成函数url_for()。url_for()函数的第一个且唯一必须指定的参数是端点名，即路由的内部名称。默认情况下，路由的端点是相应视图函数的名称。
最后使用get()获取字典中键对应的值，可以避免未找到键时抛出异常。如果指定的键不存在，则get()方法返回默认值None。
‘’‘
```

##### 闪现消息

当用户提交有一项错误的登陆表单后，服务器发回的响应重新渲染登陆表单，并在表单上面显示消息，flash()函数可以实现这种效果。

```
from flask import Flask,render_template,session,redirect,url_for,flash

@app.route('/', methods=['GET','POST'])
def index():
    form = NameForm()
    if form.validate_on_submit():
        old_name = session.get('name')
        if old_name is not None and old_name != form.name.data:
            flash('Looks like you have changed your name!')
        session['name'] = form.name.data
        return redirect(url_for('index'))
    return render_template('index.html',form = form,name = session.get('name'))
```

调用flash()函数不能把消息显示出来，应用的模板还要渲染这些消息。最好在基模板中渲染消息，因为这样所有的页面都能显示需要显示的消息。Flask把get_flashed_message()函数开放给模板，用于获取并渲染闪现消息。

```
{% block content %}
<div class="container">
    {% for message in get_flash_messages() %}
    <div class="alert alert-warning">
        <button type="button" class="close" data-dismiss="alert">&times;</buttom>
        {{ message }}
    </div>
    {% endfor %}
    
    {% block page_content %}{% endblock%}
</div>
{% endblock %}
‘’‘
这里使用了循环，在之前的请求循环中每次调用flash()函数时都会生成一个消息，所以可能有多个消息在排队等待显示。get_flashed_messages()函数获取的消息在下次调用时不会再次返回，闪现消息只显示一次就消失。
’‘’
```

#### 数据库

数据库按照一定规则保存应用的数据，应用再发起查询，取回所需的数据。Web应用最常使用基于关系模型的数据库，称为SQL数据库，使用结构化查询语言。近年来开始流行**文档数据库**和**键-值对数据库**，合称NoSQL数据库。

ORM：对象关系映射器，把高层的面向对象操作转换成低层的数据库指令。

SQLAlchemy是一个强大的关系型数据库框架，支持多种数据库后台。SQLAlchemy提供了高层ORM，也提供了使用数据库原生SQL的低层功能。Flask-SQLAlchemy是一个Flask扩展，简化了在Flask应用中使用SQLAlchemy的操作。

##### 配置数据库（以mysql为例）

| 数据库引擎 | URL                                              |
| ---------- | ------------------------------------------------ |
| MySQL      | mysql://username:password@hostname/database      |
| Postgres   | postgresql://username:password@hostname/database |
| SQLite     | sqlite:////absolute/path/to/database             |

hostname表示数据库服务所在的主机，可以是本地主机，也可以是远程服务器。数据库服务器上可以托管多个数据库，因此需要database表示要使用的数据库名。

```
from flask_sqlalchemy import SQLAlchemy
import pymysql

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql+pymysql://root:password@127.0.0.1/database'
app.config["SQLALCHEMY_TRACK_MODIFICATIONS"] = False
app.config["SECRET_KEY"] = "dan yuan ren chang jiu"
db = SQLAlchemy(app)
```

##### 定义模型

```
# 定义Role和User模型
class Role(db.Model):
    __tablename__ = 'roles'
    id = db.Column(db.Integer,primary_key=True)
    name = db.Column(db.String(64),unique=True)
    users = db.relationship('User',backref='role')
    
    def __repr__(self):
        return '<Role %r>' % self.name
class User(db.Model):
    __tablename__ = 'users'
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(64), unique=True, index=True)
    role_id = db.Column(db.Integer, db.ForeignKey('roles.id'))# 外键，这列的值是相应的Role的id值
    
    def __repr__(self):
        return '<User %r>' % self.username
‘’‘
类变量__tablename__定义在数据库中使用的表名。其余的类变量都是该模型的属性，定义为db.Column类的实例。
两个模型定义了__repr()__方法，返回一个具有可读性的字符串表示模型，供调试和测试使用。
db.relationship()中的backref参数向User模型中添加一个role属性，从而定义反向关系。通过User实例的这个属性可以获取对应的Role模型对象，而不用再通过role_id外键获取。
‘’‘

```

#####  数据库操作（增删改查）

###### 创建表

```
from hello import db
db.drop_all()
db.create_all()
```

如果数据库表已经存在数据库，create_all()不会重新创建或更新相应的表。如果修改模型后要把改动应用到现有的数据库中，暴力方式是先删除旧表再重新创建。

###### 插入行

```
from hello import Role, User
admin_role = Role(name = 'Admin')
mod_role = Role(name = 'Modertor')
user_role = Role(name = 'User')

user_john = User(username='john', role=admin_role)
user_susan = User(username='susan', role=user_role)
user_david = User(username='david', role=user_role)

db.session.add_all([admin_role, mod_role, user_role, user_john, user_susan, user_david])
#对数据库的改动通过数据库会话管理，会话由db.session表示。先添加到会话中，再调用commit()方法提交会话。
db.session.commit()
```

###### 删除行

```
db.session.delete(mod_role)
db.session.commit()
```

###### 修改行

```
admin_role.name = 'Administrator'
db.session.add(admin_role)
db.session.commit()
```

###### 查询行

Flask-SQLAlchemy为每个模型类都提供了query对象。最基本的模型查询是使用all()方法取回对应表中的所有记录。

```
Role.query.all()
User.query.all()
# 使用过滤器可以配置query对象进行更精确的数据库查询。
User.query.filter_by(role=user_role).all()
user_role = Role.query.filter_by(name='User').first() #first()方法只返回第一个结果
```

##### 在视图函数中操作数据库

```
@app.route('/', methods=['GET','POST'])
def index():
    form = NameForm()
    if form.validate_on_submit():
        user = User.query.filter_by(username=form.name.data).first()
        if user is None:
            user = User(username=form.name.data)
            db.session.add(user)
            db.session.commit()
            session['known'] = False
        else:
            session['known'] = True
        session['name'] = form.name.data
        form.name.data = ''
        return redirect(url_for('index'))
    return render_template('index.html', form=form, name=session.get('name'), known=session.get('known', False))
```

对应的模板可以进一步修改，对已知用户和新用户，显示不同的内容。

```
{% extends "base.html" %}
{% import "bootstrap/wtf.html" as wtf %}

{% block title %}Flasky{% endblock %}

{% block page_content %}
<div class="page-header">
    <h1>Hello, {% if name %}{{ name }}{% else %}Stranger{% endif %}!</h1>
    {% if not known %}
    <p>Pleased to meet you!</p>
    {% else %}
    <p>Happy to see you again!</p>
    {% endif %}
</div>
{{ wtf.quick_form(form) }}
{% endblock %}
```

