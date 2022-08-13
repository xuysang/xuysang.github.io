---
title: 前端学习day4
date: 2022-08-13 14:39:13
categories: 技术
tags: 学习
---

## 浮动

1. 什么是浮动？

   浮动就是让块级标签不独占一行。目的（使用场景）：把块级标签元素可以排在一行上。

2. 浮动的原理

   就是让元素脱离文档流，不占用标准流。

3. float的属性值：

   left：左浮动

   right：右浮动

   none：默认值，不浮动

4. 浮动后，后面的元素不管是块级还是行级元素，不会显示在下一行。

5. 清除浮动

   目的：让后面的元素自动掉到下一行。

   方法：

   1）添加空标签，并设置样式：clear:both;

   ​		clear:left; 	清除左浮动

   ​		clear:right;	清除右浮动

   ​		clear:both;	清除左右浮动

   ​		clear:none;	左右浮动都不清除

   2）在要清除浮动的父级添加样式：overflow:hidden;

   ​		overflow:hidden;  超出部分隐藏，也可以用来实现清除浮动。

   3）在要清除浮动的父级添加伪元素，并设定样式：

   ​		父元素:after{

   ​			content:"";

   ​			display:block;

   ​			clear:both;

   ​		}

   注意：在实际项目开发中，一般首先第2种方案。

   

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <style>
    .wrapper{
      width:600px;
      margin:0 auto;
      border:1px solid #666;
      /*overflow:hidden;*//*清除浮动方法2*/
    }
    .wrapper:after{/*清除浮动方法3*/
      content:"";
      display:block;
      clear:both;
    }
    .box1,.box2,.box3 {
      width:200px;
      height:150px;
    }
    .box1{
      background-color:#ff0000;
      float:left;
    }
    .box2{
      background-color:#217aff;
      float:right;
    }
    .clear{
      clear:both;/*清除浮动方法1*/
    }
    .box3{
      background-color:#58ff62;
    }
  </style>
</head>
<body>
  <!--<div class="wrapper">
    <div class="box1">box1</div><!--这里的div属于块级标签，会独占一行-->
    <div class="box2">box2</div>
    <!--清除浮动方法1-->
    <div class="clear"></div>
    <div class="box3">box3</div>
  </div>-->
	
  <div class="wrapper">
    <div class="box1">box1</div><!--这里的div属于块级标签，会独占一行-->
    <div class="box2">box2</div>
  </div> 
  <div class="box3">box3</div>
</body>
</html>
```

6）CSS盒子模型

​	每个元素都是一个盒子，一个盒子由margin（外边距），border（边框线），padding（内边距）和content（内容）组成。

​	区别外边距和内边距是以边框为参照。

​	系统默认外边距为8px。

​	1）外边距（margin）：指元素边框线之外的距离。

​		margin-left：左边距

​		margin-right：右边距

​		margin-top：上边距

​		margin-bottom：下边距

​		margin：可以用来设置任意一个边的边距，可以带1至4个参数。

​				1个（apx）：表示上下左右都有这样的外边距apx

​				2个（apx bpx）：表示上下外边距为apx，左右外边距为bpx

​				3个（apx bpx cpx）：表示上外边距为apx，下边距为cpx，左右外边距为bpx

​				4个（apx bpx cpx dpx）：表示上为apx，右为bpx，下为cpx，左为dpx

2）内边距（padding ）：指元素的文本内容与边框之间的距离。

​		用法与margin完全一样。

3）边框（border）：就是围绕元素内容和内边距的一条或多条线，设置边框的最简单的方法就是使用border属性，允许规定元素边框的样式、宽度和颜色。

​		属性：

​			border-width：设置边框的宽度

​			border-style：设置边框的样式

​					none：默认值，无边框

​					solid：定义实线边框

​					double：定义双实线边框

​					dotted：定义点状线边框

​					dashed：定义虚线边框

​			border-color：设置边框的颜色

7）盒子的真实尺寸

​		盒子宽度 = width + padding左右 + border左右

​		盒子高度 = height + padding上下 + border上下

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <style>
    div{
      width:800px;
      height:400px;
      border:1px solid red;
      /*margin:200px;*/
    }
    .span{
      /*display:block;*/
      width:300px;
      height:200px;
      background-color:#f00;
      /*margin:10px;*/
      /*margin:10px 20px;*/
      /*margin:10px 20px 30px;*/
      /*margin:10px 20px 30px 40px;*/
      display:inline-block;
    }
    .content{
      width:100px;
      height:200px;
      background-color:#46ffb1;
      display:inline-block;
    }
  </style>
</head>
<body>	 
  <div class="box">
  	<div class="span"></div>
    <div class="content"></div>
  </div>
</body>
</html>
```



8）display属性：用来设置元素的显示方式。

​		属性值：

​				none：不显示元素

​				block：块显示，在元素前后设置换行符。目的：将行级标签转换为块级标签（因为行级标签不识别宽高，而块级标签识别，转换后，行级标签也可以设置宽高了）

​				inline：行内显示，将块级标签转换为行级标签。

​				inline-block：将块级或行级标签转换为行内块级标签。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <style>
    div{
      width:800px;
      height:100px;
      background-color:#f00;
      display:inline-block;
    }
    div:first-child{
      background-color:#38ffd1;
    }
    span{
      width:300px;
      height:200px;
      background-color:#ffe351;
      /*display:block;*/
      display:inline-block;
      margin-left:-6px;
    }
  </style>
</head>
<body>	 
   <div class="span"></div>
   <div class="content"></div>
   <span>span</span>
</body>
</html>
```

9）table样式

​		table一般不用来布局，主要用来格式化数据。

​		属性：

​				width：宽度

​				height：高度

​				border-collapse:collapse; 单线边框

​				border：边框线

​		td,tr属性：

​				width：宽度

​				height：高度

​				border：边框线

​				text-align：文本左右对齐（left（默认）/center/right）

​				vertical-align：文本垂直对齐（top/middle（默认）/bottom）

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>table</title>
  <style>
    table,td{
      border:1px solid #666;
    }
    table{
      border-collapse:collapse;
      margin:0 auto;
      width:500px;
      height:300px;
      text-align:center;
    }
    td{
      /*vertical-align:top;*/
      /*vertical-align:bottom;*/
      vertical-align:middle;
    }
  </style>
</head>
<body>	 
<table>
	<tr>
  	<td>具体内容1</td>
    <td>具体内容2</td>
    <td>具体内容3</td>
    <td>具体内容4</td>
  </tr> 
  <tr>
  	<td>具体内容1</td>
    <td>具体内容2</td>
    <td>具体内容3</td>
    <td>具体内容4</td>
  </tr>  
  <tr>
  	<td>具体内容1</td>
    <td>具体内容2</td>
    <td>具体内容3</td>
    <td>具体内容4</td>
  </tr>  
</table>
</body>
</html>
```

10）列表样式

不是描述性的文本的任何内容都可以认为是列表。比如：菜单、商品列表等。

1. 列表类型

   无序（ul）、有序（ol）和自定义列表（dl）。

   ul和ol的列表项都是用li表示的，而dl是由一个dt和一个或多个dd组成的。

   dl一般用来设定一个定义，比如名词解释等。dt：标题，dd：描述，用来对dt的内容进行解释并说明的。

2. 样式（用来修改标识类型）

   list-style-image：用图像表示标识

   list-style-position：标识的位置（inside/outside（默认）

   list-style-type：标识类型

   简写：

   ​		list-style:list-style-image list-style-position list-style-type;

   ​		list-style的值可以按任意顺序列出，而且可以任意省略，只要提供一个值，其它的都自动默认。

   list-style-type的属性值：

   a）无序

   ​		disc（默认值，实心）/circle（空心）/square

   b）有序

   ​		decimal/decimal-leading-zero/lower-roman/upper-roman/lower-alpha/upper-alpha/lower-greek/lower-latin/upper-latin

   有序和无序：

   ​		none

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
     <meta charset="UTF-8">
     <title>table</title>
     <style>
       ul{
         /*list-style-type:square;*/
         /*list-style-type:none;*/
         /*list-style:none;*/
         /*list-style:circle;
         list-style-position:inside;*/
         /*list-style-image:url("icon.png");*/
         list-style:url("icon.png");
       }
       ol{
         /*list-style-type:decimal;*/
         /*list-style-type:decimal-leading-zero;*/
         /*list-style-type:lower-roman;*/
         list-style-type:lower-alpha;
       }
       dt{
         font-weight:bold;
         font-size:18px;
       }
       dd{
         margin-left:-1px;
       }
     </style>
   </head>
   <body>	 
   	<ul>
       <li>列表项1</li>
       <li>列表项2</li>
       <li>列表项3</li>
       <li>列表项4</li>
     </ul>
     <ol>
       <li>列表项1</li>
       <li>列表项2</li>
       <li>列表项3</li>
       <li>列表项4</li>
     </ol>
     <dl>
       <dt>啦啦啦</dt>
       <dd>啊啊啊</dd>
       <dd>呀呀呀</dd>
       <dd>呜呜呜</dd>
     </dl>
   </body>
   </html>
   ```

   11）轮播图

   作用：主要用于产品或公司相关宣传。

   组成：

     1. 轮播的组图（至少两张以上，不能太多）

     2. 控制器

     3. 计数器

        案例-轮播图.html

        ```html
        <!DOCTYPE html>
        <html lang="en">
        <head>
          <meta charset="UTF-8">
          <title>轮播图</title>
          <link rel="stylesheet" href="carouse.css">
        </head>
        <body>	 
          <div class="carousel">
            <!--1.轮播组图-->
            <ul class="carousel-imgs">
              <li><a href="#"><img src="img/banner_01.jpg" alt="banner"></a></li>
              <li><a href="#"><img src="img/banner_02.jpg" alt="banner"></a></li>
              <li><a href="#"><img src="img/banner_03.jpg" alt="banner"></a></li>
            </ul>
            <!--2.控制器-->
            <div class="prev"></div>
            <div class="next"></div>
            <!--3.计数器-->
            <div class="count">
              <ul>
                <li class="active"></li>
                <li></li>
                <li></li>
            </ul>
            </div>
          </div>
        </body>
        </html>
        ```

        carouse.css

        ```css
        *{
        		margin:0;
        		padding:0;
        }
        li{
        		list-style-type:none;
        }
        a{
        		text-decoration:none;
        }
        .carousel{
        		width:1000px;
        		height:300px;
          	margin:0 auto;
          	background-color:#444;
          	position:relative;/*相对定位*/
          	overflow:hidden;
        }
        /*1.轮播组图*/
        .carousel-imgs{
          width:9999px;
        }
        .carousel-imgs li{
          float:left;
        }
        .carousel-imgs img{
          width:1000px;
          height:300px;
        }
        /*2.控制器*/
        .prev,.next{
          width:32px;
          height:32px;
          position:absolute;/*绝对定位，脱离文档流，它相对于position:relative定义的元素进行定位*/
          top:50%;
          margin-top:-16px;
        }
        .prev{
          background-image:url(./img/prev.png);
          left:50px;
        }
        .next{
          background-image:url(./img/next.png);
          right:50px;
        }
        /*3.计数器*/
        .count{
          width:1000px;
          height:10px;
          position:absolute;
          bottom:25px;
        }
        .count ul{
          width:60px;
          margin:0 auto;
          /*background-color:#f00;*/
        }
        .count ul li{
          width:10px;
          height:10px;
          cursor:pointer;/*将鼠标形状设为手型*/
          background-color:#666;
          opacity:.5;/*不透明度，取值范围：[0,1]之间的一个数，可以是小数*/
          float:left;
          margin-left:10px;
          border-radius:50%;/*圆角*/
        }
        .count .active{
          background-color:#102bad;
          opacity:1;
        }
        ```

        

> 第四天学完了，开始上难度了...

