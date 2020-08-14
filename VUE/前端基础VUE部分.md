## VUE

## 前言

#### 安装

- 直接用 `<script>` 引入（本地或者cdn）
- npm `npm install vue`
- vue/cli官方脚手架

```
# 全局安装 vue/cli
npm install -g @vue/cli
# OR
yarn global add @vue/cli
# 创建一个基于 webpack 模板的新项目
vue create hello-world
# 安装依赖，走你
$ cd my-project
# 安装依赖
$ npm install
# 运行项目
$ npm run serve
```

#### 简介

Vue (读音 /vjuː/，类似于 view) 是一套用于构建用户界面的渐进式框架。Vue 的核心库只关注视图层，对应view。

Vue数据驱动，jQuery是结构驱动

#### 原理

内部使用Object.defineProperty（最低支持IE9）把所有属性全部转为 getter/setter，为每个组件绑定了watcher 实例对象，并且把属性作为依赖项，当依赖项的setter调用时，watcher将会重新计算，从而更新组件。

- [组件render]-<创建>-[getter、setter]-<收集依赖>-[watcher]
- [触发setter]-<通知>-[watcher]-<触发>-[组件渲染函数]-<更新>-[组件] 

![image-20200716153956571](C:\Users\50595\AppData\Roaming\Typora\typora-user-images\image-20200716153956571.png)

## VUE实例

#### 声明式渲染

```
<!--html-->
<div id="app">
  {{ message }}
</div>
```

```
//js
var vm = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue!'
  }
})
```

#### 数据与方法
当一个 Vue 实例被创建时，它向 Vue 的响应式系统中加入了其 data 对象中能找到的所有的属性。当这些属性的值发生改变时，视图将会产生“响应”，即匹配更新为新的值。

```
// 我们的数据对象
var data = { a: 1 }

// 该对象被加入到一个 Vue 实例中
var vm = new Vue({
  data: data
})

// 他们引用相同的对象！
vm.a === data.a // => true

// 设置属性也会影响到原始数据
vm.a = 2
data.a // => 2

// ... 反之亦然
data.a = 3
vm.a // => 3
```
当这些数据改变时，视图会进行重渲染。值得注意的是只有当实例被创建时 data 中存在的属性是响应式的。也就是说如果你添加一个新的属性，将不会触发任何视图的更新。如果你知道你会在晚些时候需要一个属性，但是一开始它为空或不存在，那么你仅需要设置一些初始值。


```
var data = { a: 1 }
var vm = new Vue({
  el: '#example',
  data: data
})

vm.$data === data // => true
vm.$el === document.getElementById('example') // => true

// $watch 是一个实例方法
vm.$watch('a', function (newValue, oldValue) {
  // 这个回调将在 `vm.a` 改变后调用
})
```
#### 自身属性和方法
vue实例自身暴露的属性和方法通过前缀$来获取
```
var data = { a: 1 }
var vm = new Vue({
  el: '#example',
  data: data
})

vm.$data === data // => true
vm.$el === document.getElementById('example') // => true
```


#### 实例生命周期

每个 Vue 实例在被创建之前都要经过一系列的初始化过程（生命周期）。在这个过程中会运行一些叫做生命周期钩子的函数，用户可以在不同阶段添加自己的代码来做一些事情。
![image](https://cn.vuejs.org/images/lifecycle.png)

- `beforeCreate:`在实例初始化之后，数据观测 (data observer) 和 event/watcher 事件配置之前被调用。
- `created:`在实例创建完成后被立即调用。在这一步，实例已完成以下的配置：数据观测 (data observer)，属性和方法的运算，watch/event 事件回调。然而，挂载阶段还没开始，$el 属性目前不可见。
- `beforeMount:`在挂载开始之前被调用：相关的 render 函数首次被调用。
- `mounted:`el 被新创建的 vm.$el 替换，并挂载到实例上去之后调用该钩子。
- `beforeUpdate:`数据更新时调用，发生在虚拟 DOM 重新渲染和打补丁之前。
- `updated:`由于数据更改导致的虚拟 DOM 重新渲染和打补丁，在这之后会调用该钩子
- `beforeDestroy:`实例销毁之前调用。在这一步，实例仍然完全可用。    
- `destroyed:`Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。 
- `activated/deactivated：`keep-alive 组件激活/停用时调用，
- `errorCaptured：`当捕获一个来自子孙组件的错误时被调用。此钩子会收到三个参数：错误对象、发生错误的组件实例以及一个包含错误来源信息的字符串。此钩子可以返回 false 以阻止该错误继续向上传播。

**注意：** 
- beforeCreate，created外的钩子在服务器端渲染期间不被调用。
- 不要在选项属性或回调上使用箭头函数，比如
```
//错误，会导致this不会指向Vue 实例
created: () => console.log(this.a)
vm.$watch('a', newValue => this.myMethod())
```

#### Vue对象的选项

```
var vm = new Vue({
  // 数据
  data: "声明需要响应式绑定的数据对象",
  props: "接收来自父组件的数据",
  propsData: "创建实例时手动传递props，方便测试props",
  computed: "计算属性",
  methods: "定义可以通过vm对象访问的方法",
  watch: "Vue实例化时会调用$watch()方法遍历watch对象的每个属性",
  // DOM
  el: "将页面上已存在的DOM元素作为Vue实例的挂载目标",
  template: "可以替换挂载元素的字符串模板",
  render: "渲染函数，字符串模板的替代方案",
  renderError: "仅用于开发环境，在render()出现错误时，提供另外的渲染输出",
  // 生命周期钩子
  beforeCreate: "发生在Vue实例初始化之后，data observer和event/watcher事件被配置之前",
  created: "发生在Vue实例初始化以及data observer和event/watcher事件被配置之后",
  beforeMount: "挂载开始之前被调用，此时render()首次被调用",
  mounted: "el被新建的vm.$el替换，并挂载到实例上之后调用",
  beforeUpdate: "数据更新时调用，发生在虚拟DOM重新渲染和打补丁之前",
  updated: "数据更改导致虚拟DOM重新渲染和打补丁之后被调用",
  activated: "keep-alive组件激活时调用",
  deactivated: "keep-alive组件停用时调用",
  beforeDestroy: "实例销毁之前调用，Vue实例依然可用",
  destroyed: "Vue实例销毁后调用，事件监听和子实例全部被移除，释放系统资源",
  // 资源
  directives: "包含Vue实例可用指令的哈希表",
  filters: "包含Vue实例可用过滤器的哈希表",
  components: "包含Vue实例可用组件的哈希表",
  // 组合
  parent: "指定当前实例的父实例，子实例用this.$parent访问父实例，父实例通过$children数组访问子实例",
  mixins: "将属性混入Vue实例对象，并在Vue自身实例对象的属性被调用之前得到执行",
  extends: "用于声明继承另一个组件，从而无需使用Vue.extend，便于扩展单文件组件",
  provide&inject: "2个属性需要一起使用，用来向所有子组件注入依赖，类似于React的Context",
  // 其它
  name: "允许组件递归调用自身，便于调试时显示更加友好的警告信息",
  delimiters: "改变模板字符串的风格，默认为{{}}",
  functional: "让组件无状态(没有data)和无实例(没有this上下文)",
  model: "允许自定义组件使用v-model时定制prop和event",
  inheritAttrs: "默认情况下，父作用域的非props属性绑定会应用在子组件的根元素上。当编写嵌套有其它组件或元素的组件时，可以将该属性设置为false关闭这些默认行为",
  comments: "设为true时会保留并且渲染模板中的HTML注释"
});
```

## 模板语法

Vue.js 使用了基于 HTML 的模板语法，必须是合法的 HTML。在底层的实现上，Vue 将模板编译成虚拟 DOM 渲染函数。

#### 插值

###### 文本

```
<!--Mustache-->
<span>Message: {{ msg }}</span>
<!--v-text-->
<span v-text="msg"></span>
<!--v-once:一次性插值-->
<span v-once>这个将不会改变: {{ msg }}</span>
```

###### HTML

```
<p>Using v-html directive: <span v-html="rawHtml"></span></p>
```

只对可信内容使用 HTML 插值，绝不要对用户提供的内容使用插值。

###### 特性

```
<div v-bind:id="dynamicId"></div>
```

在插值中可以使用表达式，但只限简单表达式。

```
{{ message.split('').reverse().join('') }}
<div v-bind:id="'list-' + id"></div>
```

#### 指令

指令 (Directives) 是带有 v- 前缀的特殊属性。 指令的职责是，当表达式的值改变时，将其产生的连带影响，响应式地作用于 DOM。

```
<p v-if="seen">现在你看到我了</p>
<a v-on:click="doSomething">...</a>
```

| 指令                    | 预期/限制                                          | 作用             |
| ----------------------- | -------------------------------------------------- | ---------------- |
| v-text                  | string                                             | 文本插值         |
| v-html                  | string                                             | html插值         |
| v-show                  | any                                                | 条件显示         |
| v-if、v-else、v-else-if | any                                                | 条件渲染         |
| v-for                   | Array/Object/number/string                         | 列表渲染         |
| v-on(@)                 | Function/Inline Statement/Object                   | 事件绑定         |
| v-bind(:)               | any (with argument)/Object (without argument)      | 特性绑定         |
| v-model                 | 仅限<input>/<select>/<textarea>/components元素使用 | 双向绑定         |
| v-pre                   |                                                    | 忽略编译         |
| v-cloak                 |                                                    | 避免显示Mustache |
| v-once                  |                                                    | 一次性渲染       |



#### 修饰符

修饰符 (Modifiers) 是以半角句号 . 指明的特殊后缀，用于指出一个指令应该以特殊方式绑定。

```
<form v-on:submit.prevent="onSubmit">...</form>
```

- **v-on能使用的修饰符：**

| 修饰符                | 作用                                               |
| --------------------- | -------------------------------------------------- |
| .stop                 | 调用 event.stopPropagation()。                     |
| .prevent              | 调用 event.preventDefault()。                      |
| .capture              | 添加事件侦听器时使用 capture 模式。                |
| .self                 | 只当事件是从侦听器绑定的元素本身触发时才触发回调。 |
| .{keyCode / keyAlias} | 只当事件是从特定键触发时才触发回调。               |
| .native               | 监听组件根元素的原生事件。                         |
| .once                 | 只触发一次回调。                                   |
| .left                 | (2.2.0) 只当点击鼠标左键时触发。                   |
| .right                | (2.2.0) 只当点击鼠标右键时触发。                   |
| .middle               | (2.2.0) 只当点击鼠标中键时触发。                   |
| .passive              | (2.3.0) 以 { passive: true } 模式添加侦听器        |



- **v-bind能使用的修饰符：**

| 修饰符 | 作用                                                         |
| ------ | ------------------------------------------------------------ |
| .prop  | 被用于绑定 DOM 属性 (property)。(差别在哪里？)               |
| .camel | (2.1.0+) 将 kebab-case 特性名转换为 camelCase. (从 2.1.0 开始支持) |
| .sync  | (2.3.0+) 语法糖，会扩展成一个更新父组件绑定值的 v-on 侦听器。 |



- **v-model能使用的修饰符：**

| 修饰符  | 作用                        |
| ------- | --------------------------- |
| .lazy   | 取代 input 监听 change 事件 |
| .number | 输入字符串转为数字          |
| .trim   | 输入首尾空格过滤            |

## 计算属性与观察者

#### 计算属性
对于任何复杂逻辑，你都应当使用计算属性，而不应直接放在模板中。

计算属性也是响应式的，但是它会基于它们的依赖进行缓存的，**只有当缓存改变，它才会重新求值**；否则会直接返回缓存的结果，而不必再次执行函数。

应当优先使用计算属性而不是侦听属性。
```html
<div id="example">
  <p>Original message: "{{ message }}"</p>
  <p>Computed reversed message: "{{ reversedMessage }}"</p>
</div>
```
```js
var vm = new Vue({
  el: '#example',
  data: {
    message: 'Hello'
  },
  computed: {
    // 计算属性的 getter
    reversedMessage: function () {
      // `this` 指向 vm 实例
      return this.message.split('').reverse().join('')
    }
  }
})
```
下面的计算属性不会更新，因为Date.now() 不是响应式依赖。
```js
computed: {
  now: function () {
    return Date.now()
  }
}
```

#### 计算属性缓存 vs 方法
```
<p>Reversed message: "{{ reversedMessage() }}"</p>
```
```js
// 在组件中
methods: {
  reversedMessage: function () {
    return this.message.split('').reverse().join('')
  }
}
```
方法在每次调用时**总会再次执行函数**。

#### setter
计算属性默认只有 getter ，不过在需要时你也可以提供一个 setter
```
computed: {
  fullName: {
    // getter
    get: function () {
      return this.firstName + ' ' + this.lastName
    },
    // setter
    set: function (newValue) {
      var names = newValue.split(' ')
      this.firstName = names[0]
      this.lastName = names[names.length - 1]
    }
  }
}
```
#### 侦听器
```
<div id="watch-example">
  <p>
    Ask a yes/no question:
    <input v-model="question">
  </p>
  <p>{{ answer }}</p>
</div>
```
```
watch: {
    // 如果 `question` 发生改变，这个函数就会运行
    question: function (newQuestion, oldQuestion) {
      this.answer = 'Waiting for you to stop typing...'
      this.getAnswer()
    }
  }
```

## Class与Style绑定

#### Class
###### 对象语法
当value为真时，绑定对应的key到class
```
<!--内联在模板中-->
<div class="static"
     v-bind:class="{ active: isActive, 'text-danger': hasError }">
</div>
<!--绑定data或者计算属性的的一个对象-->
<div v-bind:class="classObject"></div>
<!--js-->
data: {
  classObject: {
    active: true,
    'text-danger': false
  }
}
```
###### 数组语法

```
<!--模板-->
<div v-bind:class="[activeClass, errorClass]"></div>
<!--js-->
data: {
  activeClass: 'active',
  errorClass: 'text-danger'
}
<!--结果-->
<div class="active text-danger"></div>
```
也可以使用三元表达式。
```
// isActive为真添加activeClass，errorClass始终存在
<div v-bind:class="[isActive ? activeClass : '', errorClass]"></div>
```
###### 混合
```
<div v-bind:class="[{ active: isActive }, errorClass]"></div>
```
###### 用在组件上
class将被添加到该组件的根元素上面。该元素上已经存在的class不会被覆盖。
```
<my-component class="baz boo"></my-component>
```
**注意：和普通的class并存，并不会覆盖（不同名），最终会合成一个class。**
#### Style
自动侦测并添加相应浏览器引擎前缀。
###### 对象语法
CSS 属性名可以用驼峰式 (camelCase) 或短横线分隔 (kebab-case，记得用单引号括起来) 来命名。

```
<!--内联在模板中-->
<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
<!--js-->
data: {
  activeColor: 'red',
  fontSize: 30
}
<!--绑定data或者计算属性的的一个对象-->
<div v-bind:style="styleObject"></div>
<!--js-->
data: {
  styleObject: {
    color: 'red',
    fontSize: '13px'
  }
}
```
###### 数组语法
可以将多个样式对象应用到同一个元素上
```
<div v-bind:style="[baseStyles, overridingStyles]"></div>
```
###### 多重值
```
<!--常用于提供多个带前缀的值-->
<div :style="{ display: ['-webkit-box', '-ms-flexbox', 'flex'] }"></div>
```

## 条件渲染

#### v-if

根据表达式的值的真假条件渲染元素。

```
<div v-if="type === 'A'">
  A
</div>
<div v-else-if="type === 'B'">
  B
</div>
<div v-else-if="type === 'C'">
  C
</div>
<div v-else>
  Not A/B/C
</div>
```

如果需要条件渲染多个元素，可以使用<template>包裹。

```
<template v-if="ok">
  <h1>Title</h1>
  <p>Paragraph 1</p>
  <p>Paragraph 2</p>
</template>
```

key

Vue 会尽可能高效地渲染元素，通常会复用已有元素而不是从头开始渲染。**添加一个具有唯一值的 key 属性可以强制其重新渲染。**

#### v-show

根据表达式之真假值，切换元素的 display CSS 属性。

```
<h1 v-show="ok">Hello!</h1>
```

## 列表渲染

#### 数组

```
<!--普通-->
<ul id="example">
  <li v-for="item in items">
    {{ item.message }}
  </li>
</ul>
<!--带索引-->
<ul id="example">
  <li v-for="(item, index) in items">
    {{ parentMessage }} - {{ index }} - {{ item.message }}
  </li>
</ul>
<!--js-->
var example = new Vue({
  el: '#example',
  data: {
    items: [
      { message: 'Foo' },
      { message: 'Bar' }
    ]
  }
})
```
###### 数组更新检测
包含变异（改变原数组）和非变异（生成新数组，不改变原数组）两组方式，都将触发更新。
- 变异方法：push()、pop()、shift()、unshift()、splice()、sort()、reverse()
- 非变异方法（需用新数组替换原数组）：filter()、concat()、slice()

###### **不能检测的变动：**

- 当你利用索引直接设置一个项时，例如：vm.items[indexOfItem] = newValue
- 当你修改数组的长度时，例如：vm.items.length = newLength
#### 对象

```html
<!--普通-->
<li v-for="value in object">
{{ value }}
</li>
<!--带key-->
<div v-for="(value, key) in object">
  {{ key }}: {{ value }}
</div>
<!--带key、索引-->
<div v-for="(value, key, index) in object">
  {{ index }}. {{ key }}: {{ value }}
</div>
<!--js-->
new Vue({
  data: {
    object: {
      firstName: 'John',
      lastName: 'Doe',
      age: 30
    }
  }
})
```
###### 对象更改检测注意事项
Vue 不能检测对象属性的添加或删除。
- 对于已经创建的实例，Vue 不能动态添加根级别的响应式属性。
```
var vm = new Vue({
  data: {
    a: 1
  }
})
// `vm.a` 现在是响应式的

vm.b = 2
// `vm.b` 不是响应式的
```
- 可以使用 Vue.set(object, key, value) 方法向嵌套对象添加响应式属性
```
var vm = new Vue({
  data: {
    userProfile: {
      name: 'Anika'
    }
  }
})
vm.$set(this.userProfile, 'age', 27)
```
- 多个属性可以使用Object.assign() 或 _.extend()
```
this.userProfile = Object.assign({}, this.userProfile, {
  age: 27,
  favoriteColor: 'Vue Green'
})
```
#### key
当 Vue.js 用 v-for 正在更新已渲染过的元素列表时，它默认用“就地复用”策略。
建议尽可能在使用 v-for 时为每一项提供一个唯一的 key。
循环组件的时候，key是必须的。
```
<div v-for="item in items" :key="item.id">
  <!-- 内容 -->
</div>
```

#### 其他
- v-for的循环对象也可以是计算属性和带返回值的method 方法。
- 利用带有 v-for 的 <template> 渲染多个元素
```
<ul>
  <template v-for="item in items">
    <li>{{ item.msg }}</li>
    <li class="divider"></li>
  </template>
</ul>
```
- v-for和v-if处于同一节点时，v-for 具有比 v-if 更高的优先级

## 事件处理

#### 事件

```
<div id="example-3">
  <button v-on:click="say('hi')">Say hi</button>
  <!--访问原始的 DOM 事件-->
  <button v-on:click="say2('what', $event)">Say what</button>
</div>
new Vue({
  el: '#example-3',
  methods: {
    say: function (message) {
      alert(message)
    },
    say2: function (message,event) {
        // 现在我们可以访问原生事件对象
        if (event) event.preventDefault()
      alert(message)
    }
  }
})
```

#### 事件修饰符

修饰符可以串联，代码会以串联的顺序产生。

| 修饰符   | 作用                                               |
| -------- | -------------------------------------------------- |
| .stop    | 调用 event.stopPropagation()。                     |
| .prevent | 调用 event.preventDefault()。                      |
| .capture | 添加事件侦听器时使用 capture 模式。                |
| .self    | 只当事件是从侦听器绑定的元素本身触发时才触发回调。 |
| .once    | 只触发一次回调。                                   |



```
<!-- 阻止单击事件继续传播 -->
<a v-on:click.stop="doThis"></a>

<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat"></a>

<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>

<!-- 添加事件监听器时使用事件捕获模式 -->
<!-- 即元素自身触发的事件先在此处处理，然后才交由内部元素进行处理 -->
<div v-on:click.capture="doThis">...</div>

<!-- 只当在 event.target 是当前元素自身时触发处理函数 -->
<!-- 即事件不是从内部元素触发的 -->
<div v-on:click.self="doThat">...</div>
<!-- 点击事件将只会触发一次（可用于自定义组件） -->
<a v-on:click.once="doThis"></a>
```

Vue 还对应 addEventListener 中的 passive 选项提供了 .passive 修饰符，能够提升移动端的性能，但是要避免和.prevent一起使用。

```
<!-- 滚动事件的默认行为 (即滚动行为) 将会立即触发 -->
<!-- 而不会等待 `onScroll` 完成  -->
<!-- 这其中包含 `event.preventDefault()` 的情况 -->
<div v-on:scroll.passive="onScroll">...</div>
```

#### 按键修饰符

在监听键盘事件时，我们经常需要检查常见的键值。Vue 允许为 v-on 在监听键盘事件时添加按键修饰符。

```
<!-- 只有在 `keyCode` 是 13 时调用 `vm.submit()` -->
<input v-on:keyup.13="submit">
<!-- 缩写语法 -->
<input @keyup.enter="submit">
```

- **全部的按键别名：**`.enter`、`.tab`、`.delete` (捕获“删除”和“退格”键)、`.esc`、`.space`、`.up`、`.down`、`.left`、`.right`
- 自定义按键修饰符别名

```
// 可以使用 `v-on:keyup.f1`
Vue.config.keyCodes.f1 = 112
```

- 自动匹配按键修饰符

```
<!--可直接将 KeyboardEvent.key 暴露的任意有效按键名转换为 kebab-case 来作为修饰符：-->
<input @keyup.page-down="onPageDown">
```

#### 系统修饰键

`.ctrl`、`.alt`、`.shift`、`.meta`。 在和 keyup 事件一起用时，事件触发时修饰键必须处于按下状态。换句话说，只有在按住 ctrl 的情况下释放其它按键，才能触发 keyup.ctrl。而单单释放 ctrl 也不会触发事件。

```
<!-- Alt + C -->
<input @keyup.alt.67="clear">

<!-- Ctrl + Click -->
<div @click.ctrl="doSomething">Do something</div>
```

`.exact` 修饰符允许你控制由精确的系统修饰符组合触发的事件。

```
<!-- 即使 Alt 或 Shift 被一同按下时也会触发 -->
<button @click.ctrl="onClick">A</button>

<!-- 有且只有 Ctrl 被按下的时候才触发 -->
<button @click.ctrl.exact="onCtrlClick">A</button>

<!-- 没有任何系统修饰符被按下的时候才触发 -->
<button @click.exact="onClick">A</button>
```

#### 鼠标按钮修饰符

`.left`、`.right`、`.middle` 仅响应特定的鼠标按钮

## 表单输入绑定

#### 基础用法
可以用 `v-model` 指令在表单 `<input>` 及 `<textarea>` 元素上创建双向数据绑定。

`v-model`仅为`v-on:input`和`v-bind:value`的**语法糖**而已。

```
<input v-model="something">
<input
  v-bind:value="something"
  v-on:input="something = $event.target.value">
```

注意：v-model 会忽略所有表单元素的 `value、checked、selected` 特性的初始值而**总是将 Vue 实例的数据作为数据来源**。你应该通过 JavaScript 在组件的 data 选项中声明初始值。

- 文本/多行文本
```
<input v-model="message" placeholder="edit me">
<textarea v-model="message" placeholder="add multiple lines"></textarea>
<p>Message is: {{ message }}</p>
```
- 复选框
```
<div id='example-3'>
  <input type="checkbox" id="jack" value="Jack" v-model="checkedNames">
  <label for="jack">Jack</label>
  <input type="checkbox" id="john" value="John" v-model="checkedNames">
  <label for="john">John</label>
  <input type="checkbox" id="mike" value="Mike" v-model="checkedNames">
  <label for="mike">Mike</label>
  <br>
  <span>Checked names: {{ checkedNames }}</span>
</div>
```
```js
new Vue({
  el: '#example-3',
  data: {
    checkedNames: []
  }
})
//Checked names: [ "Jack", "John", "Mike" ]
```
- 单选按钮
```
<div id="example-4">
  <input type="radio" id="one" value="One" v-model="picked">
  <label for="one">One</label>
  <br>
  <input type="radio" id="two" value="Two" v-model="picked">
  <label for="two">Two</label>
  <br>
  <span>Picked: {{ picked }}</span>
</div>
```
```
new Vue({
  el: '#example-4',
  data: {
    picked: ''
  }
})
//Picked: Two
```
- 选择框
```
<div id="example-5">
  <select v-model="selected">
    <option disabled value="">请选择</option>
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select>
  <span>Selected: {{ selected }}</span>
</div>
```
```
new Vue({
  el: '...',
  data: {
    selected: ''
  }
})
//Selected: B
```
为多选时则返回一个数组`Selected: [ "A", "B" ]`
#### 值绑定
- 复选框
```
<input
  type="checkbox"
  v-model="toggle"
  true-value="yes"
  false-value="no"
>
```
- 单选按钮
```
<input type="radio" v-model="pick" v-bind:value="a">
```
- 选择框的选项
```
<select v-model="selected">
    <!-- 内联对象字面量 -->
  <option v-bind:value="{ number: 123 }">123</option>
</select>
```
#### 修饰符
- `.lazy`，默认`input`事件触发，使用此修饰则改为change事件触发
```
<!-- 在“change”时而非“input”时更新 -->
<input v-model.lazy="msg" >
```
- `.number`将输入的值转换为数值
- `.trim`过滤掉输入内容的首尾空白字符

## 组件

#### 简介
![image](https://cn.vuejs.org/images/components.png)
组件 (Component) 是 Vue.js 最强大的功能之一。组件可以扩展 HTML 元素，封装可重用的代码。组件是具有特殊功能的自定义元素。

所有的 Vue 组件同时也都是 Vue 的实例，所以可接受相同的选项对象 (除了一些根级特有的选项) 并提供相同的生命周期钩子。

#### 注册组件
###### 全局组件

```
<div id="example">
  <my-component></my-component>
</div>
//注意确保在初始化根实例之前注册组件
// 注册
Vue.component('my-component', {
  template: '<div>A custom component!</div>'
})
```
###### 局部组件

```
var Child = {
  template: '<div>A custom component!</div>'
}

new Vue({
  // ...
  components: {
    // <my-component> 将只在父组件模板中可用
    'my-component': Child
  }
})
```
###### 注意
- data必须是带return的函数
- 如果将组件用于像 `<ul>`、`<ol>`、`<table>`、`<select>` 这样的元素里面，为了遵循规范，应该使用is：
```
<table>
  <tr is="my-row"></tr>
</table>
```
以下类型模板无此限制：`<script type="text/x-template">`、JavaScript 内联模板字符串、`.vue` 组件
###### 单文件组件
可以包含`<template>`、`<script>`、`<style>`、`<docs>`四个元素。
- `<template>`内只允许有一个根元素
- `<style>`可以有多个
- `<docs>`说明文档
- `<script>`、`<style>`支持src导入

#### 组件通信
![image](https://cn.vuejs.org/images/props-events.png)
###### Prop
父组件向子组件传递数据。
```
Vue.component('child', {
  // 声明 props
  props: ['message'],
  // 就像 data 一样，prop 也可以在模板中使用
  // 同样也可以在 vm 实例中通过 this.message 来使用
  template: '<span>{{ message }}</span>'
})
<child message="hello!"></child>
```
动态 Prop:

```
<child v-bind:my-message="parentMsg"></child>
```
如果你想把一个对象的所有属性作为 prop 进行传递，可以使用不带任何参数的 v-bind
```
todo: {
  text: 'Learn Vue',
  isComplete: false
}
<todo-item v-bind="todo"></todo-item>
//等价于
<todo-item
  v-bind:text="todo.text"
  v-bind:is-complete="todo.isComplete"
></todo-item>
```
字面量语法 vs 动态语法

```
<!-- 传递了一个字符串 "1" -->
<comp some-prop="1"></comp>
<!-- 传递真正的数值 -->
<comp v-bind:some-prop="1"></comp>
```
验证

为组件的 prop 指定验证规则，会在组件实例创建之前进行校验。如果传入的数据不符合要求，Vue 会发出警告。
```
Vue.component('example', {
  props: {
    // 基础类型检测 (`null` 指允许任何类型)
    propA: Number,
    // 可能是多种类型
    propB: [String, Number],
    // 必传且是字符串
    propC: {
      type: String,
      required: true
    },
    // 数值且有默认值
    propD: {
      type: Number,
      default: 100
    },
    // 数组/对象的默认值应当由一个工厂函数返回
    propE: {
      type: Object,
      default: function () {
        return { message: 'hello' }
      }
    },
    // 自定义验证函数
    propF: {
      validator: function (value) {
        return value > 10
      }
    }
  }
})
```
**type 可以是下面原生构造器**：`String`、`Number`、`Boolean`、`Function`、`Object`、`Array`、`Symbol`

组件可以接收任意传入的特性，这些特性都会被添加到组件的根元素上，且会做合并处理。
###### 自定义事件
子组件向父组件传递数据。
- 使用 `$on(eventName)` 监听事件
- 使用 `$emit(eventName)` 触发事件
```
<div id="counter-event-example">
  <p>{{ total }}</p>
  <button-counter v-on:increment="incrementTotal"></button-counter>
  <button-counter v-on:increment="incrementTotal"></button-counter>
</div>
```
```
Vue.component('button-counter', {
  template: '<button v-on:click="incrementCounter">{{ counter }}</button>',
  data: function () {
    return {
      counter: 0
    }
  },
  methods: {
    incrementCounter: function () {
      this.counter += 1
      this.$emit('increment')
    }
  },
})

new Vue({
  el: '#counter-event-example',
  data: {
    total: 0
  },
  methods: {
    incrementTotal: function () {
      this.total += 1
    }
  }
})
```
###### 父子双向通信
- `.sync`

`@update`的语法糖
```
<comp :foo.sync="bar"></comp>
this.$emit('update:foo', newValue)
```
等价于
```
<comp :foo="bar" @update:foo="val => bar = val"></comp>
this.$emit('update:foo', newValue)
```
- v-model(仅适用于表单输入组件)

`v-on:input`和`v-bind:value`的语法糖
```
<input v-model="something">
// 通过 input 事件带出数值
this.$emit('input', Number(formattedValue))
```
等价于
```
<input
  v-bind:value="something"
  v-on:input="something = $event.target.value">
this.$emit('input', Number(formattedValue))
```
###### 非父子组件通信
- 简单场景`bus.js`

```
var bus = new Vue()
// 触发组件 A 中的事件
bus.$emit('id-selected', 1)
// 在组件 B 创建的钩子中监听事件
bus.$on('id-selected', function (id) {
  // ...
})
```
**注：** 还可以使用`$ref、$parent、$child`进行通信，不过**不推荐**。
- 复杂的场景请使用vuex
#### 插槽
为了让组件可以组合，我们需要一种方式来混合父组件的内容与子组件自己的模板。这个过程被称为内容分发。
**编译作用域：** 父组件模板的内容在父组件作用域内编译；子组件模板的内容在子组件作用域内编译。
###### 单个插槽
除非子组件模板包含至少一个 `<slot>` 插口，否则父组件的内容将会被丢弃。当子组件模板只有一个没有属性的插槽时，父组件传入的整个内容片段将插入到插槽所在的 DOM 位置，并替换掉插槽标签本身。

最初在 `<slot>` 标签中的任何内容都被视为备用内容。备用内容在子组件的作用域内编译，并且只有在宿主元素为空，且没有要插入的内容时才显示备用内容。
```
<!--子组件-->
<div>
  <h2>我是子组件的标题</h2>
  <slot>
    只有在没有要分发的内容时才会显示。
  </slot>
</div>

<!--父组件-->
<div>
  <h1>我是父组件的标题</h1>
  <my-component>
    <p>这是一些初始内容</p>
    <p>这是更多的初始内容</p>
  </my-component>
</div>

<!--结果-->
<div>
  <h1>我是父组件的标题</h1>
  <div>
    <h2>我是子组件的标题</h2>
    <p>这是一些初始内容</p>
    <p>这是更多的初始内容</p>
  </div>
</div>
```
###### 具名插槽
`<slot>` 元素可以用一个特殊的特性 name 来进一步配置如何分发内容。多个插槽可以有不同的名字。具名插槽将匹配内容片段中有对应 slot 特性的元素。

仍然可以有一个匿名插槽，它是默认插槽，作为找不到匹配的内容片段的备用插槽。如果没有默认插槽，这些找不到匹配的内容片段将被抛弃。
```
<!--子组件-->
<div class="container">
  <header>
    <slot name="header"></slot>
  </header>
  <main>
    <slot></slot>
  </main>
  <footer>
    <slot name="footer"></slot>
  </footer>
</div>

<!--父组件-->
<app-layout>
  <h1 slot="header">这里可能是一个页面标题</h1>

  <p>主要内容的一个段落。</p>
  <p>另一个主要段落。</p>

  <p slot="footer">这里有一些联系信息</p>
</app-layout>

<!--结果-->
<div class="container">
  <header>
    <h1>这里可能是一个页面标题</h1>
  </header>
  <main>
    <p>主要内容的一个段落。</p>
    <p>另一个主要段落。</p>
  </main>
  <footer>
    <p>这里有一些联系信息</p>
  </footer>
</div>
```
###### 作用域插槽
和普通的插槽对比，能够传递数据。
```
<!--子组件-->
<div class="child">
  <slot text="hello from child"></slot>
</div>

<!--父组件-->
<div class="parent">
  <child>
  <!--2.5.0+，slot-scope 能被用在任意元素或组件中而不再局限于 <template>-->
    <template slot-scope="props">
      <span>hello from parent</span>
      <span>{{ props.text }}</span>
    </template>
  </child>
</div>

<!--结果-->
<div class="parent">
  <div class="child">
    <span>hello from parent</span>
    <span>hello from child</span>
  </div>
</div>
```
#### 动态组件
通过使用保留的 `<component>` 元素，并对其 is 特性进行动态绑定，你可以在同一个挂载点动态切换多个组件：
```
var vm = new Vue({
  el: '#example',
  data: {
    currentView: 'home'
  },
  components: {
    home: { /* ... */ },
    posts: { /* ... */ },
    archive: { /* ... */ }
  }
})
```
###### keep-alive
把切换出去的组件保留在内存中,保留其状态或避免重新渲染
```
<keep-alive>
  <component :is="currentView">
    <!-- 非活动组件将被缓存！ -->
  </component>
</keep-alive>
```
#### 注意事项
- 组件复用性，松耦合
- 谨慎使用ref
- 在大型应用中使用异步加载
- PascalCase声明， kebab-case使用
- 为递归组件添加name
- 对低开销的静态组件使用 v-once

## 可复用性和组合

#### 混合

混合 (mixins) 是一种分发 Vue 组件中可复用功能的非常灵活的方式。混合对象可以包含任意组件选项。当组件使用混合对象时，所有混合对象的选项将被混入该组件本身的选项。

```
// 定义一个混合对象
var myMixin = {
  created: function () {
    this.hello()
  },
  methods: {
    hello: function () {
      console.log('hello from mixin!')
    }
  }
}

// 定义一个使用混合对象的组件
var Component = Vue.extend({
  mixins: [myMixin]
})
```

- 当组件和混合对象含有同名选项时，这些选项将以恰当的方式混合。比如，同名钩子函数将混合为一个数组，因此都将被调用。另外，混合对象的 钩子将在组件自身钩子 之前 调用 。
- 值为对象的选项，例如 methods, components 和 directives，将被混合为同一个对象。两个对象键名冲突时，取组件对象的键值对。
- `Vue.extend()` 也使用同样的策略进行合并。

#### 自定义指令

```
// 注册一个全局自定义指令 `v-focus`
Vue.directive('focus', {
  // 当被绑定的元素插入到 DOM 中时……
  inserted: function (el) {
    // 聚焦元素
    el.focus()
  }
})
// 注册一个局部自定义指令
directives: {
  focus: {
    // 指令的定义
    inserted: function (el) {
      el.focus()
    }
  }
}
//使用
<input v-focus>
```

#### 钩子函数

```
一个指令定义对象可以提供如下几个钩子函数 (均为可选)：

bind：只调用一次，指令第一次绑定到元素时调用。在这里可以进行一次性的初始化设置。
inserted：被绑定元素插入父节点时调用 (仅保证父节点存在，但不一定已被插入文档中)。
update：所在组件的 VNode 更新时调用，但是可能发生在其子 VNode 更新之前。指令的值可能发生了改变，也可能没有。但是你可以通过比较更新前后的值来忽略不必要的模板更新 (详细的钩子函数参数见下)。
componentUpdated：指令所在组件的 VNode 及其子 VNode 全部更新后调用。
unbind：只调用一次，指令与元素解绑时调用。
```

#### 钩子函数参数

指令钩子函数会被传入以下参数：

- `el：`指令所绑定的元素，可以用来直接操作 DOM 。
- `binding：`一个对象，包含以下属性：
  - `name：`指令名，不包括 v- 前缀。
  - `value：`指令的绑定值，例如：v-my-directive="1 + 1" 中，绑定值为 2。
  - `oldValue：`指令绑定的前一个值，仅在 update 和 componentUpdated 钩子中可用。无论值是否改变都可用。
  - `expression：`字符串形式的指令表达式。例如 v-my-directive="1 + 1" 中，表达式为 "1 + 1"。
  - `arg：`传给指令的参数，可选。例如 v-my-directive:foo 中，参数为 "foo"。
  - `modifiers：`一个包含修饰符的对象。例如：v-my-directive.foo.bar 中，修饰符对象为 { foo: true, bar: true }。
- `vnode：`Vue 编译生成的虚拟节点。移步 VNode API 来了解更多详情。
- `oldVnode：`上一个虚拟节点，仅在 update 和 componentUpdated 钩子中可用。

#### 过滤器

过滤器可以用在两个地方：双花括号插值和 v-bind 表达式。

```
<!-- 在双花括号中 -->
{{ message | capitalize }}

<!-- 在 `v-bind` 中 -->
<div v-bind:id="rawId | formatId"></div>
```

```
//定义局部过滤器
filters: {
  capitalize: function (value) {
    if (!value) return ''
    value = value.toString()
    return value.charAt(0).toUpperCase() + value.slice(1)
  }
}
//定义全局过滤器
Vue.filter('capitalize', function (value) {
  if (!value) return ''
  value = value.toString()
  return value.charAt(0).toUpperCase() + value.slice(1)
})
```

- 过滤器可以串联，依次执行，前面的输出作为后面一个的输入。

```
{{ message | filterA | filterB }}
```

- 过滤器可以接收参数（管道符前面的值作为第一个参数，括号内的第一个参数为第二个，依次类推）

- ```
  {{ message | filterA('arg1', arg2) }}
  ```

## Vue-Router

- 直接用 `<script>` 引入（本地或者cdn）
- npm `npm install vue`

必须要通过 `Vue.use()` 明确地安装路由功能，且要通过 router 配置参数注入Vue实例，从而让整个应用都有路由功能。

#### 作用

将页面组件(components)映射到路由(routes)，然后告诉 vue-router 在哪里渲染它们

#### Router-Link

- `to：` 属性指定目标地址，默认渲染成带有正确链接的 标签
- `replace：`相当于`router.replace()` 不会留下 history 记录
- `append：`设置 append 属性后，则在当前（相对）路径前添加基路径。例如，我们从 /a 导航到一个相对路径 b，如果没有配置 append，则路径为 /b，如果配了，则为 /a/b
- `tag:` 属性生成别的标签.。另外，当目标路由成功激活时，链接元素自动设置一个表示激活的 CSS 类名。
- `active-class：`链接激活时使用的 CSS 类名。默认值可以通过路由的构造选项 linkActiveClass 来全局配置。

将激活 class 应用在外层元素：

```
<router-link tag="li" to="/foo">
  <a>/foo</a>
</router-link>
```

在这种情况下，`<a>` 将作为真实的链接（它会获得正确的 href 的），而 "激活时的CSS类名" 则设置到外层的 `<li>`。

#### router-view

路由视图容器

```
<transition>
<!--使用路由缓存-->
  <keep-alive>
    <router-view></router-view>
  </keep-alive>
</transition>

```

如果 `<router-view>`设置了名称，则会渲染对应的路由配置中 components 下的相应组件。

```
<!--html-->
<router-view class="view one"></router-view>
<router-view class="view two" name="a"></router-view>
<router-view class="view three" name="b"></router-view>
<!--js-->
const router = new VueRouter({
  routes: [
    {
      path: '/',
      components: {
        default: Foo,
        a: Bar,
        b: Baz
      }
    }
  ]
})
```

#### 动态路由匹配

######  动态路由参数 params

```
//定义
routes: [
    // 动态路径参数 以冒号开头
    { path: '/user/:id', component: User }
  ]
//调用
$route.params.id
```

######  动态路径查询参数 query

```
//定义
routes: [
    // 动态路径参数 以冒号开头
    { path: '/user?id=6456456', component: User }
  ]
//调用
$route.query.id
```

#### 响应路由参数的变化

当路由参数变化时，组件的生命周期钩子不会再被调用。 想对路由参数的变化作出响应的话，有以下两种方式：

######  watch（监测变化）$route 对象

```
const User = {
  template: '...',
  watch: {
    '$route' (to, from) {
      // 对路由变化作出响应...
    }
  }
}
```

###### 使用beforeRouteUpdate 守卫

```
const User = {
  template: '...',
  beforeRouteUpdate (to, from, next) {
    // react to route changes...
    // don't forget to call next()
  }
}
```

####  匹配优先级

同一个路径可以匹配多个路由时，谁先定义的，谁的优先级就最高。 因此，404类的页面一定要放在最后，路由是按照声明顺序匹配，如果不是最后则404之后的页面都会跳转到404。

#### 嵌套路由

```
const router = new VueRouter({
  routes: [
    { path: '/user/:id', component: User,
      children: [
        {
          // 当 /user/:id/profile 匹配成功，
          // UserProfile 会被渲染在 User 的 <router-view> 中
          path: 'profile',
          component: UserProfile
        },
        {
          // 当 /user/:id/posts 匹配成功
          // UserPosts 会被渲染在 User 的 <router-view> 中
          path: 'posts',
          component: UserPosts
        }
      ]
    }
  ]
})
```

- 以 / 开头的嵌套路径会被当作根路径。 这让你充分的使用嵌套组件而无须设置嵌套的路径。
- 如果想在父路由渲染内容，可以定义一个空的子路由。

#### 编程式导航

###### router.push(location, onComplete?, onAbort?)

导航到不同的 URL,会向 history 栈添加一个新的记录。 在 Vue 实例内部，调用 `this.$router.push`

```
/ 字符串
router.push('home')
// 对象
router.push({ path: 'home' })
// 命名的路由
router.push({ name: 'user', params: { userId: 123 }})
// 带查询参数，变成 /register?plan=private
router.push({ path: 'register', query: { plan: 'private' }})
```

- onComplete：在导航成功完成 (在所有的异步钩子被解析之后) 调用
- onAbort：在导航终止 (导航到相同的路由、或在当前导航完成之前导航到另一个不同的路由) 调用

###### router.replace(location, onComplete?, onAbort?)

和router.push功能一样，唯一区别就是不会向 history 添加新记录

###### router.go(n)

前进或后退nN步，类似 window.history.go(n)

```
// 在浏览器记录中前进一步，等同于 history.forward()
router.go(1)
// 后退一步记录，等同于 history.back()
router.go(-1)
```

#### 重定向

```
const router = new VueRouter({
  routes: [
    //path
    { path: '/a', redirect: '/b' },
    //name
    { path: '/a', redirect: { name: 'foo' }},
    //方法
    { path: '/a', redirect: to => {
      // 方法接收 目标路由 作为参数
      // return 重定向的 字符串路径/路径对象
    }}
  ]
})
```

#### 别名

/a 的别名是 /b，意味着，当用户访问 /b 时，URL 会保持为 /b，但是路由匹配则为 /a，就像用户访问 /a 一样

```
const router = new VueRouter({
  routes: [
    { path: '/a', component: A, alias: '/b' }
  ]
})
```

#### 路由组件传参

使用 props 将组件和路由解耦

```
const User = {
  props: ['id'],
  template: '<div>User {{ id }}</div>'
}
const router = new VueRouter({
  routes: [
    { path: '/user/:id', component: User, props: true },

    // 对于包含命名视图的路由，你必须分别为每个命名视图添加 `props` 选项：
    {
      path: '/user/:id',
      components: { default: User, sidebar: Sidebar },
      props: { default: true, sidebar: false }
    }
  ]
})
```

- 如果 props 被设置为 true，route.params 将会被设置为组件属性

- 如果 props 是一个对象，它会被按原样设置为组件属性。当 props 是静态的时候有用。

```
const router = new VueRouter({
  routes: [
    { path: '/promotion/from-newsletter', component: Promotion, props: { newsletterPopup: false } }
  ]
})
```

- 你可以创建一个函数返回 props。这样你便可以将参数转换成另一种类型，将静态值与基于路由的值结合等等。

```
const router = new VueRouter({
  routes: [
    { path: '/search', component: SearchUser, props: (route) => ({ query: route.query.q }) }
  ]
})
```

#### HTML5 History 模式

vue-router 默认 hash 模式。

开启history 模式，将充分利用 history.pushState API 来完成 URL 跳转而无须重新加载页面，但需要后端配合。

```
const router = new VueRouter({
  mode: 'history',
  routes: [...]
})
```

#### 导航守卫

```
vue-router 提供的导航守卫主要用来通过跳转或取消的方式守卫导航。
```

全局：

```
//前置守卫:确保要调用 next 方法，否则钩子就不会被 resolved。
router.beforeEach((to, from, next) => {
  // ...
})
//后置守卫
router.afterEach((to, from) => {
  // ...
})
//解析守卫:在导航被确认之前，同时在所有组件内守卫和异步路由组件被解析之后，解析守卫就被调用
router.beforeResolve((to, from) => {
  // ...
})
```

参数说明：

- `to: Route:` 即将要进入的目标 路由对象

- `from: Route:` 当前导航正要离开的路由

- ```
  next: Function:
  ```

  一定要调用该方法来 resolve 这个钩子。执行效果依赖 next 方法的调用参数。

  - `next():`进行管道中的下一个钩子。如果全部钩子执行完了，则导航的状态就是 confirmed （确认的）。
  - `next(false):` 中断当前的导航。如果浏览器的 URL 改变了（可能是用户手动或者浏览器后退按钮），那么 URL 地址会重置到 from 路由对应的地址。
  - `next('/')`或者 `next({ path: '/' }):` 跳转到一个不同的地址。当前的导航被中断，然后进行一个新的导航。你可以向 next 传递任意位置对象，且允许设置诸如 `replace: true、name: 'home'` 之类的选项以及任何用在 router-link 的 to prop 或 router.push 中的选项。
  - `next(error):` (2.4.0+) 如果传入 next 的参数是一个 Error 实例，则导航会被终止且该错误会被传递给 `router.onError()` 注册过的回调。

#### 路由独享的守卫

```
//与全局前置守卫的方法参数是一样的
const router = new VueRouter({
  routes: [
    {
      path: '/foo',
      component: Foo,
      beforeEnter: (to, from, next) => {
        // ...
      }
    }
  ]
})
```

#### 路由元信息

配置meta字段记录元信息

```
//定义
{
  path: 'bar',
  component: Bar,
  // a meta field
  meta: { requiresAuth: true }
}
//访问
$route.matched
```

## Vuex

### 安装

- 直接用 `<script>` 引入（本地或者cdn）
- npm `npm install vue`
必须要通过 Vue.use() 明确地安装vuex，且要通过 store 配置参数注入Vue实例。
### 简介
Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。
![image](https://vuex.vuejs.org/zh-cn/images/vuex.png)
#### state
- 状态仓库，全局的数据共享中心
- 改变 state 中的状态的唯一途径就是显式地提交 (commit) mutation
- 获取状态使用计算属性
- mapState辅助函数
```js
// 在单独构建的版本中辅助函数为 Vuex.mapState
import { mapState } from 'vuex'

export default {
  // ...
  computed: mapState({
    // 箭头函数可使代码更简练
    count: state => state.count,

    // 传字符串参数 'count' 等同于 `state => state.count`
    countAlias: 'count',

    // 为了能够使用 `this` 获取局部状态，必须使用常规函数
    countPlusLocalState (state) {
      return state.count + this.localCount
    }
  })
}
--------------
//当映射的计算属性的名称与 state 的子节点名称相同时，我们也可以给 mapState 传一个字符串数组
computed: mapState([
  // 映射 this.count 为 store.state.count
  'count'
])
--------------
computed: {
  localComputed () { /* ... */ },
  // 使用对象展开运算符将此对象混入到外部对象中
  ...mapState({
    // ...
  })
}
```
#### Getter
如果有多处都需要从store中派生（进行二次处理）出一些状态，那么可以使用getter（store 的计算属性，依赖更新）
```js
getters: {
    //state 作为其第一个参数
    doneTodos: state => {
      return state.todos.filter(todo => todo.done)
    },
    //接受其他 getter 作为第二个参数
    doneTodosCount: (state, getters) => {
    return getters.doneTodos.length
  }
}
//调用
store.getters.doneTodosCount // -> 1
```
- mapGetters辅助函数将 store 中的 getter 映射到局部计算属性，用法和mapState一样
```
import { mapGetters } from 'vuex'
computed: {
    // 使用对象展开运算符将 getter 混入 computed 对象中
    ...mapGetters([
      'doneTodosCount',
      'anotherGetter',
      // ...
    ])
}
```
#### Mutation
更改 Vuex 的 store 中的状态的唯一方法是提交 (commit)。建议名字大写。 mutation，但是请勿进行异步操作。
```
mutations: {
    increment (state) {
      // 变更状态
      state.count++
    }
}
//调用
store.commit('increment')
```
- 提交载荷（Payload）
载荷即commit中额外的参数。
```js
mutations: {
  increment (state, n) {
    state.count += n
  }
}
//调用
store.commit('increment', 10)
-------------
//推荐使用对象
mutations: {
  increment (state, payload) {
    state.count += payload.amount
  }
}
store.commit('increment', {
  amount: 10
})
//对象风格提交
store.commit({
  type: 'increment',
  amount: 10
})
```
- mapMutations 辅助函数将组件中的 methods 映射为 store.commit 调用
```
import { mapMutations } from 'vuex'

export default {
  // ...
  methods: {
    ...mapMutations([
      'increment', // 将 `this.increment()` 映射为 `this.$store.commit('increment')`

      // `mapMutations` 也支持载荷：
      'incrementBy' // 将 `this.incrementBy(amount)` 映射为 `this.$store.commit('incrementBy', amount)`
    ]),
    ...mapMutations({
      add: 'increment' // 将 `this.add()` 映射为 `this.$store.commit('increment')`
    })
  }
}
```
#### Action
Action 类似于 mutation，区别在于：
- Action 提交的是 mutation，而不是直接变更状态。
- Action 可以包含任意异步操作。
```
actions: {
    increment (context) {
      context.commit('increment')
    }
}
//分发
store.dispatch('increment')
```
Action 函数接受一个与 store 实例（不是 store 实例本身）具有相同方法和属性的 context（`context.state/context.getters/context.commit`）对象，也可以运用参数结构。
```
actions: {
  increment ({ commit }) {
    commit('increment')
  }
}
```
- 同样支持载荷和对象方式
```
// 以载荷形式分发
store.dispatch('incrementAsync', {
  amount: 10
})

// 以对象形式分发
store.dispatch({
  type: 'incrementAsync',
  amount: 10
})
```
- mapActions 辅助函数将组件的 methods 映射为 store.dispatch 调用
```
import { mapActions } from 'vuex'

export default {
  // ...
  methods: {
    ...mapActions([
      'increment', // 将 `this.increment()` 映射为 `this.$store.dispatch('increment')`

      // `mapActions` 也支持载荷：
      'incrementBy' // 将 `this.incrementBy(amount)` 映射为 `this.$store.dispatch('incrementBy', amount)`
    ]),
    ...mapActions({
      add: 'increment' // 将 `this.add()` 映射为 `this.$store.dispatch('increment')`
    })
  }
}
```
- Promise

```js
actions: {
  actionA ({ commit }) {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        commit('someMutation')
        resolve()
      }, 1000)
    })
  },
  //调用其他action
  actionB ({ dispatch, commit }) {
    return dispatch('actionA').then(() => {
      commit('someOtherMutation')
    })
  }
}
store.dispatch('actionA').then(() => {
  // ...
})
```
- async / await
```
// 假设 getData() 和 getOtherData() 返回的是 Promise

actions: {
  async actionA ({ commit }) {
    commit('gotData', await getData())
  },
  async actionB ({ dispatch, commit }) {
    await dispatch('actionA') // 等待 actionA 完成
    commit('gotOtherData', await getOtherData())
  }
}
```
### Module
将store分割成模块，每个模块拥有自己的 state、mutation、action、getter。
- 获取根节点状态**rootState**
```
actions: {
    incrementIfOddOnRootSum ({ state, commit, rootState }) {
      if ((state.count + rootState.count) % 2 === 1) {
        commit('increment')
      }
    }
}
getters: {
    sumWithRootCount (state, getters, rootState) {
      return state.count + rootState.count
    }
}
```
- 命名空间：所有 getter、action 及 mutation 都会自动根据模块注册的路径调整命名
```
 modules: {
    account: {
      namespaced: true,

      // 模块内容（module assets）
      state: {}, // 模块内的状态已经是嵌套的了，使用 `namespaced` 属性不会对其产生影响
      getters: {},
      actions: {},
      mutations: {}
    }
}
```
- 访问全局state 和 getter
```js
getters: {
  // 在这个模块的 getter 中，`getters` 被局部化了
  // 你可以使用 getter 的第四个参数来调用 `rootGetters`
  someGetter (state, getters, rootState, rootGetters) {}
}
actions: {
    // 在这个模块中， dispatch 和 commit 也被局部化了
    // 他们可以接受 `root` 属性以访问根 dispatch 或 commit
    someAction ({ dispatch, commit, getters, rootGetters }) {}
}
```
#### 带命名空间的绑定函数
- mapState, mapGetters, mapActions 和 mapMutations的第一个参数接受模块的空间名称字符串
```
computed: {
  ...mapState('some/nested/module', {
    a: state => state.a,
    b: state => state.b
  })
},
methods: {
  ...mapActions('some/nested/module', [
    'foo',
    'bar'
  ])
}
```
- createNamespacedHelpers创建
```
import { createNamespacedHelpers } from 'vuex'

const { mapState, mapActions } = createNamespacedHelpers('some/nested/module')

export default {
  computed: {
    // 在 `some/nested/module` 中查找
    ...mapState({
      a: state => state.a,
      b: state => state.b
    })
  },
  methods: {
    // 在 `some/nested/module` 中查找
    ...mapActions([
      'foo',
      'bar'
    ])
  }
}
```
#### 模块动态注册`store.registerModule`
```
// 注册模块 `myModule`
store.registerModule('myModule', {
  // ...
})
// 注册嵌套模块 `nested/myModule`
store.registerModule(['nested', 'myModule'], {
  // ...
})
```
使用`store.unregisterModule(moduleName) `来动态卸载模块