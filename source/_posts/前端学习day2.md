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

4. 通用属性：所有标签都具有的属性。

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



### tabke表格标签

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

表单元素分为：

​		input类

​		textarea类

​		select类

​		button类