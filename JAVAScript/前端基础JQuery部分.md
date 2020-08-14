## JQuery

jQuery是一个JavaScript函数库。

jQuery是一个轻量级的"写的少，做的多"的JavaScript库。

jQuery库包含以下功能：

- HTML 元素选取
- HTML 元素操作
- CSS 操作
- HTML 事件函数
- JavaScript 特效和动画
- HTML DOM 遍历和修改
- AJAX
- Utilities

## JQuery 语法

Query 语法是通过选取 HTML 元素，并对选取的元素执行某些操作。

基础语法：

```
$(selector).action()
```

#### 文档就绪事件

```
$(document).ready(function(){
 
   // 开始写 jQuery 代码...
 
});
```

这是为了防止文档在完全加载（就绪）之前运行 jQuery 代码，即在 DOM 加载完成后才可以对 DOM 进行操作。

**提示：**简洁写法（与以上写法效果相同）:

```
$(function(){
 
   // 开始写 jQuery 代码...
 
});
```

## JQuery选择器

jQuery 选择器基于元素的 id、类、类型、属性、属性值等"查找"（或选择）HTML 元素。 它基于已经存在的 [CSS 选择器](https://www.runoob.com/cssref/css-selectors.html)，除此之外，它还有一些自定义的选择器。

jQuery 中所有选择器都以美元符号开头：$()。

#### 元素选择器

```
$("p")
```

```
$(document).ready(function(){
  $("button").click(function(){
    $("p").hide();
  });
});
```

#### #id 选择器

页面中元素的 id 应该是唯一的，所以您要在页面中选取唯一的元素需要通过 #id 选择器

```
$("#test")
```

```
$(document).ready(function(){
  $("button").click(function(){
    $("#test").hide();
  });
});
```

#### .class 选择器

```
$(".test")
```

```
$(document).ready(function(){
  $("button").click(function(){
    $(".test").hide();
  });
});
```

## JQuery事件

#### click()

click() 方法是当按钮点击事件被触发时会调用一个函数。

```
$("p").click(function(){
  $(this).hide();
});
```

#### dblclick()

当双击元素时，会发生 dblclick 事件。

```
$("p").dblclick(function(){
  $(this).hide();
});
```

#### mouseenter()

当鼠标指针穿过元素时，会发生 mouseenter 事件。

```
$("#p1").mouseenter(function(){
    alert('您的鼠标移到了 id="p1" 的元素上!');
});
```

#### mouseleave()

当鼠标指针离开元素时，会发生 mouseleave 事件

```
$("#p1").mouseleave(function(){
    alert("再见，您的鼠标离开了该段落。");
});
```

#### mousedown()

当鼠标指针移动到元素上方，并按下鼠标按键时，会发生 mousedown 事件。

```
$("#p1").mousedown(function(){
    alert("鼠标在该段落上按下！");
});
```

#### mouseup()

当在元素上松开鼠标按钮时，会发生 mouseup 事件。

```
$("#p1").mouseup(function(){
    alert("鼠标在段落上松开。");
});
```

#### hover()

hover()方法用于模拟光标悬停事件。

```
$('#p').hover(function(){
	alert('鼠标悬停在上面了')
})
```

#### focus()

当元素获得焦点时，发生 focus 事件。

```
$("input").focus(function(){
  $(this).css("background-color","#cccccc");
});
```

#### blur()

当元素失去焦点时，发生 blur 事件。

```
$("input").blur(function(){
  $(this).css("background-color","#ffffff");
});
```

## JQuery HTML

#### 获得内容 - text()、html() 以及 val()

三个简单实用的用于 DOM 操作的 jQuery 方法：

- text() - 设置或返回所选元素的文本内容
- html() - 设置或返回所选元素的内容（包括 HTML 标记）
- val() - 设置或返回表单字段的值

```
$("#btn1").click(function(){
  alert("Text: " + $("#test").text());
});
$("#btn2").click(function(){
  alert("HTML: " + $("#test").html());
});
$("#btn1").click(function(){
  alert("值为: " + $("#test").val());
});
```

#### 获取属性 - attr()

jQuery attr() 方法用于获取属性值。

```
$("button").click(function(){
  alert($("#runoob").attr("href"));
});
```

#### 设置内容 - text()、html() 以及 val()

- text() - 设置或返回所选元素的文本内容
- html() - 设置或返回所选元素的内容（包括 HTML 标记）
- val() - 设置或返回表单字段的值

```
$("#btn1").click(function(){
    $("#test1").text("Hello world!");
});
$("#btn2").click(function(){
    $("#test2").html("<b>Hello world!</b>");
});
$("#btn3").click(function(){
    $("#test3").val("zdww");
});
```

#### 设置属性 - attr()

```
$("button").click(function(){
  $("#runoob").attr("href","http://www.baidu.com");
});
```

#### jQuery - 添加元素

添加新的HTML内容

我们将学习用于添加新内容的四个 jQuery 方法：

- append() - 在被选元素的结尾插入内容
- prepend() - 在被选元素的开头插入内容
- after() - 在被选元素之后插入内容
- before() - 在被选元素之前插入内容

###### append() 方法

jQuery append() 方法在被选元素的结尾插入内容（仍然在该元素的内部）。

```
$("p").append("追加文本");
```

###### prepend() 方法

jQuery prepend() 方法在被选元素的开头插入内容。

```
$("p").prepend("在开头追加文本");
```

###### after() 和 before() 方法

jQuery after() 方法在被选元素之后插入内容（元素外面）。

jQuery before() 方法在被选元素之前插入内容（元素外面）。

```
$("img").after("在后面添加文本");
 
$("img").before("在前面添加文本");
```

#### 删除元素/内容

如需删除元素和内容，一般可使用以下两个 jQuery 方法：

- remove() - 删除被选元素（及其子元素）
- empty() - 从被选元素中删除子元素

###### remove() 方法

remove() 方法删除被选元素及其子元素。

```
$("#div1").remove();
```

###### empty() 方法

empty() 方法删除被选元素的子元素。

```
$("#div1").empty();
```

###### 过滤被删除的元素

jQuery remove() 方法也可接受一个参数，允许您对被删元素进行过滤。

该参数可以是任何 jQuery 选择器的语法。

下面的例子删除 class="test" 的所有 <p> 元素：

```
$("p").remove(".test");
```

#### 获取并设置 CSS 类

JQuery 拥有若干进行 CSS 操作的方法。我们将学习下面这些：

- addClass() - 向被选元素添加一个或多个类
- removeClass() - 从被选元素删除一个或多个类
- toggleClass() - 对被选元素进行添加/删除类的切换操作
- css() - 设置或返回样式属性

######  addClass() 方法

```
$("button").click(function(){
  $("h1,h2,p").addClass("important blue");
  $("div").addClass("important");
});
```

###### removeClass() 方法

```
$("button").click(function(){
  $("h1,h2,p").removeClass("blue");
});
```

###### toggleClass() 方法

```
$("button").click(function(){
  $("h1,h2,p").toggleClass("blue");
});
```

#### css() 方法

###### 返回 CSS 属性

如需返回指定的 CSS 属性的值，请使用如下语法：

```
css("propertyname");
```

下面的例子将返回首个匹配元素的 background-color 值：

```
$("p").css("background-color");
```

###### 设置 CSS 属性

如需设置指定的 CSS 属性，请使用如下语法：

```
css("propertyname","value");
```

```
$("p").css("background-color","yellow");
```

###### 设置多个 CSS 属性

```
css({"propertyname":"value","propertyname":"value",...});
```

```
$("p").css({"background-color":"yellow","font-size":"200%"});
```

#### jQuery 尺寸

jQuery 提供多个处理尺寸的重要方法：

- width()
- height()
- innerWidth()
- innerHeight()
- outerWidth()
- outerHeight()

![image-20200716103029039](C:\Users\50595\AppData\Roaming\Typora\typora-user-images\image-20200716103029039.png)

###### width() 和 height() 方法

width() 方法设置或返回元素的宽度（不包括内边距、边框或外边距）。

height() 方法设置或返回元素的高度（不包括内边距、边框或外边距）。

```
$("#div1").width() 
$("#div1").height()
```

######  innerWidth() 和 innerHeight() 方法

nnerWidth() 方法返回元素的宽度（包括内边距）。

innerHeight() 方法返回元素的高度（包括内边距）。

######  outerWidth() 和 outerHeight() 方法

outerWidth() 方法返回元素的宽度（包括内边距和边框）。

outerHeight() 方法返回元素的高度（包括内边距和边框）。

## jQuery 遍历

#### 向上遍历 DOM 树

- parent()
- parents()
- parentsUntil()

######  parent() 方法

parent() 方法返回被选元素的直接父元素。

该方法只会向上一级对 DOM 树进行遍历。

```
$(document).ready(function(){
  $("span").parent();
});
```

###### parents() 方法

parents() 方法返回被选元素的所有祖先元素，它一路向上直到文档的根元素 (<html>)。

```
$(document).ready(function(){
  $("span").parents();
});
```

您也可以使用可选参数来过滤对祖先元素的搜索。

下面的例子返回所有 <span> 元素的所有祖先，并且它是 <ul> 元素：

```
$(document).ready(function(){
  $("span").parents("ul");
});
```

###### parentsUntil() 方法

parentsUntil() 方法返回介于两个给定元素之间的所有祖先元素。

下面的例子返回介于 <span> 与 <div> 元素之间的所有祖先元素：

```
$(document).ready(function(){
  $("span").parentsUntil("div");
});
```

##### 向下遍历 DOM 树

- children()
- find()

###### children() 方法

children() 方法返回被选元素的所有直接子元素。

该方法只会向下一级对 DOM 树进行遍历。

```
$(document).ready(function(){
  $("div").children();
});
```

您也可以使用可选参数来过滤对子元素的搜索。

```
$(document).ready(function(){
  $("div").children("p");
});
```

###### find() 方法

find() 方法返回被选元素的后代元素，一路向下直到最后一个后代。

```
$(document).ready(function(){
  $("div").find("span");
});
```

下面的例子返回 <div> 的所有后代：

```
$(document).ready(function(){
  $("div").find("*");
});
```

#### 在 DOM 树中水平遍历

- siblings()
- next()
- nextAll()
- nextUntil()
- prev()
- prevAll()
- prevUntil()

###### siblings() 方法

siblings() 方法返回被选元素的所有同胞元素。

```
$(document).ready(function(){
  $("h2").siblings();
});
```

您也可以使用可选参数来过滤对同胞元素的搜索。

```
$(document).ready(function(){
  $("h2").siblings("p");
});
```

###### next() 方法

next() 方法返回被选元素的下一个同胞元素。

该方法只返回一个元素。

```
$(document).ready(function(){
  $("h2").next();
});
```

######  nextAll() 方法

nextAll() 方法返回被选元素的所有跟随的同胞元素。

```
$(document).ready(function(){
  $("h2").nextAll();
});
```

###### nextUntil() 方法

nextUntil() 方法返回介于两个给定参数之间的所有跟随的同胞元素。

下面的例子返回介于 <h2> 与 <h6> 元素之间的所有同胞元素：

```
$(document).ready(function(){
  $("h2").nextUntil("h6");
});
```

###### prev(), prevAll() & prevUntil() 方法

prev(), prevAll() 以及 prevUntil() 方法的工作方式与上面的方法类似，只不过方向相反而已：它们返回的是前面的同胞元素（在 DOM 树中沿着同胞之前元素遍历，而不是之后元素遍历）。

#### 过滤

三个最基本的过滤方法是：first(), last() 和 eq()，它们允许您基于其在一组元素中的位置来选择一个特定的元素。

其他过滤方法，比如 filter() 和 not() 允许您选取匹配或不匹配某项指定标准的元素。

###### first() 方法

first() 方法返回被选元素的首个元素。

下面的例子选取首个 <div> 元素内部的第一个 <p> 元素：

```
$(document).ready(function(){
  $("div p").first();
});
```

###### last() 方法

last() 方法返回被选元素的最后一个元素。

下面的例子选择最后一个 <div> 元素中的最后一个 <p> 元素：

```
$(document).ready(function(){
  $("div p").last();
});

```

###### eq() 方法

eq() 方法返回被选元素中带有指定索引号的元素。

索引号从 0 开始，因此首个元素的索引号是 0 而不是 1。下面的例子选取第二个 <p> 元素（索引号 1）：

```
$(document).ready(function(){
  $("p").eq(1);
});
```

###### filter() 方法

filter() 方法允许您规定一个标准。不匹配这个标准的元素会被从集合中删除，匹配的元素会被返回。

下面的例子返回带有类名 "url" 的所有 <p> 元素：

```
$(document).ready(function(){
  $("p").filter(".url");
});
```

###### not() 方法

not() 方法返回不匹配标准的所有元素。

提示：not() 方法与 filter() 相反。

```
$(document).ready(function(){
  $("p").not(".url");
});
```

