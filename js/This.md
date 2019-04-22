# This详解
### 作者：BlackXu 
### 参考：`<<你不知道的JavaScript>> `
## 默认绑定
- 应用默认绑定，`this`指向全局对象，严格模式下，`this`指向`undefined`，`undefined`上没有`this`对象，会抛出错误。

## 隐式绑定
- 函数的调用是在某个对象上触发的，即调用位置上存在上下文对象。典型的形式为：`XX.fn()`。
- 对象属性链中只有最后一层会影响到调用位置。

```js
function sayHi(){
    console.log('Hello,', this.name);
}
var person2 = {
    name: 'Christina',
    sayHi: sayHi
}
var person1 = {
    name: 'YvetteLau',
    friend: person2
}
person1.friend.sayHi(); //'Hello,Christina'
```

### 问题
- 绑定很容易丢失。隐式绑定格式:`XX.fn()`。

```js
function sayHi(){
    console.log('Hello,', this.name);
}
var person = {
    name: 'YvetteLau',
    sayHi: sayHi
}
var name = 'Wiliam';
var Hi = person.sayHi;
Hi();   //'Hello,Wiliam'
```

- 丢失发生在回调函数中。

```js
function sayHi(){
    console.log('Hello,', this.name);
}
var person1 = {
    name: 'YvetteLau',
    sayHi: function(){
        setTimeout(function(){
            console.log('Hello,',this.name);
        })
    }
}
var person2 = {
    name: 'Christina',
    sayHi: sayHi
}
var name='Wiliam';
person1.sayHi();    //默认绑定：'Hello, Wiliam'
setTimeout(person2.sayHi,100);  //隐式绑定丢失：'Hello, Wiliam'
setTimeout(function(){
    person2.sayHi();    //隐式绑定：'Hello, Christina'
},200);
```

## 显式绑定（硬绑定）
- 通过`call,apply,bind`的方式，显式的指定`this`所指向的对象。
- `call`和`apply`的作用一样，只是传参方式不同（`call`传参需要详细罗列，`apply`传参只需要数组）。`call`和`apply`都会执行对应的函数，而`bind`方法不会。
- 也会有绑定丢失。

```js
function sayHi(){
    console.log('Hello,', this.name);
}
var person = {
    name: 'YvetteLau',
    sayHi: sayHi
}
var name = 'Wiliam';
var Hi = function(fn) {
    fn();
}
Hi.call(person, person.sayHi);  //'Hello, Wiliam'
```

- 修改一下后：

```js
function sayHi(){
    console.log('Hello,', this.name);
}
var person = {
    name: 'YvetteLau',
    sayHi: sayHi
}
var name = 'Wiliam';
var Hi = function(fn) {
    fn.call(this);
}
Hi.call(person, person.sayHi);  //'Hello, YvetteLau'
```

## new绑定
- 使用`new`来调用函数的时候，新对象会绑定到这个函数的`this`上。

## 绑定优先级
- new绑定 > 显式绑定 > 隐式绑定 > 默认绑定

## 绑定例外
- 如果我们将`null`或者是`undefined`作为`this`的绑定对象传入`call`、`apply`或者是`bind`,这些值在调用时会被忽略，实际应用的是默认绑定规则。

### 箭头函数
- 函数体内的`this`对象，继承的是外层代码块的`this`。
- 不可以当作构造函数，也就是说，不可以使用`new`命令，否则会抛出一个错误。
- 不可以使用`arguments`对象，该对象在函数体内不存在。如果要用，可以用` rest `参数代替。
- 不可以使用`yield`命令，因此箭头函数不能用作` Generator `函数。
- 箭头函数没有自己的this，所以不能用`call()、apply()、bind()`这些方法去改变`this`的指向。

```js
var obj = {
    hi: function(){
        console.log(this);
        return ()=>{
            console.log(this);
        }
    },
    sayHi: function(){
        return function() {
            console.log(this);
            return ()=>{
                console.log(this);
            }
        }
    },
    say: ()=>{
        console.log(this);
    }
}
let hi = obj.hi();  //输出obj对象
hi();               //运行return语句，输出obj对象
let sayHi = obj.sayHi();
let fun1 = sayHi(); //输出window
fun1();             //运行return语句，输出window
obj.say();          //输出window
```

### 例题
```js
var number = 5;
var obj = {
    number: 3,
    fn: (function () {
        var number;
        this.number *= 2;
        number = number * 2;
        number = 3;
        return function () {
            var num = this.number;
            this.number *= 2;
            console.log(num);
            number *= 3;
            console.log(number);
        }
    })()
}
var myFun = obj.fn;
myFun.call(null);
obj.fn();
console.log(window.number);
```

- 结果为：`10,9,3,27,20`