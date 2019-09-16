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

信息除了从服务器流向用户，还需要把用户提供的数据交给服务器来处理。Flask-WTF

扩展对独立的WTForms包进行了包装，方便集成到Flask应用中。

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

