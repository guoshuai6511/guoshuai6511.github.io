---
title: 深入学习之 JSON
tag: 
  - javascript
  - json
categories: 
  - 深入学习系列
---

## 何为 JSON
> JSON(JavaScript Object Notation) 是一种轻量级的数据交换格式。 易于人阅读和编写。同时也易于机器解析和生成。 它基于JavaScript Programming Language, Standard ECMA-262 3rd Edition - December 1999的一个子集。 JSON采用完全独立于语言的文本格式，但是也使用了类似于C语言家族的习惯（包括C, C++, C#, Java, JavaScript, Perl, Python等）。 这些特性使JSON成为理想的数据交换语言。

JSON建构于两种结构：

- “名称/值”对的集合（A collection of name/value pairs）。不同的语言中，它被理解为对象（object），纪录（record），结构（struct），字典（dictionary），哈希表（hash table），有键列表（keyed list），或者关联数组 （associative array）。
- 值的有序列表（An ordered list of values）。在大部分语言中，它被理解为数组（array）。

JSON 都有以下形式：
- 对象  
对象是一个无序的“‘名称/值’对”集合。一个对象以“{”（左括号）开始，“}”（右括号）结束。每个“名称”后跟一个“:”（冒号）；“‘名称/值’ 对”之间使用“,”（逗号）分隔。

- 数组  
值（value）的有序集合。一个数组以“[”（左中括号）开始，“]”（右中括号）结束。值之间使用“,”（逗号）分隔。  
值（value）可以是双引号括起来的字符串（`string`）、数值(`number`)、`true`、`false`、 `null`、对象（`object`）或者数组（`array`）。这些结构可以嵌套。

- 简单值  
与javascript 相同的语法，可以用 JSON 表示`字符串`、`数值`、`布尔值`和 `null`，但不支持 **`undefined`**。  
JSON 字符串与 javascript 语法不一样，必须使用**双引号**（单引号会报语法错误）。  


## JSON 对象拥有的方法

> `JSON.parse()` is for "parsing" something that was received as JSON.  
> `JSON.stringify()` is to create a JSON string out of an object/array. 
 
> 两个方法的作用是恰好相反的。  



### 1. `JSON.parse( text [, reviver] )`

JSON.parse() 方法解析一个JSON字符串，构造由字符串描述的JavaScript值或对象。可以提供可选的reviver函数以在返回之前对所得到的对象执行变换。

**JSON.parse() 不允许用逗号结尾**

**示例：**
```js
// 基本例子
JSON.parse('{}');              // {}
JSON.parse('true');            // true
JSON.parse('"foo"');           // "foo"
JSON.parse('[1, 5, "false"]'); // [1, 5, "false"]
JSON.parse('null');            // null

// 使用 reviver 函数（还原函数）
JSON.parse('{"1": 1, "2": 2,"3": {"4": 4, "5": {"6": 6}}}', function (k, v) {
    console.log(k); // 输出当前的属性名，从而得知遍历顺序是从内向外的，
                    // 最后一个属性名会是个空字符串。
    return v;       // 返回原始属性值，相当于没有传递 reviver 参数。
});
```

### 2. `JSON.stringify( value[, replacer [, space]] )`

**参数**
- replacer  
如果该参数是一个函数，则在序列化过程中，被序列化的值的每个属性都会经过该函数的转换和处理；  
如果该参数是一个数组，则只有包含在这个数组中的属性名才会被序列化到最终的 JSON 字符串中；如果该参数为null或者未提供，则对象所有的属性都会被序列化；
- space  
指定缩进用的空白字符串，用于美化输出（pretty-print）；如果参数是个数字，它代表有多少的空格；上限为10。该值若小于1，则意味着没有空格；如果该参数为字符串(字符串的前十个字母)，该字符串将被作为空格；如果该参数没有提供（或者为null）将没有空格。


**注意：**
- 非数组对象的属性不能保证以特定的顺序出现在序列化后的字符串中。
- *布尔值*、*数字*、*字符串*的包装对象在序列化过程中会自动转换成对应的原始值。
- `undefined`、任意的`函数`以及 `symbol` 值，在序列化过程中会被忽略（出现在*非数组对象的属性值*中时）或者被转换成 `null`（出现在*数组*中时）。
- 所有以 `symbol` 为属性键的属性都会被完全忽略掉，即便 `replacer` 参数中强制指定包含了它们。
- *不可枚举*的属性会被忽略

**示例：**
```js
// 基本例子
JSON.stringify({});                        // '{}'
JSON.stringify(true);                      // 'true'
JSON.stringify("foo");                     // '"foo"'
JSON.stringify([1, "false", false]);       // '[1,"false",false]'
JSON.stringify({ x: 5 });                  // '{"x":5}'

JSON.stringify({x: undefined, y: Object, z: Symbol("")}); 
// '{}'

JSON.stringify([undefined, Object, Symbol("")]);          
// '[null,null,null]' 

```

#### replacer 参数

```js
// 参数为 函数
function replacer(key, value) {
  if (typeof value === "string") {
    return undefined;
  }
  return value;
}

var foo = {foundation: "Mozilla", model: "box", week: 45, transport: "car", month: 7};
var jsonString = JSON.stringify(foo, replacer); //  {"week":45,"month":7}

// 参数为 Array
JSON.stringify(foo, ['week', 'month']);  
// '{"week":45,"month":7}', 只保留“week”和“month”属性值。
```


#### space 参数

space 参数用来控制结果字符串里面的间距。如果是一个数字, 则在字符串化时每一级别会比上一级别缩进多这个数字值的空格（最多10个空格）；如果是一个字符串，则每一级别会比上一级别多缩进用该字符串（或该字符串的前十个字符）。

![大话JSON](https://raw.githubusercontent.com/guoshuai6511/blog/master/images/da-hua-json.png)

### 3. `toJSON`

如果一个被序列化的对象拥有 toJSON 方法，那么该 toJSON 方法就会覆盖该对象默认的序列化行为：不是那个对象被序列化，而是调用 toJSON 方法后的返回值会被序列化。
```js
var obj = {
  foo: 'foo',
  toJSON: function () {
    return 'bar';
  }
};
JSON.stringify(obj);      // '"bar"'
JSON.stringify({x: obj}); // '{"x":"bar"}'
```
**`Date.prototype.toJSON()`**  
原生 Date对象有一个 toJSON() 方法，将 Date() 对象转换成 ISO 8601 日期字符串。见[](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date/toJSON);
```js
var jsonDate = (new Date()).toJSON();// "2017-07-27T09:57:03.706Z"
```


## JSON 和 JavaScript

JSON 基于 JavaScript 而来，但又不完全一样，所以严格来说 [JSON 并不是 JavaScript 的子集](http://timelessrepo.com/json-isnt-a-javascript-subset)。

| JavaScript | JSON |
|--|--|
|对象和数组|属性名称必须是双引号字符串；后缀逗号被禁止。最后一个属性后面不能有逗号。|
|数值	| 前导0是禁止的（在JSON.stringify 0将被忽略，但在JSON.parse它将抛出SyntaxError）；小数点后必须至少有一位数字。|
|字符串|只有有限的一些字符可能会被转义；禁止某些控制字符; Unicode 行分隔符 (U+2028) 和段分隔符 (U+2029)被允许 ; 字符串必须是双引号。请参见以下示例，其中 JSON.parse() 能够正常解析，但把它当作JavaScript解析时会抛出 SyntaxError 错误: |

字符串解析错误：
```js
    let code = '"\u2028\u2029"';
    JSON.parse(code);  // 工作正常
    eval(code);  // 失败
```

## 参考来源

> [Introducing JSON](http://json.org/index.html)  
> [JSON--MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/JSON)  
> [JSON: The JavaScript subset that isn't( JSON 不是 JavaScript 的子集 )](http://timelessrepo.com/json-isnt-a-javascript-subset)