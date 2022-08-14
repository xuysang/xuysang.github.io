---
title: 前端学习day5
date: 2022-08-14 15:02:52
categories: 技术
tags: 学习
---

## 定位

### 1.定位（position）

​	设定元素在文档中的位置。会将标签（元素）转换为块级。

### 2.定位分类（属性值）

​	1）static：静态定位

​			默认值，没有定位，不能设置偏移值（left/top/right/bottom），占用标准流（文档流）

​	2）relative：相对定位

​			占用标准流（文档流），它会出现在文档流中它该出现的位置。可以通过设置偏移值改变其位置。它相对于自身所占的位置做偏移。

​	3）absolute：绝对定位

​			脱离文档流，相对于body做偏移。

​			绝对定位一般与相对定位结合使用，它相对的父级是relative定义的元素做偏移。relative的元素必须是absolute的父级。

​			在项目开发中，一般用relative+absolute结合使用。

​	4）fixed：固定定位

​			脱离文档流，相对于浏览器窗口左上角（0，0）做偏移，它与relative设定的对象没有关系，也就是说，它跟父级的定位没有关系。一般在开发中用来固定导航栏。

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
  <title>Title</title>
  <style>
    .wrapper{
      width:600px;
      height:400px;
      border:1px solid #000;
      margin:0 auto；
      position:relative;
    }
    .box1,.box2,.box3{
      width:150px;
      height:150px;
      border:1px dotted red;
      display:inline-block;
    }
    /*.box2{
    	position:static;<!--不会发生偏移-->
    	left:-100px;
    	top:100px;
    }
    */
    .box2{
    	position:absolute;
    	left:-100px;
    	top:100px;
    }
  </style>
</head>
<body>
<div class="wrapper">
  <div class="box1"></div>
  <div class="box2"></div>
  <div class="box3"></div>
</div>  
</body>
</html>
```

### 3.z-index

当多个元素添加绝对定位，元素将会叠加在一起，使用z-index可以设置元素显示的层次。

文档流默认的z-index的值为0。

用在static和relative元素上将无效。

### 4.网站开发策略

先整体再局部，至顶向下，逐步细化。

1）双飞翼布局：由三列组成，两端固定，中间自适应。

​	双飞翼布局的优点：

​	（1）兼容性好，兼容所有主流浏览器

​	（2）因为在DOM中center_panel在三列结构的最前面，因此可以实现主要内容的优先加载。

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
  <title>双飞翼布局</title>
  <style>
    .container{
      width:100%;
      overflow:hidden;
    }
    .column{
      float:left;
      height:200px;
    }
    .left{
      width:100%;
      background-color:#0f0;
      margin-left:-100%;
    }
    .center{
      width:300px;
      background-color:#f00;
    }
    .right{
      width:300px;
      background-color:#00f;
      margin-left:-300px;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="column center"></div>
    <div class="column left"></div>
    <div class="column right"></div>
  </div>  
</body>
</html>
```

2）圣杯布局

​		由三列组成，两端固定，中间自适应。外观与与双飞翼布局一样。

​		布局时与双飞翼比增加了定位和偏移设置。

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
  <title>圣杯布局</title>
  <style>
    /*头部+尾部*/
    .header,.footer{
      width:100%;
      height:100px;
      line-height:100px;
      background-color:#2fff99;
      text-align:center;
      font-size:30px;
    }
    /*主体*/
    .container{
      padding:0 200px;
      overflow:hidden;
    }
    .column{
      float:left;
      height:200px;
      position:relative;
    }
    .left{
      width:200px;
      background-color:#f00;
      left:-200px;
    }
    .center{
      width:100%;
      background-color:#0f0;
    }
    .right{
      width:200px;
      background-color:#0ff;
      right:-200px;
    }
  </style>
</head>
<body>
  <!--一个网页通常由上中下部分组成-->
  <!--1.header头部-->
  <div class="header">#header</div>
  <!--2.content主体内容区-->
  <div class="container">
    <div class="column center"></div>
    <div class="column left"></div>
    <div class="column right"></div>
  </div> 
  <!--3.footer尾部-->
  <div class="footer">#footer</div>
</body>
</html>
```

3）侧边栏固定布局

1. 两栏布局

   a. 左侧固定，右侧自适应

   b. 左侧自适应，右侧固定

   c. 左右都固定

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
  <title>两栏布局，左固定</title>
  <style>
    body{
      font-size:18px;
      min-width:600px;
    }
    .container{
      width:100%;
      overflow:hidden;
    }
    .left{
      width:150px;
      height:200px;/*实际开发中，不要给出高度，高度是由内容自行撑开*/
      float:left;
      background-color:#f00;
      color:#fff;
      margin-right:-150px;
      position:relative;
    }
    .right{
      width:100%;
      height:200px;
      float:left;
      background-color:#0f0;
      color:#fff;
      margin-left:155px;
    }
    
  </style>
</head>
<body>
  <div class="container">
    <div class="left">左侧固定</div>
    <div class="right">右侧自适应</div>
  </div>
</body>
</html>
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
  <title>两栏布局，左自适应右固定</title>
  <style>
    body{
      font-size:18px;
      min-width:600px;
    }
    .container{
      width:100%;
      overflow:hidden;
    }
    .left{
      width:100%;
      height:200px;
      float:left;
      background-color:#f00;
    }
    .right{
      width:150px;
      height:200px;
      float:left;
      background-color:#0ff;
      color:#fff;
      margin-left:-150px;
    }
    
  </style>
</head>
<body>
  <div class="container">
    <div class="left">左侧自适应</div>
    <div class="right">右侧固定</div>
  </div>
</body>
</html>
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
  <title>两栏布局，左右都固定</title>
  <style>
    body{
      font-size:18px;
      min-width:600px;
    }
    .container{
      width:1000px;
      overflow:hidden;
    }
    .left{
      width:200px;
      height:200px;
      float:left;
      background-color:#f00;
      color:#fff;
    }
    .right{
      width:780px;
      height:200px;
      float:right;
      background-color:#0ff;
      color:#fff;
    }
    
  </style>
</head>
<body>
  <div class="container">
    <div class="left">左侧固定</div>
    <div class="right">右侧固定</div>
  </div>
</body>
</html>
```

2. 三栏布局

   a. 左侧固定，中间自适应，右侧固定

   b. 左侧自适应，中间和右侧固定

   c. 左侧和中间固定，右边自适应

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
  <title>左侧固定，中间自适应，右侧固定</title>
  <style>
    .container{
      width:1000px;
      overflow:hidden;
      color:#fff;
    }
    .left,.right{
      height:200px;
      float:left;
      line-height:200px;
      position:relative;
    }
    .left{
      width:200px;
      background-color:#00ff00;
      margin-right:-200px;
    }
    .center{
      float:left;
      width:100%;
      background-color:#ff0;
      line-height:200px;
    }
    .content{
      margin:0 200px;
    }
    .right{
      width:150px;
      background-color:#0ff;
      margin-left:-150px;
    }
    
    
  </style>
</head>
<body>
  <div class="container">
    <div class="left">左侧固定</div>
    <div class="center">
    	<div class="content">中间自适应</div>
    </div>
    <div class="right">右侧固定</div>
  </div>
</body>
</html>
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
  <title>左侧自适应，中间和右侧固定</title>
  <style>
    .container{
      overflow:hidden;
      color:#fff;
    }
    .left{
      width:100%;
      float:left;
      background-color:#ad513d;
      margin-right:-300px;
    }
    .content{
      line-height:200px;
      height:200px;
      margin-right:300px;
    }
    .center,.right{
      width:150px;
      height:200px;
      float:right;
      line-height:200px;
    }
    .center{
      background-color:#44ffc5;
    }
    
    .right{
      background-color:#ff6bb1;
    }  
  </style>
</head>
<body>
  <div class="container">
    <div class="left">
      <div class="content">左侧自适应</div>
    </div>
    <div class="center">中间固定</div>
    <div class="right">右侧固定</div>
  </div>
</body>
</html>
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
  <title>右侧自适应，中间和左侧固定</title>
  <style>
    .container{
      overflow:hidden;
      color:#fff;
    }
    .center,.left{
      position:relative;
      width:200px;
      height:150px;
      float:left;
      line-height:150px;
    }
    .left{
      background-color:#79ff40;
    }
    .center{
      background-color:#ff8499;
    }
    
    .right{
      float:right;
      width:100%;
      height:150px;
      line-height:150px;
      background-color:#5b4cff;
      margin-left:-400px;
    }  
    .content{
      margin-left:400px;
    }
    
  </style>
</head>
<body>
  <div class="container">
    <div class="left">左侧固定</div>
    <div class="center">中间固定</div>
    <div class="right">
    	<div class="content">右侧自适应</div>
    </div>
  </div>
</body>
</html>
```

### BFC&IFC

​		FC：Fomatting Context（格式上下文）。它是CSS2.1规范中的一个概念。它是页面中的一块渲染区域，并且有一套渲染规则，它决定了其子元素将如何定位，以及和其他元素的关系和相互作用。分为：BFC和IFC。

1）BFC：块级格式上下文

a）形成BFC的条件

​	i）浮动元素（float除none以外的值）

​	ii）定位元素（position（absolute/fixed））

​	iii）display（值为inline-block/table-cell/table-caption时）

​	iv）overflow（值为hidden/auto/scroll时）

b）BFC特性

​	i）内部的盒子会在垂直方向上一个接一个的放置

​	ii）垂直方向上的距离会重叠，值由最大margin值决定（如果不想要margin值重叠，需要将该盒子变成一个独立的盒子）

​	iii）BFC的区域不会与float元素区域重叠

​	iv）计算BFC的高度时，浮动元素也参与计算

​	v）BFC就是页面上的一个独立的容器，容器里面的子元素不会影响到外面的元素

c）BFC作用

​	i）解决margin重叠的问题（添加独立BFC）

​	ii）解决浮动高度塌陷的问题（在父级添加overflow:hidden）

​	iii）解决侵占浮动元素的问题（添加overflow:hidden清除浮动）

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
  <title>BFC</title>
  <style>
    /*i）内部的盒子会在垂直方向上一个接一个的放置*/
    /*.box1,.box2{
      width:200px;
      height:100px;
      border:1px solid #000;
    }*/
    
    /*ii）垂直方向上的距离由最大margin值决定，如果不想要margin值重叠，需要将其变成一个独立的容器*/
    /*.container{
      overflow:hidden;
      width:100px;
      height:100px;
      background-color:#f00;
    }
    .box1{
      height:20px;
      margin:10px 0;
      background-color:#0f0;
    }
    .box2{
      height:20px;
      margin:20px 0;
      background-color:#00f;
    }*/
    
    /*iii）BFC的区域不会与float元素区域重叠*/
    /*.box1{<!--BFC-->
      float:left;
      width:200px;
      height:100px;
      background-color:#61ff9c;
    }
    .box2{<!--BFC-->
      overflow:hidden;
      height:200px;
      background-color:#ff4f46;
    }*/
    
    /*iv）计算BFC的高度时，浮动元素也参与计算*/
    .box2{
      width:200px;
      height:100px;
      background-color:#ff9a45;
      float:left;
    }
    .container{<!--如果想让父级也被撑开，就必须把它设置成一个BFC-->
      width:300px;
      border:1px solid #000;
      overflow:hidden;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="wrapper">
      <div class="box1"></div>
    </div>
    <div class="box2"></div>
  </div>
</body>
</html>
```

2）IFC：内联（行级）格式上下文

​		a）形成IFC的条件

​			i）font-size

​			ii）line-height

​			iii）height

​			iv）vertical-align

​		b）IFC特性（规则）

​			i）IFC的元素会在一行中从左至右排列

​			ii）在一行上的所有元素会在该区域形成一个行框

​			iii）行宽的高度为包含框的高度，高度为行框中最高元素的高度

​			iv）浮动的元素不会在行框中，并且浮动元素会压缩行框的宽度

​			v）行框的宽度容纳不下子元素时，子元素会换下一行显示，并且会产生新行框

​			vi）行框的元素内遵循text-align和vertical-align

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
  <title>IFC</title>
  <style>
    /*i）IFC的元素会在一行中从左至右排列*/
    span{
      font-size:30px;
      background-color:#f4ff57;
      /*width:200px;<!--行级标签不识别宽高-->
      display:inline-block;<!--如果要让行标签识别宽高，必须用display把它设为块级标签-->*/
    }
    strong{
      font-size:16px;
      background-color:#ffadf5;
    }
    .box{
      float:left;
      font-size:50px;
    }
  </style>
</head>
<body>
  <span>span</span>
  <strong>strong</strong>
  <em class="box">box</em>
</body>
</html>
```

6.容器的高度：

​	height = line-height + vertical-align





> 学习苦！学习累！学习学的人奔溃😭