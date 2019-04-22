# Event Loop详解
### 作者：BlackXu  
### 参考：`<<你不知道的JavaScript>> `
## 概念
1. 所有同步任务都在主线程上执行，形成一个执行栈。
2. 异步任务会被放置到`Task Table`，当异步任务有了运行结果，就将该函数移入任务队列。
3. 一旦执行栈中的所有同步任务执行完毕，引擎就会读取任务队列，然后将任务队列中的第一个任务压入执行栈中运行。
4. 主线程不断重复第三步，也就是只要主线程空了，就会去读取任务队列，该过程不断重复，这就是所谓的事件循环。

### 宏任务和微任务
- 宏任务：`script(整体代码)`、`setTimeout`、`setInterval`、`I/O`、事件、`postMessage`、`MessageChannel`、`setImmediate`
- 微任务：`Promise.then`、`MutaionObserver`、`process.nextTick`
- 执行的顺序依次是：`同步任务->微任务->宏任务`

## 各异步函数的分析
### Promise函数
```js
let p = new Promise(resolve => {
  resolve(1);
  Promise.resolve().then(() => console.log(2));
  console.log(4);
}).then(t => console.log(t));
```
- 代码块先将`Promise.resolve()`即2放入微任务队列；然后将4放入同步队列；最后`resolve(1)`执行，根据`then()`，将1放入微任务；
- 执行顺序为`4->2->1`

```js
setTimeout(() => {
  console.log('A');
}, 0);
var obj = {
  func: function() {
    setTimeout(function() {
      console.log('B');
    }, 0);
    return new Promise(function(resolve) {
      console.log('C');
      resolve();
    });
  },
};
obj.func().then(function() {
  console.log('D');
});
```

- 首先将A放入宏任务；然后执行`obj.func()`，将B放入宏任务，将C放入同步任务；最后执行`then()`，将D放入微任务。
- 顺序依次为`C->D->A->B`

### async/await函数
```js
async function foo() {
  //A段
  await bar();
  //B段
}
//...略
```

- 实际上相当于是，A段是同步队列，中间可转化为`Promise.resolve(bar())`，B段是微任务。

```js
async function async1() {
  console.log('A');
  await async2();
  console.log('B');
}
async function async2() {
  console.log('C');
}
console.log('D');
setTimeout(function() {
  console.log('E');
}, 0);
async1();
new Promise(function(resolve) {
  console.log('F');
  resolve();
}).then(function() {
  console.log('G');
});
console.log('H');
```

- 首先将D放入同步序列；然后将E放入宏任务；执行`async1()`，将A放入同步序列，执行`Promise.resolve(asnyc2())`，将C放入同步序列，将B放入微任务；将F放入同步，将G放入微任务；将H放入同步任务。
- 顺序依次为`D->A->C->F->H->B->G->E`

## 例题
```js
const p1 = new Promise((resolve, reject) => {
  console.log('A');
  resolve();
})
  .then(() => {
    console.log('B');
    new Promise((resolve, reject) => {
      console.log('C');
      resolve();
    })
      .then(() => {
        console.log('D');
      })
      .then(() => {
        console.log('E');
      });
  })
  .then(() => {
    console.log('F');
  });

const p2 = new Promise((resolve, reject) => {
  console.log('G');
  resolve();
}).then(() => {
  console.log('H');
});
```

```js
const p1 = new Promise((resolve, reject) => {
  console.log('A'); 
  resolve();
})
  .then(() => {
    console.log('B'); 
    return new Promise((resolve, reject) => {
      console.log('C'); 
      resolve();
    })
      .then(() => {
        console.log('D'); 
      })
      .then(() => {
        console.log('E'); 
      });
  })
  .then(() => {
    console.log('F'); 
  });
```

#### 答案
- `A->G->B->C->H->D->E->F`
- `A->B->C->D->E->F`