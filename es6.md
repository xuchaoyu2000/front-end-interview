**解构**

ES6允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）。

    ES5
    var a = 1;
    var b = 2;
    var c = 3;

	ES6 
	var [a, b, c] = [1, 2, 3];


> 上面代码表示，可以从数组中提取值，按照对应位置，对变量赋值。
> 本质上，这种写法属于“模式匹配”，只要等号两边的模式相同，左边的变量就会被赋予对应的值


*如果解构不成功，变量的值就等于undefined。*

    var [foo] = [];
    var [foo] = 1;
    var [foo] = 'Hello';
    var [foo] = false;
    var [foo] = NaN;
    var [bar, foo] = [1];
以上几种情况都属于解构不成功，foo的值都会等于undefined。另一种情况是不完全解构。

    var [x, y] = [1, 2, 3];
上面代码中，x和y可以顺利取到值。

*如果对undefined或null进行解构，会报错。*

> 解构赋值不仅适用于var命令，也适用于let和const命令。

    var [v1, v2, ..., vN ] = array;
    let [v1, v2, ..., vN ] = array;
    const [v1, v2, ..., vN ] = array;


**对象的解构赋值**

解构不仅可以用于数组，还可以用于对象。

    var { foo, bar } = { foo: "aaa", bar: "bbb" };
    foo // "aaa"
    bar // "bbb"
对象的解构与数组有一个重要的不同。数组的元素是按次序排列的，变量的取值由它的位置决定；而对象的属性没有次序，变量必须与属性同名，才能取到正确的值。


	var { bar, foo } = { foo: "aaa", bar: "bbb" };
	foo // "aaa"
	bar // "bbb"
	
	var { baz } = { foo: "aaa", bar: "bbb" };
	baz // undefined



----------
**Symbol**

> ** JavaScript 第七种原始类型 **


ES5的对象属性名都是字符串，这容易造成属性名的冲突。比如，你使用了一个他人提供的对象，但又想为这个对象添加新的方法（mixin模式），新方法的名字就有可能与现有方法产生冲突。如果有一种机制，保证每个属性的名字都是独一无二的就好了，这样就从根本上防止属性名的冲突。这就是ES6引入Symbol的原因。

ES6引入了一种新的原始数据类型Symbol，表示独一无二的值。它是JavaScript语言的第七种数据类型，前六种是：Undefined、Null、布尔值（Boolean）、字符串（String）、数值（Number）、对象（Object）。

Symbol值通过Symbol函数生成。这就是说，对象的属性名现在可以有两种类型，一种是原来就有的字符串，另一种就是新增的Symbol类型。凡是属性名属于Symbol类型，就都是独一无二的，可以保证不会与其他属性名产生冲突。


	let s = Symbol();
	
	typeof s
	// "symbol"

Symbol类型的值不能与其他类型的值进行运算，会报错

	var sym = Symbol('My symbol');
	'' + sym
	// TypeError: Cannot convert a Symbol value to a string
但是，Symbol类型的值可以转为字符串。


	String(sym)
	// 'Symbol(My symbol)'
	
	sym.toString()
	// 'Symbol(My symbol)'
symbol的最大特点，就是每一个Symbol都是不相等的，保证产生一个独一无二的值。

	// 创建一个独一无二的 symbol
	 var isMoving = Symbol("isMoving");
	 ...
	 if (element[isMoving]) {
	 smoothAnimations(element);
	 }
	 element[isMoving] = true;

Symbol("isMoving")中的 isMoving 被称作描述。你可以通过 console.log()将它
打印出来，对调试非常有帮助；你也可以用.toString()方法将它转换为字符串呈现；
它也可以被用在错误信息中。

element[isMoving]被称作一个以 symbol 为键（symbol-keyed）的属性。简而言
之，它的名字是 symbol 而不是一个字符串。除此之外，它与一个普通的属性没有什么
区别。

以 symbol 为键的属性属性与数组元素类似，不能被类似 obj.name 的点号法访问，
你必须使用方括号访问这些属性。

获取 symbol 的方法：

调用 Symbol() 这种方式每次调用都会返回一个新的
唯一 symbol。

		var obj = {};
		var foo = Symbol("foo");
		Object.defineProperty(obj, foo, {
		    value: "foobar",
		});
		Object.getOwnPropertyNames(obj)
		// []
		Object.getOwnPropertySymbols(obj)
		// [Symbol(foo)]

使用Object.getOwnPropertyNames方法得不到Symbol属性名

使用Object.getOwnPropertySymbols方法得到所有Symbols
Reflect.ownKeys方法返回所有类型的键名。

		let obj = {
		  [Symbol('my_key')]: 1,
		  enum: 2,
		  nonEnum: 3
		};
		
		Reflect.ownKeys(obj)
		// [Symbol(my_key), 'enum', 'nonEnum']


----------
**Iterator（遍历器）**

遍历器（Iterator）是一种接口规格，任何对象只要部署这个接口，就可以完成遍历操作。
它的作用有两个，一是为各种数据结构，提供一个统一的、简便的接口，
二是使得对象的属性能够按某种次序排列。在ES6中，遍历操作特指for...of循环，
即Iterator接口主要供for...of循环使用。

遍历器提供了一个指针，指向当前对象的某个属性，使用next方法，就可以将指针移动到下一个属性。next方法返回一个包含value和done两个属性的对象。其中，value属性是当前遍历位置的值，done属性是一个布尔值，表示遍历是否结束。下面是一个模拟next方法返回值的例子。

	function makeIterator(array){
	  var nextIndex = 0;
	  return {
	    next: function(){
	      return nextIndex < array.length ?
	        {value: array[nextIndex++], done: false} :
	        {value: undefined, done: true};
	    }
	  }
	}
	
	var it = makeIterator(['a', 'b']);
	
	it.next() // { value: "a", done: false }
	it.next() // { value: "b", done: false }
	it.next() // { value: undefined, done: true }

上面代码定义了一个makeIterator函数，它的作用是返回一个遍历器对象，用来遍历参数数组。next方法依次遍历数组的每个成员，请特别注意，next返回值的构造。

Iterator接口返回的遍历器，原生具备next方法，不用自己部署。所以，真正需要部署的是Iterator接口，让其返回一个遍历器。在ES6中，有三类数据结构原生具备Iterator接口：数组、类似数组的对象、Set和Map结构。


**for...of循环**
	
	var arr = [1,3,5];
	for (let a in arr) {
	  console.log(a); // 1 3 5
	}

for...of循环调用遍历器接口，数组的遍历器接口只返回具有数字索引的属性。

- 这是最简洁、最直接的遍历数组元素的语法
- 这个方法避开了for-in循环的所有缺陷

for-in循环用来遍历对象属性。

for-of循环用来遍历数据—例如数组中的值。

for-of循环也支持字符串遍历，它将字符串视为一系列的Unicode字符来进行遍历：






----------

## 函数的扩展 ##
**函数参数的默认值**

在ES6之前，不能直接为函数的参数指定默认值，只能采用变通的方法。
ES6 允许为函数的参数设置默认值，即直接写在参数定义的后面。

	function log(x, y = 'World') {
	  console.log(x, y);
	}

	function point(x = 0, y = 0) {
	  console.log(x, y);
	}

可以看到，ES6 的写法比 ES5 简洁许多，而且非常自然

除了简洁，ES6 的写法还有两个好处：首先，阅读代码的人，可以立刻意识到哪些参数是可以省略的，不用查看函数体或文档；其次，有利于将来的代码优化，即使未来的版本在对外接口中，彻底拿掉这个参数，也不会导致以前的代码无法运行。

参数变量是默认声明的，所以不能用let或const再次声明。

	function foo(x = 5) {
	  let x = 1; // error
	  const x = 2; // error
	}

上面代码中，参数变量x是默认声明的，在函数体中，不能用let或const再次声明，否则会报错。



**rest参数 (不定参数)**

ES6 引入 rest 参数（形式为“...变量名”），用于获取函数的多余参数，这样就不需要使用arguments对象了。rest 参数搭配的变量是一个数组，该变量将多余的参数放入数组中。
	
	function add(...values) {
	  let sum = 0;
	
	  for (var val of values) {
	    sum += val;
	  }
	
	  return sum;
	}
	
	add(2, 5, 3) // 10


rest 参数中的变量代表一个数组，所以数组特有的方法都可以用于这个变量。下面是一个利用 rest 参数改写数组push方法的例子。

	function push(arr,...data){
        for(var value of data){
            arr.push(value);
        }
    }
	
	var a = [];
	push(a, 1, 2, 3)	//a = [1,2,3]

注意，rest 参数之后不能再有其他参数（即只能是最后一个参数），否则会报错。

	// 报错
	function f(a, ...b, c) {
	  // ...
	}


**箭头函数**

ES6允许使用“箭头”（=>）定义函数。

	var f = v => v;
上面的箭头函数等同于：

	var f = function(v) {
	  return v;
	};

如果箭头函数不需要参数或需要多个参数，就使用一个圆括号代表参数部分。
	
	var f = () => 5;
	// 等同于
	var f = function () { return 5 };

	var sum = (num1, num2) => num1 + num2;
	// 等同于
	var sum = function(num1, num2) {
	  return num1 + num2;
	};
如果箭头函数的代码块部分多于一条语句，就要使用大括号将它们括起来，并且使用return语句返回。

	var sum = (num1, num2) => { return num1 + num2; }
由于大括号被解释为代码块，所以如果箭头函数直接返回一个对象，必须在对象外面加上括号。

	var getTempItem = id => ({ id: id, name: "Temp" });


*箭头函数使得表达更加简洁*
	
	//示例1
	//old
	function (x) {
	  return x * x;
	}
	//简化版
	x => x * x
	
	//示例2
	const isEven = n => n % 2 == 0;
	const square = n => n * n;
