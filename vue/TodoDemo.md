# TodoList未模块化简易版 
### 作者：BlackXu 
## 用Vue开发一个TodoList（未模块化简易版）

- 看了基础部分，总要去coding实现下功能，下面去入门最基础的todolist来感受下vue的魅力。原来的js都是直接操作dom，而vue是直接操作数据。

## 需求
- 先来划分下功能需求。直接用div来划分。

```html
<template>
<div id="todolist">
  <div class="top">
    <p>
      <input type="text" >
      <button>add</button>
    </p>
  </div>
  <ul class="center">
    <li>
    </li>
  </ul>
  <div class="bottom"></div>
</div>
</template>
```
- top来放输入框，希望功能有：回车直接添加，点击添加按钮添加，添加完成后清空输入框。
- center放list列表，希望的功能有：checkbox来表示是否finish，中间内容如果finish就变灰中划线，后面跟一个删除按钮直接删除此项。
- bottom放分类和项目剩余，最后有一个按钮可以将所有完成项目删除。

## 初级版
###首先完成top
- 一个input和一个button就够了。把top变成这样：

```html
<div class="top">
  <p>
    <input type="text" 
           class="addInput" 
           v-model="todo" 
           @keyup.enter="addItem"
           placeholder="What to do next?Please use enter to add." 
    >
    <button @click="addItem" class="addButton">ADD</button>
  </p>
</div>
```
- 后面跟上script：
```javascript
export default {
  name: 'todolist',
  data() {
    return {
      todo: ''
    }
  },
  methods: {
    addItem() {
      if(this.todo.trim()){
        this.list.push({content:this.todo,state:false});
        this.todo = "";
      }
    },
  }
}
```

### 完成center：
- 用li来循环v-for指令完成，前面跟一个checkbox来确认finish状态，后面跟一个button来删除，用:key来提高性能。
* 完成checkbox一定要双向绑定。

```html
<div class="top">
    <p>
      <input type="text" 
             class="addInput" 
             v-model="todo" 
             @keyup.enter="addItem"
             placeholder="What to do next?Please use enter to add." 
      >
      <button @click="addItem" class="addButton">ADD</button>
    </p>
  </div>
  <ul class="center">
    <li v-for="(item,index) in list" :key="index" :track-by="index">
      <input type="checkbox" class="checkButton" v-model="item.state" >
      <span :class="{'finished':item.state}" >{{index + 1}}. {{item.content}}</span>
      <button @click="delItem(item)" class="delButton">DEL</button>
    </li>
  </ul>
```
- 后面跟上script和简易样式：

```javascript
export default {
  name: 'todolist',
  data() {
    return {
      todo: '',
      list: []
    }
  },
  methods: {
    addList() {
      if(this.todo){
        this.todos.unshift(this.todo);
        this.todo = "";
      }
    },
    delItem(index) {
      this.todos.splice(this.index,1)
    }
  }
}
<style scoped>

.addInput{
  width: 600px;
}
ul {
  list-style:none;
}
.finished {
  text-decoration: line-through;
}
</style>
```

### 完成bottom：
- 用span来包裹一个项目元素，一个按钮直接清空已经完成的内容。

```html
<p class="bottom">
  <span>{{unFinishedLength}} items left</span>
  <button @click="clearAllCompleted">Clear All Completed</button>
</p>
```
- 最终的html部分
```html
<template>
<div id="todolist">
  <div class="top">
    <p>
      <input type="text" 
             class="addInput" 
             v-model="todo" 
             @keyup.enter="addItem"
             placeholder="What to do next?Please use enter to add." 
      >
      <button @click="addItem" class="addButton">ADD</button>
    </p>
  </div>
  <ul class="center">
    <li v-for="(item,index) in list" :key="index" :track-by="index">
      <input type="checkbox" class="checkButton" v-model="item.state" >
      <span :class="{'finished':item.state}" >{{index + 1}}. {{item.content}}</span>
      <button @click="delItem(item)" class="delButton">DEL</button>
    </li>
  </ul>
  <p class="bottom">
    <span>{{unFinishedLength}} items left</span>
    <button @click="clearAllCompleted">Clear All Completed</button>
  </p>
</div>
</template>
```

- 最终的js部分

```javascript
export default {
  name: 'todolist',
  data() {
    return {
      todo: '',
      list: []
    }
  },
  computed: {
    unFinishedLength() {
      return this.list.filter(todo => !todo.state).length
    }
  },
  methods: {
    addItem() {
      if(this.todo.trim()){
        this.list.push({content:this.todo,state:false});
        this.todo = "";
      }
    },
    delItem(item) {
      this.list.splice(this.list.indexOf(item),1)
    },
    clearAllCompleted() {
      this.list = this.list.filter(todo => todo.state === false)
    }
  }
}
```
### 功能展示
- 没写太多样式，准备在模块化的时候好好写样式。

![](https://i.imgur.com/kTECHyL.png)