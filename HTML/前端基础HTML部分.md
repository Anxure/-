# 什么是HTML?

###### html是用来描述网页的一种语言。

- HTML 指的是超文本标记语言: HyperText Markup Language
- HTML 不是一种编程语言，而是一种标记语言
- 标记语言是一套标记标签 (markup tag)
- HTML 使用标记标签来描述网页
- HTML 文档包含了HTML 标签及文本内容
- HTML文档也叫做 web 页面

## HTML标签
HTML 标记标签通常被称为 HTML 标签 (HTML tag)
- HTML 标签是由尖括号包围的关键词，比如 `<html>`
- HTML 标签通常是成对出现的，比如 `<b> `和 `</b>`
- 标签对中的第一个标签是开始标签，第二个标签是结束标签
- 开始和结束标签也被称为开放标签和闭合标签

## HTML元素

- HTML 标签" 和 "HTML 元素" 通常都是描述同样的意思.

  

## HTML编辑器

- VS Code

- Sublime Text

- Webstorm

  

##  HTML基础

#### HTML标题

​	HTML 标题（Heading）是通过`<h1>` - `<h6> `标签来定义的.

#### HTML段落

​	HTML 段落是通过标签 `<p>` 来定义的.

####  HTML 链接

​	HTML 链接是通过标签 `<a>` 来定义的.

#### HTML 图像

​	HTML 图像是通过标签 `<img>` 来定义的.

##  HTML元素

 #### HTML元素语法

- HTML 元素以**开始标签**起始

- HTML 元素以**结束标签**终止

- **元素的内容**是开始标签与结束标签之间的内容

- 某些 HTML 元素具有**空内容（empty content）**

- 空元素**在开始标签中进行关闭**（以开始标签的结束而结束）

- 大多数 HTML 元素可拥有**属性**

####  HTML提示

- 不要忘记结束标签（即使你忘记了结束标签，有的浏览器也会正常显示，但会产生不可预料的结果或错误）
- 使用小写标签 HTML标签对大小写不敏感，但是在未来版本会强制使用小写

##  HTML属性

- HTML 元素可以设置**属性**

- 属性可以在元素中添加**附加信息**

- 属性一般描述于**开始标签**

- 属性总是以名称/值对的形式出现，**比如：name="value"**。

#### 属性实例

HTML 链接由 `<a> `标签定义。链接的地址在 **href 属性**中指定：

`

<a href="http://www.baidu.com">这是一个链接</a>

`

#### 常用的属性列表

- class    为html元素定义一个或多个类名（classname）(类名从样式文件引入)

- id   定义元素的唯一id
- style  规定元素的行内样式（inline style）
- title  描述了元素的额外信息 (作为工具条使用)

## HTML头部

#### HTML `<head>` 元素

`<head>` 元素包含了所有的头部标签元素。在 <head>元素中你可以插入脚本（scripts）, 样式文件（CSS），及各种meta信息。

可以添加在头部区域的元素标签为: `<title>, <style>, <meta>, <link>, <script>, <noscript> 和 <base>`。

#### HTML `<title>`元素

`<title>` 标签定义了不同文档的标题。

`<title>` 在 HTML/XHTML 文档中是必须的。

`<title>`元素：

	- 定义了浏览器工具栏的标题
	- 当网页添加收藏夹时，显示在收藏夹钟的标题
	- 显示再搜索引擎结果页面的标题

实例：

#### HTML `<base>` 元素

`<base>` 标签描述了基本的链接地址/链接目标，该标签作为HTML文档中所有的链接标签的默认链接:

```
<head>
<base href="http://www.runoob.com/images/" target="_blank">
</head>
```

#### HTML`<link>`元素

`<link> `标签定义了文档与外部资源之间的关系。

`<link>` 标签通常用于链接到样式表:

```
<head>
<link rel="stylesheet" type="text/css" href="mystyle.css">
</head>
```

#### HTML `<style>` 元素

`<style>` 标签定义了HTML文档的样式文件引用地址.


在`<style>` 元素中你也可以直接添加样式来渲染 HTML 文档:

```
<head>
<style type="text/css">
body {background-color:yellow}
p {color:blue}
</style>
</head>
```

#### HTML`<meta>`元素

meta标签描述了一些基本的元数据。

`<meta>` 标签提供了元数据.元数据也不显示在页面上，但会被浏览器解析。

META 元素通常用于指定网页的描述，关键词，文件的最后修改时间，作者，和其他元数据。

元数据可以使用于浏览器（如何显示内容或重新加载页面），搜索引擎（关键词），或其他Web服务。

`<meta>` 一般放置于 `<head>` 区域

`<meta>`标签使用实例：

- 为搜索引擎定义关键词:

  ```
  <meta name="keywords" content="HTML, CSS, XML, XHTML, JavaScript">
  ```

- 为网页描述内容：

  ```
  <meta name="description" content="中电万维 前端开发">
  ```

- 定义网页作者：

  ```
  <meta name="author" content="xulian">
  ```

- 每30秒钟刷新当前页面:

  ```
  <meta http-equiv="refresh" content="30">
  ```

#### HTML `<script> `元素

`<script>`标签用于加载脚本文件，如： JavaScript。

`<script>` 元素在以后的章节中会详细描述。

## HTML CSS

CSS (Cascading Style Sheets) 用于渲染HTML元素标签的样式。

#### 如何使用css

CSS 是在 HTML 4 开始使用的,是为了更好的渲染HTML元素而引入的.

CSS 可以通过以下方式添加到HTML中:

- 内联样式 - 在HTML元素中使用"style" **属性**

- 内部样式表 - 在HTML文档头部 <head> 区域使用<style> **元素** 来包含CSS

- 外部引用 - 使用外部 CSS **文件**

注意：最好的方式是通过外部引用CSS文件.

#### 内联样式

当特殊的样式需要应用到个别元素时，就可以使用内联样式。 使用内联样式的方法是在相关的标签中使用样式属性。样式属性可以包含任何 CSS 属性。

```
<p style="color:blue;margin-left:20px;">这是一个段落。</p>
```

#### 内部样式表

当单个文件需要特别样式时，就可以使用内部样式表。你可以在`<head>` 部分通过 `<style>`标签定义内部样式表:

```
<head>
<style type="text/css">
body {background-color:yellow;}
p {color:blue;}
</style>
</head>
```

#### 外部样式表

当样式需要被应用到很多页面的时候，外部样式表将是理想的选择。使用外部样式表，你就可以通过更改一个文件来改变整个站点的外观。

```
head>
<link rel="stylesheet" type="text/css" href="mystyle.css">
</head>
```

## HTML表格

表格由 `<table>` 标签来定义。每个表格均有若干行（由 `<tr>` 标签定义），每行被分割为若干单元格（由 `<td> `标签定义）。字母 td 指表格数据（table data），即数据单元格的内容。数据单元格可以包含文本、图片、列表、段落、表单、水平线、表格等等。

<table border="1">
    <tr>
        <td>row 1, cell 1</td>
        <td>row 1, cell 2</td>
    </tr>
    <tr>
        <td>row 2, cell 1</td>
        <td>row 2, cell 2</td>
    </tr>
</table>

#### HTML 表格表头

表格的表头使用 `<th>` 标签进行定义。

<table border="1">
    <tr>
        <th>Header 1</th>
        <th>Header 2</th>
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

## HTML列表

HTML 支持有序、无序和定义列表:

#### HTML无序列表

无序列表使用 <ul> 标签

<ul>
<li>Coffee</li>
<li>Milk</li>
</ul>

#### HTML有序列表

有序列表始于 <ol> 标签。每个列表项始于 <li> 标签

<ol>
<li>Coffee</li>
<li>Milk</li>
</ol>
#### HTML自定义列表

自定义列表不仅仅是一列项目，而是项目及其注释的组合。

自定义列表以 `<dl> `标签开始。每个自定义列表项以 `<dt> `开始。每个自定义列表项的定义以 `<dd> `开始。

<dl>
<dt>Coffee</dt>
<dd>- black hot drink</dd>
<dt>Milk</dt>
<dd>- white cold drink</dd>
</dl>

## HTML区块

#### HTML区块元素

大多数 HTML 元素被定义为**块级元素**或**内联元素**。

块级元素在浏览器显示时，通常会以新行来开始（和结束）。

实例: `<h1>`, `<p>`, `<ul>`,` <table>`

#### HTML内联元素

内联元素在显示时通常不会以新行开始。

实例: `<b>`, `<td>`, `<a>`, `<img>`

#### HTML `<div>` 元素

HTML `<div>` 元素是块级元素，它可用于组合其他 HTML 元素的容器。

<div> 元素没有特定的含义。除此之外，由于它属于块级元素，浏览器会在其前后显示折行。

如果与 CSS 一同使用，<div> 元素可用于对大的内容块设置样式属性。

`<div>` 元素的另一个常见的用途是文档布局。它取代了使用表格定义布局的老式方法。使用 `<table>` 元素进行文档布局不是表格的正确用法。`<table>` 元素的作用是显示表格化的数据。

#### HTML `<span>` 元素

HTML `<span>` 元素是内联元素，可用作文本的容器

`<span>` 元素也没有特定的含义。

当与 CSS 一同使用时，`<span>` 元素可用于为部分文本设置样式属性。

## HTML表单

表单是一个包含表单元素的区域。

表单元素是允许用户在表单中输入内容,比如：文本域(textarea)、下拉列表、单选框(radio-buttons)、复选框(checkboxes)等等。

表单使用表单标签 <form> 来设置:

#### 文本域（Text Fields）

<form>
First name: <input type="text" name="firstname"><br>
Last name: <input type="text" name="lastname">
</form>

#### 密码字段

密码字段通过标签<input type="password"> 来定义:

<form>
Password: <input type="password" name="pwd">
</form>

#### 单选按钮

<input type="radio"> 标签定义了表单单选框选项

<form>
<input type="radio" name="sex" value="male">Male<br>
<input type="radio" name="sex" value="female">Female
</form>

#### 复选框

<input type="checkbox"> 定义了复选框. 用户需要从若干给定的选择中选取一个或若干选项。

<form>
<input type="checkbox" name="vehicle" value="Bike">I have a bike<br>
<input type="checkbox" name="vehicle" value="Car">I have a car 
</form>

#### 提交按钮

<input type="submit"> 定义了提交按钮.

当用户单击确认按钮时，表单的内容会被传送到另一个文件。表单的动作属性定义了目的文件的文件名。由动作属性定义的这个文件通常会对接收到的输入数据进行相关的处理。

<form name="input" action="html_form_action.php" method="get">
Username: <input type="text" name="user">
<input type="submit" value="Submit">
</form>

#### 下拉选框

<form action="">
<select name="cars">
<option value="volvo">Volvo</option>
<option value="saab">Saab</option>
<option value="fiat" selected>Fiat</option>
<option value="audi">Audi</option>
</select>
</form>

## HTML脚本

JavaScript 使 HTML 页面具有更强的动态和交互性。

#### HTML `<script>` 标签

<script> 标签用于定义客户端脚本，比如 JavaScript。

<script> 元素既可包含脚本语句，也可通过 src 属性指向外部脚本文件。
JavaScript 最常用于图片操作、表单验证以及内容动态更新。

下面的脚本会向浏览器输出"Hello World!"：

<script> document.write("Hello World!"); </script>

#### HTML`<noscript>` 标签

<noscript> 标签提供无法使用脚本时的替代内容，比方在浏览器禁用脚本时，或浏览器不支持客户端脚本时。

<noscript>元素可包含普通 HTML 页面的 body 元素中能够找到的所有元素。

只有在浏览器不支持脚本或者禁用脚本时，才会显示 <noscript> 元素中的内容：

## HTML5

#### 什么是HTML5

HTML5 是下一代 HTML 标准。

HTML , HTML 4.01的上一个版本诞生于 1999 年。自从那以后，Web 世界已经经历了巨变。

HTML5 仍处于完善之中。然而，大部分现代浏览器已经具备了某些 HTML5 支持。

#### HTML新元素

- 新多媒体元素

  `<audio> `定义音频内容

  `<video>`定义视频

  `<source>` 定义多媒体资源`<audio>和<video>`

  .......

- 新的表单元素

  `<datalist>` 定义选项列表。请与input元素配合使用，来定义input可能的值

  `<keygen>`规定用于表单的密钥生成器字段

  `<output>`定义不同类型的输出，比如脚本的输出

- 新的语义和结构元素

  `<article>` 定义页面独立的内容区域

  `<aside>`定义页面的侧边栏内容

  `<footer>` 定义section或document的页脚

  `<header>`定义了文档的头部区域

  `<nav>` 定义了导航链接的部分

  `<section>`定义文档的节

  .....