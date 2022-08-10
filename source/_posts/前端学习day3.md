---
title: 前端学习day3
date: 2022-08-10 19:01:49
categories: 技术
tags: 学习
---

1. #### css：层叠样式表，用来美化网页的。做到结构（HTML）和表现（CSS）分离。

2. #### 基本语法：

   选择器{

   ​		属性：属性值；

   }

3. #### css引用方式：行间样式、内部样式、外部样式、导入外部样式。

   ​	行间样式：直接在标签上书写样式。

   ​	内部样式：在文件的内部书写样式。

   ```html
   		<style>
   		    样式内容
   		</style>
   ```

   ​	外部样式：（1）先创建一个CSS文件；（2）再用link标签引入这个文件。

   ​	导入外部样式：（1）先创建一个CSS文件；（2）在style标签中用import导入外部样式文件。

   ​	以上四种CSS引用方式的区别：

   ​			行间样式只作用于当前标签；而内部样式作用于当前文件；外部样式可以被多个HTML文件引用。

   ​			在实际项目开发中，最好使用外部样式。

   ​			外部样式分为link引入和import引入两种方式。这两种方式区别：

   ​					1）link是XHTML标签，除了加载CSS外，还可以定义RSS等其他事务；@import属于CSS范畴，只能加载CSS。

   ​					2）link引用CSS时，在页面载入时同时加载；@import需要页面网页完全载入以后加载。

   ​					3）link是XHTML标签，无兼容问题；@import是在CSS2.1提出的，低版本的浏览器不支持。

   ​					4）link支持使用Javascript控制DOM去改变样式；而@import不支持。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>css引用方式</title>
    <!--3.引入外部样式文件-->
    <!--Emmet语法写法：link:css-->
    <link rel="stylesheet" href="css/style.css" />
    <!--2.内部样式表-->
    <style>
        @import "css/test.css";
        p{
            background-color:#eeeeee;
            font-size:18px;
            font-style:italic;
        }
	</style>
</head>

<body>
    <!--1.行间样式(嵌入式样式)-->
	<div style="color:olive;width:100px;border:1px solid blue;">行间样式测试1</div>
	<div>行间样式测试2</div>
    <p>段落1</p>
    <p>段落2</p>
    <span>外部样式测试</span>
    
    <div class="box">导入外部样式</div>
    <div class="box">导入外部样式</div>
    <div class="box">导入外部样式</div>
    
    <em class="box">同学们好！</em>
</body>
</html>

```

css/style.css

```html
span{
	font-size:15px;
	color:rgba(65,206,110,0.79);
	display:block;
}
```

css/test.css

```
.box{
	font-weight:bold;
	font-size:16px;
}
```



#### 4. CSS选择器分类：

1）`*`：匹配html中所有元素（注意：*的性能差，因为它要匹配所有元素，所以在开发时，不建议使用）

2）标签选择器：用来匹配对应的标签

3）类选择器：用来选择class命名的标签

4）ID选择器：用来选择用id命名的标签

5）派出选择器：根据上下文来确定选择的标签

6）伪类选择器（后面学）

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>css选择器</title>
    <style>
        <!--1.*-->
        *{
            color:red;
        }
        <!--2.标签选择器-->
        span{
            display:block;
            margin-right:20px;
            border:1px solid gray;
        }
        <!--3.类选择器-->
        .wrapper{
            color:aqua;
        }
        <!--4.id选择器-->
        #content{
            color:pink;
        }
        <!--5.派出选择器-->
        .box li {
            color:chartreuse;
        }
	</style>
</head>

<body>
    <p>这是P标签</p>
    <strong>这是strong标签</strong>
    <span>这是span标签</span>
    <div>这是div标签</div>
    <div class="wrapper">这是div标签</div>
    
    <p id="content">这是内容</p>
    <ul class="box1">
        <li>li001</li>
        <li>li002</li>
        <li>li003</li>
    </ul>
    <ul class="box2">
        <li>li001</li>
        <li>li002</li>
        <li>li003
            <ul>
                <li>subli1</li>
                <li>subli2</li>
            </ul>
        </li>
    </ul>
</body>
</html>

```



#### 选择器的分组

​		让多个选择器（元素）具有相同的样式，一般用于设置公共样式。

#### 选择器的继承

​		子元素可以继承父元素的样式，反之不可以。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>css选择器</title>
    <style>
        <!--1.选择器的分组-->
        h1, .box, p{
            color:red;
        }
        p {
            width:100px;
            background-color:#999999;
            color:blue;
        }
        <!--2.样式继承-->
        .test{
            font-size;18px;
        }
        /*.test span{
            font-weight:bold;
        }*/
        .test span{
            font-weight:bold;
            font-size:12px;/*改写父元素传过来的样式*/
        }
        
	</style>
</head>

<body>
    <h1>h1</h1>
    <div class="box">box</div>
    <p>p</p>
    <div class="test">这是一段测试<span>内容</span>。</div>
    
</body>
</html>

```

#### 样式权重

！important（10000）>内联样式（1000）>id选择器（100）>类、伪类选择器（10）>标签选择器（1）

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>样式权重</title>
    <style>
        <!--1.选择器的分组-->
        p {
            color:blue!important;
        }
        #content div.main_content h2{/*权重：100+1+10+1=112*/
            color:red;
        }
        #content .main_content h2{/*权重：100+10+1=111*/
            color:blue;
        }
        
	</style>
</head>

<body>
    <p style="color:red;">这是内容1</p>
    <p>这是内容2</p>
    <div id="content">
        <div class="main_content">
            52
            <h2>这是一个h2标题</h2>
        </div>
    </div>
</body>
</html>

```



#### CSS字体

- font-size：字号（px/%）

- font-family：文本字体

- font-style：文本字体的样式（normal/italic/oblique）

- font-weight：文本字体的粗细（normal/bold/bolder/lighter/100-900）

- line-height：行高，字体最底端与字体内部顶端之间的距离。（px/数字/em等）

- color：文字颜色（颜色的单词/rgb()->r:0-255，g:0-255，b:0-255/16进制，后跟6位(#rrggbb)或3位(#rgb)16进制数）

- text-decoration：文本字体的修饰（none/underline/overline/line-through）

- text-align：文本字体的对齐方式（left/right/center）

- text-transform：文本字体的大小写（capitalize/uppercase/lowercase/none）

- text-indent：文本字体的首行缩进（px/em/%/pt等）

  Tip：

  font复合属性：

  ​		font：font-style font-variant font-weight font-size/line-height font-family;

  ​		注意：

  ​				1）属性值的位置顺序

  ​				2）除了font-size和font-family之外，其它任何一个属性值都可以省略

  ​				3）font-variant：文本修饰 normal/small-caps（让大写字母变得小一些）

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>css字体</title>
    <style>
        p {
            font-size:16px;
            font-family:微软雅黑;
            /*font-style:italic;*/
            line-height:20px;
            /*text-align:left;*/
            /*text-indent:30px;*/
            text-indent:2em;
        }
        p span{
            font-weight:bold;
            /*color:red;*/
            /*color:rgb(255,0,0);*/
            /*color:#ff0000;*/
            /*color:#f00;*/
        }
        em{
            text-decoration:underline;
        }
        div{
            text-transform:capitalize;
        }
        .news{
            font:italic small-caps bolder 18px/1.5 宋体;
        }

	</style>
</head>

<body>
    <p><span>汪文斌表示，</span>我们一贯反对美国议员窜访台湾，<em>佩洛西</em>是美国第三号政治人物，坐着美国军机赴台，在窜台期间张口闭口代表美国，声称这是一次官方访问，民进党当局更宣扬佩窜台是“台美关系的重大突破”，这些都充分表明佩窜台是升级美台交往的重大政治挑衅，违背美方在《中美建交公报》当中所做的“仅与台保持非官方关系”的承诺，违背国际社会广泛认可，并由联大第2758号决议所确认的一个中国原则，违背联合国宪章确立的不干涉内政的国际法准则。</p>
    <div>
        How are you?
    </div>
    <p class="news">How are you?违背美方在《中美建交公报》当中所做的“仅与台保持非官方关系”的承诺，违背国际社会广泛认可，并由联大第2758号决议所确认的一个中国原则，违背联合国宪章确立的不干涉内政的国际法准则。</p>
</body>
</html>

```



#### css背景

1）background-color：背景色（transparent/color）

2）background-image：背景图（none/url）

3）background-repeat：背景图铺排方式（repeat/no-repeat/repeat-x/repeat-y）

4）background-position：设置对象的背景图像位置（{x-number | top | center | bottom} {y-number | left | center | right }}）

5）background-attachment：背景图像滚动位置（scroll/fixed）

6）background：设置背景的复合写法。

​			background：color image repeat attachment position

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>css背景</title>
    <style>
        body {
            /*background-color:#eee;*/*/
            /*background-color:transparent;*/
            background-image:url(./images/bg.jpg);
            background-repeat:no-repeat;
            /*background-position:100px 50px;*/
            background-position:top;/*如果只带一个参数，默认y向为50%*/
            background-attachment:scroll;
            background:#888888 url(./images/bg.jpg) repeat-x fixed 0 30%;
        }
       

	</style>
</head>

<body>

</body>
</html>

```



#### CSS伪类选择器

​		伪类：专门用来表示元素的一种特殊状态。

​		常用伪类选择器：

​				1）a标签的伪类：

​							:link/:visited/:hover/:active

​				2）:focus 获得焦点

​				3)   :first-child/:last-child/:nth-child(number)       

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>css伪类选择器</title>
    <style>
      	<!--未被访问前-->
        a:link{/*这里的:link可以省略*/}{
            color:red;
        }
      	<!--访问后-->
        a:visited{
            color:green;
        }
      	<!--鼠标悬停时-->
        a:hover{
            color:yellow;
        }
      	<!--激活后-->
        a:active{
            color:blue;
        }
      	
      	input:focus{
        	outline: 1px solid #f00;
      	}
      	
        ul li:first-child{
          color:#ff1299;
        }
      	ul li:last-child{
          color:#38ff24;
        }
      	ul li:nth-child(2){
          color:#2c3cff;
        }       

	</style>
</head>

<body>
	<a href="#">单击我跳转</a>
  <input type="text">
  <ul>
    <li>aaaa</li>
    <li>aaaa</li>
    <li>aaaa</li>
    <li>aaaa</li>
  </ul>
</body>
</html>

```



#### 属性选择器

[属性名]：包含有指定属性名的元素（常用）

[属性名=值]：属性名的值为指定值的元素（常用）

[属性名~=值]：属性名的值包含指定值的元素

[属性名^=值]：属性名的值以指定值的开头的元素

[属性名$=值]：属性名的值以指定值的结尾的元素

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>CSS属性选择器</title>
    <style>
      	<!--未被访问前-->
      div.content[title]{
        font-weight:bold;
      }
      input[name=usr]{
        background-color:#eee;
      }
      /*div[class~=box1]{
        background-color:#5aff29;
      }*/
      /*div[class^=content2]{
        background-color:#5aff29;
        color:#fff;
      }*/
      div[class$=box2]{
        background-color:#5aff29;
        color:#fff;
      }

	</style>
</head>

<body>
	<div class="content1 box1 box2" title="内容">content1</div>
  <div class="content2 box2">content1</div>
  
  <form action="">
    <input type="text" name="account">
    <input type="text" name="usr">
  </form>
</body>
</html>


```



#### 关系选择器

1）空格：后代选择器

2）>：只选择儿子元素

3）+：兄弟选择

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>关系选择器</title>
    <style>
      /*后代选择器*/
      /*h1 strong{
        color:#fff;
        background-color:#000;
      }*/
      /*儿子选择器*/
      /*h1>strong{
        color:#fff;
        background-color:#000;
      }*/
      /*兄弟选择器*/
      ul li+li+li{
        list-style-type:none;
        color:red;
      }
	</style>
</head>

<body>
	<h1>
    <strong>关系1</strong><span><strong>关系2</strong></span>
  </h1>
  <ul>
    <li>li1</li>
    <li>li2</li>
    <li>li3</li>
    <li>li4</li>
    <li>li5</li>
  </ul>
</body>
</html>

```



#### CSS伪元素

伪元素：用于向某些选择器设置特殊效果。

1）伪元素与伪类区别：

css引入伪类和伪元素概念是为了格式化文档树以外的信息。也就是说，伪类和伪元素是用来修饰不在文档树中的部分。

伪类用于当已有元素处于的某个状态时，为其添加对应的样式，这个状态是根据用户行为而动态变化的。它只有处于dom树无法描述的状态下才能为元素添加样式，所以将其称为伪类。

伪元素用于创建一些不在文档树中的元素，并为其添加样式。比如说，我们可以通过:before来中一个元素前增加一些文本，并为这些文本添加样式。虽然用户可以看到这些文本，但是这些文本实际上不在文档树中。

2）伪元素&伪类的特点：

伪元素和伪类都不会出现在源文档或者文档树中

伪类允许出现在选择器的任何位置，而一个伪元素只能跟在选择器的最后一个简单选择器后面

伪元素名和伪类名都是大小写不敏感的

有些伪类是互斥的，而其它的可以同时用在一个元素上。（在规则冲突的情况下，常规层叠顺序决定结果）。

3）:before/:after/:first-letter/:first-line：前面可以是1个冒号也可以是双冒号

​	::selection/::placeholder/::backdrop：前面只能是双冒号

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>关系选择器</title>
    <style>
      p:first-letter{
        font:30px 黑体;
        color:#2c3cff;
        text-indent:2em; 
      }
      p:first-line{
        text-decoration:underline;
      }
      p:before{
        content:'$';
      }
      p:after{
        content:'......';
      }
	</style>
</head>

<body>
	<p>伪类允许出现在选择器的任何位置，而一个伪元素只能跟在选择器的最后一个简单选择器后面</p>
</body>
</html>


```





> 种一棵树最好的时间是十年之前，其次就是现在咯。学习亦然。