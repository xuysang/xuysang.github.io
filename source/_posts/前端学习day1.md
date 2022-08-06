---
title: 前端学习day1
date: 2022-08-06 13:46:34
categories: 技术
tags: 学习
---

#### HTML:

- HTML：超文本标记语言，是标识性的语言，非编程语言，不能使用逻辑运算。通过标签将网络上的文档格式进行统一，使分散网络资源连接为一个逻辑整体。
- 超文本，是一种组织信息的方法，通过超链接将多种媒介关联起来。
- 标记：标签。用<>包裹的具有一定含义的内容，比如：`<strong></strong>`

- 静态网页：HTML代码和内容书写完毕后，页面的内容和显示效果基本上不会发生变化了，除非修改页面代码。有动画效果，内容本身没有变化也属于静态网页。 
- 动态网页：页面代码没有变，但是显示的内容可以随着时间、环境或者数据库操作的结果而发生改变。

- 浏览器：解释和执行HTML源码的工具。

  五大主流浏览器：Internet Explorer(IE)，FireFox(火狐)，Chrome(谷歌)，Opera(欧朋)，Safari(苹果)。

- 浏览器内核：

  1. Trident：代表产品IE，使微软开发的一种排版引擎

  2. Gecko：代表产品Mozilla,FireFox，是一套开源的C++编写的排版引擎

  3. WebKit：代表产品Safari，主要用于MacOS系统

  4. Presto：世界公认最快的渲染速度的引擎，已被弃用

  5. Blink：Google和Opera Software开发的浏览器排版引擎，Chrome和Opera内核

##### HTML基本结构：

```html
<!DOCTYPE html> <!--!表示申明的意思。这一行代码意思是：下面的文档标签将以html5规范去解析-->
<html>
  <!--1.头部，主要用来完成一个网页的相关设置的。-->
  <head>
  	<meta charset="utf-8"><!--汉字编码--><!--meta:元，主要用来完成对应设置的-->
    <meta name="keywords" content=""><!--设置一个网站的搜索关键字-->
    <meta name="description" content=""><!--网站的描述内容-->
    <title>...</title><!--标题-->
    <!--设置网站小图标-->
    <link rel="shortcut icon" href="" type="image/png">
    <style>
      /*书写样式的地方*/
    </style>
    <link rel="styleshrrt" href="style.css"><!--用来引入外部样式文件-->
  </head>
  <!--2.主体部分-->
  <body>
    <p>这是一个段落</p>
  </body>
  <script>
    // 放脚本代码的地方
  </script>
</html>
```



##### HTML基本标签

- div：用来布局的，没有具体含义。层

  ```html
  <div></div>
  ```

  

- hx：标题，从1级到6级，1级标题最大，会自动加粗，有默认字号，h1h2...

  ```html
  <h1>...</h1>
  <h2>...</h2>
  <h6>...</h6>
  ```

  

- p：表示段落，相当于一个回车

  ```html
  <p>...</p>
  ```

  

- br /：单标签，生成一个换行符，表示换行

  ```html
  <p>
    xxxxxx<br />
  </p>
  ```

  

- hr /：单标签，生成一条水平线，主要起装饰作用。可以设置width,align,color,size(高度)

  ```html
  <hr width="80%" align="center" color="red" size="2px"
  ```

  

- a：用来设置超文本链接，实现链接跳转。target：`_blank `/`_self`/`_parent`/`_top`

  ```html
  <a href="http://baidu.com" title="百度">百度</a><!--title是提示文字-->
  <a href="http://baidu.com" target="_blank">百度</a>
  <a href="http://baidu.com" target="_self">百度</a>
  ```

  |  参数   | 功能                                                         |
  | :-----: | ------------------------------------------------------------ |
  | _blank  | 浏览器总在一个新打开、未命名的窗口中载入目标文档             |
  |  _self  | 这个目标的值对所有没有指定目标的`<a>`标签是默认目标，它使目标文档载入并显示值相同的框架或者窗口中作为源文档。这个目标是多余且不必要的，除非和文档标题`<base>`标签中的target属性一起使用 |
  | _parent | 这个目标使得文档载入父窗口或者包含来超链接引用的框架的框架集。如果这个引用是在窗口或者在顶级框架中，那么它与目标_self等效。 |
  |  _top   | 这个目标使得文档载入包含这个超链接的窗口，用_top目标将会清除所有被包含的框架并将文档载入整个浏览器窗口。 |

  

- img：用来加载外部图片、图像。src：用来设定加载的图片或者图像的路径

  ```html
  <img src="" title="" alt=""><!--alt表示图片加载不出来的时候显示的内容，否则不会显示-->
  ```

  

- span：作用与div一样，都是用来布局的，不同的是div会单独占一行，而span不会,span标签用于行内布局。

  ```html
  <span></span>
  ```

   

- ul/ol：列表，前者是无序列表，后者是有序列表，它们的列表内容都用的是li标签。

  ```html
  <ul>
    <li>li1</li>
    <li>li2</li>
    <li>li3</li>
  </ul>
  <ol>
    <li>li1</li>
    <li>li2</li>
    <li>li3</li>
  </ol>
  ```

  

- <!--注释-->：浏览器不会解析注释的内容的

  

##### HTML标签属性

- 标签属性：

  1. 通常由属性名=“属性值”组成
  2. 起附加信息的作用
  3. 不是所有标签都有属性，比如br标签

  ```html
  <p title="段落" class="content" id="content">
    这是一个测试段落
  </p>
  ```

- 文本格式化标签：就是通过标签来美化文本外观

  1. b和strong：都有加粗作用，且都是行级标签（不会自动换行），但strong除了加粗还有强调作用。注：强调主要用于SEO时，便于提取关键字。

     ```html
     <b>加粗</b>
     <strong>加粗且强调</strong>
     ```

  2. i和em：使文字倾斜，em具有强调作用。如果只是简单的倾斜效果，用i标签就可以，比如添加图标等。

     ```html
     <i>文字倾斜</i>
     <em>文字倾斜且强调</em>
     ```

  3. pre：预格式化文本，保留换行和空格及宽度，文字的字号会小一号（块级标签（在浏览器中会独占一行））。

     ```html
     <pre>预格式化文本，保留
                换行和空格
     及宽度</pre>
     ```

  4. small和big：分别让文字缩小一号和放大一号（行级标签（不会独占一行，且不识别宽高））。big在HTML5中淘汰了，但并没有删除。在开发中尽量不要使用淘汰了的标签。浏览器支持的最小字号为12px字，如果要显示比12px还小的文字效果，需要处理。

     ```html
     <p>我说正常大小的文字</p>
     <small>我是小一号的文字</small>
     <big>我是大一号的文字</big>
     ```

  5. sub和sup：设置文本为下标和上标，用来调整文本正常显示的基线，且文字会自动小一号

     ```html
     <p>正常显示：X1+X2=Y</p>
     <p>下标：X<sub>1</sub>+X<sub>2</sub>=Y</p>
     <p>上标：X<sup>2</sup>+Y<sup>2</sup>=Z</p>
     ```

     

- 单标记：指的是由一个标签组成

  换行符：`<br/>`

  水平线：`<hr/>`

  图片标签：`<img/>`

  文本标签：`<input/>`

  link标签：`<link/>`

  元信息标签：`<meta/>`

- 双标记：由开始标签和结束标签两部分构成，必须成双成对使用。

  `<html>`、`<head>`、`<title>`、`<body>`、`<table>`、`<span>`、`<div>`、`<p>`、`<h1>`等等

- 实体转义：通过实体字符来解决网站认为是标签而无法直接显示在页面中的问题

  ```html
  <p>    aa    bb</p>
  <p>    aa&nbsp;&nbsp;&nbsp;&nbsp;bb</p>
  <p>1&times;2=2</p>
  ```

  | 实体字符   | 编译后字符  |
  | ---------- | ----------- |
  | `&lt;`     | 小于号（<） |
  | `&gt;`     | 大于号（>） |
  | `&amp;`    | 与号（&）   |
  | `&nbsp;`   | 空格        |
  | `&copy;`   | 版权（©️）   |
  | `&times;`  | 乘号（✖️）   |
  | `&divide;` | 除号（➗）   |

  

- 块状元素：（相当于执行了display:block;操作）会独占一行，其宽度自动填满其父元素宽度，可以设置width,height属性，用来搭建网站架构、布局、承载内容

  包括以下标签：

  ```html
  address、dir、div、dl、dt、dd、fieldset、form、h1~h6、hr、menu、noframes、ol、p、pre、table、ul等。
  ```

- 行内元素：（相当于执行了display:inline;操作）不会独占一行，相邻的行内元素会排列在同一行里，直到一行排不下才会换行，宽度随元素的内容而变化，设置weight和height无效。一般用在网站内容之中的某些细节或部位，用以“强调、区分样式、上标、下标、锚点”等等。其内只有包含行级元素。

  包括以下标签：

  ```html
  a、b、bdo、big、small、br、cite、em、font、i、img、input、kbd、label、select、span、strong、sub、sup、textarea等。
  ```



##### 文件命名规范

- 项目开发时，项目文件或目录中不能出现汉字和空格之类的其它符号，文件和目录名一般以字母或下划线开头_



> 学海无涯苦作舟

