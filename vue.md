# Vue基础
### 作者：black徐 
## Vue 实例
- el绑定一个实例，与div中id相同，以后可以在此div中写入数据方法等。

``` javascript
<div id="app">
  {{ message }}
</div>
var app = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue!'
  }
})
```



## 生命周期图示
![](https://i.imgur.com/X91QFWu.png)

生命周期就是vue在某一时间点自动执行的函数。
- beforeCreate：初始化事件之后执行。
- created：初始化双向绑定等事件之后执行。可用data值。
- beforeMount：el渲染之后、template渲染之前执行。$mount操作在此。
- mounted：template渲染之后执行。一般异步请求在此。
- beforeUpdate：数据发生改变，还没渲染之前执行。增加方法来改变DOM数据，此处并没有立即更新数据。
- updated：数据发生改变，渲染之后执行。内容与DOM数据同步。
- activated：
- deactivated：
- beforeDestroy：当组件即将被销毁时执行。
- destroyed：当组件被销毁后执行。
- errorCaptured：


## Vue语法

### 文本语法

#### 1.`Mustache`双大括号写法

- 数据绑定最常见的形式就是使用 `Mustache` 语法（双大括号）的文本插值，`Mustache` 标签将会被替代为对应数据对象上` world` 属性的值 ,而且一直会监听`world`的值，一但改变会跟着改变：

``` javascript
<p>hello {{world}}</p>

data () {
  return {
    world : "world"
  }
}
```
#### 2.v-text
- 输出纯文本格式。
``` javascript
<p v-text='text'></p>
data () {
  return {
    text : 'hello'
  }
}
```

#### 3.v-html 
- 输出真正的 HTML格式。
- 你不能使用 v-html 来复合局部模板，因为 Vue 不是基于字符串的模板引擎。
``` javascript
<p v-html='html'></p>
data () {
  return {
    html : `<span style='color : red;'>红色</span>`
  }
}
```

**你的站点上动态渲染的任意 HTML 可能会非常危险，因为它很容易导致 XSS 攻击。请只对可信内容使用 HTML 插值，绝不要对用户提供的内容使用插值。**

#### 4.v-once 
- 通过指令我们可以对文本值进行一次性赋值操作，只进行第一次的数据渲染，如果再次改变值，文本值也不会改变，这会影响到该节点上的其它数据绑定。
`<p v-once>hello {{world}}</p>`


### 属性
#### 1.v-bind:
- 在组件中传递时需要用,其它元素上的绑定属性都需要这个功能。
- 简写：`可以省略v-bind，直接输入：`。
``` javascript
<p :id='id'>id</p>
data () {
  return {
    id ： 2
  }
}
```

#### 2.v-on:
- 使用javascript表达式，比如一个点击事件。
- 简写：`可以省略v-on:  直接输入@`。
``` javascript
<button @click='add'>增加</button>
data () {
  return {
    count : 0
  }
},
methods: {
  add() {
    this.count ++;
  }
}
```

### 条件渲染
#### 1.v-if,v-else,v-else-if
- 切换后文本会注释掉此内容。
- `v-else`，`v-else-if` 也必须紧跟在带 `v-if `或者 `v-else-if` 的元素之后。
``` javascript
<template v-if="show">
  <h1>Title</h1>
  <p>Paragraph 1</p>
  <p>Paragraph 2</p>
</template>
<h1 v-else>No</h1>
<button @click="toggle">toggle</button>
data () {
  return {
    show : true
  }
},
methods: {
  toggle() {
    this.show = !this.show
  }
}
```

#### 2.v-show
- 类似`v-if`，但是不支持 `<template>` 元素，也不支持` v-else`。
- 不同的是带有` v-show` 的元素始终会被渲染并保留在 DOM 中。`v-show` 只是简单地切换元素的 CSS 属性` display`。

``` javascript
<h1 v-show="show">Show</h1>
<button @click="toggle">toggle</button>
data () {
  return {
    show : true
  }
},
methods: {
  toggle() {
    this.show = !this.show
  }
}
```

#### 区别
- `v-if` 是“真正”的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建。

- `v-if` 也是惰性的：如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。

- 相比之下，`v-show` 就简单得多——不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 进行切换。

- if控制DOM存在与否，show控制DOM显示与否。

- 一般来说，`v-if` 有更高的切换开销，而 `v-show` 有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用 `v-show `较好；如果在运行时条件很少改变，则使用` v-if` 较好。

### 列表渲染
#### v-for
- `v-for` 指令需要使用 `item in items` 形式的特殊语法，items 是源数据数组并且 item 是数组元素迭代的别名。
``` javascript
<ul>
  <li v-for="(item, index) in items">
    {{ item.message }} - {{ index }}
  </li>
</ul>
data: {
  items: [
    { message: 'Foo' },
    { message: 'Bar' }
  ]
}
```
- 你也可以用 of 替代 in 作为分隔符。
`<div v-for="item of items"></div>`



## 计算属性，方法与侦听器
### 计算属性computed
- 保证属性不被污染，适用于复杂逻辑。
- 有缓存概念，计算属性只有在它的相关依赖发生改变时才会重新求值。
- getter
- setter

```javascript
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

### 方法methods
- 没有缓存概念，只要页面触发重新渲染就会再次运算。

#### 与计算属性的区别
1. 计算属性页面重新渲染时不会变化，直接读取缓存使用，适用于大量计算和改变频率较低的属性。
2. 方法每次渲染都会重新调用。


### 侦听器watch
- 有缓存，依赖的数据不发生变化，不会运算。
- 比计算属性复杂，所以同时可以用侦听器和计算属性的时候要用计算属性。
- 当需要在数据变化时执行异步或开销较大的操作时，这个方式是最有用的。

```html
<div id="watch-example">
  <p>
    Ask a yes/no question:
    <input v-model="question">
  </p>
  <p>{{ answer }}</p>
</div>
```

```javascript
<script src="https://cdn.jsdelivr.net/npm/axios@0.12.0/dist/axios.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/lodash@4.13.1/lodash.min.js"></script>
<script>
var watchExampleVM = new Vue({
  el: '#watch-example',
  data: {
    question: '',
    answer: 'I cannot give you an answer until you ask a question!'
  },
  watch: {
    // 如果 `question` 发生改变，这个函数就会运行
    question: function (newQuestion, oldQuestion) {
      this.answer = 'Waiting for you to stop typing...'
      this.getAnswer()
    }
  },
  methods: {
    // `_.debounce` 是一个通过 Lodash 限制操作频率的函数。
    // 在这个例子中，我们希望限制访问 yesno.wtf/api 的频率
    // AJAX 请求直到用户输入完毕才会发出。想要了解更多关于
    // `_.debounce` 函数 (及其近亲 `_.throttle`) 的知识，
    // 请参考：https://lodash.com/docs#debounce
    getAnswer: _.debounce(
      function () {
        if (this.question.indexOf('?') === -1) {
          this.answer = 'Questions usually contain a question mark. ;-)'
          return
        }
        this.answer = 'Thinking...'
        var vm = this
        axios.get('https://yesno.wtf/api')
          .then(function (response) {
            vm.answer = _.capitalize(response.data.answer)
          })
          .catch(function (error) {
            vm.answer = 'Error! Could not reach the API. ' + error
          })
      },
      // 这是我们为判定用户停止输入等待的毫秒数
      500
    )
  }
})
</script>
```