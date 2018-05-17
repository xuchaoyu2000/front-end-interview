# 初入Es6
### 作者：black徐 
### 参考 ： [阮一峰：ES6入门](http://es6.ruanyifeng.com/) 
## let与const
### let
- let不存在变量提升，只在let命令所在的代码块内有效。
```js
{
    let a = 10;
    var b = 1;
}
a // ReferenceError: a is not defined.
b //1
```
- 循环计数器，适合let。
- let不允许在相同作用域内，重复声明同一个变量。

```js
var lis = document.getElementsByTagName("li");
for(let i = 0;i < lis.length;i++){
	lis[i].onclick = function(){
		console.log(i);
	}
}
```
### const
- const也用来声明变量，但是声明的是常量 :一旦声明，常量的值如果是简单类型就不能改变。改变会报错，只声明不赋值也会报错。

```js	
const PI = 3.14;
```
- 对于复合类型的数据（主要是对象和数组），变量指向的内存地址，保存的只是一个指针，const只能保证这个指针是固定的，至于它指向的数据结构是不是可变的，就完全不能控制了。

```js
const a = [];
a.push('Hello'); // 可执行
a.length = 0;    // 可执行
a = ['Dave'];    // 报错
const foo = {};// 为 foo 添加一个属性，可以成功
foo.prop = 123;
foo.prop // 123
// 将 foo 指向另一个对象，就会报错
foo = {}; // TypeError: "foo" is read-only
```

## ES6循环数组的方法
### for of
	for (var v of ary){
		console.log(v);
	}
#### 在对象里使用for of,即使用迭代器
	//使用迭代器
	var stu = {
		age:13,
		[Symbol.iterator]:function(){
			return this
		},
		next:function(){
			var done;
			this.age --;
			if(this.age <= 0){
				done = true;
			}
			return {
				done:done,
				value:this.age
			}
		}
	}
	for(var v of stu){
		console.log(v);
	}
	
### forEach
	ary.forEach(function(ele,index){
		console.log(ele,index);	//数组，下标
	});
### map
	var ary1 = ary.map(function(ele){	
		console.log(ele);
		return ele*5;	
	});
	console.log(ary1);
### filter
	var ary2 = ary.filter(function(ele){	
		console.log(ele);
		return true;	
	});
	console.log(ary2);	//与map区别在于，map将返回与数组同等的元素个数，而filter多了个筛选功能，用if语句返回true，不需要的可以写false或不写。
### reduce
	var ary3 = ary.reduce(function(a,b){	
		console.log(a,b);
		return a + b;	
	});			//返回的是函数计算结果
	console.log(ary3);
## 生成器
	function*say(){
		yield "hello";
		yield "hello js";
		yield "hello es6";
	}
	var iterator = say();
	console.log(iterator.next().value);
	console.log(iterator.next().value);
	console.log(iterator.next().value);

	function*say(){
		for(var i = 0;;i++){
			yield i;
		} 
	}
	var iterator = say();
	document.getElementById("btn").onclick = function(){
		document.getElementById("pp").innerHTML = iterator.next().value;
	}
## 反撇号
	var str = "javascript";
	console.log(`this is ${str}`);
## 不定参数和默认参数
	var func = function(str ="默认值",...params){
		console.log(str,params);
	}
	func("a",1,2,3,4);
## 解构
	var ary = ["a","b","c","d"];
	var [a1,a2,a3] = ary;
	console.log(a1,a2,a3);

	var obj = {
		name:"aa",
		age:30
	}
	var {name:na,age} = obj;
	console.log(na,age);
## 优雅使用箭头函数
```js
function (x) {
    return x * x;
}
```
- 简化后:`x => x * x`

**箭头函数相当于匿名函数，并且简化了函数定义。**

#### 多条语句时，不能省略`{}`和`return`。
```js
x => {
    if (x > 0) {
        return x * x;
    }
    else {
        return - x * x;
    }
}
```

#### 当参数不止一个时，需要括号。
```js
(x, y, ...rest) => {
    var i, sum = x + y;
    for (i=0; i<rest.length; i++) {
        sum += rest[i];
    }
    return sum;
}
```

#### 要返回对象时，要避免和函数体的语法冲突，用括号包裹。
```js
x => ({ foo: x })
```

#### 箭头函数内部的this是词法作用域，由上下文确定。
```js
var obj = {
    birth: 1990,
    getAge: function () {
        var b = this.birth; // 1990
        var fn = () => new Date().getFullYear() - this.birth; // this指向obj对象
        return fn();
    }
};
obj.getAge(); // 25
```
- 不在需要以前的hack写法：`var that = this`。
- 用call()或者apply()调用箭头函数时，无法对this进行绑定。
- 不可以使用arguments对象。

```js
var func1 = () =>{
	console.log("....");
}
setTimeout(()=>console.log(1),1000);
```

## Symbol：设定属性值时不会重复

## 集合
### set集合:里面值不允许重复,用于去重
	var set = new set();
	set.add("str");
	set.add(true);
	set.add({name:"a"});
	console.log(set.size);
	for (var v of set){
		console.log(v);
	} 
### map集合
	var map = new map();
	map.set("name","aaa");
	map.set("age",18);
	map.set("gender","男");
	console.log(map.size);
	for(var [key,value] of map){
		console.log(key,value);
	}


### 类:对象的抽象。
	class Student{
		constructor(name,age){
			this.name = name;
			this.age = age;
		}
		show(){
			console.log("名字:"+this.name,"年龄:"+this.age);
		}
	}
	class F36Student extends Student{
		constructor(name,age){
			super(name,age);
		}
		area(){
			console.log("hello");
		}
	}
	var stu1 = new Student("aaaa",18);
	stu1.show();
	var stu2 = new F36Student("bbb",15);
	stu2.show();
	stu2.area();
