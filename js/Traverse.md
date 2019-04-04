# 用ES6来看JS的高级遍历
### 作者：BlackXu 
## for of(ES6)
- for of只可以循环可迭代对象的可迭代属性(包括 Array, Map, Set, String, TypedArray，arguments 对象等等)。
- 循环不会循环对象的key,所以不能循环普通的对象,需要通过和Object.keys()搭配使用。

```js
for(let v of arr){
  console.log(v);
}
//遍历对象
for(let v of Object.keys(obj)){
  console.log(v);
}
```

## forEach
- 对数组遍历，执行回调函数。
- 对于空数组是不会执行回调函数的。
- arr.forEach(回调函数名),后面可以再写函数，便于复用。
- 回调函数还有个参数，指定this的值，arr.forEach(xx,this)。
**与map的区别：没有返回值**，不赋值，对数组的改变用forEach。

```js
arr.forEach((v,i,array) => console.log(v +" : "+ i));
```

## map
- 对数组遍历，**返回一个新数组**，数组中的元素为原始数组元素调用函数处理的后值。  
- 不会对空数组执行。
- 不会改变原始数组。
- 函数后也有个参数指定this的值。
- 对数组的改变后

```js
let arr1 = arr.map((v,i,array) => v + 1);
```