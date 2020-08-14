# TypeScript --- 基础篇

### 什么是TypeScript

[TypeScript](http://www.typescriptlang.org/) 是 JavaScript 的一个超集，主要提供了**类型系统**和**对 ES6 的支持**

### 安装TypeScript

TypeScript 的命令行工具安装方法如下：

```
npm install -g typescript
```

以上命令会在全局环境下安装 `tsc` 命令，安装完成之后，我们就可以在任何地方执行 `tsc` 命令了。

编译一个 TypeScript 文件很简单：

```
tsc hello.ts
```

我们约定使用 TypeScript 编写的文件以 `.ts` 为后缀，用 TypeScript 编写 React 时，以 `.tsx` 为后缀。

### 原始数据类型

原始数据类型包括：布尔值、数值、字符串、`null`、`undefined` 以及 [ES6 中的新类型 `Symbol`](http://es6.ruanyifeng.com/#docs/symbol)。

#### 布尔值

布尔值是最基础的数据类型，在 TypeScript 中，使用 `boolean` 定义布尔值类型：

```
let isDone: boolean = false
```

注意，使用构造函数 `Boolean` 创造的对象**不是**布尔值,返回的是一个Boolean对象

```
let createdByNewBoolean: boolean = new Boolean(1);
// Type 'Boolean' is not assignable to type 'boolean'.
// 'boolean' is a primitive, but 'Boolean' is a wrapper object. Prefer using 'boolean' when possible.
```

#### 数值 

使用number定义数值类型：

```
let count: number = 6
/ ES6 中的二进制表示法
let binaryLiteral: number = 0b1010;
// ES6 中的八进制表示法
let octalLiteral: number = 0o744;
```

#### 字符串

使用string定义字符串类型：

```
let myName: string = 'Tom';
let myAge: number = 25;

// 模板字符串
let sentence: string = `Hello, my name is ${myName}.
I'll be ${myAge + 1} years old next month.`;
```

#### 空值

JavaScript 没有空值（Void）的概念，在 TypeScript 中，可以用 `void` 表示没有任何返回值的函数：

```
function alertName: void {
	alert('My name is Tom')
}
```

声明一个 `void` 类型的变量没有什么用，因为你只能将它赋值为 `undefined` 和 `null`：

```
let unusable: void = undefined;
```

#### Null 和 Undefined

在 TypeScript 中，可以使用 `null` 和 `undefined` 来定义这两个原始数据类型：

```
let u: undefined = undefined;
let n: null = null;
```

与 `void` 的区别是，`undefined` 和 `null` 是所有类型的子类型。也就是说 `undefined` 类型的变量，可以赋值给 `number` 类型的变量：

```
// 这样不会报错
let num: number = undefined;
```

### 任意值

任意值(Any)用来表示允许赋值任意类型

#### 什么是任意类型

如果是一个普通类型，在赋值过程中改变类型是不被允许的：

```
let myFavoriteNumber: string = 'seven';
myFavoriteNumber = 7;
// error Type 'number' is not assignable to type 'string'.
```

但如果是any类型，则允许被赋值位任意类型

```
let myFavoriteNumber: any = 'seven';
myFavoriteNumber = 7 
// it’s ok
```

#### 任意值的属性和方法

在任意值上访问的任何属性都是被允许的：

```
let anyThing: any = 'hello';
console.log(anyThing.myName);
console.log(anyThing.myName.firstName);
```

也允许调用任何方法：

```
let anyThing: any = 'Tom';
anyThing.setName('Jerry');
anyThing.setName('Jerry').sayHello();
anyThing.myName.setFirstName('Cat');
```

可以认为，**声明以一个变量为任意值之后，对它的任何操作，返回的内容的类型都是任意值**

#### 未声命类型的变量

**变量如果在声明的时候，未指定其类型，那么它会被识别为任意值类型**：

```
let something;
something = 'seven';
something = 7;

something.setName('Tom');
```

等价于：

```
let something: any;
something = 'seven';
something = 7;

something.setName('Tom');
```

### 类型推断

如果没有明确的指定类型，那么 TypeScript 会依照类型推论（Type Inference）的规则推断出一个类型。

#### 什么是类型推断

以下代码虽然没有指定类型，但是会在编译的时候报错：

```
let myFavoriteNumber = 'seven';
myFavoriteNumber = 7;
// error TS2322: Type 'number' is not assignable to type 'string'.
```

等价于：

```
let myFavoriteNumber: string = 'seven';
myFavoriteNumber = 7;
// error TS2322: Type 'number' is not assignable to type 'string'.
```

TypeScript 会在没有明确的指定类型的时候推测出一个类型，这就是类型推论。

**如果定义的时候没有赋值，不管之后有没有赋值，都会被推断成 `any` 类型而完全不被类型检查**：

```
let myFavoriteNumber;
myFavoriteNumber = 'seven';
myFavoriteNumber = 7;
```

### 联合类型

联合类型（Union Types）表示取值可以为多种类型中的一种。

#### 简单的例子

```
let count : string | number
count = 7
count = '7'
// it's ok
```

```
let count : string | number
count = 7
count = true
// error Type 'boolean' is not assignable to type 'string | number'.
```

**联合类型使用 `|` 分隔每个类型。**

#### 访问联合类型的属性或方法

当 TypeScript 不确定一个联合类型的变量到底是哪个类型的时候，我们**只能访问此联合类型的所有类型里共有的属性或方法**：

```
function getLength(something: string | number): number {
    return something.length;
}

// index.ts(2,22): error TS2339: Property 'length' does not exist on type 'string | number'.
//   Property 'length' does not exist on type 'number'.
```

上例中，`length` 不是 `string` 和 `number` 的共有属性，所以会报错。

访问 `string` 和 `number` 的共有属性是没问题的：

```
function getString(something: string | number): string {
    return something.toString();
}
```

联合类型的变量在被赋值的时候，会根据类型推论的规则推断出一个类型：

```
let myFavoriteNumber: string | number;
myFavoriteNumber = 'seven';
console.log(myFavoriteNumber.length); // 5
myFavoriteNumber = 7;
console.log(myFavoriteNumber.length); // 编译时报错

// index.ts(5,30): error TS2339: Property 'length' does not exist on type 'number'.
```

例中，第二行的 `myFavoriteNumber` 被推断成了 `string`，访问它的 `length` 属性不会报错。

而第四行的 `myFavoriteNumber` 被推断成了 `number`，访问它的 `length` 属性时就报错了。

### 对象的类型 -- 接口

**在 TypeScript 中，我们使用接口（Interfaces）来定义对象的类型。**

#### 什么是接口

在面向对象语言中，接口（Interfaces）是一个很重要的概念，它是对行为的抽象，而具体如何行动需要由类（classes）去实现（implement）。

TypeScript 中的接口是一个非常灵活的概念，除了可用于[对类的一部分行为进行抽象](https://ts.xcatliu.com/advanced/class-and-interfaces.html#类实现接口)以外，也常用于对「对象的形状（Shape）」进行描述。

#### 简单的例子

```
interface Person {
    name: string;
    age: number;
}

let tom: Person = {
    name: 'Tom',
    age: 25
};
```

上面的例子中，我们定义了一个接口 `Person`，接着定义了一个变量 `tom`，它的类型是 `Person`。这样，我们就约束了 `tom` 的形状必须和接口 `Person` 一致。

定义的变量比接口少了一些属性是不允许的：

```
interface Person {
    name: string;
    age: number;
}

let tom: Person = {
    name: 'Tom'
};

//  error TS2322: Type '{ name: string; }' is not assignable to type 'Person'.
//  Property 'age' is missing in type '{ name: string; }'.
```

多一些属性也是不允许的：

```
interface Person {
    name: string;
    age: number;
}

let tom: Person = {
    name: 'Tom',
    age: 25,
    gender: 'male'
};

// error TS2322: Type '{ name: string; age: number; gender: string; }' is not assignable to type 'Person'.
// Object literal may only specify known properties, and 'gender' does not exist in type 'Person'.
```

可见，**赋值的时候，变量的形状必须和接口的形状保持一致**。

#### 可选属性

有时我们希望不要完全匹配一个形状，那么可以用可选属性：

```
interface Person {
    name: string;
    age?: number;
}

let tom: Person = {
    name: 'Tom'
};
```

```
interface Person {
    name: string;
    age?: number;
}

let tom: Person = {
    name: 'Tom',
    age: 25
};
```

可选属性的含义是该属性可以不存在。

这时**仍然不允许添加未定义的属性**：

```
interface Person {
    name: string;
    age?: number;
}

let tom: Person = {
    name: 'Tom',
    age: 25,
    gender: 'male'
};
```

#### 任意属性

有时候我们希望一个接口有任意属性，可以使用如下方式：

```
interface Person {
	name: string;
	age?: number;
	[propName: string]: any;
}
let tom: Person = {
	name: 'Tom',
	age: 20,
	gender: 'male'
}
```

需要注意的是，**一旦定义了任意属性，那么确定属性和可选属性的类型都必须是它的类型的子集**：

```
interface Person {
	name: string;
	age?: number;
	[propName: string]: string
}
let tom: Person = {
	name: 'tom',
	age: 24,
	gender: 'male'
}
// error Property 'age' of type 'number' is not assignable to string index type 'string'.
```

上例中，任意属性的值允许是 `string`，但是可选属性 `age` 的值却是 `number`，`number` 不是 `string` 的子属性，所以报错了。

一个接口中只能定义一个任意属性。如果接口中有多个类型的属性，则可以在任意属性中使用联合类型：

```
interface Person {
	name: string;
	age?: number;
	[propName: string]: number | string
}
let tom: Person = {
	name: 'tom',
	age: 24,
	gender: 'male'
}
```

#### 只读属性

有时候我们希望对象中的一些字段只能在创建的时候被赋值，那么可以用 `readonly` 定义只读属性：

```
interface Person {
	readonly id: number;
	name: string;
	age?: number;
	[propName: string]: number | string
}
let tom: Person = {
	id: 1,
	name: 'tom'
}
tom.id = 2 // error Cannot assign to 'id' because it is a constant or a read-only property.
```

**注意，只读的约束存在于第一次给对象赋值的时候，而不是第一次给只读属性赋值的时候**：

```
interface Person = {
	readonly id: number;
	name: string;
	age?: number;
	[propName: string]: string | number
}
let tom: Person = {
	name: 'tom',
	age: 23
}
// error Type '{ name: string; gender: string; }' is not assignable to type 'Person'.
Property 'id' is missing in type '{ name: string; gender: string; }'.
Cannot assign to 'id' because it is a constant or a read-only property.
```

上例中，报错信息有两处，第一处是在对 `tom` 进行赋值的时候，没有给 `id` 赋值。

第二处是在给 `tom.id` 赋值的时候，由于它是只读属性，所以报错了。

### 数组的类型

在TypeScript中，数组的类型有多种定义方式，比较灵活

####  类型+方括号 表示法

最简单的方法是使用【类型+方括号】来表示数组：

```
let countArray : number[] = [1,2,3,4,5]
```

数组的项中不允许出现其他的类型：

```
let countArray: number[] = [1,2,3,'4']
// error Type 'string' is not assignable to type 'number'.
```

数组的一些方法的参数也会根据数组在定义时约定的类型进行限制：

```
let countArray: number[] = [1,2,3,4]
countArray.push('2')
// error Argument of type '"2"' is not assignable to parameter of type 'number'.
```

#### 数组泛型

我们也可以使用数组泛型（Array Generic） `Array<elemType>` 来表示数组：

```
let countArray: Array<number> = [1,2,3,4,5]
```

注：关于泛型，后续会介绍

#### 用接口表示数组

接口也可以用来描述数组：

```
interface NumberArray {
	[index: number]: number
}
let countArray: NumberArray = [1,2,3,4,5]
```

`NumberArray` 表示：只要索引的类型是数字时，那么值的类型必须是数字。

虽然接口也可以用来描述数组，但是我们一般不会这么做，因为这种方式比前两种方式复杂多了。

不过有一种情况例外，那就是它常用来表示类数组。

#### 类数组

类数组（Array-like Object）不是数组类型

```
function sum() {
    let args: number[] = arguments;
}

// Type 'IArguments' is missing the following properties from type 'number[]': pop, push, concat, join, and 24 more.
```

上例中，`arguments` 实际上是一个类数组，不能用普通的数组的方式来描述，而应该用接口：

```
function sum() {
    let args: {
        [index: number]: number;
        length: number;
        callee: Function;
    } = arguments;
}
```

在这个例子中，我们除了约束当索引的类型是数字时，值的类型必须是数字之外，也约束了它还有 `length` 和 `callee` 两个属性。

事实上常用的类数组都有自己的接口定义，如 `IArguments`, `NodeList`, `HTMLCollection` 等：

```
function sum() {
    let args: IArguments = arguments;
}
```

其中 `IArguments` 是 TypeScript 中定义好了的类型，它实际上就是：

```
interface IArguments {
    [index: number]: any;
    length: number;
    callee: Function;
}
```

关于内置对象，可以参考[内置对象](https://ts.xcatliu.com/basics/built-in-objects.html)一章。

#### any 在数组中的应用

一个比较常见的作法是，用`any`表示数组允许出现任何类型

```
let countArray:any[] = ['1',2,{name:'12', age: 24}]
```

### 函数的类型

在 JavaScript 中，有两种常见的定义函数的方式——函数声明（Function Declaration）和函数表达式（Function Expression）：