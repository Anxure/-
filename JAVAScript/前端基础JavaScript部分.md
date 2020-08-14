## JavaScript简介

#### JavaScript是脚本语言

JavaScript 是一种轻量级的编程语言。

JavaScript 是可插入 HTML 页面的编程代码。

JavaScript 插入 HTML 页面后，可由所有的现代浏览器执行。

## JavaScript用法

HTML 中的脚本必须位于 `<script>` 与 `</script>` 标签之间。

脚本可被放置在 HTML 页面的 `<body>` 和 `<head>` 部分中。

## JavaScript输出

JavaScript 没有任何打印或者输出的函数。

#### JavaScript显示数据

JavaScript 可以通过不同的方式来输出数据：

- 使用 **window.alert()** 弹出警告框。
- 使用 **document.write()** 方法将内容写到 HTML 文档中。
- 使用 **innerHTML** 写入到 HTML 元素。
- 使用 **console.log()** 写入到浏览器的控制台。

## JavaScript变量

#### 声明（创建） JavaScript 变量

我们使用 var 关键词来声明变量：

```
var carname;
```

变量声明之后，该变量是空的（它没有值）。

如需向变量赋值，请使用等号：

```
carname="Volvo";
```

不过，您也可以在声明变量时对其赋值：

```
var carname="Volvo";
```

您可以在一条语句中声明很多变量。该语句以 var 开头，并使用逗号分隔变量即可：

```
var lastname="Doe", age=30, job="carpenter";
```

#### 重新声明 JavaScript 变量

果重新声明 JavaScript 变量，该变量的值不会丢失：

在以下两条语句执行后，变量 carname 的值依然是 "Volvo"：

```
var carname="Volvo"; 
var carname;
```

## JavaScript数据类型

**值类型(基本类型)**：字符串（String）、数字(Number)、布尔(Boolean)、对空（Null）、未定义（Undefined）、Symbol。

**引用数据类型**：对象(Object)、数组(Array)、函数(Function)。

**注：**Symbol *是 ES6 引入了一种新的原始数据类型，表示独一无二的值。*

#### JavaScript 拥有动态类型

JavaScript 拥有动态类型。这意味着相同的变量可用作不同的类型：

```
var x;               // x 为 undefined
var x = 5;           // 现在 x 为数字
var x = "John";      // 现在 x 为字符串
```

#### 声明变量类型

当您声明新变量时，可以使用关键词 "new" 来声明其类型：

```
var carname=new String;
var x=      new Number;
var y=      new Boolean;
var cars=   new Array;
var person= new Object;
```

## JavaScript 对象

#### 对象定义

你可以使用字符来定义和创建 JavaScript 对象:

```
var person = {firstName:"李", lastName:"华", age:50, eyeColor:"blue"};
```

#### 访问对象的属性

```
person.lastName;
person["lastName"];
```

## JavaScript 函数

函数是由事件驱动的或者当它被调用时执行的可重复使用的代码块。

```
function functionName () {
	console.log('这是我的第一个函数')
}
```

注： JavaScript 对大小写敏感。关键词 function 必须是小写的，并且必须以与函数名称相同的大小写来调用函数。

#### 带参数的函数

在调用函数时，您可以向其传递值，这些值被称为参数。

```
function messageTip (name) {
	console.log("welcome" + name + "回来")
}
```

#### 带有返回值的函数

通过使用 return 语句就可以实现。

在使用 return 语句时，函数会停止执行，并返回指定的值。

```
function returnFunction () {
	var x = 5 ;
	retun x
}
```

#### 局部 JavaScript 变量

在 JavaScript 函数内部声明的变量（使用 var）是*局部*变量，所以只能在函数内部访问它。（该变量的作用域是局部的）。

您可以在不同的函数中使用名称相同的局部变量，因为只有声明过该变量的函数才能识别出该变量。

只要函数运行完毕，本地变量就会被删除。

#### 全局 JavaScript 变量

在函数外声明的变量是*全局*变量，网页上的所有脚本和函数都能访问它。

#### JavaScript 变量的生存期

JavaScript 变量的生命期从它们被声明的时间开始。

局部变量会在函数运行以后被删除。

全局变量会在页面关闭后被删除。

#### 向未声明的 JavaScript 变量分配值

如果您把值赋给尚未声明的变量，该变量将被自动作为 window 的一个属性。

## JavaScript 作用域

作用域是可访问变量的集合。

#### JavaScript 局部作用域

变量在函数内声明，变量为局部作用域。

局部变量：只能在函数内部访问。

```
// 此处不能调用 carName 变量
function myFunction() {
    var carName = "Volvo";
    // 函数内可调用 carName 变量
}
```

#### JavaScript 全局变量

变量在函数外定义，即为全局变量。

全局变量有 **全局作用域**: 网页中所有脚本和函数均可使用。 

```
var carName = " Volvo";
 
// 此处可调用 carName 变量
function myFunction() {
    // 函数内可调用 carName 变量
}
```

如果变量在函数内没有声明（没有使用 var 关键字），该变量为全局变量。

以下实例中 carName 在函数内，但是为全局变量。

```
// 此处可调用 carName 变量
 
function myFunction() {
    carName = "Volvo";
    // 此处可调用 carName 变量
}
```

##  JavaScript 事件

| 属性                                                         | 描述                                   | DOM  |
| :----------------------------------------------------------- | :------------------------------------- | :--- |
| [onclick](https://www.runoob.com/jsref/event-onclick.html)   | 当用户点击某个对象时调用的事件句柄。   | 2    |
| [oncontextmenu](https://www.runoob.com/jsref/event-oncontextmenu.html) | 在用户点击鼠标右键打开上下文菜单时触发 |      |
| [ondblclick](https://www.runoob.com/jsref/event-ondblclick.html) | 当用户双击某个对象时调用的事件句柄。   | 2    |
| [onmousedown](https://www.runoob.com/jsref/event-onmousedown.html) | 鼠标按钮被按下。                       | 2    |
| [onmouseenter](https://www.runoob.com/jsref/event-onmouseenter.html) | 当鼠标指针移动到元素上时触发。         | 2    |
| [onmouseleave](https://www.runoob.com/jsref/event-onmouseleave.html) | 当鼠标指针移出元素时触发               | 2    |
| [onmousemove](https://www.runoob.com/jsref/event-onmousemove.html) | 鼠标被移动。                           | 2    |
| [onmouseover](https://www.runoob.com/jsref/event-onmouseover.html) | 鼠标移到某元素之上。                   | 2    |
| [onmouseout](https://www.runoob.com/jsref/event-onmouseout.html) | 鼠标从某元素移开。                     | 2    |
| [onmouseup](https://www.runoob.com/jsref/event-onmouseup.html) | 鼠标按键被松开。                       | 2    |

```
<button onclick="getElementById('demo').innerHTML= Date()">现在的时间是?</button>
<p id="demo"></p>
```

## JavaScript 算术运算符

| 运算符 | 描述         | 例子  | x 运算结果                                                   | y 运算结果 |
| :----- | :----------- | :---- | :----------------------------------------------------------- | :--------- |
| +      | 加法         | x=y+2 | 7                                                            | 5          |
| -      | 减法         | x=y-2 | 3                                                            | 5          |
| *      | 乘法         | x=y*2 | 10                                                           | 5          |
| /      | 除法         | x=y/2 | 2.5                                                          | 5          |
| %      | 取模（余数） | x=y%2 | 1                                                            | 5          |
| ++     | 自增         | x=++y | 6                                                            | 6          |
| x=y++  | 5            | 6     | [实例 »](https://www.runoob.com/try/try.php?filename=tryjs_oper_incr2) |            |
| --     | 自减         | x=--y | 4                                                            | 4          |
| x=y--  | 5            | 4     | [实例 »](https://www.runoob.com/try/try.php?filename=tryjs_oper_decr2) |            |

## JavaScript 比较 和 逻辑运算符

#### 比较运算符

x=5，下面的表格解释了比较运算符：

| 运算符 | 描述                                               | 比较                                                         | 返回值  |
| :----- | :------------------------------------------------- | :----------------------------------------------------------- | :------ |
| ==     | 等于                                               | x==8                                                         | *false* |
| x==5   | *true*                                             | [实例 »](https://www.runoob.com/try/try.php?filename=tryjs_comparison2) |         |
| ===    | 绝对等于（值和类型均相等）                         | x==="5"                                                      | *false* |
| x===5  | *true*                                             | [实例 »](https://www.runoob.com/try/try.php?filename=tryjs_comparison4) |         |
| !=     | 不等于                                             | x!=8                                                         | *true*  |
| !==    | 不绝对等于（值和类型有一个不相等，或两个都不相等） | x!=="5"                                                      | *true*  |
| x!==5  | *false*                                            | [实例 »](https://www.runoob.com/try/try.php?filename=tryjs_comparison7) |         |
| >      | 大于                                               | x>8                                                          | *false* |
| <      | 小于                                               | x<8                                                          | *true*  |
| >=     | 大于或等于                                         | x>=8                                                         | *false* |
| <=     | 小于或等于                                         | x<=8                                                         | *true*  |

#### 逻辑运算符

逻辑运算符用于测定变量或值之间的逻辑。

给定 x=6 以及 y=3，下表解释了逻辑运算符：

| 运算符 | 描述 | 例子                      |
| :----- | :--- | :------------------------ |
| &&     | and  | (x < 10 && y > 1) 为 true |
| \|\|   | or   | (x==5 \|\| y==5) 为 false |
| !      | not  | !(x==y) 为 true           |

#### 条件运算符

```
variablename=(condition)?value1:value2 
```

```
color = type === 'success' ? 'green' : 'red'
```

## JavaScript if...Else 语句

- **if 语句** - 只有当指定条件为 true 时，使用该语句来执行代码
- **if...else 语句** - 当条件为 true 时执行代码，当条件为 false 时执行其他代码
- **if...else if....else 语句**- 使用该语句来选择多个代码块之一来执行

## JavaScript switch 语句

```
switch(n)
{
    case 1:
        执行代码块 1
        break;
    case 2:
        执行代码块 2
        break;
    default:
        与 case 1 和 case 2 不同时执行的代码
}
```

```
var d=new Date().getDay(); 
switch (d) 
{ 
  case 0:x="今天是星期日"; 
  break; 
  case 1:x="今天是星期一"; 
  break; 
  case 2:x="今天是星期二"; 
  break; 
  case 3:x="今天是星期三"; 
  break; 
  case 4:x="今天是星期四"; 
  break; 
  case 5:x="今天是星期五"; 
  break; 
  case 6:x="今天是星期六"; 
  break; 
}
```

## JavaScript 循环

JavaScript 支持不同类型的循环：

- **for** - 循环代码块一定的次数
- **for/in** - 循环遍历对象的属性
- **while** - 当指定的条件为 true 时循环指定的代码块
- **do/while** - 同样当指定的条件为 true 时循环指定的代码块

#### For循环

for 循环是您在希望创建循环时常会用到的工具。

下面是 for 循环的语法：

```
for (语句 1; 语句 2; 语句 3)
{
    被执行的代码块
}
```

**语句 1** （代码块）开始前执行

**语句 2** 定义运行循环（代码块）的条件

**语句 3** 在循环（代码块）已被执行之后执行

实例：

```
<p>点击按钮循环代码5次。</p>
<button onclick="myFunction()">点击这里</button>
<p id="demo"></p>
<script>
function myFunction(){
	var x="";
	for (var i=0;i<5;i++){
		x=x + "该数字为 " + i + "<br>";
	}
	document.getElementById("demo").innerHTML=x;
}
</script>

```

#### For/In 循环

JavaScript for/in 语句循环遍历对象的属性：

```
<p>点击下面的按钮，循环遍历对象 "person" 的属性。</p>
<button onclick="myFunction()">点击这里</button>
<p id="demo"></p>
<script>
function myFunction(){
	var x;
	var txt="";
	var person={fname:"Bill",lname:"Gates",age:56}; 
	for (x in person){
		txt=txt + person[x];
	}
	document.getElementById("demo").innerHTML=txt;
}
</script>
```

#### While循环

while 循环会在指定条件为真时循环执行代码块。

while (*条件*)
{
  *需要执行的代码*
}

```
while (i<5)
{
    x=x + "The number is " + i + "<br>";
    i++;
}
```

```
<p>点击下面的按钮，只要 i 小于 5 就一直循环代码块。</p>
<button onclick="myFunction()">点击这里</button>
<p id="demo"></p>
<script>
function myFunction(){
	var x="",i=0;
	while (i<5){
		x=x + "该数字为 " + i + "<br>";
		i++;
	}
	document.getElementById("demo").innerHTML=x;
}
</script>

```

## JavaScript break 和 continue 语句

break 语句用于跳出循环。

continue 用于跳过循环中的一个迭代。

## JavaScript HTML DOM

通过 HTML DOM，可访问 JavaScript HTML 文档的所有元素。

通过可编程的对象模型，JavaScript 获得了足够的能力来创建动态的 HTML。

- JavaScript 能够改变页面中的所有 HTML 元素
- JavaScript 能够改变页面中的所有 HTML 属性
- JavaScript 能够改变页面中的所有 CSS 样式
- JavaScript 能够对页面中的所有事件做出反应

#### 查找 HTML 元素

通常，通过 JavaScript，您需要操作 HTML 元素。

为了做到这件事情，您必须首先找到该元素。有三种方法来做这件事：

- 通过 id 找到 HTML 元素
- 通过标签名找到 HTML 元素
- 通过类名找到 HTML 元素

###### 通过 id 查找 HTML 元素

```
var x=document.getElementById("intro");
```

###### 通过标签名查找 HTML 元素

本例查找 id="main" 的元素，然后查找 id="main" 元素中的所有 <p> 元素：

```
var x=document.getElementById("main");
var y=x.getElementsByTagName("p");
```

###### 通过类名找到 HTML 元素

```
var x=document.getElementsByClassName("intro");
```

#### 改变HTML

###### 改变 HTML 内容

修改 HTML 内容的最简单的方法是使用 innerHTML 属性。

如需改变 HTML 元素的内容，请使用这个语法：

```
document.getElementById(id).innerHTML=新的 HTML
```

```
<h1 id="header">Old Header</h1>

<script>
var element=document.getElementById("header");
element.innerHTML="新标题";
</script>

```

###### 改变 HTML 属性

如需改变 HTML 元素的属性，请使用这个语法：

```
document.getElementById(id).attribute=新属性值
```

#### 改变CSS

```
document.getElementById(id).style.property=新样式
```

```
<h1 id="id1">我的标题 1</h1>
<button type="button" 
onclick="document.getElementById('id1').style.color='red'">
点我!</button>
```

#### DOM元素（节点）

###### 创建新的 HTML 元素 (节点) - appendChild()

以下代码是用于创建 <p> 元素:

```
var para = document.createElement("p");
```

为 <p> 元素创建一个新的文本节点：

```
var node = document.createTextNode("这是一个新的段落。");
```

将文本节点添加到 <p> 元素中：

```
para.appendChild(node);
```

最后，在一个已存在的元素中添加 p 元素。

查找已存在的元素：

```
var element = document.getElementById("div1");
```

添加到已存在的元素中:

```
element.appendChild(para);
```

###### 创建新的 HTML 元素 (节点) - insertBefore()

以上的实例我们使用了 **appendChild()** 方法，它用于添加新元素到尾部。

如果我们需要将新元素添加到开始位置，可以使用 **insertBefore()** 方法:

###### 移除已存在的元素 - removeChild

```
<div id="div1">
<p id="p1">这是一个段落。</p>
<p id="p2">这是另外一个段落。</p>
</div>
 
<script>
var parent = document.getElementById("div1");
var child = document.getElementById("p1");
parent.removeChild(child);
</script>
```

###### 替换 HTML 元素 - replaceChild()

```
<div id="div1">
<p id="p1">这是一个段落。</p>
<p id="p2">这是另外一个段落。</p>
</div>
 
<script>
var para = document.createElement("p");
var node = document.createTextNode("这是一个新的段落。");
para.appendChild(node);
 
var parent = document.getElementById("div1");
var child = document.getElementById("p1");
parent.replaceChild(para, child);
</script>
```

