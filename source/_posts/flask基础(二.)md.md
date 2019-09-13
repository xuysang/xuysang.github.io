---
title: flask基础(二)
date: 2019-09-13 21:35:25
categories: 技术
tags: 基础
---

**中秋节快乐!**

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

##### 表单类

