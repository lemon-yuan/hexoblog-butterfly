---
title: HTML复习
date: 2020-06-29 16:26:48
tags:
  - html
categories: 终身学习
description: HTML基础复习
cover: https://upyun-cdn.mistill.com/img/post_cover/post_cover_020.webp
abbrlink: review-html-base
---


# HTML基础

## HTML标题

标题（`heading`）是通过`<h1>`-`<h6>`等标签进行定义的。

```html
<h1>This is a heading</h1>
<h2>This is a heading</h2>
```

<!-- more -->

## HTML段落

段落（`paragraph`）通过`<p>`标签进行定义。

```html
<p>This is a paragraph.</p>
```

## HTML链接

链接是通过`<a>`标签进行定义的。

```html
<a href="http://www.w3school.com.cn">This is a link</a>
```

href属性中指定链接的地址。



## HTML图像

图像是通过`<img>`标签进行定义的。

```html
<img src="w3school.jpg" width="104" height="142" />
```

这里的名称和尺寸是以属性形式提供的。



# HTML元素

## HTML元素

HTML元素指的是从开始标签（start tag）到结束标签（endtag）的所有代码。

| 开始标签                | 元素内容            | 结束标签 |
| ----------------------- | ------------------- | -------- |
| &#60;p>                    | This is a paragraph | &#60;/p>    |
| &#60;a href="default.htm"> | This is a link      | &#60;/a>    |
| &#60;br />                 | &nbsp; | &nbsp; |

注：开始标签常被称为开放标签（opening tag）,结束标签被称为闭合标签（closing tag）。

## HTML元素语法

- HTML元素以开始标签其实
- HTML元素以结束标签终止
- **元素**的内容是开始标签与结束标签之间的内容
- 某些HTML元素具有**空内容（empty content）**
- 空元素在开始标签中进行关闭（以开始标签的结束而结束）
- 大多数HTML元素可拥有**属性**

## 嵌套的HTML元素

大多数HTML元素可以嵌套（可以包含其他HTML元素）

HTML文档由嵌套的HTML元素构成。

```html
<html>
    <body>
        <p>
            Thi is my first paragraph.
        </p>
    </body>
</html>
```

上面的例子包含三个HTML元素。

## 空的HTML元素

没有内容的HTML元素被称为空元素。空元素是在开始标签中关闭的。

`<br>`就是没有关闭的空元素。

在XHTML、XML以及未来版本的HTML中，所有元素都必须被关闭。

比如`<br />`是关闭空元素的正确方法。

## HTML提示：使用小写标签

HTML对大小写不敏感。



# HTML属性

## HTML属性

HTML标签可以拥有属性。属性提供了有关HTML元素的更多信息。

属性总是以名称/值对的形式出现，比如：**name="value"**

属性总是在HTML元素的开始标签中规定。

## 属性实例

```html
<a href="http://www.w3school.com.cn">This is a link</a>
<h1 aligen="center">#关于对齐方式的属性
<body bgcolor="yellow"># 关于背景颜色的属性
```

## 始终为属性值加引号

```html
name='Bill "HelloWorld" Gates'
```



# HTML样式

## HTML的style属性

style属性的作用：

**提供了一种改变所有HTML元素的样式的通用方法。**

通过HTML样式，能够使用style属性直接将样式添加到HTML元素，或者间接的在独立的样式表中（CSS文件）进行定义。

## 不赞成使用的标签和属性

在 HTML 4 中，有若干的标签和属性是被废弃的。被废弃（Deprecated）的意思是在未来版本的 HTML 和 XHTML 中将不支持这些标签和属性。

这里传达的信息很明确：请避免使用这些被废弃的标签和属性！

### 应该避免使用下面这些标签和属性：

| 标签                   | 描述               |
| :--------------------- | :----------------- |
| &#60;center>              | 定义居中的内容。   |
| &#60;font> 和 &#60;basefont> | 定义 HTML 字体。   |
| &#60;s> 和&#60;strike>       | 定义删除线文本     |
| &#60;u>                   | 定义下划线文本     |
| 属性                   | 描述               |
| align                  | 定义文本的对齐方式 |
| bgcolor                | 定义背景颜色       |
| color                  | 定义文本颜色       |

## HTML样式实例 - 背景颜色

```html
<html>
    <body style="background-color:yellow">
        <h2 style="background-color:red">
            This is a heading.
        </h2>
        <p style="backgound-color:green">
            This is a paragraph.
        </p>
    </body>
</html>
```

## HTML样式实例 - 字体、颜色和尺寸

```html
<html>
    <body>
        <h1 style="font-family:verdana">
            A heading
        </h1>
        <p style="font-family:arial;color:red;font-size:20px;">
            A paragraph.
        </p>
    </body>
</html>
```

## HTML样式实例 - 文本对齐

```html
<html>
    <body>
        <h1 style="text-align:center">
            This is a heading.
        </h1>
        <p>
            The heading above is aligned to the center of this page.
        </p>
    </body>
</html>
```

**style 属性淘汰了旧的“align”属性**



# HTML格式化

## HTML格式化实例

```html
<html>
<body>
<b>This text is bold</b> #定义粗体

<strong>This text is strong</strong> #定义加重语气

<big>This text is big</big> #定义大号字

<em>This text is emphasized</em> #定义着重文字

<i>This text is italic</i> #定义斜体字

<small>This text is small</small> #定义小号字

This text contains
<sub>subscript</sub> #定义下标字

This text contains
<sup>superscript</sup> #定义上标字
</body>
</html>

```

```html
<pre> #定义预格式文本
这是
预格式文本。
它保留了      空格
和换行。
</pre>
```

```html
#这些标签常用于计算机/编程代码
<code>Computer code</code> #定义计算机代码
<br />
<kbd>Keyboard input</kbd> #定义键盘码
<br />
<tt>Teletype text</tt> #定义打字机代码
<br />
<samp>Sample text</samp> #定义计算机代码样本
<br />
<var>Computer variable</var> #定义变量
<br />
```

```html
#块引用
<blockquote>
这是长的引用。这是长的引用。这是长的引用。这是长的引用。这是长的引用。这是长的引用。这是长的引用。这是长的引用。这是长的引用。这是长的引用。这是长的引用。
</blockquote>

这是短的引用：
<q>
这是短的引用。
</q>
```



# HTML注释

```html
<!-- 在此处写注释 -->
```



# HTML CSS

## 如何使用样式

当浏览器读到一个样式表，它就会按照这个样式表来对文档进行格式化。有以下三种方式来插入样式表：

### 外部样式表

当样式需要被应用到很多页面的时候，外部样式表将是理想的选择。使用外部样式表，你就可以通过更改一个文件来改变整个站点的外观。

```html
<head>
    <link rel="stylesheet" type="text/css" href="mystyle.css"
</head>
```

### 内部样式表

当单个文件需要特别样式时，就可以使用内部样式表。你可以在 head 部分通过 &#60;style> 标签定义内部样式表。

```html
<head>
    <style type="text/css">
        body {background-color: red}
        p {margin-left: 20px}
    </style>
</head>
```

### 内联样式

当特殊的样式需要应用到个别元素时，就可以使用内联样式。 使用内联样式的方法是在相关的标签中使用样式属性。样式属性可以包含任何 CSS 属性。以下实例显示出如何改变段落的颜色和左外边距。

```html
<p style="color: red; margin-left: 20px">
    This is a paragraph.
</p>
```



# HTML链接

## HTML链接语法

`href`属性规定链接的目标。

开始标签和结束标签之间的文字被作为超级链接来显示。

```html
<a href="www.baidu.com">Text here</a>
```



## target属性

使用 Target 属性，你可以定义被链接的文档在何处显示。

下面的这行会在新窗口打开文档：
```html
<a href="http://www.w3school.com.cn/" target="_blank">Visit W3School</a>
```


# HTML图像

## 图像标签和源属性(src)

在 HTML 中，图像由 `<img> `标签定义。

`<img>` 是空标签，意思是说，它只包含属性，并且没有闭合标签。

要在页面上显示图像，你需要使用源属性（src）。src 指 "source"。源属性的值是图像的 URL 地址。

定义图像的语法是：

```html
<img src="url" />
```

## 替换文本属性(Alt）

alt 属性用来为图像定义一串预备的可替换的文本。替换文本属性的值是用户定义的。

```html
<img src="boat.gif" alt="Big Boat">
```



# HTML表格

表格由` <table>` 标签来定义。每个表格均有若干行（由 `<tr> `标签定义），每行被分割为若干单元格（由 `<td> `标签定义）。字母 td 指表格数据（table data），即数据单元格的内容。数据单元格可以包含文本、图片、列表、段落、表单、水平线、表格等等。

```html
<table border="1">
    <tr>
    <td>row1, cell1</td>
    <td>row1, cell2</td>
    </tr>
    <tr>
    <td>row2, cell1</td>
    <td>row2, cell2</td>
    </tr>
</table>
```

## 表格和边框属性

如果不定义边框属性，表格将不显示边框。有时这很有用，但是大多数时候，我们希望显示边框。

使用边框属性来显示一个带有边框的表格：

```html
<table border="1">
<tr>
<td>Row 1, cell 1</td>
<td>Row 1, cell 2</td>
</tr>
</table>
```

## 表格的表头

表格的表头使用 <th> 标签进行定义。

大多数浏览器会把表头显示为粗体居中的文本：

```html
<table border="1">
<tr>
<th>Heading</th> #定义表头
<th>Another Heading</th>
</tr>
<tr>
<td>row 1, cell 1</td>
<td>row 1, cell 2</td>
</tr>
<tr>
<td>row 2, cell 1</td>
<td>row 2, cell 2</td>
</tr>
</table>
```

## 表格中的空单元格

在一些浏览器中，没有内容的表格单元显示得不太好。如果某个单元格是空的（没有内容），浏览器可能无法显示出这个单元格的边框。

**注意：**这个空的单元格的边框没有被显示出来。为了避免这种情况，在空单元格中添加一个空格占位符，就可以将边框显示出来。

```html
<table border="1">
<tr>
<td>row 1, cell 1</td>
<td>row 1, cell 2</td>
</tr>
<tr>
<td>&nbsp;</td>
<td>row 2, cell 2</td>
</tr>
</table>
```



# HTML列表

HTML支持有序、无序和定义列表

## 无序列表

无序列表始于`<ul>`标签。每个列表项始于`<li>`。

```html
<ul>
    <li>coffee</li>
    <li>milk</li>
</ul>
```

## 有序列表

有序列表始于`<ol>`标签。每个列表项始于`<li>`标签。

```html
<ol>
    <li>coffee</li>
    <li>milk</li>
</ol>
```

## 定义列表

自定义列表不仅仅是一列项目，而是项目及其注释的组合。

自定义列表以`<dl>`标签开始。每个自定义列表项以`<dt>`开始。每个自定义列表项的定义以`<dd>`开始。

```html
<dl>
    <dt>coffee</dt>
    <dd>Black hot drink</dd>
    <dt>milk</dt>
    <dd>White cold drink</dd>
</dl>
```

定义列表的列表项内部可以使用段落、换行符、图片、链接以及其他列表等等。



# HTML块

可以通过&#60;div>和&#60;span>

## HTML块元素

大多数HTML元素被定义为块级元素或内联元素。

块级元素（block level element）, 内联元素（inline element）

块级元素在浏览器显示时，通常会以新行来开始（和结束）。

例子：`<h1>, <p>, <ul>, <table>`

## HTML内联元素

内联元素在显示时通常不会以新行开始。

例子：`<b>, <td>, <a>, <img>`

## HTML&#60;div>元素

HTML&#60;div>元素时块级元素，它是可用于组合其他HTML元素的容器。

&#60;div> 元素没有特定的含义。除此之外，由于它属于块级元素，浏览器会在其前后显示折行。

如果与 CSS 一同使用，&#60;div> 元素可用于对大的内容块设置样式属性。

&#60;div> 元素的另一个常见的用途是文档布局。它取代了使用表格定义布局的老式方法。使用 &#60;table> 元素进行文档布局不是表格的正确用法。&#60;table> 元素的作用是显示表格化的数据。

## HTML&#60;span>元素

HTML&#60;span>元素是内联元素，可用作文本的容器。

&#60;span>元素也没有特定的含义。

当与CSS一起使用时，&#60;span>元素可用于部分文本设置样式属性。



# HTML类

对 HTML 进行分类（设置类），使我们能够为元素的类定义 CSS 样式。

为相同的类设置相同的样式，或者为不同的类设置不同的样式。

实例：

```html
<!DOCTYPE html>
<html>
<head>
<style>
.cities {
    background-color:black;
    color:white;
    margin:20px;
    padding:20px;
} 
</style>
</head>

<body>

<div class="cities">
<h2>London</h2>
<p>
London is the capital city of England. 
It is the most populous city in the United Kingdom, 
with a metropolitan area of over 13 million inhabitants.
</p>
</div> 

</body>
</html>
```

## 分类块级元素

HTML&#60;div>元素是块级元素。它能够用作其它HTML元素的容器。

设置&#60;div>元素的类，使我们能够为相同的&#60;div>元素设置相同的类：

```html
<!DOCTYPE html>
<html>
<head>
<style>
.cities {
    background-color:black;
    color:white;
    margin:20px;
    padding:20px;
} 
</style>
</head>

<body>

<div class="cities">
<h2>London</h2>
<p>London is the capital city of England. 
It is the most populous city in the United Kingdom, 
with a metropolitan area of over 13 million inhabitants.</p>
</div>

<div class="cities">
<h2>Paris</h2>
<p>Paris is the capital and most populous city of France.</p>
</div>

<div class="cities">
<h2>Tokyo</h2>
<p>Tokyo is the capital of Japan, the center of the Greater Tokyo Area,
and the most populous metropolitan area in the world.</p>
</div>

</body>
</html>
```

## 分类行内元素

HTML&#60;span>元素是行内元素，能够作为文本的容器。

设置&#60;span>元素的类，能够为相同的&#60;span>元素设置相同的样式。

```html
<!DOCTYPE html>
<html>
<head>
<style>
  span.red {color:red;}
</style>
</head>
<body>

<h1>My <span class="red">Important</span> Heading</h1>

</body>
</html>
```



# HTML布局

## 使用&#60;div>元素的HTML布局

**注释：**&#60;div> 元素常用作布局工具，因为能够轻松地通过 CSS 对其进行定位。

这个例子使用了四个 &#60;div> 元素来创建多列布局：

```html
<!DOCTYPE html>
<html>

<head>
<style>
#header {
    background-color:black;
    color:white;
    text-align:center;
    padding:5px;
}
#nav {
    line-height:30px;
    background-color:#eeeeee;
    height:300px;
    width:100px;
    float:left;
    padding:5px;	      
}
#section {
    width:350px;
    float:left;
    padding:10px;	 	 
}
#footer {
    background-color:black;
    color:white;
    clear:both;
    text-align:center;
   padding:5px;	 	 
}
</style>
</head>

<body>

<div id="header">
<h1>City Gallery</h1>
</div>

<div id="nav">
London<br>
Paris<br>
Tokyo<br>
</div>

<div id="section">
<h2>London</h2>
<p>
London is the capital city of England. It is the most populous city in the United Kingdom,
with a metropolitan area of over 13 million inhabitants.
</p>
<p>
Standing on the River Thames, London has been a major settlement for two millennia,
its history going back to its founding by the Romans, who named it Londinium.
</p>
</div>

<div id="footer">
Copyright ? W3Schools.com
</div>

</body>
</html>
```

## 使用HTML5的网站布局

html5提供的新语义元素定于了网页的不同部分：

### HTML5语义元素

| header  | 定义文档或节的页眉             |
| ------- | ------------------------------ |
| nav     | 定义导航链接的容器             |
| section | 定义文档中的节                 |
| article | 定义独立的自包含文章           |
| aside   | 定义内容之外的内容（比如侧栏） |
| footer  | 定义文档或节的页脚             |
| details | 定义额外的细节                 |
| summary | 定义 details 元素的标题        |

```html
<!DOCTYPE html>
<html>

<head>
<style>
header {
    background-color:black;
    color:white;
    text-align:center;
    padding:5px;	 
}
nav {
    line-height:30px;
    background-color:#eeeeee;
    height:300px;
    width:100px;
    float:left;
    padding:5px;	      
}
section {
    width:350px;
    float:left;
    padding:10px;	 	 
}
footer {
    background-color:black;
    color:white;
    clear:both;
    text-align:center;
    padding:5px;	 	 
}
</style>
</head>

<body>

<header>
<h1>City Gallery</h1>
</header>

<nav>
London<br>
Paris<br>
Tokyo<br>
</nav>

<section>
<h1>London</h1>
<p>
London is the capital city of England. It is the most populous city in the United Kingdom,
with a metropolitan area of over 13 million inhabitants.
</p>
<p>
Standing on the River Thames, London has been a major settlement for two millennia,
its history going back to its founding by the Romans, who named it Londinium.
</p>
</section>

<footer>
Copyright W3Schools.com
</footer>

</body>
</html>
```

# HTML响应式Web设计

## 什么是响应式 Web 设计？

- RWD 指的是响应式 Web 设计（Responsive Web Design）
- RWD 能够以可变尺寸传递网页
- RWD 对于平板和移动设备是必需的

## 创建自己的响应式设计

创建响应式设计的一个方法，是自己来创建它：

```html
<!DOCTYPE html>
<html lang="en-US">
<head>
<style>
.city {
float: left;
margin: 5px;
padding: 15px;
width: 300px;
height: 300px;
border: 1px solid black;
} 
</style>
</head>

<body>

<h1>W3School Demo</h1>
<h2>Resize this responsive page!</h2>
<br>

<div class="city">
<h2>London</h2>
<p>London is the capital city of England.</p>
<p>It is the most populous city in the United Kingdom,
with a metropolitan area of over 13 million inhabitants.</p>
</div>

<div class="city">
<h2>Paris</h2>
<p>Paris is the capital and most populous city of France.</p>
</div>

<div class="city">
<h2>Tokyo</h2>
<p>Tokyo is the capital of Japan, the center of the Greater Tokyo Area,
and the most populous metropolitan area in the world.</p>
</div>

</body>
</html>
```

## 使用Bootstrap

另一个创建响应式设计的方法，是使用现成的 CSS 框架。

Bootstrap 是最流行的开发响应式 web 的 HTML, CSS, 和 JS 框架。

Bootstrap 帮助您开发在任何尺寸都外观出众的站点：显示器、笔记本电脑、平板电脑或手机：

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="stylesheet" 
  href="http://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
</head>

<body>

<div class="container">
<div class="jumbotron">
  <h1>W3School Demo</h1> 
  <p>Resize this responsive page!</p> 
</div>
</div>

<div class="container">
<div class="row">
  <div class="col-md-4">
    <h2>London</h2>
    <p>London is the capital city of England.</p>
    <p>It is the most populous city in the United Kingdom,
    with a metropolitan area of over 13 million inhabitants.</p>
  </div>
  <div class="col-md-4">
    <h2>Paris</h2>
    <p>Paris is the capital and most populous city of France.</p>
  </div>
  <div class="col-md-4">
    <h2>Tokyo</h2>
    <p>Tokyo is the capital of Japan, the center of the Greater Tokyo Area,
    and the most populous metropolitan area in the world.</p>
  </div>
</div>
</div>

</body>
</html>
```



# HTML表单和输入

## HTML表单

表单元素是允许用户在表单中输入内容,比如：文本域(textarea)、下拉列表、单选框(radio-buttons)、复选框(checkboxes)等等。

表单使用表单标签 &#60;form> 来设置:

```html
<form>
    input 元素
</form>
```

## HTML表单-输入元素

多数情况下被用到的表单标签是输入标签（&#60;input>）。

输入类型是由类型属性（type）定义的。大多数经常被用到的输入类型如下：

### 文本域（Text Fields）

```html
<form>
    First name:<input type="text" name="firstname"><br />
    Last name:<input type="text" name="lastname">
</form>
```

### 密码字段

通过&#60;input type="password">来定义：

```html
<form>
    Password:<input type="password" name="pwd">
</form>
```

### 单选按钮（Radio Buttons）

```html
<form>
    <input type="radio" name="sex" value="male">Male<br />
    <input type="radio" name="sex" value="female">Female
</form>
```

### 复选框（Checkboxes）

```html
<form>
    <input type="checkbox" name="vehicle" value="Bike">I have a bike<br />
    <input type="checkbox" name="vehicle" value="Car">I have a car
</form>
```

### 提交按钮（Submit Button)

当用户单击确认按钮时，表单的内容会被传送到另一个文件。表单的动作属性定义了目的文件的文件名。由动作属性定义的这个文件通常会对接收到的输入数据进行相关的处理。

```html
<form name="input" action="html_form_action.php" method="get">
    Username:<input type="text" name="user">
    <input type="submit" value="submit">
</form>
```



# HTML框架

通过使用框架，你可以在同一个浏览器窗口中显示不止一个页面。

**iframe语法:**

```html
<iframe src="URL"></iframe>
该URL指向不同的网页。
```

## iframe - 设置高度与宽度

height 和 width 属性用来定义iframe标签的高度与宽度。

属性默认以像素为单位, 但是你可以指定其按比例显示 (如："80%")。

```html
<iframe src="demo_iframe.htm" width="200" height="200"></iframe>
```

## iframe - 移除边框

frameborder 属性用于定义iframe表示是否显示边框。

设置属性值为 "0" 移除iframe的边框:

```html
<iframe src="demo_iframe.htm" frameborder="0"></iframe>
```



# HTML颜色

HTML 颜色由红色、绿色、蓝色混合而成。

## 颜色值

HTML 颜色由一个十六进制符号来定义，这个符号由红色、绿色和蓝色的值组成（RGB）。

每种颜色的最小值是0（十六进制：#00）。最大值是255（十六进制：#FF）。

这个表格给出了由三种颜色混合而成的具体效果：

## 1600万种不同颜色

三种颜色 红，绿，蓝的组合从0到255，一共有1600万种不同颜色(256 x 256 x 256)。

在下面的颜色表中你会看到不同的结果，从0到255的红色，同时设置绿色和蓝色的值为0,随着红色的值变化，不同的值都显示了不同的颜色。

## HTML颜色名

141个颜色名称是在HTML和CSS颜色规范定义的（17标准颜色，再加124）。下表列出了所有颜色的值，包括十六进制值。

 **提示:** 17标准颜色：黑色，蓝色，水，紫红色，灰色，绿色，石灰，栗色，海军，橄榄，橙，紫，红，白，银，蓝绿色，黄色。点击其中一个颜色名称（或一个十六进制值）就可以查看与不同文字颜色搭配的背景颜色。

点击：[HTML颜色名](https://www.runoob.com/html/html-colornames.html)



# HTML脚本

JavaScript使HTML页面具有更强的动态和交互性。

## HTML&#60;script>标签

&#60;script> 标签用于定义客户端脚本，比如 JavaScript。

&#60;script> 元素既可包含脚本语句，也可通过 src 属性指向外部脚本文件。


JavaScript 最常用于图片操作、表单验证以及内容动态更新。

下面的脚本会向浏览器输出"Hello World!"：

```html
<script>
doucument.write("Hello World!")
</script>
```

## HTML&#60;noscript>标签

&#60;noscript>标签提供无法使用脚本时的替代内容，比方在浏览器禁用脚本时，或浏览器不支持客户端脚本时。

&#60;noscript>元素可包含普通 HTML 页面的 body 元素中能够找到的所有元素。

只有在浏览器不支持脚本或者禁用脚本时，才会显示 &#60;noscript> 元素中的内容：

```html
<script>
document.write("Hello World!")
</script>
<noscript>抱歉，你的浏览器不支持</noscript>
```



# HTML字符实体

HTML 中的预留字符必须被替换为字符实体。

一些在键盘上找不到的字符也可以使用字符实体来替换。

## HTML实体

在 HTML 中，某些字符是预留的。

在 HTML 中不能使用小于号（<）和大于号（>），这是因为浏览器会误认为它们是标签。

如果希望正确地显示预留字符，我们必须在 HTML 源代码中使用字符实体（character entities）。 字符实体类似这样：

```html
&#entity_name;
或
&#entity_number;
```

如需显示小于号，我们必须这样写：**`&lt` **或 **`&#60`** 或 **`&#060`**

## 不间断空格

HTML 中的常用字符实体是不间断空格(`&nbsp;`)。

浏览器总是会截短 HTML 页面中的空格。如果您在文本中写 10 个空格，在显示该页面之前，浏览器会删除它们中的 9 个。如需在页面中增加空格的数量，您需要使用 `&nbsp;` 字符实体。

## 结合音标符

发音符号是加到字母上的一个"glyph(字形)"。

一些变音符号, 如 尖音符 ( ̀) 和 抑音符 ( ́) 。

变音符号可以出现字母的上面和下面，或者字母里面，或者两个字母间。

变音符号可以与字母、数字字符的组合来使用。



# HTML URL

统一资源定位器（Uniform Resource Locators)

URL 是一个网页地址。

URL可以由字母组成，如"runoob.com"，或互联网协议（IP）地址： 192.68.20.50。大多数人进入网站使用网站域名来访问，因为名字比数字更容易记住。