1. 
function reverseString(str) {
  return str.split("").reverse().join("");
}

2. 
function factorialize (num) { 
  return num < 0 ? -1 : (num ===0 || num ===1) ? 1 : num * factorialize(num - 1);
}
console.log(factorialize(5)); //120

6. 
function largestOfFour(arr) {
  var newArr = [];
  for(var i= 0;i < arr.length;i++){
    for(var j = 0;j < arr[i].length;j++){
      arr[i].sort((a,b) => a-b);
    }
    newArr.push(arr[i][arr[i].length-1]);
  }  
  return newArr;
}
console.log(largestOfFour([[4, 5, 1, 3], [13, 27, 18, 26], [32, 35, 37, 39], [1000, 1001, 857, 1]]));//[27,5,39,1001]

15. 
function where(arr, num) {
  // 请把你的代码写在这里
  arr.sort((a,b) => a-b);
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
console.log(where([2, 5, 10], 15)); //3

**进阶算法前面加空格。**

1. 
function sumAll(arr) {
  return (arr[0] + arr[1]) * (Math.abs(arr[0] - arr[1] + 1)) / 2;
}
console.log(sumAll([12, 1]));  //55