# 在FreeCodeCamp中学习的日子
### 作者：BlackXu 
## 算法练习
**看了这个代码你能收获什么？**
- 能在算法中获得与前端的平衡，并收获计算机算法的兴趣。
- 不断迭代代码，收获更多前端技术。
- 本博文大量采用ES5/6语法，充分使用箭头函数，let/const等。

## 基础算法
## 1.翻转字符串
**先把字符串转化成数组，再借助数组的reverse方法翻转数组顺序，最后把数组转化成字符串。**
```js
function reverseStr(str) { 
	return str.split("").reverse().join(""); 
}
console.log(reverseString("Greetings from Earth")); //"htraE morf sgniteerG"
```

## 2.计算一个整数的阶乘 
**如果用字母n来代表一个整数，阶乘代表着所有小于或等于n的整数的乘积。**
```js
function factorialize (num) { 
   return num < 0 ? -1 : (num === 0 || num === 1) ? 1 : num * factorialize(num - 1); 
}
console.log(factorialize(5)); //120
```

## 3.检查回文字符串
**如果给定的字符串是回文，返回true，反之，返回false。如果一个字符串忽略标点符号、大小写和空格，正着读和反着读一模一样，那么这个字符串就是palindrome(回文)。注意你需要去掉字符串多余的标点符号和空格，然后把字符串转化成小写来验证此字符串是否为回文。**
```js
function palindrome(str) {
  str = str.replace(/[\ |\~|\`|\!|\@|\#|\$|\%|\^|\&|\*|\(|\)|\-|\_|\+|\=|\||\\|\[|\]|\{|\}|\;|\:|\"|\'|\,|\<|\.|\>|\/|\?]/g,"").toLowerCase();
  return str === str.split("").reverse().join("") ? true : false; 
}
console.log(palindrome("never odd or even")); //true
console.log(palindrome("0_0 (: /-\ :) 0-0"));  //true
```

## 4.找出最长单词
**在句子中找出最长的单词，并返回它的长度。**
```js
function findLongestWord(str) {
  let max = 0;
  for(let v of str.split(" ")){
  	if(max < v.length){
  		max = v.length
  	}
  };
  return max;
}
console.log(findLongestWord("The quick brown fox jumped over the lazy dog")); //6
```

## 5.句中单词首字母大写
**确保字符串的每个单词首字母都大写，其余部分小写。**
```js
function titleCase(str) {
  return str.toLowerCase().replace(/( |^)[a-z]/g, F => F.toUpperCase());
}
console.log(titleCase("HERE IS MY HANDLE HERE IS MY SPOUT")); //"Here Is My Handle Here Is My Spout"
```

## 6.找出多个数组中的最大数
**大数组中包含了4个小数组，分别找到每个小数组中的最大值，然后把它们串联起来，形成一个新数组。**
```js
function largestOfFour(arr) {
  const max = [];
  for(let i= 0;i < arr.length;i++){
    arr[i].sort((a,b) => b - a);
    max.push(arr[i][0]);
  }
  return max;
}
console.log(largestOfFour([[4, 5, 1, 3], [13, 27, 18, 26], [32, 35, 37, 39], [1000, 1001, 857, 1]]));//[5,27,39,1001]
```

## 7.检查字符串结尾
**判断一个字符串(str)是否以指定的字符串(target)结尾。如果是，返回true;如果不是，返回false。**
```js
function confirmEnding(str, target) {
  return target === str.slice(str.length -target.length)
}
console.log(confirmEnding("He has to give me a new name", "me")); //true
```
或者：
```js
function confirmEnding(str, target) {
  return target === str.substr(-target.length,target.length)
}
console.log(confirmEnding("He has to give me a new name", "me")); //true
```

## 8.重复输出字符串
**重复一个指定的字符串 num次，如果num是一个负数则返回一个空字符串。**
```js
function repeat(str, num) {
  let str1 = str;
  for(let i = 1;i < num;i++){
  	str += str1;
  }
  return num > 0 ? str : "";
}
console.log(repeat("abc", 3));//"abcabcabc"
```

## 9.截断字符串
**如果字符串的长度比指定的参数num长，则把多余的部分用`...`来表示。切记，插入到字符串尾部的三个点号也会计入字符串的长度。但是，如果指定的参数num小于或等于3，则添加的三个点号不会计入字符串的长度。**
```js
function truncate(str, num) {
    return str = num >= str.length ? str :  num > 3 ? str.slice(0,num - 3) + "..." : str.slice(0,num) + "...";
}
console.log(truncate("A-tisket a-tasket A green and yellow basket", 11));  //"A-tisket..."
```

## 10.分割数组
**把一个数组arr按照指定的数组大小size分割成若干个数组块。**
```js
function chunk(arr, size) {
  const newArr = [];
  for(let i = 0;i < arr.length;i += size){
    newArr.push(arr.slice(i,i + size)); 
  }
  return newArr;
}
console.log(chunk([0, 1, 2, 3, 4, 5, 6], 3));//[[0, 1, 2], [3, 4, 5], [6]]
```

## 11.截断数组
**返回一个数组被截断n个元素后还剩余的元素，截断从索引0开始。**
```js
function slasher(arr, howMany) {
  return arr.slice(howMany);
}
console.log(slasher([1, 2, 3], 2)); //[3]
```

## 12.比较字符串
**如果数组第一个字符串元素包含了第二个字符串元素的所有字符，函数返回true。举例，["hello", "Hello"]应该返回true,["hello", "hey"]应该返回false，["Alien", "line"]应该返回true。**
```js
function mutation(arr) {
  for(let i = 0;i < arr[1].length;i++){
    if(arr[0].toLowerCase().indexOf(arr[1][i].toLowerCase()) === -1){
      return false;
    }
  }
  return true;
}
mutation(["Alien", "line"]) //true
```

## 13.过滤数组假值
**删除数组中的所有假值。在JavaScript中，假值有`false`、`null`、`0`、`""`、`undefined` 和 `NaN`。**
```js
function bouncer(arr) {
  return arr.filter(Boolean);
}
console.log(bouncer([7, "ate", "", false, 9]));//[7,"ate",9]
```

## 14.摧毁数组
**实现一个摧毁(destroyer)函数，第一个参数是待摧毁的数组，其余的参数是待摧毁的值。**
```js
function destroyer(arr) {
  for(let i = 0;i < arr.length;i++){
	for(let j = 1;j <= arguments.length;j++){
		if(arr[i] === arguments[j] ){
      		arr.splice(i--,1);
			break;
    	}
	}
  }
  return arr;
}
console.log(destroyer([1, 2, 3, 1, 2, 3], 2, 3));//[1,1]
console.log(destroyer(["tree", "hamburger", 53], "tree", 53));["hamburger"]
```
或者：
```js
function destroyer(arr) {
  const args = [];
  for(let i = 1; i < arguments.length; i++){
    args.push(arguments[i]);
  }
  const temp = arr.filter(function(item,index,array){
    return args.indexOf(item) < 0;
  });
  return temp;
}
console.log(destroyer([1, 2, 3, 1, 2, 3], 2, 3));//[1,1]
console.log(destroyer(["tree", "hamburger", 53], "tree", 53));["hamburger"]
```

## 15.数组排序并找出元素索引
**先给数组排序，然后找到指定的值在数组的位置，最后返回位置对应的索引。**
```js
function where(arr, num) {
  arr.sort((a,b) => a - b);
  for(let i = 0;i < arr.length;i++){
    if(num <= arr[i]){
      return i;
      break;
    }
  }
  if(num > arr[arr.length - 1]){
    return arr.length;
  }
}
console.log(where([5, 3, 20, 3], 5)); //2
console.log(where([2, 5, 10], 15));	//3
```

## 16.凯撒密码
**一个常见的案例就是ROT13密码，字母会移位13个位置。由'A' ↔ 'N', 'B' ↔ 'O'，以此类推。写一个ROT13函数，实现输入加密字符串，输出解密字符串。所有的字母都是大写，不要转化任何非字母形式的字符(例如：空格，标点符号)，遇到这些特殊字符，跳过它们。**
```js
function rot13(str) { 
  let str1="";
  for(let v of str){
    str1 += v.charCodeAt() > 77 ? String.fromCharCode(v.charCodeAt() - 13) : v.charCodeAt() > 64 ?  String.fromCharCode(v.charCodeAt() + 13) : v;
  }
  return str1;
}
console.log(rot13("SERR PBQR PNZC"));//"FREE CODE CAMP"
```

## 进阶算法
## 1. 求和
**传递给你一个包含两个数字的数组。返回这两个数字和它们之间所有数字的和。**
```js
function sumAll(arr) {
  return (arr[0] + arr[1]) * (Math.abs(arr[0] - arr[1] + 1)) / 2;
}
console.log(sumAll([10, 1]));  //55
```

## 2.比较
**比较两个数组，然后返回一个新数组，该数组的元素为两个给定数组中所有独有的数组元素。换言之，返回两个数组的差异。**
```js
function diff(arr1,arr2){
  const newArr = [];
  arr1.forEach( v => {
    if(arr2.indexOf(v) === -1){
      newArr.push(v);
    }
  });
  arr2.forEach( v => {
    if(arr1.indexOf(v) === -1){
      newArr.push(v);
    }
  });
  return newArr;
}
console.log(diff([1, 2, 3, 4, 5], [1, 2, 3, 4, 5])); //[]
console.log(diff([1, "calf", 3, "piglet"], [7, "filly"]));  //[1, "calf", 3, "piglet", 7, "filly"]
```

## 3.罗马数字转换
**将给定的数字转换成罗马数字;所有返回的罗马数字都应该是大写形式。**
```js
function convert(num){
  let a,b,c,d;  //分别表示个十百千位
  a = parseInt(num / 1000);
  b = parseInt(num / 100 % 10);
  c = parseInt(num / 10 % 10);
  d = parseInt(num % 10);
  const sum = [];
  for(let i = 0;i < a;i++){
    sum.push('M');
  }
  switch(b){
    case 1: sum.push('C');break;  
    case 2: sum.push('CC');break;   
    case 3: sum.push('CCC');break;  
    case 4: sum.push('CD');break;   
    case 5: sum.push('D');break;   
    case 6: sum.push('DC');break;   
    case 7: sum.push('DCC');break;  
    case 8: sum.push('DCCC');break;  
    case 9: sum.push('CM');break;  
    default: break;  
  }
  switch(c){
    case 1: sum.push('X');break;  
    case 2: sum.push('XX');break;   
    case 3: sum.push('XXX');break;  
    case 4: sum.push('XL');break;   
    case 5: sum.push('L');break;   
    case 6: sum.push('LX');break;   
    case 7: sum.push('LXX');break;  
    case 8: sum.push('LXXX');break;  
    case 9: sum.push('XC');break;  
    default: break;  
  }
  switch(d){
    case 1: sum.push('I');break;  
    case 2: sum.push('II');break;   
    case 3: sum.push('III');break;  
    case 4: sum.push('IV');break;   
    case 5: sum.push('V');break;   
    case 6: sum.push('VI');break;   
    case 7: sum.push('VII');break;  
    case 8: sum.push('VIII');break;  
    case 9: sum.push('IX');break;   
    default: break;  
  }
  return sum.join("");
}
console.log(convert(2864));    //MMDCCCLXIV
```


## 4.找到匹配对象属性
**写一个 function，它遍历一个对象数组（第一个参数）并返回一个包含相匹配的属性-值对（第二个参数）的所有对象的数组。如果返回的数组中包含 source 对象的属性-值对，那么此对象的每一个属性-值对都必须存在于 collection 的对象中。**
```js
function where(collection, source) {
  let arr = [];
  const key = Object.keys(source);
  arr = collection.filter(item => {
    for(let v of key){
      if(!item.hasOwnProperty(v) || item[v] !== source[v]){
        return false;
      }
    }
    return true;
  });
  return arr;
}
console.log(where([{ first: "Romeo", last: "Montague" }, { first: "Mercutio", last: null }, { first: "Tybalt", last: "Capulet" }], { last: "Capulet" })); //[{first: "Tybalt", last: "Capulet"}]
```
## 5.查找并替换
- 使用给定的参数对句子执行一次查找和替换，然后返回新句子。
- 第一个参数是将要对其执行查找和替换的句子。
- 第二个参数是将被替换掉的单词（替换前的单词）。
- 第三个参数用于替换第二个参数（替换后的单词）。
- 注意：替换时保持原单词的大小写。例如，如果你想用单词 "dog" 替换单词 "Book" ，你应该替换成 "Dog"。

```js
function myReplace(str, before, after) {
  if(before[0] === before[0].toUpperCase()){
    after = after[0].toUpperCase() + after.slice(1); 
  }
  return str.replace(before, after);
}
myReplace("He is Sleeping on the couch", "Sleeping", "sitting"); //He is Sitting on the couch
```

## 6.隐语 
- 把指定的字符串翻译成 pig latin。
- Pig Latin 把一个英文单词的第一个辅音或辅音丛（consonant cluster）移到词尾，然后加上后缀 "ay"。
- 如果单词以元音开始，你只需要在词尾添加 "way" 就可以了。

```js
function translate(str) {
  const arr = ["a","e","i","o","u"];
  if(arr.indexOf(str[0]) !== -1){
    return str + "way";
  }
  while(arr.indexOf(str[0]) === -1){
    str = str.substr(1) + str.substr(0,1);
  }
  return str + "ay";
}
console.log(translate("glove")); //"oveglay"
```

## 7.DNA链配对  
- DNA 链缺少配对的碱基。依据每一个碱基，为其找到配对的碱基，然后将结果作为第二个数组返回。
- Base pairs（碱基对） 是一对 AT 和 CG，为给定的字母匹配缺失的碱基。
- 在每一个数组中将给定的字母作为第一个碱基返回。
- 例如，对于输入的 GCG，相应地返回 [["G", "C"], ["C","G"],["G", "C"]]
- 字母和与之配对的字母在一个数组内，然后所有数组再被组织起来封装进一个数组。

```js
function pair(str) {
  const arr = [];
  for(let v of str){
	switch(v){
	  case "C" : arr.push(["C","G"]);;break;
	  case "G" : arr.push(["G","C"]);;break;
	  case "A" : arr.push(["A","T"]);;break;
      case "T" : arr.push(["T","A"]);;break;
	  default: break;
	}
  }
  return arr;
}
console.log(pair("GCG")); // [["G", "C"], ["C","G"],["G", "C"]]
```

## 8.缺失的字母
**从传递进来的字母序列中找到缺失的字母并返回它，如果所有字母都在序列中，返回 undefined。**
```js
function fearNotLetter(str) {
  const arr = [];
  let str1 ="";
  for(let v of str){
    arr.push(v.charCodeAt());
  }
  for(let i= 0;i<arr.length -1;i++){
    if(arr[i + 1] - arr[i] !== 1){
      str1 += String.fromCharCode(arr[i]+1);
    }
  }
  if(!str1){
    return undefined;
  }
  return str1;
}
console.log(fearNotLetter("abce")); //"d"
```

## 9.检测布尔值
**检查一个值是否是基本布尔类型，并返回 true 或 false，基本布尔类型即 true 和 false。**
```js
function boo(bool) {
  return bool === Boolean(bool)
}
console.log(boo(null));//false
```

## 10.联合排序
- 写一个方法，传入两个或两个以上的数组，返回一个以给定的原始数组排序的不包含重复值的新数组。
- 换句话说，所有数组中的所有值都应该以原始顺序被包含在内，但是在最终的数组中不包含重复值。
- 非重复的数字应该以它们原始的顺序排序，但最终的数组不应该以数字顺序排序。

```js
function unite(){
  let arr = Array.from(arguments);
  const concatArr = arr.reduce((pre,cur) => pre.concat(cur));
  return arr = concatArr.filter((v,i) => concatArr.indexOf(v) === i);
}
console.log(unite([1, 3, 2], [1, [5]], [2, [4]])); //[1, 3, 2, [5], [4]]
```

## 11.转换HTML实体
**将字符串中的字符 &、<、>、" （双引号）, 以及 ' （单引号）转换为它们对应的 HTML 实体。** 
```js
function convert(str){
  const reg = {"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&apos;"},arr = str.match(/[&<>"']/g);
  if(arr){
    for(let v of arr){
      str = str.replace(v,reg[v]);
    }
  }
  return str;
}
console.log(convert("Dolce & Gabbana")); //Dolce &​amp; Gabbana
```

## 12.转换连字符
**将字符串转换为 spinal case。Spinal case 是 all-lowercase-words-joined-by-dashes 这种形式的，也就是以连字符连接所有小写单词。**
```js
let spinalCase = str => str.replace(/\s|_/g,'-').replace(/([a-z])([A-Z])/g,'$1-$2').toLowerCase();  
console.log(spinalCase('This Is Spinal Tap')); //'this-is -spinal-tap'
```

## 13.斐波纳契奇数求和
- 给一个正整数num，返回小于或等于num的斐波纳契奇数之和。
- 斐波纳契数列中的前几个数字是 1、1、2、3、5 和 8，随后的每一个数字都是前两个数字之和。
- 例如，sumFibs(4)应该返回 5，因为斐波纳契数列中所有小于4的奇数是 1、1、3。

**提示：此题不能用递归来实现斐波纳契数列。因为当num较大时，内存会溢出，推荐用数组来实现。**
```js
function sumFibs(num) {
  let arr = [1, 1],temp = 0,sum = 2;
  while(true){
    temp = arr[0] + arr[1];
    if(temp > num){
      return sum;
    }
    if(temp % 2 !== 0){
      sum += temp;
    }
    arr[0] = arr[1];
    arr[1] = temp;
  }
}
console.log(sumFibs(4)); //5
```

## 14.质数求和 
- 求小于等于给定数值的质数之和。
- 只有 1 和它本身两个约数的数叫质数。例如，2 是质数，因为它只能被 1 和 2 整除。1 不是质数，因为它只能被自身整除。
- 给定的数不一定是质数。

```js
let sumPrimes = num => {
  let answer = 0;
  for(let i = 2; i <= num; i++){   
    if(isPrime(i)){
      answer += i;
    }
  }
  return answer;
};
let isPrime = val => {
  for(let i = 2; i < val; i++){
    if(val % i === 0){
      return false;
    }
  }
  return true;
}
console.log(sumPrimes(10)); //17
```

## 15.最小公倍数
- 找出能被两个给定参数和它们之间的连续数字整除的最小公倍数。
- 范围是两个数字构成的数组，两个数字不一定按数字顺序排序。
- 例如对 1 和 3 —— 找出能被 1 和 3 和它们之间所有数字整除的最小公倍数。

```js
function smallestCommons(arr) {
  arr = arr.sort((a,b) => a - b);
  let num = arr[0];
  for(let i = arr[0] + 1;i <= arr[1];i++){
     num *= i / gbs(num,i);
  }
  return num;
}
let gbs = (m,n) =>  m % n === 0 ? n : gbs(n,m % n);
console.log(smallestCommons([13,1])); //360360
```

## 16.发现者 
**写一个方法，它遍历数组，并返回数组中第一个满足方法的返回值的元素。举个例子，如果数组为 [1, 2, 3]，方法为 function(num) {return num === 2; }，那么 find 的返回值应为 2。**
```js
let find = (arr, func) => {
  arr = arr.filter(func);
  return arr[0];
};
console.log(find([1, 5, 8, 9], num =>  num % 2 === 0 )); //8
```

## 17.丢弃数组
- 让我们来丢弃数组的元素，从左边开始，直到回调函数return true就停止。
- 第二个参数，func，是一个函数。用来测试数组的第一个元素，如果返回fasle，就从数组中抛出该元素(注意：此时数组已被改变)，继续测试数组的第一个元素，如果返回fasle，继续抛出，直到返回true。
- 最后返回数组的剩余部分，如果没有剩余，就返回一个空数组。

```js
let drop = (arr, func) => {
  let len = arr.length;
  for(let i = 0;i < len;i++){
    if(!func(arr[0])){
      arr.shift();
    }
  }
  return arr;  
};
console.log(drop([1, 2, 3], n => n > 3)); //[]
```

## 18.压服 
**对嵌套的数组进行扁平化处理。你必须考虑到不同层级的嵌套。**
```js
let steamroller = arr => {
  let res = [];
  for(let i = 0;i < arr.length;i++){
    Array.isArray(arr[i]) ? res = res.concat(steamroller(arr[i])) : res.push(arr[i]);
  }  
  return res;
};
console.log(steamroller([1, [2], [3, [[4]]]])); //[1,2,3,4]
```

## 19.二进制代理 
**传入二进制字符串，翻译成英语句子并返回。二进制字符串是以空格分隔的。**
```js
let binaryAgent = str => {
  let str1 = str.split(" ").map( v => parseInt(v,2));
  str = "";
  str1.forEach( v => str += String.fromCharCode(v) );
  return str;
};
console.log(binaryAgent("01000001 01110010 01100101 01101110 00100111 01110100 00100000 01100010 01101111 01101110 01100110 01101001 01110010 01100101 01110011 00100000 01100110 01110101 01101110 00100001 00111111")); //Aren't bonfires fun!?
```

## 20.一切都是真的  
**完善编辑器中的every函数，如果集合(collection)中的所有对象都存在对应的属性(pre)，并且属性(pre)对应的值为真。函数返回ture。反之，返回false。记住：你只能通过中括号来访问对象的变量属性(pre)。**
```js
function every(collection, pre) {
  return collection.every(v => v[pre]);
}
every([{"user": "Tinky-Winky", "sex": "male"}, {"user": "Dipsy", "sex": "male"}, {"user": "Laa-Laa", "sex": "female"}, {"user": "Po", "sex": "female"}], "sex"); //true
```

## 21.可选参数
- 创建一个计算两个参数之和的 function。如果只有一个参数，则返回一个 function，该 function 请求一个参数然后返回求和的结果。
- 例如，add(2, 3) 应该返回 5，而 add(2) 应该返回一个 function。
- 调用这个有一个参数的返回的 function，返回求和的结果：
- var sumTwoAnd = add(2);
- sumTwoAnd(3) 返回 5。
- 如果两个参数都不是有效的数字，则返回 undefined。

```js
function add() {
  if(typeof arguments[0] === "number" && typeof arguments[1] === "number"){
    return arguments[0] + arguments[1];
  }
  else if(arguments.length === 1 && typeof arguments[0] === "number"){
    return v => {if(typeof v === "number")return arguments[0] + v;};
  }
}
console.log(add(2,3)); //5
```

## 高级算法
## 1.确认美国电话号码
**如果传入字符串是一个有效的美国电话号码，则返回 true。**
```js
let telephoneCheck = str => /^1? ?(\(\d{3}\)|\d{3})[ |-]?\d{3}[ |-]?\d{4}$/.test(str);
telephoneCheck("555-555-5555"); 
```

## 2.对称差分
- 创建一个函数，接受两个或多个数组，返回所给数组的 对等差分`(symmetric difference) (△ or ⊕)`数组。
- 给出两个集合 (如集合` A = {1, 2, 3}` 和集合` B = {2, 3, 4})`， 而数学术语 `"对等差分"` 的集合就是指由所有只在两个集合其中之一的元素组成的集合`(A △ B = C = {1, 4})`。 对于传入的额外集合 (如 `D = {2, 3}`)， 你应该安装前面原则求前两个集合的结果与新集合的对等差分集合` (C △ D = {1, 4} △ {2, 3} = {1, 2, 3, 4})`。

```js
function sym() {
  let arr = [];
  for(let v of arguments){
    arr.push([...new Set(v)]);
  }
  arr.reduce((a,b) => {
    a.forEach(v => b.indexOf(v) === -1 ? b.push(v) : b.splice(b.indexOf(v),1));
    return b;
  });
  return arr[arr.length - 1];
}
console.log(sym([1, 2, 2, 3], [5, 2, 1, 4])); //[5,4,3]
```

## 3.精确变化
- 设计一个收银程序 `checkCashRegister()`，其把购买价格`(price)`作为第一个参数 ， 付款金额 `(cash)`作为第二个参数， 和收银机中零钱 `(cid) `作为第三个参数。
- ` cid` 是一个二维数组，存着当前可用的找零。
- 当收银机中的钱不够找零时返回字符串 `"Insufficient Funds"`。 如果正好则返回字符串 `"Closed"`。
- 否则， 返回应找回的零钱列表，且由大到小存在二维数组中。

```js
let checkCashRegister = (price, cash, cid) => {
  let remainder = cash - price,arr = [],j = 0,total = 0 ,value = remainder;
  const array = [0.01,0.05,0.1,0.25,1,5,10,20,100];
  for(let i = cid.length - 1;i >= 0;i--){
    total += cid[i][1];
    if(remainder > array[i] && cid[i][1] > 0){
      let c = parseInt(remainder / array[i]);
      if(remainder > cid[i][1]){
        remainder -= cid[i][1];
      }else{
        remainder -= c * array[i];
        cid[i][1] = c * array[i];
      }
      remainder = remainder.toFixed(2);
      arr[j++] = cid[i];
    }   
  }
  if(total === value){
    return "Closed";
  }else if(total < value || remainder != 0){
    return "Insufficient Funds";
  }
  return arr;
};
checkCashRegister(19.50, 20.00, [["PENNY", 1.01], ["NICKEL", 2.05], ["DIME", 3.10], ["QUARTER", 4.25], ["ONE", 90.00], ["FIVE", 55.00], ["TEN", 20.00], ["TWENTY", 60.00], ["ONE HUNDRED", 100.00]]); 
```

## 4.库存更新
**依照一个存着新进货物的二维数组，更新存着现有库存(在 arr1 中)的二维数组。 如果货物已存在则更新数量 。 如果没有对应货物则把其加入到数组中，更新最新的数量。 返回当前的库存数组，且按货物名称的字母顺序排列。**
```js
let updateInventory = (arr1, arr2) => {
  arr2.forEach( v => {
    let i = hasValue(v[1],arr1);
    i === undefined ? arr1.push(v) : arr1[i][0] += v[0];
  });
  return arr1.sort((a,b) => a[1].charCodeAt(0) - b[1].charCodeAt(0));
};
let hasValue = (str,arr) => {
   for(let i in arr){
    if(arr[i][1] === str) return i;
   }
};
updateInventory([[21, "Bowling Ball"], [2, "Dirty Sock"], [1, "Hair Pin"], [5, "Microphone"]], [[2, "Hair Pin"], [3, "Half-Eaten Apple"], [67, "Bowling Ball"], [7, "Toothpaste"]]);
```

## 5.没有连续重复字符
- 把一个字符串中的字符重新排列生成新的字符串，返回新生成的字符串里没有连续重复字符的字符串个数。连续重复只以单个字符为准
- 例如, aab 应该返回 2 因为它总共有6中排列` (aab, aab, aba, aba, baa, baa)`， 但是只有两个 `(aba and aba)`没有连续重复的字符 (在本例中是 a)。

```js
let permAlone = str => {
  const reg = /(.)\1+/g,arr = str.split('') , array = [];
  let swap = (i1, i2) => [arr[i1],arr[i2]] = [arr[i2],arr[i1]];
  let generate = len => {
    if (len === 1) {
      array.push(arr.join(''));
    } else {
      for (let i = 0; i < len; i++) {
        generate(len - 1);
        swap(len % 2 ? 0 : i, len - 1);
      }
    }
  };
  generate(arr.length);
  return array.filter( str => !str.match(reg) ).length;
};
permAlone('aab');
```

## 6.让日期区间更友好
- 把常见的日期格式如:`YYYY-MM-DD` 转换成一种更易读的格式。
- 易读格式应该是用月份名称代替月份数字，用序数词代替数字来表示天 (1st 代替 1)。
- 记住不要显示那些可以被推测出来的信息： 如果一个日期区间里结束日期与开始日期相差小于一年，则结束日期就不用写年份了；在这种情况下，如果月份开始和结束日期如果在同一个月，则结束日期月份也不用写了。
- 另外, 如果开始日期年份是当前年份，且结束日期与开始日期小于一年，则开始日期的年份也不用写。

```js
let makeFriendlyDates = arr => {  
  const months = {"01" : "January","02" : "February","03" : "March", "04" : "April","05" : "May", "06" : "June", "07" : "July","08" : "August", "09" : "September","10" : "October", "11" : "November","12" : "December"  };  
  let date1 = arr[0].split("-"); 
  let date2 = arr[1].split("-");
  let date = new Date();  
  let dateChange = day => {  
    if(day[0] === "0"){  
      day = day.substr(1);  
      if(day === "1") return day + "st";  //01->1st
      if(day === "2") return day + "nd";  //02->2nd
      if(day === "3") return day + "rd";  //03->3rd
      else return day + "th";  
    }  
    else{  
      if(day.substr(1,1) === "1" && day.substr(0,1) === "2") return day + "st";  //21->21st
      if(day.substr(1,1) === "1" && day.substr(0,1) === "3") return day + "st";  //31->31st
      if(day.substr(1,1) === "2" && day.substr(0,1) === "2") return day + "nd";  //22->22nd
      if(day.substr(1,1) === "3" && day.substr(0,1) === "2") return day + "rd";  //23->23rd
      else return day + "th";   
    }    
  };  
  let sameYear = (d1, d2) => {  
    if(d2[0] - d1[0] > 1) return false;  
    else{  
      if(d1[0] === d2[0]) return true;   
      else{  //判断相减为1的时候
        if(d2[1] > d1[1]) return false;  
        if(d2[1] < d1[1]) return true; //判断在一年以内返回true
        else return d2[2] < d1[2] ? true : false; //判断是否在一年以内
      }  
    }  
  };  
  if (sameYear(date1, date2)) { 
    if(date1[0] === date2[0]){  
      if(date1[1] === date2[1]){  //月份相同 
        if(date1[2] === date2[2]){  //日期相同
          let dateArr = [];  
          dateArr.push(months[date1[1]] + " " + dateChange(date1[2]) + ", " + date1[0]);  
          return dateArr;  
        }  
        else{  
          let dateArr = [];  
          dateArr.push(months[date1[1]] + " " + dateChange(date1[2]));  
          dateArr.push(dateChange(date2[2]));  
          return dateArr;  
        }  
      }
      else{  //月份不同
        let dateArr = [];  
        dateArr.push(months[date1[1]] + " " + dateChange(date1[2]));  
        dateArr.push(months[date2[1]] + " " + dateChange(date2[2]));  
        return dateArr;  
      }  
    }  
    if(date1[0] == date.getFullYear() - 1){  //开始年份为当前年份 
      let dateArr = [];  
      dateArr.push(months[date1[1]] + " " + dateChange(date1[2]));  
      dateArr.push(months[date2[1]] + " " + dateChange(date2[2]));  
      return dateArr;  
    }  
    else{  
      let dateArr = [];  
      dateArr.push(months[date1[1]] + " " + dateChange(date1[2]) + ", " + date1[0]);  
      dateArr.push(months[date2[1]] + " " + dateChange(date2[2]));  
      return dateArr;  
    }  
  }    
  if (date2[0] > date1[0]){  //不同年且d2比d1大时
    let dateArr = [];  
    dateArr.push(months[date1[1]] + " " + dateChange(date1[2]) + ", " + date1[0]);  
    dateArr.push(months[date2[1]] + " " + dateChange(date2[2]) + ", " + date2[0]);  
    return dateArr;  
  }  
};  
makeFriendlyDates(["2017-02-05", "2017-03-03"]); 
```

## 7.构造一个对象
- 用下面给定的方法构造一个对象。
- 方法有 `getFirstName()，getLastName()， getFullName(), setFirstName(first)， setLastName(last)， and setFullName(firstAndLast)`。
- 所有有参数的方法只接受一个字符串参数。
- 所有的方法只与实体对象交互。

```js
var Person = function(firstAndLast) {
  let first, last;
  this.getFirstName = () => first;
  this.getLastName = () => last;
  this.getFullName = () => first + ' ' + last;
  this.setFirstName = firstName => first = firstName;
  this.setLastName = lastName => last = lastName;
  this.setFullName = name => {
    name = name.split(' ');
    first = name[0];
    last = name[1];
  };
  this.setFullName(firstAndLast);
};
var bob = new Person('Bob Ross');
bob.getFullName();
```

## 8.地图碎片
- 返回一个数组，其内容是把原数组中对应元素的平均海拔转换成其对应的轨道周期。
- 原数组中会包含格式化的对象内容，像这样 `{name: 'name', avgAlt: avgAlt}`。
- 至于轨道周期怎么求，戳这里 on wikipedia (不想看英文的话可以自行搜索以轨道高度计算轨道周期的公式)。
- 求得的值应该是一个与其最接近的整数，轨道是以地球为基准的.
- 地球半径是 `6367.4447 kilometers`，地球的GM值是 `398600.4418`，圆周率为`Math.PI`。

```js
let orbitalPeriod = arr => {
  let GM = 398600.4418,earthRadius = 6367.4447;
  for(let i = 0;i < arr.length;i++){
    let r = (arr[i].avgAlt + 6367.4447);
    let t = r * 2 * Math.PI * Math.sqrt((r / GM));
    delete arr[i].avgAlt;
    arr[i].orbitalPeriod = Math.round(t);
  }
  return arr;
};
orbitalPeriod([{name : "sputnik", avgAlt : 35873.5553}]); 
```

## 9.找到你的另一半
- 有一个能力数组`[7,9,11,13,15]`，按照最佳组合值为20来计算，只有`7+13`和`9+11`两种组合。而7在数组的索引为0，13在数组的索引为3，9在数组的索引为1，11在数组的索引为2。
- 所以我们说函数：`pairwise([7,9,11,13,15],20)` 的返回值应该是`0+3+1+2`的和，即6。

```js
let pairwise = (arr, arg) => {
  let arr2 = arr,count = 0;
  for(let i = 0;i < arr.length;i++){
    for(let j = i + 1;j < arr2.length;j++){
        if(arr[i] + arr2[j] === arg){
          count += i + j;
          arr[i] = "false";
          arr[j] = "false";
        }      
    }
  }
  return count;  
};
pairwise([1, 3, 2, 4], 4); 
```