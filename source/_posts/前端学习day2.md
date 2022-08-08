---
title: 前端学习day2
date: 2022-08-07 21:12:41
categories: 技术
tags: 学习
---

### HTML标签

1. 标签由标签名、标签属性和文本内容三部分组成（注意：单标签没有文本内容）。

2. 标签属性是对标签的一种描述方式。

3. 标签属性分通用属性、自有属性和自定义属性。

4. 通用属性：所有标签都具有的属性。（除`<br/>`标签外）

   通用属性有：

   ​	id：用来给标签取一个<u>唯一</u>的名称。id名称在一个网页中必须是唯一的。

   ​	class：用来给标签取一个类名。

   ​	style：用来设置该标签的行内样式。

   ​	title：当鼠标移到该标签，所显示的提示内容。

5. 自定义标签属性：通常用来传值或用于图片懒加载等方面。

   格式：data-*

   ```html
   <img data-src="图片名" alt="提示文本"/>
   <p data-id="goodsid">...</p>
   ```



### table表格标签

table主要用于呈现格式化数据。表格是由行和列组成。

表格属性：

​		border：设置表格边框，默认单位是像素

​			width：设置表格宽度，默认单位是像素

​			align：设置表格对齐（left（默认）/center/right）

​			cellpadding：设置单元格文本与边框的距离

​			cellspacing：设置像素间隙，单元格边框间距

格式：

```html
<table border="1" width="400" cellspacing="0" cellpadding="10" align="center">
  <tr><!--表示行-->
    <th>学号</th><!--th:表头，主要对下面的内容起说明作用。th的内容会自动加粗和居中显示-->
    <th>姓名</th>
    ...
  </tr>
  <tr>
    <td>007</td><!--表示列-->
    <td>张三</td>
    ...
  </tr>
  ...
</table>
```

跨行/跨列属性主要用来绘制复杂表格。

​		rowspan：跨行

​		colspan：跨列

```html
<table border="1" width="500" align="center">
  <tr>
  	<td rowspan="2" align="center" valign="middle">内容区01</td><!--valign:垂直对齐（top/middle/bottom）-->
    <td>内容区02</td>
    <td rowspan="3">内容区03</td>
  </tr>
  <tr>
    <td>内容区02</td>
  </tr>
  <tr align="center">
  	<td>内容区01</td>
    <td>内容区02</td>
  </tr>
</table>
```

```html
<table border="1" width="500" align="center">
  <tr>
  	<td>内容区01</td>
    <td colspan="2">内容区02</td>
  </tr>
  <tr>
    <td>内容区01</td>
    <td>内容区02</td>
    <td>内容区03</td>
  </tr>
  <tr>
  	<td colspan="3" align="center">内容区01</td>
  </tr>
</table>
```

完整表格组成：caption（标题）、 thread（表头）、 tbody（表体）、 tfoot （表尾）四部分组成。

```html
<table border="1" width="600" align="center">
  <caption>学生信息表</caption>
  <thead>
    <tr>
      <th>学号</th>
      <th>姓名</th>
      <th>家庭住址</th>
      <th>备注</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>001</td>
      <td>Tom*</td>
      <td>aaaa</td>
      <td>该生为“三好学生”</td>
    </tr>
    <tr>
      <td>002</td>
      <td>Mickle</td>
      <td>bbbbb</td>
      <td></td>
    </tr>
    <tr>
      <td>003</td>
      <td>Mary*</td>
      <td>ccccc</td>
      <td></td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td colspan="4">附注：*为优秀学生。</td>
    </tr>
  </tfoot>
</table>
```



### form表单标签

form表单标签是所有标签最核心标签之一。它是用来实现前后端交互的一个重要标签。

常用属性：

​		name：表单名称

​		action：表单数据提交的地方（通常是一个后台文件名（.jsp/.php/.asp/.aspx/.py等），或网址）

​		method：前端提交数据到后端的方法，主要有：get和post，默认是get。

```html
<form name="stuInfo" action="#" method="get">
  <input type="submit">
</form>
```

#### 表单元素分为：

##### input类：主要用来输入，或发出指令。

 type：text/password/radio/checkbox/file/button/image/submit/reset

######  a.text：单行文本输入框 type="text"可以不写，默认值。

​		属性：placeholder（提示）/name（命名）/minlength和maxlength（最少/多输入的字符个数）/disabled（失效）/value（默认值）/pattern（正则匹配）

###### b.password：密码框 属性与text一样

###### c.radio：单选钮，通常是两项以上。

​		常用属性有：name（必须要有）/value/checked（选中）/disabled（失效）/readonly（只读）

###### d.checkbox：复选框，可以用来选择0项、1项或多项。

​		常用属性：name（必须要有）/value/checked（选中）/disabled（失效）/readonly（只读）

###### e.file（文件上传）

###### f.button：普通按钮，用它去调用脚本代码。

​		常用属性：value（按钮的标题）/disabled（失效）

###### g.image：图片按钮，用法与button一样。

​		有一个特殊属性：src（用来加载提示图片，用它替换了value）它有提交功能，与submit功能一样。

###### h.submit：提交按钮，用来将表单数据提交到后台。

​		常用属性：value（按钮的标题）/disabled（失效）

###### j.reset：重置按钮，将表单所有组件输入的内容全部清空，还原为初始状态。

​		常用属性：value（按钮的标题）/disabled（失效）

```html
<form action="">
    <!--1.文本框-->
    <!--<input type="text" name="test" placeholder="请输入一个数字" value="100" disabled="disabled"><br>-->
    <!--<input type="text" name="test" placeholder="请输入一个数字" value="100" readonly="readonly"><br>-->
    <!--<input type="text" name="test" placeholder="请输入一个数字" value="100" minlength="3" maxlength="6"><br>-->
    <!--2.密码框-->
    <input type="password"><br>
    <!--3.单选钮-->
    <input type="radio" name="sex" checked>男
    <input type="radio" name="sex">女
    
    <input type="radio" name="num">1
    <input type="radio" name="num">2
    <input type="radio" name="num" checked>3
    <!--4.复选框/检查框-->
    <input type="checkbox" name="hobby" checked>听音乐
    <input type="checkbox" name="hobby" checked>码代码
    <input type="checkbox" name="hobby">其他
    <!--5.文件上传按钮-->
    <input type="file"><br>
    <!--6.普通按钮-->
    <input type="button" value="登录" disabled><br>
    <!--7.图片按钮-->
    <input type="image" src="" title="刷新">
  	<!--8.提交按钮-->
  	<input type="submit">
  	<!--9.重置按钮-->
  	<input type="reset" value="取消">
</form>
```

##### 	textarea类：文本域（也可以叫多行文本框），主要用于输入大批量的内容。

​	常用属性：name/id/cols（列数）/rows（行数）/placeholder/minlength/maxlength/required（必须输入）/value

```html
<form action="">
  <textarea name="memo" id="memo" cols="30" rows="10">备注：</textarea>
</form>
```

##### 	select类：下拉列表框，默认用于单项选择。用option呈现每个选项。

​	multiple属性：表示可以多选，这时的下拉列表框变成了列表框

​	size：最多显示的行数

```html
<form action="">
  <label for="sex">性别：</label>
  <select id="sex">
    <option value="male">男</option>
    <option value="female">女</option>
  </select><br>
  <label for="course">课程：</label>
  <select id="course" multiple size="2">
    <option value="语文">语文</option>
    <option value="数学">数学</option>
    <option value="计算机">计算机</option>
    <option value="其它">其它</option>
  </select>
</form>
```

##### 	button类：普通按钮，具有提交功能。可以单独使用，不写在form元素中；如果写在form中，有提交功能

```html
<button id="btnOk">确认</button><!--这里的button主要用来调用js代码-->
<form action="">
  <input type="text" name="info">
  <button>提交</button><!--这里的button功能与input中的submit按钮功能一样-->
</form>
```



### iframe框架标签

iframe：框架集，是用来将多个网页文件组合成一个文件。

常用属性：

​		name：框架名

​		src：引入的外部html文件

​		scrolling：滚动条（yes/no/auto）

​		width：宽度（%/px）

​		height：高度（%/px）

​		frameborder：是否有边框（1/0）

​		marginheight：框架离顶部和底端的距离（%/px）

​		marginwidtnh：框架离左右的距离（%/px）

​		注意：在实际开发中尽量减少使用iframe，因为它破坏了前进和后退功能，且不利于SEO。

```html
<!--banner-->
<iframe src="iframe/banner.html" scrolling="no" width="100%" frameborder="0"></iframe>
<!--导航-->
<iframe src="iframe/nav.html" scrolling="no" width="30%" frameborder="0"></iframe>
<!--核心内容区-->
<iframe src="iframe/content.html" scrolling="no" width="70%" frameborder="0"></iframe>
```



> 没想到无聊也能成为生产力