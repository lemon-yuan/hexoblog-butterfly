---
title: HTML5学习笔记
date: 2020-06-29 16:27:01
tags:
  - html
  - html5
categories: 终身学习
description: HTML5
cover: https://blog-butterfly-cdn.mistill.com/img/post_cover/post_cover_019.webp
abbrlink: learn-html5-note
---


# HTML5 简介

HTML5是HTML最新的修订版本，2014年10月由万维网联盟（W3C）完成标准制定。

HTML5的设计目的是为了在移动设备上支持多媒体。

HTML5 简单易学。

<!-- more -->

## 什么是HTML5

HTML5 是下一代 HTML 标准。

HTML , HTML 4.01的上一个版本诞生于 1999 年。自从那以后，Web 世界已经经历了巨变。

HTML5 仍处于完善之中。然而，大部分现代浏览器已经具备了某些 HTML5 支持。

## HTML是如何起步的

HTML5 是 W3C 与 WHATWG 合作的结果,WHATWG 指 Web Hypertext Application Technology Working Group。

WHATWG 致力于 web 表单和应用程序，而 W3C 专注于 XHTML 2.0。在 2006 年，双方决定进行合作，来创建一个新版本的 HTML。

HTML5 中的一些有趣的新特性：

- 用于绘画的 canvas 元素
- 用于媒介回放的 video 和 audio 元素
- 对本地离线存储的更好的支持
- 新的特殊内容元素，比如 article、footer、header、nav、section
- 新的表单控件，比如 calendar、date、time、email、url、search

## 最小的HTML5文档

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>文档标题</title>
</head>
 
<body>
文档内容......
</body>
 
</html>
```

**注意：***对于中文网页需要使用 **&#60;meta charset="utf-8">** *声明编码，否则会出现乱码。*



# HTML5 新元素

为了更好地处理今天的互联网应用，HTML5添加了很多新元素及功能，比如: 图形的绘制，多媒体内容，更好的页面结构，更好的形式 处理，和几个api拖放元素，定位，包括网页 应用程序缓存，存储，网络工作者，等。

## &#60;canvas>新元素

&#60;canvas>标签定义图形，比如图表和其他图像。该标签基于 JavaScript 的绘图 API

## 新多媒体元素

| 标签      | 描述                                                         |
| --------- | ------------------------------------------------------------ |
| &#60;audio>  | 定义音频内容                                                 |
| &#60;video>  | 定义视频（video 或者 movie）                                 |
| &#60;source> | 定义多媒体资源 &#60;video> 和 &#60;audio>                          |
| &#60;embed>  | 定义嵌入的内容，比如插件。                                   |
| &#60;track>  | 为诸如 &#60;video> 和 &#60;audio> 元素之类的媒介规定外部文本轨道。 |

## 新表单元素

| 标签        | 描述                                                         |
| ----------- | ------------------------------------------------------------ |
| &#60;datalist> | 定义选项列表。请与 input 元素配合使用该元素，来定义 input 可能的值。 |
| &#60;keygen>   | 规定用于表单的密钥对生成器字段。                             |
| &#60;output>   | 定义不同类型的输出，比如脚本的输出。                         |

## 新的语义和结构元素

| 标签                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [&#60;artile>](https://www.runoob.com/tags/tag-article.html)    | 定义页面独立的内容区域。                                     |
| [&#60;aside>](https://www.runoob.com/tags/tag-aside.html)       | 定义页面的侧边栏内容。                                       |
| [&#60;bdi>](https://www.runoob.com/tags/tag-bdi.html)           | 允许您设置一段文本，使其脱离其父元素的文本方向设置。         |
| [&#60;commande>](https://www.runoob.com/tags/tag-command.html)  | 定义命令按钮，比如单选按钮、复选框或按钮                     |
| [&#60;details>](https://www.runoob.com/tags/tag-details.html)   | 用于描述文档或文档某个部分的细节                             |
| [&#60;dialog>](https://www.runoob.com/tags/tag-dialog.html)     | 定义对话框，比如提示框                                       |
| [&#60;summary>](https://www.runoob.com/tags/tag-summary.html)   | 标签包含 details 元素的标题                                  |
| [&#60;figure>](https://www.runoob.com/tags/tag-figure.html)     | 规定独立的流内容（图像、图表、照片、代码等等）。             |
| [&#60;figcaption>](https://www.runoob.com/tags/tag-figcaption.html) | 定义 &#60;figure> 元素的标题                                    |
| [&#60;footer>](https://www.runoob.com/tags/tag-footer.html)     | 定义 section 或 document 的页脚。                            |
| [&#60;header>](https://www.runoob.com/tags/tag-header.html)     | 定义了文档的头部区域                                         |
| [&#60;mark>](https://www.runoob.com/tags/tag-mark.html)         | 定义带有记号的文本。                                         |
| [&#60;meter>](https://www.runoob.com/tags/tag-meter.html)       | 定义度量衡。仅用于已知最大和最小值的度量。                   |
| [&#60;nav>](https://www.runoob.com/tags/tag-nav.html)           | 定义导航链接的部分。                                         |
| [&#60;progress>](https://www.runoob.com/tags/tag-progress.html) | 定义任何类型的任务的进度。                                   |
| [&#60;ruby>](https://www.runoob.com/tags/tag-ruby.html)         | 定义 ruby 注释（中文注音或字符）。                           |
| [&#60;rt>](https://www.runoob.com/tags/tag-rt.html)             | 定义字符（中文注音或字符）的解释或发音。                     |
| [&#60;rp>](https://www.runoob.com/tags/tag-rp.html)             | 在 ruby 注释中使用，定义不支持 ruby 元素的浏览器所显示的内容。 |
| [&#60;section>](https://www.runoob.com/tags/tag-section.html)   | 定义文档中的节（section、区段）。                            |
| [&#60;time>](https://www.runoob.com/tags/tag-time.html)         | 定义日期或时间。                                             |
| [&#60;wbr>](https://www.runoob.com/tags/tag-wbr.html)           | 规定在文本中的何处适合添加换行符。                           |

## 已移除的元素

- &#60;acronym>
- &#60;applet>
- &#60;basefont>
- &#60;big>
- &#60;center>
- &#60;dir>
- &#60;font>
- &#60;frame>
- &#60;frameset>
- &#60;noframes>
- &#60;strike>
- &#60;tt>



# HTML5 Canvas

&#60;canvas> 标签定义图形，比如图表和其他图像，您必须使用脚本来绘制图形。

在画布上（Canvas）画一个红色矩形，渐变矩形，彩色矩形，和一些彩色的文字。

## 创建一个画布（Canvas）

一个画布在网页中是一个矩形框，通过 &#60;canvas> 元素来绘制.

**注意:** 默认情况下&#60;canvas> 元素没有边框和内容。

&#60;canvas>简单实例如下:

```html
<canvas id="myCanvas" width="200" height="100"></canvas>
```

**注意:** 标签通常需要指定一个id属性 (脚本中经常引用), width 和 height 属性定义的画布的大小.

**提示:**你可以在HTML页面中使用多个 &#60;canvas> 元素.

使用 style 属性来添加边框:

```html
<canvas id="myCanvas" width="200" height="100" style="border:1px bolid #000000;">
</canvas>
```

## 使用JavaScript来绘制图像

canvas 元素本身是没有绘图能力的。所有的绘制工作必须在 JavaScript 内部完成：

```javascript
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.fillStyle="#FF0000";
ctx.fillRect(0,0,150,75);
```

## Canvas 坐标

canvas 是一个二维网格。

canvas 的左上角坐标为 (0,0)

上面的 fillRect 方法拥有参数 (0,0,150,75)。

意思是：在画布上绘制 150x75 的矩形，从左上角开始 (0,0)。

## Canvas 路径

在Canvas上画线，我们将使用以下两种方法：

- moveTo(*x,y*) 定义线条开始坐标
- lineTo(*x,y*) 定义线条结束坐标

绘制线条我们必须使用到 "ink" 的方法，就像stroke().

实例：

定义开始坐标(0,0), 和结束坐标 (200,100)。然后使用 stroke() 方法来绘制线条:

```javascript
var c=doucument.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.moveTo(0,0);
ctx.lineTo(200,100);
ctx.stroke();
```

## Canvas 文本

使用 canvas 绘制文本，重要的属性和方法如下：

- font - 定义字体
- fillText(*text,x,y*) - 在 canvas 上绘制实心的文本
- strokeText(*text,x,y*) - 在 canvas 上绘制空心的文本

使用 fillText():

```javascript
var c=doucument.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.font="30px Arial";
ctx.fillText("Hello World",10,50)
```

## Canvas 渐变

## Canvas 图像





# HTML5 内联SVG

## 什么是SVG？

- SVG 指可伸缩矢量图形 (Scalable Vector Graphics)
- SVG 用于定义用于网络的基于矢量的图形
- SVG 使用 XML 格式定义图形
- SVG 图像在放大或改变尺寸的情况下其图形质量不会有损失
- SVG 是万维网联盟的标准

## SVG优势

与其他图像格式相比（比如 JPEG 和 GIF），使用 SVG 的优势在于：

- SVG 图像可通过文本编辑器来创建和修改
- SVG 图像可被搜索、索引、脚本化或压缩
- SVG 是可伸缩的
- SVG 图像可在任何的分辨率下被高质量地打印
- SVG 可在图像质量不下降的情况下被放大

## 将SVG直接嵌入HTML页面

```html
<!DOCTYPE html>
<html>
<body>
 
<svg xmlns="http://www.w3.org/2000/svg" version="1.1" height="190">
  <polygon points="100,10 40,180 190,60 10,60 160,180"
  style="fill:lime;stroke:purple;stroke-width:5;fill-rule:evenodd;">
</svg>
 
</body>
</html>
```

## SVG与Canvas两者间的区别

SVG 是一种使用 XML 描述 2D 图形的语言。

Canvas 通过 JavaScript 来绘制 2D 图形。

SVG 基于 XML，这意味着 SVG DOM 中的每个元素都是可用的。您可以为某个元素附加 JavaScript 事件处理器。

在 SVG 中，每个被绘制的图形均被视为对象。如果 SVG 对象的属性发生变化，那么浏览器能够自动重现图形。

Canvas 是逐像素进行渲染的。在 canvas 中，一旦图形被绘制完成，它就不会继续得到浏览器的关注。如果其位置发生变化，那么整个场景也需要重新绘制，包括任何或许已被图形覆盖的对象。



# HTML5 MathML

HTML5 可以在文档中使用 MathML 元素，对应的标签是 &#60;math>...&#60;/math> 。

MathML 是数学标记语言，是一种基于XML（标准通用标记语言的子集）的标准，用来在互联网上书写数学符号和公式的置标语言。

```html
<!DOCTYPE html>
<html>
   <head>
      <meta charset="UTF-8">
      <title>菜鸟教程(runoob.com)</title>
   </head>
    
   <body>
    
      <math xmlns="http://www.w3.org/1998/Math/MathML">
        
         <mrow>
            <msup><mi>a</mi><mn>2</mn></msup>
            <mo>+</mo>
                
            <msup><mi>b</mi><mn>2</mn></msup>
            <mo>=</mo>
                
            <msup><mi>c</mi><mn>2</mn></msup>
         </mrow>
            
      </math>
        
   </body>
</html> 
```



# HTML5 拖放（Drag和Drop）



# HTML5 地理定位



# HTML5 Video(视频)

## HTML5 视频如何工作

```html
<video width="320" height="240" controls>
	<source src="movie.mp4" type="video/mp4">
    <source src="movie.ogg" type="video/ogg">
您的浏览器不支持 video元素。
</video>
```



# HTML5 Audio(音频)

## HTML5 Audio音频如何工作

```html
<audio controls>
	<source src="hores.ogg" type="audio/ogg">
    <source src="hores.mp3" type="audio/mpeg">
您的浏览器不支持audio元素。
</audio>
```



# HTML5 新的Input类型

HTML5 拥有多个新的表单输入类型。这些新特性提供了更好的输入控制和验证。

本章全面介绍这些新的输入类型：

- color
- date
- datetime
- datetime-local
- email
- month
- number
- range
- search
- tel
- time
- url
- week

**注意:**并不是所有的主流浏览器都支持新的input类型，不过您已经可以在所有主流的浏览器中使用它们了。即使不被支持，仍然可以显示为常规的文本域。

## Input类型：color

color 类型用在input字段主要用于选取颜色，如下所示，从拾色器选择一个颜色

```html
选择你喜欢的颜色：<input type="color" name="favcolor">
```

## Input类型：date

date 类型允许你从一个日期选择器选择一个日期。定义一个使劲啊控制器：

```html
生日：<input type="date" name="bday">
```

## Input类型：datetime

datetime 类型允许你选择一个日期（UTC 时间）。定义一个日期和时间控制器

```html
生日（日期和时间）:<input type="datetime" name="bdaytime">
```

## Input类型：datetime-local

datetime-local 类型允许你选择一个日期和时间 (无时区).定义一个日期和时间 (无时区):

```html
生日（日期和时间）：<input type="datetime-local" name="bdaytime">
```

## Input类型：email

email 类型用于应该包含 e-mail 地址的输入域。在提交表单时，会自动验证 email 域的值是否合法有效:

```html
E-mail:<input type="email" name="email">
```

## Input类型：month

month 类型允许你选择一个月份。定义月与年 (无时区):

```html
生日（月和年）：<input type="month" name="bdaymonth">
```

## Input类型：number

number 类型用于应该包含数值的输入域。

您还能够设定对所接受的数字的限定：

定义一个数值输入域(限定):

```html
数量（1-5之间）：<input type="number" name="quantity" min="1" max="5">
```

使用下面的属性来规定对数字类型的限定：

| 属性      | 描述                       |
| :-------- | :------------------------- |
| disabled  | 规定输入字段是禁用的       |
| max       | 规定允许的最大值           |
| maxlength | 规定输入字段的最大字符长度 |
| min       | 规定允许的最小值           |
| pattern   | 规定用于验证输入字段的模式 |
| readonly  | 规定输入字段的值无法修改   |
| required  | 规定输入字段的值是必需的   |
| size      | 规定输入字段中的可见字符数 |
| step      | 规定输入字段的合法数字间隔 |
| value     | 规定输入字段的默认值       |

## Input类型：range

range 类型用于应该包含一定范围内数字值的输入域。

range 类型显示为滑动条。

定义一个不需要非常精确的数值（类似于滑块控制）:

```html
<input type="range" name="points" min="1" max="10">
```

请使用下面的属性来规定对数字类型的限定：

- max - 规定允许的最大值
- min - 规定允许的最小值
- step - 规定合法的数字间隔
- value - 规定默认值

## Input类型：search

search 类型用于搜索域，比如站点搜索或 Google 搜索。

定义一个搜索字段 (类似站点搜索或者Google搜索):

```html
Search Google: <input type="search" name="googlesearch">
```

## Input类型：tel

定义输入电话号码字段:

```html
电话号码：<input type="tel" name="usrtel">
```

## Input类型：time

time 类型允许你选择一个时间。

定义可输入时间控制器（无时区）：

```html
选择时间：<input type="time" name="usr_time">
```

## Input类型：url

url 类型用于应该包含 URL 地址的输入域。

在提交表单时，会自动验证 url 域的值。

定义输入URL字段:

```html
添加您的主页：<input type="url" name="homepage">
```

## Input类型：week

week 类型允许你选择周和年。

定义周和年 (无时区):

```html
选择周：<input type="week" name="week_year">
```



# HTML5 表单元素

HTML5 有以下新的表单元素:

- &#60;datalist>
- &#60;keygen>
- &#60;output>

## HTML5 &#60;datalist>元素

&#60;datalist> 元素规定输入域的选项列表。

&#60;datalist> 属性规定 form 或 input 域应该拥有自动完成功能。当用户在自动完成域中开始输入时，浏览器应该在该域中显示填写的选项：

使用 &#60;input> 元素的列表属性与 &#60;datalist> 元素绑定.

&#60;input> 元素使用&#60;datalist>预定义值:

```html
<input list="browsers">

<datalist id="browsers">
	<option value="Internet Explorer">
	<option value="FireFox">
    <option value="Chrome">
</datalist>
```

## HTML5 &#60;keygen>元素

&#60;keygen> 元素的作用是提供一种验证用户的可靠方法。

&#60;keygen>标签规定用于表单的密钥对生成器字段。

当提交表单时，会生成两个键，一个是私钥，一个公钥。

私钥（private key）存储于客户端，公钥（public key）则被发送到服务器。公钥可用于之后验证用户的客户端证书（client certificate）。

带有keygen字段的表单:

```html
<form action="demo_kegen.asp" method="get">
    用户名：<input type="text" name="usr_name">
    密码：<keygen name="security">
    <input type="submit">
</form>
```

## HTML5 &#60;output>元素

&#60;output> 元素用于不同类型的输出，比如计算或脚本输出：

将计算结果显示在 &#60;output> 元素:

```html
<form oniput="x.value=parseInt(a.value)+parseInt(b.value)">0
    <input type="range" id="a" value="50">100
    +<input type="number" id="b" value="50">
    =<output name="x" for="a b"></output>
</form>
```

# HTML5 表单属性

## HTML5 新的表单属性

HTML5 的 &#60;form> 和 &#60;input>标签添加了几个新属性.

&#60;form>新属性：

- autocomplete
- novalidate

&#60;input>新属性：

- autocomplete
- autofocus
- form
- formaction
- formenctype
- formmethod
- formnovalidate
- formtarget
- height 与 width
- list
- min 与 max
- multiple
- pattern (regexp)
- placeholder
- required
- step



# HTML5 语义元素

## 什么是语义元素

一个语义元素能够清楚的描述其意义给浏览器和开发者。

**无语义** 元素实例: &#60;div> 和 &#60;span> - 无需考虑内容.

**语义**元素实例: &#60;form>, &#60;table>, and &#60;img> - 清楚的定义了它的内容.

## HTML5中新的语义元素

许多现有网站都包含以下HTML代码： &#60;div id="nav">, &#60;div class="header">, 或者 &#60;div id="footer">, 来指明导航链接, 头部, 以及尾部.

HTML5 提供了新的语义元素来明确一个Web页面的不同部分:

- &#60;header>
- &#60;nav>
- &#60;section>
- &#60;article>
- &#60;aside>
- &#60;figcaption>
- &#60;figure>
- &#60;footer>

## HTML5&#60;section>元素

&#60;section> 标签定义文档中的节（section、区段）。比如章节、页眉、页脚或文档中的其他部分。

根据W3C HTML5文档: section 包含了一组内容及其标题。

```html
<section>
  <h1>WWF</h1>
  <p>The World Wide Fund for Nature (WWF) is....</p>
</section>
```

## HTML5&#60;article>元素

&#60;article> 标签定义独立的内容。.

&#60;article> 元素使用实例:

- Forum post
- Blog post
- News story
- Comment

```html
<article>
  <h1>Internet Explorer 9</h1>
  <p>Windows Internet Explorer 9(缩写为 IE9 )在2011年3月14日21:00 发布。</p>
</article>
```

## HTML5&#60;nav>元素

&#60;nav> 标签定义导航链接的部分。

&#60;nav> 元素用于定义页面的导航链接部分区域，但是，不是所有的链接都需要包含在 &#60;nav> 元素中!

```html
<nav>
    <a href="/html/">HTML</a> |
    <a href="/css/">CSS</a> |
    <a href="/js/">JavaScript</a> |
    <a href="/jquery/">jQuery</a>
</nav>
```

## HTML5 &#60;aside> 元素

&#60;aside> 标签定义页面主区域内容之外的内容（比如侧边栏）。

aside 标签的内容应与主区域的内容相关.

```html
<p>My family and I visited The Epcot center this summer.</p>
 
<aside>
  <h4>Epcot Center</h4>
  <p>The Epcot Center is a theme park in Disney World, Florida.</p>
</aside>
```

## HTML5 &#60;header> 元素

&#60;header>元素描述了文档的头部区域

&#60;header>元素主要用于定义内容的介绍展示区域.

在页面中你可以使用多个&#60;header> 元素.

以下实例定义了文章的头部:

```html
<article>
  <header>
    <h1>Internet Explorer 9</h1>
    <p><time pubdate datetime="2011-03-15"></time></p>
  </header>
  <p>Windows Internet Explorer 9(缩写为 IE9 )是在2011年3月14日21:00发布的</p>
</article>
```

## HTML5 &#60;footer> 元素

&#60;footer> 元素描述了文档的底部区域.

&#60;footer> 元素应该包含它的包含元素

一个页脚通常包含文档的作者，著作权信息，链接的使用条款，联系信息等

文档中你可以使用多个 &#60;footer>元素.

```html
<footer>
  <p>Posted by: Hege Refsnes</p>
  <p><time pubdate datetime="2012-03-01"></time></p>
</footer>
```

## HTML5 &#60;figure> 和 &#60;figcaption> 元素

&#60;figure>标签规定独立的流内容（图像、图表、照片、代码等等）。

&#60;figure> 元素的内容应该与主内容相关，但如果被删除，则不应对文档流产生影响。

&#60;figcaption> 标签定义 &#60;figure> 元素的标题.

&#60;figcaption>元素应该被置于 "figure" 元素的第一个或最后一个子元素的位置。

```html
<figure>
  <img src="img_pulpit.jpg" alt="The Pulpit Rock" width="304" height="228">
  <figcaption>Fig1. - The Pulpit Pock, Norway.</figcaption>
</figure>
```



# HTML5 Web存储

# HTML5 Web SQL数据库

# HTML5 应用程序缓存

# HTMl5 Web Workers

# HTML5 SSE(Server-Sent Events)

服务器发送事件

# HTML5 WebSocket

WebSocket 是 HTML5 开始提供的一种在单个 TCP 连接上进行全双工通讯的协议。