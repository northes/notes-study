## 新的变量声明方式

ES6 引入了新的变量声明方式，包括 `let`、`const`、`import` 和 `class`，这些新的声明方式带来了更严格的作用域控制和更清晰的代码结构。以下是对这些新特性的总结：

### 1. `let`
- **块级作用域**：`let` 声明的变量只在其声明的代码块内有效，例如在 `if` 语句或 `for` 循环中。
- **暂时性死区**（Temporal Dead Zone, TDZ）：在变量声明之前，该变量处于不可访问状态，尝试访问会抛出错误。
- **不允许重复声明**：在同一作用域内，不能重复声明同一个变量。

### 2. `const`
- **声明常量**：`const` 用于声明一个只读的常量，必须在声明时初始化。
- **块级作用域**：与 `let` 相同，`const` 也具有块级作用域。
- **不支持变量提升**：`const` 声明的常量不能在声明之前访问，存在暂时性死区。
- **对象属性可变性**：对于对象类型的常量，对象本身不可重新赋值，但对象的属性可以修改。

### 3. `import`
- **模块导入**：`import` 用于从其他模块导入绑定到变量或命名空间。
- **重命名导入**：可以使用 `as` 关键字为导入的变量指定新名称。
- **提升效果**：`import` 语句会被提升到模块的顶部执行。

### 4. `class`
- **类的定义**：`class` 关键字用于定义类，它是构造函数的语法糖。
- **构造函数**：类的 `constructor` 方法相当于构造函数，用于初始化实例属性。
- **原型方法**：类的方法定义在类的原型上，所有实例共享这些方法。
- **实例化**：使用 `new` 关键字创建类的实例。
- **不存在变量提升**：`class` 声明必须在使用前定义，不存在变量提升。

### 总结

ES6 的新变量声明方式提供了更强大的作用域控制和更清晰的代码结构，使得 JavaScript 编程更加规范和安全。`let` 和 `const` 通过块级作用域和暂时性死区减少了作用域相关的错误，而 `import` 和 `class` 则简化了模块导入和面向对象编程。合理使用这些新特性可以提高代码的可读性和可维护性，减少调试时间，提高开发效率。


## 解构

### 数组

```js
// ES5
var arr = [111,222,333]
var first = arr[0]
var second = arr[1]
var third = arr[3]
// ES6
let [first,second,third] = arr;
```

本质上属于 `模式匹配`、`映射关系`，只要等号两边的模式相同，一一对应，左边的变量就会被赋值给右边对应的值

```js
// 左右不匹配
let [x,y] = ['a'];
x // "a"
y // "undefined"
// 设置默认值可解
let [x,y='b'] = ['a']
y // 'b'
```

```js
// 使用简单的方式将数组的值分别赋值到多个变量中，使用下标对应
let [a,b,c] = [1,2,3]
```

```js
// 获取二维数组，三维数组，甚至多维数组中的值
let [foo,[[bar],baz]] = [1,[[2],3]]
foo // 1
bar // 2
baz // 3

// 不需要匹配的位置可以留空
[,,third] = [1,2,3];
third // 3

// 使用...拓展运算符
let [head,...body] = [1,2,3,4]
body // [2,3,4]

// 使用...拼接数组
let arr1 = [8]
let arr2 = [9,11,12,13]
arr1.push(arr2) // [8,[9,11,12,13]]
arr1.push(...arr2) // [8,9,11,12,13]
```

### 对象

数组元素的解构是按照下标对应的，对象的属性没有次数，由 `key` 对应

```js
let {a,b} = {a:"111",z:"222"}
a // 111
b // undefined

// 修改变量名与映射可解，自定义属性名称
let {a,z:b} = {a:"111",z:"222"}
a // 111
b // 222
```

```js
let itemObj = {
	arr: [
		"aaa",
		{ secondLevel: "bbb" }
	]
};
let { arr: [firstLevel,{ secondLevel }] } = itemObj;
firstLevel // "aaa"
secondLevel // "bbb"
```

### 字符串

```js
const [a,b,c,d,e] = 'hello';
a // "h"
b // "e"
c // "l"
d // "l"
e // "o"

let { length: len } = 'hello'
len // 5 (将hello的length结果解构到len变量中)
```

### 数值和布尔值

只要等号右边的值不是对象或数组，就先将其转为对象。如果转换之后的对象或原对象拥有 `Iterator` 接口，则可以进行解构赋值，否则会报错。

```js
// 数值和布尔值的包装对象都有toString属性
let { toString: str } = 111;
str === Number.prototype.toString // true

let {toString: str} = true;
str === Boolean.prototype.toString // true

// 不能转换成有prop属性的对象，报错
let {prop: x} = undefined; // TypeError
let {prop: y} = null // TypeError

// ES6 中，Set或Generator生成器函数等都有 Iterator 接口，因此也可以进行解构
let [a,b,c] = new Set([1,2,3])
a // 1
b // 2 
c // 3
```

### 圆括号

```js
let obj;
{obj}={obj:'James'}
obj // 报错。大括号 { 位于行首，且匹配 } , js会认为这是一个代码块，所以等号就报错了

// 解决
({obj}={obj:'James'})
obj // 'James'
```

### 实际用途

```js
// 交换变量
let x = 1;
let y = 2;
[x,y]=[y,x]
x // 2
y // 1
```

```js
// 函数参数定义
function foo([width,height,left,right]) {
 // ...
}
foo([100,200,300,300])

// 使用对象解构
function foo({width,height,left,right}) {
 // ...
}
foo({left:300, width:100, right:300, height:200})
```

```js
// 从函数返回多个值
// 返回一个数组
function foo() {
 return [1,2,3]
}
let [a,b,c] = foo();

// 返回一个对象
function foo2() {
 return {
  a: 1,
  b: 2
 }
}
let {a,b} = foo2();
```

```js
// 引入模块指定方法
```