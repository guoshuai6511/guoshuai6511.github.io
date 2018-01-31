---
title: 深入学习之 Array
tag: 
  - javascript
categories: 
  - 深入学习系列
---

数组是 `javascript` 中很重要的一种对象，本篇总结了几乎所有的数组方法（包括最新的），这里把这些方法分成几类：
- 执行后会修改原数组的
- 执行后不改变原数组
- 数组自身上的方法（其他均为继承数组原型上的方法）

## 执行后会修改原数组的

<summary><strong>toString</strong></summary>
<details>

`toString()` 返回一个字符串，表示指定的数组及其元素。
- 语法
```js
arr.toString()
```  
- 示例
```js
['Jan', 'Feb', 'Mar', 'Apr'].toString(); 
// "Jan,Feb,Mar,Apr"
// 实际上是调用了数组原型上的 join() 方法
```
</details>

<details>
<summary><strong>push</strong></summary>

`push()` 方法将一个或多个元素添加到数组的末尾，并返回数组的新长度。
- 语法
```js
arr.push(element1, ..., elementN)
```
- 示例
```js
var numbers = [1, 2, 3];
numbers.push(5, 6, 7);
console.log(numbers); 
// [1, 2, 3, 4, 5, 6, 7]
```
</details>

<details>
<summary><strong>pop</strong></summary>

`pop()` 方法从数组中删除最后一个元素，并返回该元素的值。此方法更改数组的长度。
- 语法
```js
arr.pop()
```
- 示例
```js
let myFish = ["angel", "clown", "mandarin", "surgeon"];
let popped = myFish.pop();

console.log(myFish); 
// ["angel", "clown", "mandarin"]
```
</details>

<details>
<summary><strong>shift</strong></summary>

`shift()` 方法从数组中删除第一个元素，并返回该元素的值。此方法更改数组的长度。
- 语法
```js
arr.shift()
```
- 示例
```js
let myFish = ['angel', 'clown', 'mandarin', 'surgeon'];
var shifted = myFish.shift(); 

console.log('调用 shift 之后: ' + myFish); 
```
</details>

<details>
<summary><strong>unshift</strong></summary>

`unshift()` 方法将一个或多个元素添加到数组的开头，并返回新数组的长度。
- 语法
```js
arr.unshift(element1, ..., elementN)
```
- 示例
```js
var arr = [1, 2];

arr.unshift(-2, -1); // = 5
//arr is [-2, -1, 0, 1, 2]
```
</details>

<details>
<summary><strong>reverse</strong></summary>


`reverse()` 方法将数组中元素的位置颠倒。
- 语法
```js
arr.reverse()
```
- 示例
```js
var myArray = ['one', 'two', 'three'];
myArray.reverse(); 

console.log(myArray) // ['three', 'two', 'one']
```
</details>

<details>
<summary><strong>sort</strong></summary>

`sort()` 方法在适当的位置对数组的元素进行排序，并返回数组。 sort 排序不一定是稳定的。  
默认排序顺序是根据 **字符串Unicode码点**。
- 语法
```js
arr.sort() 
arr.sort(compareFunction)  // 用来指定按某种顺序进行排列的函数
```
- 返回值  
返回排序后的新数组。原数组被修改。
- 示例
```js
var fruit = ['cherries', 'apples', 'bananas'];
fruit.sort(); 
// ['apples', 'bananas', 'cherries']

var scores = [1, 10, 21, 2]; 
scores.sort(); 
// [1, 10, 2, 21]

// 比较数值大小
var numbers = [4, 2, 5, 1, 3];
numbers.sort(function(a, b) {
  return a - b;
});
console.log(numbers);

// [1, 2, 3, 4, 5]
```
</details>

<details>
<summary><strong>splice</strong></summary>

`splice()` 方法通过删除现有元素和/或添加新元素来更改一个数组的内容。原数组被修改。
- 语法
```js
array.splice(start)
array.splice(start, deleteCount) 
array.splice(start, deleteCount, item1, item2, ...)
```
- 返回值  
由被删除的元素组成的一个数组。如果只删除了一个元素，则返回只包含一个元素的数组。如果没有删除元素，则返回空数组。
- 示例
```js
var myFish = ["angel", "clown", "mandarin", "surgeon"];

//从第 2 位开始删除 1 个元素，然后插入 "trumpet"
removed = myFish.splice(2, 1, "trumpet");
//运算后的myFish: ["angel", "clown", "trumpet", "surgeon"]
//被删除元素数组：["drum"]
```
</details>


<details>
<summary><strong>fill</strong></summary>


`fill()` 方法用一个固定值填充一个数组中从起始索引到终止索引内的全部元素。
- 语法
```js
arr.fill(value) 
arr.fill(value, start) 
arr.fill(value, start, end)
```
- 示例
```js
[1, 2, 3].fill(4)            // [4, 4, 4]
[1, 2, 3].fill(4, 1)         // [1, 4, 4]
[1, 2, 3].fill(4, 1, 2)      // [1, 4, 3]
```
</details>

## 执行后不改变原数组


<details>
<summary><strong>concat</strong></summary>

`concat()` 方法用于合并两个或多个数组。此方法不会更改现有数组，而是返回一个新数组。
 
 - 语法  
 ```js
 var new_array = old_array.concat(value1[, value2[, ...[, valueN]]])
 ```
 - 示例
 ```js
let arr1 = ["a", "b"];
let arr2 = ["c", "d"];
console.log( arr1.concat(arr2) )  // ['a','b','c','d']

// 还可以连接数组和非数组值
console.log(arr1.concat(1,arr2))  // ['a','b','1','c','d']
 ```
</details>
 
<details>
<summary><strong>join</strong></summary>

`join()` 方法将数组（或一个类数组对象）的所有元素连接到一个字符串中。**join() 方法，不会改变原数组！**
- 语法
```js
str = arr.join()
// 默认为 ","
str = arr.join("")
// 分隔符 === 空字符串 ""
str = arr.join(separator)
// 分隔符
```
- 备注  
如果元素是 `undefined` 或 `null`，则会被转化为空字符串。

- 示例
```js
console.log(['a','b','c'].join())  // 'a,b,c'
console.log(['a','b','c'].join(''))  // 'abc'
console.log(['a','b','c'].join('_'))  // 'a_b_c'
```
</details>

<details>
<summary><strong>slice</strong></summary>

`slice()` 方法返回一个从开始到结束（不包括结束）选择的数组的一部分浅拷贝到一个新数组对象。  
原始数组不会被修改。
- 语法
```js
arr.slice()
arr.slice(begin)
arr.slice(begin, end)
```
- 备注  
**类似数组（Array-like）对象**  
`slice` 方法可以用来将一个类数组（`Array-like`）对象/集合转换成一个数组。你只需将该方法绑定到这个对象上。下述代码中 list 函数中的 `arguments` 就是一个类数组对象。
```js
function list() {
  return Array.prototype.slice.call(arguments);
}

var list1 = list(1, 2, 3); // [1, 2, 3]
```
`Array.prototype.slice.call(arguments)`，你也可以简单的使用 `[].slice.call(arguments)` 来代替。更多见 [Slice--MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)。

- 示例
```js
var fruits = ['Banana', 'Orange', 'Lemon', 'Apple', 'Mango'];
var citrus = fruits.slice(1, 3);

// fruits contains ['Banana', 'Orange', 'Lemon', 'Apple', 'Mango']
// citrus contains ['Orange','Lemon']
```
</details>

<details>
<summary><strong>forEach</strong></summary>

`forEach()` 方法对数组的每个元素执行一次提供的函数。
- 语法
```js
array.forEach(callback(currentValue, index, array){
    //do something
}, this)

array.forEach(callback[, thisArg])
```
- 备注

- 示例
```js
let a = ['a', 'b', 'c'];

a.forEach(function(element) {
    console.log(element);
});
```
</details>

<details>
<summary><strong>map</strong></summary>

`map()` 方法创建一个新数组，其结果是该数组中的每个元素都调用一个提供的函数后返回的结果。
- 语法
```js
let array = arr.map(function callback(currentValue, index, array) { 
    // Return element for new_array 
}[, thisArg])
```
- 备注

- 示例
```js
let numbers = [1, 4, 9];
let roots = numbers.map(Math.sqrt);

// roots is now [1, 2, 3]
// numbers is still [1, 4, 9]
```

#### `.reduce`
`reduce()` 方法对累加器和数组中的每个元素 (从左到右)应用一个函数，将其减少为单个值。更多见 [Reduce--MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)。
- 语法
```js
array.reduce(function(accumulator, currentValue, currentIndex, array), initialValue)
```
- 示例
```js
var total = [0, 1, 2, 3].reduce(function(sum, value) {
  return sum + value;
}, 0);
// total is 6
```
</details>

<details>
<summary><strong>reduceRight</strong></summary>

`reduceRight()` 方法接受一个函数作为累加器（accumulator）和数组的每个值（从右到左）将其减少为单个值。更多参见 [Reduce--MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)。

#### `.every`
`every()` 方法测试数组的所有元素是否都通过了指定函数的测试。
- 语法
```js
arr.every(callback[, thisArg])
```
- 备注  
`every` 方法为数组中的每个元素执行一次 `callback` 函数，直到它找到一个使 `callback` 返回 `false`（表示可转换为布尔值 `false` 的值）的元素。如果发现了一个这样的元素，`every` 方法将会立即返回 `false`。否则，`callback` 为每一个元素返回 `true`，`every` 就会返回 `true`。  
`callback` 被调用时传入三个参数：元素值，元素的索引，原数组。
- 示例
```js
function isBigEnough(element, index, array) {
  return (element >= 10);
}
var passed = [12, 5, 8, 130, 44].every(isBigEnough);
// passed is false
passed = [12, 54, 18, 130, 44].every(isBigEnough);
// passed is true
```
</details>

<details>
<summary><strong>some</strong></summary>

`some()` 方法测试数组中的某些元素是否通过由提供的函数实现的测试。同`every` 方法互补。
- 语法
```js
arr.some(callback[, thisArg])
```
- 备注  
some 为数组中的每一个元素执行一次 callback 函数，直到找到一个使得 callback 返回一个“真值”（即可转换为布尔值 true 的值）。如果找到了这样一个值，some 将会立即返回 true。否则，some 返回 false。
- 示例
```js
const isBiggerThan10 = (element, index, array) => {
  return element > 10;
}

[2, 5, 8, 1, 4].some(isBiggerThan10);  
// false

[12, 5, 8, 1, 4].some(isBiggerThan10); 
// true
```
</details>

<details>
<summary><strong>filter</strong></summary>

filter() 方法创建一个新数组, 其包含通过所提供函数实现的测试的所有元素。
- 语法
```js
var new_array = arr.filter(callback[, thisArg])
```
- 备注  
`filter` 为数组中的每个元素调用一次 callback 函数，并利用所有使得 callback 返回 true 或 等价于 true 的值 的元素创建一个新数组。
- 示例
```js
function isBigEnough(element) {
  return element >= 10;
}
var filtered = [12, 5, 8, 130, 44].filter(isBigEnough);
// filtered is [12, 130, 44]
```
</details>

<details>
<summary><strong>copyWithin</strong></summary>

- 语法
```js
arr.copyWithin(target, start, end)

// start end 可选
// target: 目标位置,复制序列到该位置
// start: 开始复制元素的起始位置
// end: 开始复制元素的结束位置
```
- 备注

- 示例
```js
["alpha", "beta", "copy", "delta"].copyWithin(1, 2, 3);
// ["alpha", "copy", "copy", "delta"]
```
</details>

<details>
<summary><strong>entries</strong></summary>

`entries()` 方法返回一个新的`Array Iterator`对象，该对象包含数组中每个索引的键/值对。
更多参见 [Entries--MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/entries)
</details>

<details>
<summary><strong>keys</strong></summary>

`keys()` 方法返回一个新的Array迭代器，它包含数组中每个索引的键。
更多参见 [Entries--MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/keys)
</details>


### 元素查找

<details>
<summary><strong>indexOf</strong></summary>

`indexOf()` 方法返回在数组中可以找到一个给定元素的**第一个索引**，如果不存在，则返回**-1**。
- 语法
```js
arr.indexOf(searchElement)
arr.indexOf(searchElement[, fromIndex = 0])
```
- 备注  
基于严格相等进行匹配查找。起始索引值如果为负，如-2，则从倒数第二个元素开始查找。
- 示例
```js
[2,3,4].indexOf(3)  // 1
[2,3,4].indexOf(5)  // -1
```
</details>

<details>
<summary><strong>lastIndexOf</strong></summary>

`lastIndexOf()` 方法返回在数组中可以找到一个给定元素的**第一个索引**，如果不存在，则返回**-1**。
- 语法
```js
arr.lastIndexOf(searchElement)
arr.lastIndexOf(searchElement[, fromIndex = arr.length-1])
```
- 备注  
基于严格相等进行匹配查找。起始索引值如果为负，如-2，则从倒数第二个元素开始查找。
- 示例
```js
[2,3,5,3,4].lastIndexOf(3)  // 3
```
#### `.find`
`find()` 方法返回数组中满足提供的测试函数的第一个元素的值。否则返回 `undefined`。
- 语法
```js
arr.find(callback[, thisArg])
```
- 示例
```js
function isBigEnough(element) {
  return element >= 15;
}

[12, 5, 8, 130, 44].find(isBigEnough); // 130
```
</details>

<details>
<summary><strong>findIndex</strong></summary>

`findIndex()` 方法返回数组中满足提供的测试函数的第一个元素的索引。否则返回-1。
- 语法
```js
arr.findIndex(callback[, thisArg])
```
- 示例
```js
function isBigEnough(element) {
  return element >= 15;
}

[12, 5, 8, 130, 44].findIndex(isBigEnough); // 3
```
</details>

<details>
<summary><strong>includes</strong></summary>

`includes()` 方法用来判断一个数组是否包含一个指定的值，如果是，酌情返回 true或 false。
- 语法
```js
arr.includes(searchElement)
arr.includes(searchElement, fromIndex)

// searchElement: 查找元素
// fromIndex: 从该索引处开始查找
```
- 备注  
如果`fromIndex` 大于等于数组长度 ，则返回 `false` 。该数组不会被搜索。
如果`fromIndex` 为负值 ，计算出的索引将作为开始搜索`searchElement`的位置。如果计算出的索引小于 0，整个数组都会被搜索。见下面：  
```js
// 数组长度是3
// fromIndex 是 -100
// computed index 是 3 + (-100) = -97
```
- 示例
```js
let a = [1, 2, 3];
a.includes(2); // true 
a.includes(4); // false
```
</details>

## 数组自身的方法

<details>
<summary><strong>Array.isArray</strong></summary>

用于确定传递的值是否是一个 `Array`。
- 语法
```js
Array.isArray(obj)
```
- 备注
假如不存在Array.isArray()方法，
```js
if (!Array.isArray) {
  Array.isArray = function(arg) {
    return Object.prototype.toString.call(arg) === '[object Array]';
  };
}
```

- 示例
```js
// 下面的函数调用都返回 true
Array.isArray([]);
Array.isArray([1]);
Array.isArray(new Array());
// 鲜为人知的事实：其实 Array.prototype 也是一个数组。
Array.isArray(Array.prototype);

// 下面的函数调用都返回 false
Array.isArray();
Array.isArray({});
Array.isArray(null);
Array.isArray(undefined);
Array.isArray(17);
Array.isArray('Array');
Array.isArray(true);
```
</details>

<details>
<summary><strong>Array.from</strong></summary>

`Array.from()` 方法从一个类似数组或可迭代的对象中创建一个新的数组实例。
- 语法
```js
Array.from(arrayLike[, mapFn[, thisArg]])
```
- 备注

- 示例
```js
Array.from('foo'); 
// ["f", "o", "o"]

let m = new Map([[1, 2], [2, 4], [4, 8]]);
Array.from(m); 
// [[1, 2], [2, 4], [4, 8]]

function f() {
  return Array.from(arguments);
}

f(1, 2, 3);

// [1, 2, 3]
```
</details>

<details>
<summary><strong>Array.of</strong></summary>

`Array.of()` 方法创建一个具有可变数量参数的新数组实例，而不考虑参数的数量或类型。

`Array.of()` 和 `Array` 构造函数之间的区别在于处理整数参数：`Array.of(7)` 创建一个具有单个元素 7 的数组，而 `Array(7)` 创建一个包含 7 个 `undefined` 元素的数组。
- 语法
```js
Array.of(element0[, element1[, ...[, elementN]]])
```
- 备注

- 示例
```js
Array.of(7);       // [7] 
Array.of(1, 2, 3); // [1, 2, 3]

Array(7);          // [ , , , , , , ]
Array(1, 2, 3);    // [1, 2, 3]
```
</details>