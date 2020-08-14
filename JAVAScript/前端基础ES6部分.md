## ECMAScript6

ECMAScript 6.0（以下简称 ES6）是 JavaScript 语言的下一代标准，已经在 2015 年 6 月正式发布了。它的目标，是使得 JavaScript 语言可以用来编写复杂的大型应用程序，成为企业级开发语言。

## let 和 const 命令

#### let命令

ES6 新增了`let`命令，用来声明变量。它的用法类似于`var`，但是所声明的变量，只在`let`命令所在的代码块内有效。

```
{
  let a = 10;
  var b = 1;
}

a // ReferenceError: a is not defined.
b // 1
```

```
for(var i = 0; i< 10 ; i++) {
    setTimeout(() => {
    	console.log(i)
    },1000);
}
```

#### let不存在变量提升

```
/ var 的情况
console.log(foo); // 输出undefined
var foo = 2;

// let 的情况
console.log(bar); // 报错ReferenceError
let bar = 2;
```

#### 暂时性死区

在代码块内，使用`let`命令声明变量之前，该变量都是不可用的。这在语法上，称为“暂时性死区”（temporal dead zone，简称 TDZ）。

```
var tmp = 123;

if (true) {
  tmp = 'abc'; // ReferenceError
  let tmp;
}
```

上面代码中，存在全局变量`tmp`，但是块级作用域内`let`又声明了一个局部变量`tmp`，导致后者绑定这个块级作用域，所以在`let`声明变量前，对`tmp`赋值会报错。

#### 不允许重复声明

#### 块级作用域

```javascript
var tmp = new Date();

function f() {
  console.log(tmp);
  if (false) {
    var tmp = 'hello world';
  }
}

f(); // undefined
```

```
function f1() {
  let n = 5;
  if (true) {
    let n = 10;
  }
  console.log(n); // 5
}
```

#### 小结：

- let关键字就是用来声明变量的
- 使用let关键字声明的变量具有块级作用域
- 在一个大括号中 使用let关键字声明的变量才具有块级作用域 var关键字是不具备这个特点的
- 防止循环变量变成全局变量
- 使用let关键字声明的变量没有变量提升
- 使用let关键字声明的变量具有暂时性死区特性

#### const

声明常量，常量就是值（内存地址）不能变化的量

###### 具有块级作用域

```
 if (true) { 
     const a = 10;
 }
console.log(a) // a is not defined
```

###### 声明常量时必须赋值

```
const PI; // Missing initializer in const declaration
```

###### 常量赋值后，值不能修改

```
const PI = 3.14;
PI = 100; // Assignment to constant variable.

const ary = [100, 200];
ary[0] = 'a';
ary[1] = 'b';
console.log(ary); // ['a', 'b']; 
ary = ['a', 'b']; // Assignment to constant variable.
```

小结：

- const声明的变量是一个常量
- 既然是常量不能重新进行赋值，如果是基本数据类型，不能更改值，如果是复杂数据类型，不能更改地址值
- 声明 const时候必须要给定值

#### let、const、var 的区别

- 使用 var 声明的变量，其作用域为该语句所在的函数内，且存在变量提升现象
- 使用 let 声明的变量，其作用域为该语句所在的代码块内，不存在变量提升
- 使用 const 声明的是常量，在后面出现的代码中不能再修改该常量的值

![image-20200716145751579](C:\Users\50595\AppData\Roaming\Typora\typora-user-images\image-20200716145751579.png)

## 解构赋值

ES6中允许从数组中提取值，按照对应位置，对变量赋值，对象也可以实现解构

#### 数组解构

```
let [a, b, c] = [1, 2, 3];
 console.log(a)//1
 console.log(b)//2
 console.log(c)//3
//如果解构不成功，变量的值为undefined
```

#### 对象的解构

```
let person = { name: 'zhangsan', age: 20 }; 
 let { name, age } = person;
 console.log(name); // 'zhangsan' 
 console.log(age); // 20

 let {name: myName, age: myAge} = person; // myName myAge 属于别名
 console.log(myName); // 'zhangsan' 
 console.log(myAge); // 20

```

#### 小结

- 解构赋值就是把数据结构分解，然后给变量进行赋值
- 如果结构不成功，变量跟数值个数不匹配的时候，变量的值为undefined
- 数组解构用中括号包裹，多个变量用逗号隔开，对象解构用花括号包裹，多个变量用逗号隔开
- 利用解构赋值能够让我们方便的去取对象中的属性跟方法

## 字符串扩展

#### 查找

- `includes(String)`：是否找到参数字符串。
- `startsWith(String)`：是否以参数字符串开头。
- `endsWith(String)`：是否以参数字符串结尾。

```
let s = 'Hello world!';
s.includes('o') // true
//均可接受第二个位置参数
```

#### 重复

- `repeat(Number)`

```
'x'.repeat(3) // "xxx"
```

#### 模板字符串

- 支持变量、表达式、函数调用，允许嵌套
- 反引号需使用反斜杠转义
- trim消除空格和换行

```
$('#result').append(`
  There are <b>${basket.count}</b> items
   in your basket, <em>${basket.onSale}</em>
  are on sale!
`);
//trim
$('#list').html(`
<ul>
  <li>first</li>
  <li>second</li>
</ul>
`.trim());
```

## 数值的扩展

- `Number.isFinite()`-只对数值返回true
- `Number.isNaN()`-只对NaN返回true
- `Number.isInteger()`-只对整数返回true
- `Number.isSafeInteger()`-只对安全整数（-253到253，不含端点）返回true
- `Number.MAX_SAFE_INTEGER`,`Number.MIN_SAFE_INTEGER`安全整数的上下限常量

```
Number.isInteger(25) // true
Number.isInteger(25.0) // true
Number.isInteger(25.1) // false
```

Math对象扩展：http://es6.ruanyifeng.com/#docs/number#Math-对象的扩展

## 函数的扩展

- 参数默认值，建议用于尾参数，不可在函数内再次声明

  ```
  function log(x, y = 'World') {}
  ```

  

- length：从第一个参数到首个指定默认值参数间参数的个数
```js
(function (a, b = 1, c) {}).length // 1
```
- rest：获取函数的多余参数，须用于尾参数
```js
function add(...values) {}
add(2, 5, 3)
```
- name：函数的名字
```js
function f() {}
//或者
var f = function () {};
f.name // "f"
```
### 箭头函数
- 只有一个参数，可省略参数的小括号，无参数时不可省略
- 如果只有一条语句且无return，可以省略语句块的大括号
- 如果只有一条语句且有return，可以省略大括号和return，仅有return（即return后无参数）时不可省略
- 直接返回对象，须使用小括号包裹
```js
let getTempItem = id => ({ id: id, name: "Temp" });
```
- 可以使用解构赋值，可以嵌套
```
const full = ({ first, last }) => first + ' ' + last;
const pipeline = (...funcs) =>
  val => funcs.reduce((a, b) => b(a), val);
```
注意：
- 函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。
- 不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。
- 不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。
- 不可以使用yield命令，因此箭头函数不能用作 Generator 函数。

## 数组的扩展

#### 扩展运算符
用于数组赋值须放在参数的最后一位。
```js
console.log(1, ...[2, 3, 4], 5) // 1 2 3 4 5
//复制数组
const a1 = [1, 2];
const a2 = [...a1];// 写法一
const [...a2] = a1;// 写法二
//合并数组
const a2 = [3, 4];
[...a1, ...a2] //[1,2,3,4]
//配合解构赋值
const [first, ...rest] = [1, 2, 3, 4, 5];// first= 1;rest= [2, 3, 4, 5]
//字符串
[...'hello'] // [ "h", "e", "l", "l", "o" ]
```
#### 新增方法
- `Array.from()`：将数组对象（有length属性）或可遍历的对象（包括 ES6 新增的数据结构 Set 和 Map）转为真正的数组，接受第二个参数（对每个元素进行处理，处理值返回数组）。
```js
let arrayLike = {
    '0': 'a',
    '1': 'b',
    '2': 'c',
    length: 3
};
let arr2 = Array.from(arrayLike); // ['a', 'b', 'c']
```
- `Array.of()`：将一组值转换为数组。
```js
Array.of(3, 11, 8) // [3,11,8]
```
- `copyWithin（target[必需，替换开始位置，负值为倒数], start = 0[可选，读取开始位置，负值为倒数], end = this.length[可选，读取结束位置，负值为倒数]）`：在当前数组内部，将指定位置的成员复制到其他位置（会覆盖原有成员），然后返回当前数组。
```js
[1, 2, 3, 4, 5].copyWithin(0, 3) // [4, 5, 3, 4, 5]
```
- `find(fn)` 和 `findIndex(fn)`：找出第一个符合条件的数组成员。如果无符合条件的成员，返回undefined。
```js
//find方法的回调函数可以接受三个参数，依次为当前的值、当前的位置和原数组
[1, 5, 10, 15].find(function(value, index, arr) {
  return value > 9;
}) // 10 15
```
- `fill(text[必需，填充内容],start = 0[可选，开始位置，负值为倒数], end = this.length[可选，结束位置，负值为倒数])`: 使用给定值，填充一个数组。
```
['a', 'b', 'c'].fill(7, 1, 2) // ['a', 7, 'c']
```
- `includes(text[必需，内容],start = 0[可选，搜索开始位置，负值为倒数], end = this.length[可选，搜索结束位置，负值为倒数])`：搜索数组是否包含给定的值。
```
[1, 2, 3].includes(3, -1); // true
```

## 对象的扩展

- 简洁表示：对象的key和value一样时，可以省略key，方法可省略function

```js
const foo = 'bar';
const baz = {
	foo,
   method() {
    return "Hello!";
  }
}
```
- 属性名表达式: 不能使用简洁表示
```js
let propKey = 'foo';

let obj = {
  [propKey]: true,
  ['a' + 'bc']: 123
}
```
- `Object.is()`: 判断两值是否相等
```js
//和===的区别
+0 === -0 //true
NaN === NaN // false
Object.is(+0, -0) // false
Object.is(NaN, NaN) // true
```
- `Object.assign(target[目标对象], source1, source2，...)`: 将源对象所有可枚举属性复制合并到目标对象。
```js
const target = { a: 1, b: 1 };
const source1 = { b: 2, c: 2 };
const source2 = { c: 3 };
Object.assign(target, source1, source2);
target // {a:1, b:2, c:3}
```
  - 浅拷贝:Object.assign方法实行的是浅拷贝，而不是深拷贝。也就是说，如果源对象某个属性的值是对象，那么目标对象拷贝得到的是这个对象的引用。
  - 遇到同名属性，Object.assign的处理方法是后面替换前面的。
  - Object.assign可以用来处理数组，但是会把数组视为对象。
  - Object.assign只能进行值的复制，如果要复制的值是一个取值函数，那么将求值后再复制。

## Set数据结构

ES6 提供了新的数据结构  Set。它类似于数组，但是成员的值都是唯一的，没有重复的值。

Set本身是一个构造函数，用来生成  Set  数据结构

```javascript
const s = new Set();
```

Set函数可以接受一个数组作为参数，用来初始化。

```javascript
const set = new Set([1, 2, 3, 4, 4]);//{1, 2, 3, 4}

```

#### 实例方法

- add(value)：添加某个值，返回 Set 结构本身
- delete(value)：删除某个值，返回一个布尔值，表示删除是否成功
- has(value)：返回一个布尔值，表示该值是否为 Set 的成员
- clear()：清除所有成员，没有返回值

```javascript
 const s = new Set();
 s.add(1).add(2).add(3); // 向 set 结构中添加值 
 s.delete(2)             // 删除 set 结构中的2值   
 s.has(1)                // 表示 set 结构中是否有1这个值 返回布尔值 
 s.clear()               // 清除 set 结构中的所有值
 //注意：删除的是元素的值，不是代表的索引
```

#### 遍历

Set 结构的实例与数组一样，也拥有forEach方法，用于对每个成员执行某种操作，没有返回值。

```javascript
s.forEach(value => console.log(value))

```

## Promise对象

Promise 是异步编程的一种解决方案，比传统的解决方案（回调函数和事件），更合理和更强大。

- 特点：
  - 对象的状态[pending（进行中）、fulfilled（已成功）和rejected（已失败）]不受外界影响
  - 一旦状态改变，就不会再变，任何时候得到的都是这个结果
- 缺点:
  - 无法取消Promise，一旦新建它就会立即执行，无法中途取消。
  - 如果不设置回调函数，Promise内部抛出的错误，不会反应到外部。
  - 当处于Pending状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）。

```
const promise = new Promise(function(resolve, reject) {
  // ... some code
  if (/* 异步操作成功 */){
    resolve(value); //将Promise对象的状态从“未完成”变为“成功”,并将异步操作的结果，作为参数传递出去
  } else {
    reject(error); //将Promise对象的状态从“未完成”变为“失败”,并将异步操作报出的错误，作为参数传递出去
  }
});
//调用
promise.then(value=> {
  // success
}, error=> { //可选
  // failure
});
//或者
promise.then(value => {
  // success
}).catch(error => {
  // failure
});
```

- `Promise.all([p1, p2, ...])`: 将多个 Promise 包装成一个新的 Promise ，状态和值取决于里面的实例（fulfilled：需均成功，返回包含每个实例返回值的数组；rejected：至少一个失败，返回第一个失败的实例返回值）
- `Promise.race([p1, p2, ...])`: 将多个 Promise 包装成一个新的 Promise，状态和参数均由里面第一个改变的状态的实例决定
- `Promise.resolve()`：简写，将现有对象转为 状态为fulfilled的Promise 对象。

```
Promise.resolve('foo')
// 等价于
new Promise(resolve => resolve('foo'))
```

- `Promise.reject()`：简写，将现有对象转为 状态为rejected的Promise 对象。

```
const p = Promise.reject('出错了');
// 等同于
const p = new Promise((resolve, reject) => reject('出错了'))
```

##  Iterator（遍历器）

数据集合：主要是Array，Object，Map，Set。 遍历器（Iterator）为上述数据集合提供了**统一**的访问机制。

Iterator 的作用有三个：

- 一是为各种数据结构，提供一个统一的、简便的访问接口；
- 二是使得数据结构的成员能够按某种次序排列；
- 三是 ES6 创造了一种新的遍历命令for...of循环，Iterator 接口主要供for...of消费。

#### for...of 循环

```
const arr = ['red', 'green', 'blue'];

for(let v of arr) {
  console.log(v); // red green blue
}
```

区别：

- for...in遍历键名，for...of遍历键值

```
var arr = ['a', 'b', 'c', 'd'];

for (let a in arr) {
  console.log(a); // 0 1 2 3
}

for (let a of arr) {
  console.log(a); // a b c d
}
```

- for...of可以配合break、continue和return使用

```
for (var n of fibonacci) {
  if (n > 1000)
    break;
  console.log(n);
}
```

## Class 

#### 定义类

```
//以前
function Point(x, y) {
  this.x = x;
  this.y = y;
}

Point.prototype.toString = function () {
  return '(' + this.x + ', ' + this.y + ')';
};

var p = new Point(1, 2);

使用的时候，也是直接对类使用new命令，跟构造函数的用法完全一致。
```

ES6 的class可以看作只是一个语法糖，它的绝大部分功能，ES5 都可以做到，新的class写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。

```
//es6
class Point {
//构造方法
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }
}
var p = new Point(1, 2);
```

#### 继承类

```
class Point {
}

class ColorPoint extends Point {
}
```

## Module

#### 简介

在 ES6 之前，社区制定了一些模块加载方案，最主要的有 CommonJS 和 AMD 两种。前者用于服务器，后者用于浏览器。ES6 在语言标准的层面上，实现了模块功能，而且实现得相当简单，完全可以取代 CommonJS 和 AMD 规范，成为浏览器和服务器通用的模块解决方案。

#### 严格模式

ES6 的模块自动采用严格模式，不管你有没有在模块头部加上`"use strict";`。

严格模式主要有以下限制：

- 变量必须声明后再使用
- 函数的参数不能有同名属性，否则报错
- 不能使用with语句
- 不能对只读属性赋值，否则报错
- 不能使用前缀 0 表示八进制数，否则报错
- 不能删除不可删除的属性，否则报错
- 不能删除变量delete prop，会报错，只能删除属性delete global[prop]
- eval不会在它的外层作用域引入变量
- eval和arguments不能被重新赋值
- arguments不会自动反映函数参数的变化
- 不能使用arguments.callee
- 不能使用arguments.caller
- 禁止this指向全局对象
- 不能使用fn.caller和fn.arguments获取函数调用的堆栈
- 增加了保留字（比如protected、static和interface）

#### export 命令

定义模块的对外接口。 一个模块就是一个独立的文件。该文件内部的所有变量，外部无法获取。如果你希望外部能够读取模块内部的某个变量，就必须使用export关键字输出该变量。 以下是几种用法：

```
//------输出变量------
export var firstName = 'Michael';
export var lastName = 'Jackson';
//等价于
var firstName = 'Michael';
export {firstName}; //推荐，能清除知道输出了哪些变量
//------输出函数或类------
export function multiply(x, y) {
  return x * y;
};
//------输出并as重命名------
var v1 = 'Michael';
function v2() { ... }
export {
  v1 as streamV1,
  v2 as streamV2
};
//------输出default------
export default function () { ... }
```

注意：`export default`在一个模块中只能有一个。

#### import 命令

使用export命令定义了模块的对外接口以后，其他 JS 文件就可以通过import命令加载这个模块。 以下是几种用法，必须和上面的export对应：

```
//------加载变量、函数或类------
import {firstName, lastName} from './profile.js';
//------加载并as重命名------
import { lastName as surname } from './profile.js';
//------加载有default输出的模块------
import v1 from './profile.js';
//------执行所加载的模块------
import 'lodash';
//------加载模块所有输出------
import  * as surname from './profile.js';
```

#### 复合写法

如果在一个模块之中，先输入后输出同一个模块，import语句可以与export语句写在一起。

```
export { foo, bar } from 'my_module';

// 等同于
import { foo, bar } from 'my_module';
export { foo, bar };
```

## Proxy

代理器（拦截器），Proxy 可以理解成，在目标对象之前架设一层“拦截”，外界对该对象的访问，都必须先通过这层拦截，因此提供了一种机制，可以对外界的访问进行过滤和改写。

```
var proxy = new Proxy(target, handler);
```

- target参数表示所要拦截的目标对象
- handler参数也是一个对象，用来定制拦截行为。

```
var obj = new Proxy({}, {
  get: function (target, key, receiver) {
    console.log(`getting ${key}!`);
    return target.key;
  },
  set: function (target, key, value, receiver) {
    console.log(`setting ${key}!`);
    return target.key=value;
  }
});
```

## Symbol

原始数据类型Symbol，表示独一无二的值。

```
let s = Symbol();

typeof s
// "symbol"
```

Symbol函数可以接受一个字符串作为参数，表示对 Symbol 实例的描述，主要是为了在控制台显示，或者转为字符串时，比较容易区分。

```
let s1 = Symbol('foo');
let s2 = Symbol('bar');

s1 // Symbol(foo)
s2 // Symbol(bar)

s1.toString() // "Symbol(foo)"
s2.toString() // "Symbol(bar)"
```

