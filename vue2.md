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