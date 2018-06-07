# FreeCodeCamp Exercises
### Writen By Blackchaos 
## Intermediate Algorithm Scripting
**What can you get from this code?**
- It can get the balance with the front end in the algorithm and harvest the interest of the computer algorithm.
- Constantly iterate the code to gain more front-end technology.
- This blog uses ES5/6 syntax extensively, and makes full use of arrow functions, let/const and so on.

## Basic Algorithm Scripting
## 1.Reverse a String
**You may need to turn the string into an array before you can reverse it.Your result must be a string.**
```js
function reverseString(str) {
  return str.split("").reverse().join("");
}
console.log(reverseString("Greetings from Earth")); //"htraE morf sgniteerG"
```

## 2.Factorialize a Number 
**Return the factorial of the provided integer.If the integer is represented with the letter n, a factorial is the product of all positive integers less than or equal to n.Factorials are often represented with the shorthand notation `n!`**
```js
function factorialize (num) { 
    return num < 0 ? -1 : (num === 0 || num === 1) ? 1 : num * factorialize(num - 1); 
}
console.log(factorialize(5)); //120
```

## 3.Check for Palindromes
**Return true if the given string is a palindrome. Otherwise, return false.A palindrome is a word or sentence that's spelled the same way both forward and backward, ignoring punctuation, case, and spacing.You'll need to remove all non-alphanumeric characters (punctuation, spaces and symbols) and turn everything lower case in order to check for palindromes.**
```js
function palindrome(str) {
  str = str.replace(/[\ |\~|\`|\!|\@|\#|\$|\%|\^|\&|\*|\(|\)|\-|\_|\+|\=|\||\\|\[|\]|\{|\}|\;|\:|\"|\'|\,|\<|\.|\>|\/|\?]/g,"").toLowerCase();
  return str === str.split("").reverse().join("") ? true : false; 
}
console.log(palindrome("never odd or even")); //true
console.log(palindrome("0_0 (: /-\ :) 0-0"));  //true
```

## 4.Find the Longest Word in a String
**Return the length of the longest word in the provided sentence.Your response should be a number.**
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

## 5.Title Case a Sentence
**Return the provided string with the first letter of each word capitalized. Make sure the rest of the word is in lower case.For the purpose of this exercise, you should also capitalize connecting words like "the" and "of".**
```js
function titleCase(str) {
  return str.toLowerCase().replace(/( |^)[a-z]/g, F => F.toUpperCase());
}
console.log(titleCase("HERE IS MY HANDLE HERE IS MY SPOUT")); //"Here Is My Handle Here Is My Spout"
```

## 6.Return Largest Numbers in Arrays
**Return an array consisting of the largest number from each provided sub-array. For simplicity, the provided array will contain exactly 4 sub-arrays.Remember, you can iterate through an array with a simple for loop, and access each member with array syntax arr[i].**
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

## 7.Confirm the Ending
**Check if a string (first argument, str) ends with the given target string (second argument, target).This challenge can be solved with the .endsWith() method, which was introduced in ES2015. But for the purpose of this challenge, we would like you to use one of the JavaScript substring methods instead.**
```js
function confirmEnding(str, target) {
  return target === str.slice(str.length -target.length)
}
console.log(confirmEnding("He has to give me a new name", "me")); //true
```
or:
```js
function confirmEnding(str, target) {
  return target === str.substr(-target.length,target.length)
}
console.log(confirmEnding("He has to give me a new name", "me")); //true
```

## 8.Repeat a string
**Repeat a given string (first argument) num times (second argument). Return an empty string if num is not a positive number.**
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

## 9.Truncate a string
**Truncate a string (first argument) if it is longer than the given maximum string length (second argument). Return the truncated string with a ... ending.Note that inserting the three dots to the end will add to the string length.However, if the given maximum string length num is less than or equal to 3, then the addition of the three dots does not add to the string length in determining the truncated string.**
```js
function truncate(str, num) {
    return str = num >= str.length ? str :  num > 3 ? str.slice(0,num - 3) + "..." : str.slice(0,num) + "...";
}
console.log(truncate("A-tisket a-tasket A green and yellow basket", 11));  //"A-tisket..."
```

## 10.Chunky Monkey
**Write a function that splits an array (first argument) into groups the length of size (second argument) and returns them as a two-dimensional array.**
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

## 11.Slasher Flick
**Return the remaining elements of an array after chopping off n elements from the head.The head means the beginning of the array, or the zeroth index.**
```js
function slasher(arr, howMany) {
  return arr.slice(howMany);
}
console.log(slasher([1, 2, 3], 2)); //[3]
```

## 12.Mutations
**Return true if the string in the first element of the array contains all of the letters of the string in the second element of the array.For example, ["hello", "Hello"], should return true because all of the letters in the second string are present in the first, ignoring case.The arguments ["hello", "hey"] should return false because the string "hello" does not contain a "y".Lastly, ["Alien", "line"], should return true because all of the letters in "line" are present in "Alien".**
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

## 13.Falsy Bouncer
**Remove all falsy values from an array.Falsy values in JavaScript are `false`、`null`、`0`、`""`、`undefined` 和 `NaN`.**
```js
function bouncer(arr) {
  return arr.filter(Boolean);
}
console.log(bouncer([7, "ate", "", false, 9]));//[7,"ate",9]
```

## 14.Seek and Destroy
**You will be provided with an initial array (the first argument in the destroyer function), followed by one or more arguments. Remove all elements from the initial array that are of the same value as these arguments.**
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
or:
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

## 15.Where do I belong
**Return the lowest index at which a value (second argument) should be inserted into an array (first argument) once it has been sorted. The returned value should be a number.**
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

## 16.Caesars Cipher
**One of the simplest and most widely known ciphers is a Caesar cipher, also known as a shift cipher. In a shift cipher the meanings of the letters are shifted by some set amount.A common modern use is the ROT13 cipher, where the values of the letters are shifted by 13 places. Thus 'A' ↔ 'N', 'B' ↔ 'O' and so on.Write a function which takes a ROT13 encoded string as input and returns a decoded string.All letters will be uppercase. Do not transform any non-alphabetic character (i.e. spaces, punctuation), but do pass them on.**
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

## Intermediate Algorithm Scripting
## 1. Sum All Numbers in a Range
**We'll pass you an array of two numbers. Return the sum of those two numbers and all numbers between them.**
```js
function sumAll(arr) {
  return (arr[0] + arr[1]) * (Math.abs(arr[0] - arr[1] + 1)) / 2;
}
console.log(sumAll([10, 1]));  //55
```

## 2.Diff Two Arrays
**Compare two arrays and return a new array with any items only found in one of the two given arrays, but not both. In other words, return the symmetric difference of the two arrays.**
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

## 3.Roman Numeral Converter
**Compare two arrays and return a new array with any items only found in one of the two given arrays, but not both. In other words, return the symmetric difference of the two arrays.**
```js
function convert(num){
  let a,b,c,d;  
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



## 4.Where art thou
**Make a function that looks through an array of objects (first argument) and returns an array of all objects that have matching property and value pairs (second argument). Each property and value pair of the source object has to be present in the object from the collection if it is to be included in the returned array.**
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

## 5.Search and Replace 
- Perform a search and replace on the sentence using the arguments provided and return the new sentence.
- First argument is the sentence to perform the search and replace on.
- Second argument is the word that you will be replacing (before).
- Third argument is what you will be replacing the second argument with (after).
- NOTE: Preserve the case of the original word when you are replacing it. For example if you mean to replace the word "Book" with the word "dog", it should be replaced as "Dog".

```js
function myReplace(str, before, after) {
  if(before[0] === before[0].toUpperCase()){
    after = after[0].toUpperCase() + after.slice(1); 
  }
  return str.replace(before, after);
}
myReplace("He is Sleeping on the couch", "Sleeping", "sitting"); //He is Sitting on the couch
```

## 6.Pig Latin 
- Translate the provided string to pig latin.
- Pig Latin takes the first consonant (or consonant cluster) of an English word, moves it to the end of the word and suffixes an "ay".
- If a word begins with a vowel you just add "way" to the end.
- Input strings are guaranteed to be English words in all lowercase.

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

## 7.DNA Pairing  
- The DNA strand is missing the pairing element. Take each character, get its pair, and return the results as a 2d array.
- Base pairs are a pair of AT and CG. Match the missing element to the provided character.
- Return the provided character as the first element in each array.
- For example, for the input GCG, return [["G", "C"], ["C","G"],["G", "C"]]
- The character and its pair are paired up in an array, and all the arrays are grouped into one encapsulating array.

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

## 8.Missing letters
**Find the missing letter in the passed letter range and return it.If all letters are present in the range, return undefined.**
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

## 9.Boo who
**Check if a value is classified as a boolean primitive. Return true or false.Boolean primitives are true and false.**
```js
function boo(bool) {
  return bool === Boolean(bool)
}
console.log(boo(null));//false
```

## 10.Sorted Union
- Write a function that takes two or more arrays and returns a new array of unique values in the order of the original provided arrays.
- In other words, all values present from all arrays should be included in their original order, but with no duplicates in the final array.
- The unique numbers should be sorted by their original order, but the final array should not be sorted in numerical order.

```js
function unite(){
  let arr = Array.from(arguments);
  const concatArr = arr.reduce((pre,cur) => pre.concat(cur));
  return arr = concatArr.filter((v,i) => concatArr.indexOf(v) === i);
}
console.log(unite([1, 3, 2], [1, [5]], [2, [4]])); //[1, 3, 2, [5], [4]]
```

## 11.Convert HTML Entities
**Convert the characters &, <, >, " (double quote), and ' (apostrophe), in a string to their corresponding HTML entities.** 
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

## 12.Spinal Tap Case
**Convert a string to spinal case. Spinal case is all-lowercase-words-joined-by-dashes.**
```js
let spinalCase = str => str.replace(/\s|_/g,'-').replace(/([a-z])([A-Z])/g,'$1-$2').toLowerCase();  
console.log(spinalCase('This Is Spinal Tap')); //'this-is -spinal-tap'
```

## 13.Sum All Odd Fibonacci Numbers
- Given a positive integer num, return the sum of all odd Fibonacci numbers that are less than or equal to num.
- The first two numbers in the Fibonacci sequence are 1 and 1. Every additional number in the sequence is the sum of the two previous numbers. The first six numbers of the Fibonacci sequence are 1, 1, 2, 3, 5 and 8.
- For example, sumFibs(10) should return 10 because all odd Fibonacci numbers less than 10 are 1, 1, 3, and 5.

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

## 14.Sum All Primes 
- Sum all the prime numbers up to and including the provided number.
- A prime number is defined as a number greater than one and having only two divisors, one and itself. For example, 2 is a prime number because it's only divisible by one and two.
- The provided number may not be a prime.

```js
let sumPrimes = num => {
  let answer = 0;
  for(let i = 2; i <= num; i++){   
    if(isPrime(i)){
      answer += i;
    }
  }
  return answer;
}
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

## 15.Smallest Common Multiple
- Find the smallest common multiple of the provided parameters that can be evenly divided by both, as well as by all sequential numbers in the range between these parameters.
- The range will be an array of two numbers that will not necessarily be in numerical order.
- e.g. for 1 and 3 - find the smallest common multiple of both 1 and 3 that is evenly divisible by all numbers between 1 and 3.

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

## 16.Finders Keepers  
**Create a function that looks through an array (first argument) and returns the first element in the array that passes a truth test (second argument).**
```js
let find = (arr, func) => {
  arr = arr.filter(func);
  return arr[0];
};
console.log(find([1, 5, 8, 9], num =>  num % 2 === 0 )); //8
```

## 17.Drop it
- Drop the elements of an array (first argument), starting from the front, until the predicate (second argument) returns true.
- The second argument, func, is a function you'll use to test the first elements of the array to decide if you should drop it or not.
- Return the rest of the array, otherwise return an empty array.

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

## 18.Steamroller 
**Flatten a nested array. You must account for varying levels of nesting.**
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

## 19.Binary Agents 
**Return an English translated sentence of the passed binary string.The binary string will be space separated.**
```js
let binaryAgent = str => {
  let str1 = str.split(" ").map( v => parseInt(v,2));
  str = "";
  str1.forEach( v => str += String.fromCharCode(v) );
  return str;
};
console.log(binaryAgent("01000001 01110010 01100101 01101110 00100111 01110100 00100000 01100010 01101111 01101110 01100110 01101001 01110010 01100101 01110011 00100000 01100110 01110101 01101110 00100001 00111111")); //Aren't bonfires fun!?
```

## 20.Everything Be True  
**Check if the predicate (second argument) is truthy on all elements of a collection (first argument).Remember, you can access object properties through either dot notation or [] notation.**
```js
function every(collection, pre) {
  return collection.every(v => v[pre]);
}
every([{"user": "Tinky-Winky", "sex": "male"}, {"user": "Dipsy", "sex": "male"}, {"user": "Laa-Laa", "sex": "female"}, {"user": "Po", "sex": "female"}], "sex"); //true
```

## 21.Arguments Optional
- Create a function that sums two arguments together. If only one argument is provided, then return a function that expects one argument and returns the sum.
- For example, addTogether(2, 3) should return 5, and addTogether(2) should return a function.
- Calling this returned function with a single argument will then return the sum:
- var sumTwoAnd = addTogether(2);
- sumTwoAnd(3) returns 5.
- If either argument isn't a valid number, return undefined.

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

## Advanced Algorithm Scripting
## 1.Validate US Telephone Numbers
**If the incoming string is a valid American phone number, it returns true.**
```js
let telephoneCheck = str => /^1? ?(\(\d{3}\)|\d{3})[ |-]?\d{3}[ |-]?\d{4}$/.test(str);
telephoneCheck("555-555-5555"); 
```

## 2.Symmetric Difference
- Create a function that takes two or more arrays and returns an array of the symmetric difference (△ or ⊕) of the provided arrays.
- Given two sets (for example` set A = {1, 2, 3} `and `set B = {2, 3, 4}`), the mathematical term "symmetric difference" of two sets is the set of elements which are in either of the two sets, but not in both` (A △ B = C = {1, 4})`. For every additional symmetric difference you take (say on a `set D = {2, 3}`), you should get the set with elements which are in either of the two the sets but not both` (C △ D = {1, 4} △ {2, 3} = {1, 2, 3, 4})`.

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

## 3.Exact Change
- Design a cash register drawer function checkCashRegister() that accepts purchase price as the first argument (price), payment as the second argument (cash), and cash-in-drawer (cid) as the third argument.
- cid is a 2D array listing available currency.
- Return the string "Insufficient Funds" if cash-in-drawer is less than the change due. Return the string "Closed" if cash-in-drawer is equal to the change due.
- Otherwise, return change in coin and bills, sorted in highest to lowest order.

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

## 4.Inventory Update
**Compare and update the inventory stored in a 2D array against a second 2D array of a fresh delivery. Update the current existing inventory item quantities (in arr1). If an item cannot be found, add the new item and quantity into the inventory array. The returned inventory array should be in alphabetical order by item.**
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

## 5.No repeats please
- Return the number of total permutations of the provided string that don't have repeated consecutive letters. Assume that all characters in the provided string are each unique.
- For example, aab should return 2 because it has 6 total permutations (aab, aab, aba, aba, baa, baa), but only 2 of them (aba and aba) don't have the same letter (in this case a) repeating.

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

## 6.Friendly Date Ranges
- Convert common date formats such as YYYY-MM-DD to a more readable format.
- The easy to read format should be the month name instead of the month number, and the ordinal number instead of the number to represent the day (1st instead of 1).
- Remember not to show the information that can be speculated: if the end date is less than one year in a date interval and the start date is less than one year, the end date doesn't have to write the year; in this case, if the month start and end date are in the same month, the date month will not be written.
- In addition, if the year of the start date is the current year, and the end date and the start date are less than one year, the year of the start date is not to be written.

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
      else{  
        if(d2[1] > d1[1]) return false;  
        if(d2[1] < d1[1]) return true; 
        else return d2[2] < d1[2] ? true : false; 
      }  
    }  
  };  
  if (sameYear(date1, date2)) { 
    if(date1[0] === date2[0]){  
      if(date1[1] === date2[1]){   
        if(date1[2] === date2[2]){ 
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
      else{  
        let dateArr = [];  
        dateArr.push(months[date1[1]] + " " + dateChange(date1[2]));  
        dateArr.push(months[date2[1]] + " " + dateChange(date2[2]));  
        return dateArr;  
      }  
    }  
    if(date1[0] == date.getFullYear() - 1){   
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
  if (date2[0] > date1[0]){  
    let dateArr = [];  
    dateArr.push(months[date1[1]] + " " + dateChange(date1[2]) + ", " + date1[0]);  
    dateArr.push(months[date2[1]] + " " + dateChange(date2[2]) + ", " + date2[0]);  
    return dateArr;  
  }  
};  
makeFriendlyDates(["2017-02-05", "2017-03-03"]); 
```

## 7.Make a Person
- Fill in the object constructor with the following methods below:getFirstName(),getLastName(),,getFullName(),setFirstName(first),setLastName(last),setFullName(firstAndLast).
- Run the tests to see the expected output for each method.
- The methods that take an argument must accept only one argument and it has to be a string.
- These methods must be the only available means of interacting with the object.

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

## 8.Map the Debris
- Return a new array that transforms the element's average altitude into their orbital periods.
- The array will contain objects in the format {name: 'name', avgAlt: avgAlt}.
- You can read about orbital periods on wikipedia.
- The values should be rounded to the nearest whole number. The body being orbited is Earth.
- The radius of the earth is 6367.4447 kilometers, and the GM value of earth is 398600.4418 km3s-2.

```js
let orbitalPeriod = arr => {
  const GM = 398600.4418,earthRadius = 6367.4447;
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

## 9.Pairwise
- For example `pairwise([7, 9, 11, 13, 15], 20)` returns 6. The pairs that sum to 20 are [7, 13] and [9, 11]. We can then write out the array with their indices and values.
- Below we'll take their corresponding indices and add them.`7 + 13 = 20 → Indices 0 + 3 = 3`,`9 + 11 = 20 → Indices 1 + 2 = 3`,`3 + 3 = 6 → Return 6`.

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