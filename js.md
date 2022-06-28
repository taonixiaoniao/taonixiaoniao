# 基础知识

### 数组

#### 添加属性

数组不仅能使用`arr[0] = 0`这样的形式添加属性，也可以通过`arr['str'] = str`来为数组添加属性，不过这样只是给数组添加了一个普通的属性，它在数组中不占有长度，即没有索引。

```js
let arr = []
arr[0] = 0;
arr[1] = 1;
arr['三'] = 3
console.log(arr); // [ 0, 1, '三': 3 ]
console.log(arr.length); // 2
console.log(arr['三']); // 3
```

如果试图向数组添加一个属性，但是属性名看起来像一个数字(例如字符串'1')，那它就会变成一个数值下标。

```js
let arr = [0, 1, 2]
arr['3'] = 3
console.log(arr); // [ 0, 1, 2, 3 ]
console.log(arr.length); // 4
```
### 对象

#### 对象是什么
对象就是键/值对的集合，可以通过`.[propName]`或者`["propName"]`语法来获取属性值。访问属性时，引擎实际上会调用内部的默认操作`[[Get]]`操作，检查对象是否包含这个属性，如果没有就查找`[[Prototype]]`链。

##### null为对象bug
```js
console.log(typeof(null)) // object
```
这是js语言本身的bug，null是基本类型之一
**原理：**不同的对象底层都表示为二进制，在js中二进制前三位为0则会判断为object类型，而null在二进制中的表示全为0，就被误判为object了

#### 内置对象
##### 概念
`js` 还有一些特殊的对象子类型，被称为内置对象

- `String` 
- `Number` 
- `Boolean`
- `Object`
- `Function`
- `Array`
- `Math` 数学对象
- `Date` 日期对象
- `RegExp` 正则对象
- `Error` 错误对象

这些对象(`Math`除外)可以通过类似`new String('a')`使用new关键字来创建一个实例，即它们都可以当做**构造函数**来调用，从而构造一个对应子类型的新对象。

**注意：**

- `null`和`undefined`没有对应的构造形式，它们只有文字形式，而`Date`正好相反，有构造形式没有文字形式，所以只能使用`date = new Date()`的方式来创建一个日期对象。
- `Date`对象是基于1970年1月1日（世界标准时间）起的毫秒数（时间戳）
##### 基本包装类型
- 把简单数据类型包装成为复杂数据类型，这样基本数据类型就有了属性和方法。为了方便操作基本数据类型，`js`还提供了三个特殊的引用类型：`String`、`Number`、`Boolean`，也是三种`js`的内置对象

##### 字符串的不可变
字符串里面的值不可变。虽然看上去内容改变了，但其实是地址变了，内存中开辟了一个新的内存空间。重新给str赋值或者拼接字符串的时候，电脑会一直开辟新的空间来保存新的str的值，所以要尽量避免进行大量的字符串赋值和平拼接操作。

#### 内置对象方法
内置对象为开发者提供了许多基础且实用的方法
###### Number
- Number.isNaN() 判断是不是非数字，如果是数字返回false，如果不是数字返回true
###### Math
- Math.abs(num)  绝对值 隐式转换 自动把字符型数字转化成数值型
- Math.ceil(num)  向上取整；
- Math.floor(num)  向下取整
- Math.max(num1, num2)  求最大值
- Math.min(num1, num2)  求最小值
- Math.pow(a, n)  a的n次方
- Math.sqrt(a)  对a开根号
- Math.PI  圆周率
- Math.round(num)  四舍五入 就近取整 -1.5取-1而不是-2
- Math.random()  返回一个随机的小数 取值范围[0,1)
- (num/n).toFixed(m)  将结果保留m位小数

###### Date
`Date`方法参数的常用写法

- 数字型：2021,7,25	
- 字符串型： '2021-7-25 00:00:00'
- 数字型的返回值比输入的值大一个月

日期格式化
- `date.getFullYear()`  获得 `date` 年
- `date.getMonth()`  获得 `date` 月（0-11）返回的月份小一个月
- `date.getDate()`  获得 `date` 天日期 （0-6）周日是0
- `date.getDay()`  获得 `date` 星期几（1-7）
- `date.getHours()`  获得 `date` 小时
- `date.getMinutes()`  获得 `date` 分钟
- `date.getSeconds()`  获得 `date` 秒钟
```js
let date = new Date('2021-11-7 10:02:33')
console.log(date.getFullYear()) // 2021
console.log(date.getMonth()) // 11
console.log(date.getDate()) // 0
console.log(date.getDay()) // 7
```
获取时间（戳）
- `time.valueOf()`：返回`time`的时间戳
- `time.getTime()`：返回`time`的时间戳
- `let date = new Date()` ：获取当前地区标准时间
- `let date = +new Date()` ：`+new Date()`可以直接返回当前时间戳
- `let date = Date.now()`：获取当前时间戳
```js
let date = new Date()
console.log(date) // 2021 22:11:54 GMT+0800 (中国标准时间)

let time = new Date('2021-11-6 10:02:33')
valueOf(time) // 1636164153000
getTime(time) // 1636164153000

let date = +new Date()
console.log(date) // 1636166214823
let date2 = Date.now()
console.log(date2) // 1636166214823
```
###### Array
**增减元素**

- `arr.unshift(x1,x2...)`：开头添加一个或多个元素，修改原数组,返回新的长度
- `arr.push(x1,x2...)`：末尾添加一个或多个元素，修改原数组，返回新的长度
- `arr.shift()`：删除arr数组的第一个元素，修改原数组，返回它删除的元素的值
- `arr.pop() `：删除数组最后一个元素，修改原数组，返回它删除的元素的值
```js
let arr = [1, 2, 3]
console.log(arr.pop()) // 3
console.log(arr) // [ 1, 2 ]
arr.unshift(0)
console.log(arr) // [0, 1, 2]
```
**数组排序**

- `arr.reverse()`：颠倒数组中元素的顺序，无参数，该方法会改变原来的数组，返回新数组
- `arr.sort()`：对数组元素进行排序，该方法会改变原来的数组，返回新数组
	- `arr.sort((a, b) => a - b)` 升序排序
	- `arr.sort((a, b) => b - a)` 降序排序
```js
let arr = [2, 4, 1, 3]
arr.reverse()
console.log(arr) // [ 3, 1, 4, 2 ]

arr.sort((a, b) => a - b)
console.log(arr) // [ 1, 2, 3, 4 ]

arr.sort((a, b) => b - a)
console.log(arr) // [ 4 ,3, 2, 1 ]
```
**数组索引**

- `arr.indexOf(a)`：数组中查找给定元素`a`，从前往后查找，如果存在返回索引号，否则返回-1
- `arr.lastIndexOf(a)`：数组中查找给定元素`a`，从后往前查找，如果存在返回索引号，否则返回-1
- 这两种方法都只返回第一个满足元素的索引号。
```js
let arr = [1, 2, 3, 1]
console.log(arr.indexOf(1)) // 0
console.log(arr.lastIndexOf(1)) // 1
```
- `arr.findIndex(callback)` 返回数组中满足测试函数的第一个元素的索引。若没有找到对应元素则返回-1。`callback`会自动将传入以下参数：
	- `element` 当前元素
	- `index` 当前元素索引
	- `arr` 调用 `findIndex` 方法的数组
```js
	// 查找数组中第一个2的倍数
	const arr = [1, 2, 3, 4, 5]
	console.log(arr.findIndex(num => num % 2 === 0)); // 1
```

**其他方法**

- `arr. toString()`：把数组转化成字符串，逗号分隔每一项，返回一个字符串。
- `arr.join`('分隔符') ：把数组中的所有元素转化为一个字符串，返回一个字符串。
```js
let arr = [1, 2, 3]
console.log(arr.toString()) // 1, 2, 3

let arr2 = [a, b, c]
console.log(arr2.join('')) // abc
```
- `arr.concat(arr1, arr2...)` ：连接两个或多个数组，不影响原数组，返回新的数组
- `arr.slice(start, end)` ：从start截取到end，返回截取后的新数组。end截取不到，不传end默认截取到数组末尾。
- `arr.splice()`：数组删除、替换、添加
	- `arr.splice(indx, n)`：从`index`索引开始删除`n`项，会影响原数组
		- `n === 0`时不删除，`n === 1`删除一项，`n === 2`删除两项，以此类推
	- `arr.splice(indx, n, x)`：从`index`索印开始`x`替换`n`项，会影响原数组
		- `n === 0`时则为插入操作，`n === 1`替换一项，`n === 2`替换两项，以此类推
- `arr.entries()`：返回一个新的`Array Iterator`对象，该对象包含数组中每个索引的键/值对。
- 将一个数组重构为长度为n、每个元素为0的数组：`const arr = new Array(n).fill(0)`
- 构建一个`m * n`二元数组：`const arr = Array(n).fill(0).map(item => Array(m).fill(0))`
```js
const arr = ['a', 'b', 'c', 'd']
arr.splice(1, 1)
console.log(arr) // ['a', 'c', 'd']

arr.splice(1, 0, 'b')
console.log(arr) // ['a', 'b', 'c', 'd']

arr.splice(4, 1, 'e')
console.log(arr) // ['a', 'b', 'c', 'd', 'e']

const arr1 = ['a', 'b', 'c']
const iterator1 = arr1.entries()
console.log(iterator1.next().value) // [0, "a"]
console.log(iterator1.next().value) // [1, "b"]

const arr2 = new Array(3).fill(0)
console.log(arr2) // [ 0, 0, 0]
```
- `arr.includes()`判断一个数组是否包含一个指定的值，根据情况，如果包含则返回 true，否则返回 false。
```js
const arr = [1, 2, 3, 4]
console.log(arr.includes(2)); // true
console.log(arr.includes(5)); // false

// 多重条件判断时使用
// 原代码
if (type == 1 || type == 2 || type == 3 ||) {}
// 改进后代码
const arr = [1, 2, 3]
if (arr.includes(type)) {}
```

**操作数组**

- arr.reduce() 对数组中的每个元素执行一个由您提供的**reducer**函数(升序执行)，将其结果汇总为单个返回值
```js
const array1 = [1, 2, 3, 4];
const reducer = (previousValue, currentValue) => previousValue + currentValue;

// 1 + 2 + 3 + 4
console.log(array1.reduce(reducer));
// expected output: 10

// 5 + 1 + 2 + 3 + 4
console.log(array1.reduce(reducer, 5));
// expected output: 15
```
- arr.flat()  按照一个可指定的深度递归遍历数组，并将所有元素与遍历到的子数组中的元素合并为一个新数组返回。
```js
let arr = [[1, 2], [3, 4]]
console.log(arr.flat()); // [ 1, 2, 3, 4 ]
let arr1 = [[1, 2], [[3, 4]]]
console.log(arr1.flat()); // [ 1, 2, [ 3, 4 ] ]
console.log(arr1.flat(2)); // [ 1, 2, 3, 4 ]
```
###### String

**检查字符位置**
- `str.indexOf(s)`  在str中顺序查找`s`第一次出现的位置，如果存在返回其索引，否则返回-1，同数组
- `str.lastIndexOf(s)`  在`str`中逆序查找`s`第一次出现的位置，如果存在返回其索引，否则返回-1，同数组
- `str.includes()` 判断一个字符串是否包含在字符串`str`中，如果是返回`true`，否则返回`false`


**操作字符串**

- `str.concat(str1, str2...)` ：等效于‘+’，用于拼接多个字符串，与数组同
- `str.substring(start, end) `：从start位置开始，截取到end位置，end取不到，不影响原字符串
	- 如果`start=end`返回空字符串
	- 如果省略`end`，一直取到字符串末尾
	- 如果任一参数大于`str.length`，则被当做`str.length`
	- 如果`start > end`，执行结果就像两个参数调换了一样
- `str.slice(start, end)`：从start位置开始，截取到end位置，end取不到，不影响原字符串
	- 接受负值，`-3`被看做是`str.length - 3`
	- `start > end`时不会像`substring`一样产生参数倒置的效果，而是直接返回空字符串
- `str.replace('a', 'b')` 替换字符，将`str`中的字符串`'a'`替换为`'b'`，只替换第一个`'a'`
	- `replace`可以通过正则实现全局替换、忽略大小写等功能
	- `replace`第二个参数可以接受一个回调函数实现替换
```js
let str="Mr Blue has a blue house and a blue car";
let n=str.replace(/blue/g,"red"); //全局替换
//Mr Blue has a red house and a red car

var str="Mr Blue has a blue house and a blue car";
var n=str.replace(/blue/gi, "red"); // 全局替换并且忽略大小写
// Mr red has a red house and a red car

let template = '我是{{name}}，年龄{{age}}，性别{{sex}}'
let data = {
  name: '卢本伟',
  age: 18,
  sex: '男'
}
console.log(render(template, data));
function render(template, data) {
  let computed = template.replace(/\{\{(\w+)\}\}/g, function (match, key) {
    console.log(match, key);
    return data[key]
  })
  return computed
}
//{{name}} name {{age}} age {{sex}} sex 我是卢本伟，年龄18，性别男
```
- str.split('分隔符')  字符转化为数组，以分隔符有为界限，把字符串分成n个数组元素
- str.charAt(index)  返回字符串中index位置(索引)的字符
###### 字符串编码
- str.charCodeAt()  该方法可以把字符串编码转换为一个数字，只对第一个字符有效
	- 字符串'0'-'9'对应48-57
	- 字符串'a'-'z'对应97-122
###### 字符串翻转
一般字符串不能直接翻转，但是可以把字符串转化成数组进行翻转，然后再转换回字符串
str.split('').reverse('').join('') 就可以翻转str

```js
let str = 'abc'
str = str.split('').reverse().join('')
console.log(str) // cba
```
- str.match()   检索返回一个字符串匹配正则表达式的结果。
```js
let str = 'aa bb cc dd'
console.log(str.match(/\b\w+\b/g)); //[aa, bb, cc, dd]
```

#### 对象的内容
###### 对象属性的存储
在引擎内部，对象的属性的存储方式是多种多样的，一般不会直接存储在对象容器内部。存储在对象内部的是这些属性的名称，它们就像指针一样指向属性值真正的存储位置
###### 访问对象属性
加入对象Obj中有一个属性为a，如果要访问Obj上a位置上的值，有两种语法可以做到
- Obj.a 被称为"属性访问"
- Obj['a'] 被称为"键访问"
- 区别：
	- .操作符要求属性名满足标识符的命名规范
	- ['..']操作符可以接受任意UTF-8/Unicode字符串作为属性名
	- 例如要引用名称为'Super-Fun'的属性，就必须使用['..']语法访问
- 在对象中，属性名永远是字符串，如果使用string以外的其他值作为属性名，则其会被转换成一个字符串，即使是数字也不例外
###### 可计算属性名
es6增加了计算属性名，可以在文字中使用[ ]包裹一个表达式来当做属性名
```js
const prefix = 'foo'
const Obj = {
	[prefix + 'bar'] : "hello",
	[prefix + 'baz'] : "world"
}
```
###### 复制对象
如何准确地表示对象Obj的复制：首先判断是浅复制(浅拷贝)还是深复制(深拷贝)，对于深拷贝来说，如果Obj中包含了复制的目的对象，那么就会造成死循环的问题，解决方案如下：
- JSON化，这种方法需要保证对象是JSON安全的，所以只使用部分情况
```js
const newObj = JSON.parse(JSON.stringfy(Obj))
```
###### 浅拷贝
es6定义了`Object.assign(targetObj, obj1, obj2...)`方法实现浅拷贝，该方法的第一个参数是目标对象，其他参数都是被拷贝的源对象。它会遍历源对象的所有**可枚举**的**自有键**并把它们复制(使用=赋值)到目标对象，最后返回目标对象
```js
const Obj1 = {
  b: false
}
const arr = []
function fn() { }
const Obj = {
  a: 2,
  b: arr,
  c: fn,
  d: Obj1
}
const newObj = Object.assign({}, Obj)
console.log(newObj) 
// { a: 2, b: [], c: [Function: fn], d: { b: false } }
```
###### 属性描述符
`es5` 之前，`js `语言本身没有提供可以直接检测属性特性的方法，比如判断属性是否是只读属性。
`es5` 之后，所有属性都具备了属性描述符

- `writable `：是否可以修改属性的值，`true ->`可以修改，`false ->`不可修改
- `enumerable `：是否可以被枚举，`true ->` 可枚举，`false ->` 不可枚举
- `configurable `：是否可以被更改配置，如果属性可配置，就可以使用 `defineProperty` 更改属性描述符
	- 注意，即使属性是`configurable:false`，还是可以把writable由状态true改为false，但是无法由false改为true
	- 将 `configurable`改为 `false`是单向操作，不可逆转，而且还会禁止删除这个属性
- 检测属性描述：`Object.getOwnPropertyDescriptor(Obj, 'a')`，读取Obj对象的a属性的属性描述符
- 配置属性描述符：如果 `configurable`为true，就可以使用 `defineProperty`更改属性描述符，`defineProperty(obj, a, {writable:false})`可以把 `obj`对象中的属性 `a `的属性描述符 `writable`修改为 `false`
- `Object.defineProperty()`： 在一个对象上定义一个新属性，或者修改一个对象的现有属性，并返回此对象，该操作被称为**对象劫持**。
```js
const Obj = {
  a: 3
}
console.log(Object.getOwnPropertyDescriptor(Obj, 'a'))
// { value: 3, writable: true, enumerable: true, configurable: true }

Object.defineProperty(Obj, 'a', {value: 2, writable: false })

console.log(Object.getOwnPropertyDescriptor(Obj, 'a'))
// { value: 2, writable: false, enumerable: true, configurable: true }
```
###### 禁止扩展
- 如果要使一个对象不可扩展，也就是不能添加新的属性，可以使用`Object.preventExtensions(obj)`

```js
const Obj = {
	a : 2
}
Object.preventExtensions(Obj)

Obj.b = 3
console.log(Obj.b) // undefined
```
###### 密封
`Object.seal(obj)`可以创建一个"密封"的对象，这个方法实际上会在一个现有对象上调用`Object.preventExtensions(Obj)`并把现有的所有属性标记为`configurable:false`

```js
const Obj = {
  a: 1
}
Object.seal(Obj)

delete (Obj.a)
console.log(Obj.a) // 1

Obj.b = 2 
console.log(Obj.b) // undefined

Object.defineProperty(Obj, 'a', { writable: false })
console.log(Object.getOwnPropertyDescriptor(Obj, 'a')) 
// { value: 1, writable: true, enumerable: true, configurable: false }
```
###### 冻结
`Object.freeze(obj)`会创建一个冻结对象，该方法会在一个现有对象上调用Object.seal()并把所有的'数据访问'属性标记为`writable:false`，这样就无法修改他们的值。这个方法是对象上级别最高的不可变性，它会禁止对于对象本身及其任意直接属性的修改。
```js
const obj = {
  a: 1
}
Object.freeze(obj)
obj.a = 2
delete obj.a
console.log(obj.a); // 1

obj.b = 2
console.log(obj.b); // undefined
```
###### [[Get]]
在语言规范中obj.a在obj对象上实际上是实现了`[[Get]]`操作，有点像函数调用`[[Get]]()`，对象默认的[[Get]]操作首先在对象中查找是否有名称相同的属性，如果有则返回属性的值，如果没有，则会去obj的原型链上去查找，如果没找到则会返回undefined
```js
Object.prototype.a = 1
const obj = {}
console.log(obj.a); // 1
console.log(obj.b); // undefined
```
###### [[Put]]
一般来说，给对象的属性赋值时会触发[[Put]]操作，但[[Put]]被触发时，实际的行为取决于多种因素。
1.如果对象中已经存在该属性，[[Put]]算法大致会检查以下内容
- 属性是否是访问描述符，如果是并且存在就调用getter和setter
- 属性的数据描述中writable是否为false，如果是，在非严格模式下静默失败，在严格模式下抛出TypeError异常
- 如果都不是，将该值设置为属性的值
###### getter和setter
在es5中可以使用getter和setter部分来改写默认操作，它们都是隐藏函数，getter会在获取属性值得时候调用，setter会在设置属性值得时候调用。如果给一个属性定义getter或者setter或者两者都有时，js会忽略它们的value和writable属性，取而代之的是关心get和set特性。
- 
```js
const obj = {
  get a() {
    return 1
  }
}
console.log(obj.a); // 1

const obj = {
  get a() {
    return this._a
  },

  set a(val) {
    this._a = val
  }
}
console.log(obj.a); // undefined
obj.a = 1
console.log(obj.a); // 1
```
###### 存在性
当一个对象的某个属性的值为undefined时，可能有两种情况
- 这个值不存在
- 这个值本身为undefined

如何区分？我们可以在不访问属性值的情况下判断对象中是否有这个属性。
**in操作符**
in操作符会检查属性是否在对象及其[[Prototype]]原型链中
```js
const obj = {
	a:2
} 
console.log('a' in obj) // true
console.log('b' in obj) // false
```
**hasOwnProperty**
obj.hasOwnProperty(a)只会检查a属性是否存在于obj对象中，不会检查[[Prototype]]原型链，接受的参数必须是字符串。
**注意：**所有的普通对象都可以通过Object.protype的委托来访问hasOwnPeoperty(...)，但是有的对象有可能没有连接到Object.prototype，比如Object.create(null)，在这种情况下就会失败。这时可以使用更强硬的方法来判断：`Object.prototype.hasOwnProperty.call(obj, 'a')

###### 枚举
- `obj.propertyIsEnumerable()`  判断对象 `obj` 中某个属性是否可以枚举，该方法会检查给定的属性名是否存在于对象中（不查找原型链）并且满足 `enumerable : true`。
- `Object.keys()` 返回一个数组，包含所有可枚举属性，不查找原型链，在`es6`之后的标准中，传入非对象参数会强制转化成对象。
```js
Object.keys(1) // []
Object.keys('a') // ['1']
Object.keys('a', 'a') // ['1', '2']
Object.keys(true) // []
Object.keys(Symbol()) // []
```
- `Object.values()` 返回一个数组，包含所有可枚举的属性的值，不查找原型链
- `Object.getOwnPropertyNames()` 返回一个数组，包含所有属性，无论是否可以枚举。

###### 遍历
如何遍历对象的可枚举属性的值，js中提供的许多的遍历方法如 `forEach`、`every`、`some `等没有顺序，在一些场景下不可靠，普通的 `for` 循环遍历的是下标或者说是指向值的指针。`for of` 循环可以实现遍历属性的值，它会向被访问对象请求一个迭代器对象，然后通过这个迭代器对象的 `next()` 方法来遍历所有返回值。js中所有可迭代的数据结构和对象都内置了`@@iterator` 接口，`ES6`中有一个符号 `Symbol.iterator` 来获取对象的 `@@iterator` 内部属性。
```js
const myObj = {
  a: 1,
  b: 2
}
Object.defineProperty(myObj, Symbol.interator, {
  enumerable: false,
  writable: false,
  configurable: true,
  value: function () {
    let that = this,
      i = 0,
      ks = Object.keys(that)
    return {
      next: function () {
        return {
          value: that[ks[i++]],
          done: i > ks.length
        }
      }
    }
  }
})
const obj = myObj[Symbol.interator]()
console.log(obj.next()); // { value: 1, done: false }
console.log(obj.next()); // { value: 2, done: false }
console.log(obj.next()); // { value: [Function: value], done: true }
```
```js
const obj = {}
Object.defineProperty(obj, 'a', {
  enumerable: true,
  value: 2
})
Object.defineProperty(obj, 'b', {
  enumerable: false,
  value: 3
})

console.log(obj.propertyIsEnumerable('a')); // true
console.log(obj.propertyIsEnumerable('b')); // false
console.log(obj.propertyIsEnumerable('c')); // false
```
我们也可以直接在定义对象时进行声明，比如`const obj = {[Symbol.iterator]:function(){}}`
#### 对象的方法
###### Object的方法
- Object.defineProperty() 在一个对象上定义一个新属性，或者修改一个对象的现有属性，并返回此对象，也称为劫持对象的属性，可以定义或者修改属性描述符，也被称为数据劫持
- Object.create() 创建一个新对象，使用现有的对象来提供新创建的对象的__proto__，可以定义或者修改属性描述符
```js
var person = {
	name : "Van"
};
var anotherPerson = Object.create(person, {
	name : {
		value : "Louis"
	}
});
console.log(anotherPerson.name);//"Louis"

anotherPerson.defineProperty(anotherPerson, name, {
	value: 'Lubenwei'
})
console.log(anotherPerson.name) // 'Lubenwei'
```
- Object.valueOf() 返回对象的原始值，Array返回数组对象本身；Boolean返回布尔值；Date返回时间戳；Function返回函数本身；Number返回数字值；Object返回对象本身；String返回字符串值；Math和Error没有valueOf方法
- Object.toString() 可以通过 toString() 来获取每个对象的类型
```js
const arr = [1, 2, 'ac', 'acb']
console.log(arr.valueOf()); // [ 1, 2, 'ac', 'acb' ]
console.log(arr[0].valueOf()); // 1
console.log(arr[2].valueOf()); // 'ac'
console.log(toString.call(arr)); // [object Array]
console.log(toString.call(arr[0])); // [object Number]
console.log(toString.call(arr[2])); // [object String]

const obj = {
  foo: function () { },
  b: new Date(),
  c: true
}
console.log(obj.valueOf());  // { foo: [Function: foo], b: 2021-11-12T13:19:40.335Z, c: true }
console.log(obj.foo.valueOf());// [Function: foo]
console.log(obj.b.valueOf()); // 1636723180335
console.log(obj.c.valueOf()); // true
console.log(toString.call(obj)) // [object Object] 
console.log(toString.call(obj.foo)) // [object Function]
console.log(toString.call(obj.b)) // [object Date]
console.log(toString.call(obj.c)) // [object Boolean]
```

- `Object.getOwnPropertySymbols()`：返回一个给定对象自身的所有 `Symbol` 属性的数组
- `Object.fromEntries()`：把键值对列表转换为一个对象，可以将 `Map` 转化为 `Object`
- `Object.assign(target, obj1, obj2, ...)`：将任意多个对象浅拷贝给 `target`

### 类
#### js中的类
`javaScript` 中的类和其他语言的类不是一种东西，因为 `javaScript` 是原型式的继承，`javaScript` 中的类是为了满足于类设计模式这个普遍需求而创造出来的，只是构造函数的语法糖
###### 语法糖
- 语法糖 （英语： Syntactic sugar ）是由英国 计算机科学家 彼得·兰丁 发明的一个术语，指计算机语言中添加的某种语法，这种语法对语言的功能没有影响，但是更方便程序员使用。语法糖让程序更加简洁，有更高的可读性。
- 语法糖用更简练的言语表达较复杂的含义。在得到广泛接受的情况之下，可以提升交流的效率。
- 语法糖不只是因为加糖后代码功能与加糖前一致，更重要的是，**糖在不改变其所在的位置的语法结构前提下，实现了运行时等价**
#### 类的机制
类是一个抽象的表示，它描述了实例所需要做的事情，但它自身并不是一个实例。必须实例化类才能进行相关操作。
##### 建造
一个类就是一个蓝图。为了可以获得可以交互的对象，需要按照类来建造（实例化）一个东西，这个东西称为实例。
##### 构造函数
类实例是由一个特殊的类方法构造的，这个方法名通常和类名相同，被称为构造函数。这个方法的任务就是初始化实例所需要的所有状态。
#### 类的继承
在面向对象的语言中，可以先定义一个父类，再定义一个继承父类的子类。定义好一个子类后，相对于父类来说他就是一个独立并完全不同的类。子类会包含父类行为的原始副本，但也可以重写所有继承的行为甚至定义新行为。
##### 多态
同一操作作用于不同的对象上面，可以产生不同的解释和不同的执行结果。
在类的继承中，多态表现为：

- 任何方法都可以继承层次中高层的方法（无论高层的方法和当前方法是否重名）
- 在继承链的不同层次中一个方法名可以被定义多次，当调用方法时选择合适的定义。
- 子类通过相对多态引用父类的方法得到的仅仅是父类方法的一个副本，子类对继承到的方法重写不会影响父类的方法。
##### 多重继承
- 有些面向类的语言允许子类继承多个父类，所有父类的定义都会被复制到子类中。
- 对类而言多重继承是一个非常有用的功能，可以把多种功能组合在一起，然而这也会带来很多复杂的问题。
	- 如果两个父类都定义了`fn1`方法，子类引用的是哪一个？如果每次对手动指定具体父类的`fn1`方法，多态 继承的很多优点就不存在了。
	- 钻石问题：子类`D`继承自两个父类`B`和`C`，这两个父类都继承自`A`。如果`A`中有`fn1`方法并且`B`和`C`都重写了这个方法（多态），那么`D`引用`fn1`时应该使用哪个`fn1`？
	- 在`c++`中解决钻石问题的方法：`B`和`C`继承`A`时都使用`virtual`来标注，对于每一个`D`对象，`c++`会保证只有一个`A`类的子类会被创建，也就是`B`和`C`只有一个会生效。
##### super关键字
- `super`关键字可以认为是实现相对多态引用的`api`
###### 作为函数使用
当使用`class`和`extends`关键字声明一个子类继承父类时，子类没有自己的`this`，而是继承父类的`this`，因此必须调用一次`super`方法。假如父类名称为`Father`，那么`super`就等同于`Father.prototype.constructor.call(this, props)`
```js
class Father {
  constructor() {
    console.log(new.target.name);
  }
}

class Son extends Father {
  constructor() {
    super()
  }
}
console.log(new Father()); // Father
console.log(new Son()); // Son
```
###### 作为对象使用
在普通方法中，指向父类的原型对象；在静态方法中，指向父类。
```js
class A {
  c() {
    return 2;
  }
}

class B extends A {
  constructor() {
    super();
    console.log(super.c()); // 2
  }
}

let b = new B();
```
上面代码中，子类 B 当中的 `super.c()`，就是将 `super` 当作一个对象使用。这时，`super` 在普通方法之中，指向 `A.prototype`，所以 `super.c()` 就相当于 `A.prototype.c()`
**通过 `super` 调用父类的方法时，`super` 会绑定子类的 `this`**
### 函数

###### new.target

`new.target` 属性检测函数或构造方法是否是通过 `new`运算符被调用的。在通过`new`运算符被初始化的函数或构造方法中，`new.target`返回一个指向构造方法或函数的引用。在普通的函数调用中，`new.target` 的值是 `undefined`

```js
function Fun(a, b) {
  this.a = a
  this.b = b
  this.newTarget = () => {
    console.log(new.target.name);
  }
}
const fn = new Fun(1, 2)
fn.newTarget() // Fun
```

### HTML

###### window上的方法和属性
- `window.requestAnimationFrame(callback)`：以每秒60次的频率来执行回调函数，通常用于页面渲染。
- `window.history`：用来获取 `History`  对象的引用，`History`  对象提供了操作浏览器**会话历史**（浏览器地址栏中访问的页面，以及当前页面中通过框架加载的页面）的接口，`history` 有如下方法
	- `history.back()`：等同于点击浏览器的回退按钮
	- `history.go(-1)`：等同于 `history.back()`
- `window.history.forword()`：在会话历史中向前移动一页。与 `history.go(-1)` 的效果相同
###### html元素的方法

- `onkeydown`，当用户按下某个键触发 `javaScript` 事件。
```html
<--在input元素中绑定onkeydown方法-->
<input type="text" onkeydown="myFunction()">
```
- `onkeyup`：当用户释放键时执行 `javaScript` 事件。
- `onblur`：当用户离开输入字段时执行 `javaScript` 事件。
- `element.remove()`：删除一个 `DOM` 节点。
- `element.outerHTML`： 获取节点本身。
- `element.setAttribute()`：为元素设置指定的属性。 
- `element.removeAttribute() `：移除元素指定的属性。
```js
// 获取一个button元素并设置禁用属性
const btn = document.getElementById('btn')
btn.setAttribute('disabled', true)
```
###### document
- `document.forms[]` 返回当前文档中的 `<form>`元素的一个集合，可用于获取表单信息，中括号中可以是索引也可以是 `name` 的值
```js
// 获取 name 为 loginForm 的表单
const form = document.forms['loginForm'] 
```
###### 陌生html元素
- 简单功能标签
	- `hr`：水平分隔线（`horizontal rule`）
	- `br`：换行符
	- `tr`：定义 `HTML` 表格中的行， tr 元素包含一个或多个 th 或 td 元素
	- `th`： `HTML` 表头单元格（包含头部信息），包含两行两列
	- `td`： `HTML` 标准单元格（包含数据），包含两行两列
	- `b`：粗体文本
- `meter`：显示已知范围内的标量测量值。例如磁盘用量、查询结果的相关性。注意mater标签不应该用于进度条，进度条使用 `progress`（h5）。
```html
<meter value="3" min="0" max="10">十分之三</meter>
```

- `mark`：定义带有记号的文本，文本高亮显示（h5）。
```html
<p>Do not forget to buy <mark>突出显示部分文本</mark> today.</p>  <!--突出显示部分文本-->
```

- `textarea`：定义多行的文本输入控件，文本区可以容纳无限数量的文本
	- 在文本输入区内的文本行间，用  `%OD%OA`（回车/换行）进行分隔
	- 可以通过 `cols` 和 `rows` 属性来规定 `textarea` 的尺寸，不过更好的办法是使用 `CSS` 的 `height` 和 `width` 属性
```html
<textarea rows="3" cols="20">
在w3school，你可以找到你所需要的所有的网站建设教程。
</textarea>
```
### CSS

###### position
- `position: fixed`：相对于整个窗口的绝对定位，元素使用该 `css` 属性后可以相对窗口使用 `top/button/left/right` 来定位
###### background
- `background: url("cal-icon.png") no-repeat center` 背景图定义的简写，各属性含义如下

  | background-image:url(图片)  | 设置背景图片   |
  | --------------------------- | -------------- |
  | background-repeat:no-repeat | 背景图片不重复 |
  | background-position: center | 水平居中       |

- `background-size: contain | cover | width height`：规定背景图像的尺寸
	
	- `cover`：图片宽高比不变、铺满整个容器的宽高，而图片多出的部分则会被截掉
	- `contain`：图片自身的宽高比不变，缩放至图片自身能完全显示出来，所以容器会有留白区域
	
- `background-position`：设置背景图像的位置，在动画中常用

- `background-image: linear-gradient(to bottom, #fff, #fd0)`：背景图设置渐变效果
	
	-  `linear-gradient`：线性渐变函数，生成一个线性渐变图片，来作为赋值给背景，第一个参数表示渐变的方向(默认从上往下),后面的参数是渐变的颜色，从哪种颜色渐变到哪种颜色。颜色参数可以大于两个。
	-  渐变方向用角度表示，单位为 `deg`，有几个特殊的角度有对应的英文。`0deg -> to top `从下往上；`90deg -> to right`从左往右；`180deg -> to bottom` 从上往下；`270deg -> to left` 从右往左；`to top left` 右下角到左上角；`to bottom right` 左下角到右上角。
###### user-select
控制用户能否选中文本。除了文本框内，它对被载入为 `chrome` 的内容没有影响。
- `user-select: none`：文本无法被选中
- `user-select: auto auto`：的具体取值取决于一系列条件，具体如下
	- 在 `::before` 和 `::after` 伪元素上，采用的属性值是 `none`
	- 如果元素是可编辑元素，则采用的属性值是 `contain`
	- 如果此元素的父元素的 `user-select` 采用的属性值为 all，则该元素采用的属性值也为 `all`
	- 如果此元素的父元素的 `user-select` 采用的属性值为 `none`，则该元素采用的属性值也为 `none` 
	- 否则，采用的属性值为 `text`
- `user-select: text`：用户可以选择文本
- `user-select: all`：在一个 `HTML` 编辑器中，当双击子元素或者上下文时，那么包含该子元素的最顶层元素也会被选中
- `user-select: contain`：允许在元素内选择；但是，选区将被限制在该元素的边界之内
- `user-select: element`：与 `contain` 相同，但仅在 `Internet Explorer` 中受支持
###### border边框
- border-image 	将图片规定为div元素的边框，border-image 属性是一个简写属性，用于设置以下属性：
	- border-image-source  图片路径
	- border-image-slice  图片边框向内偏移量
	- border-image-width  图片边框的宽度
	- border-image-outset  边框图像区域超出边框的量
	- border-image-repeat  图像边框是否应平铺(repeated)、铺满(rounded)或拉伸(stretched)。

###### outline轮廓

outline （轮廓）是绘制于元素周围的一条线，位于边框边缘的外围，可起到突出元素的作用。不计入盒模型大小中，也不一定是矩形。

outline 可以按顺序设置一下属性
| ***outline-color*** | **规定边框的颜色** |
| :-------------- | :------------- |
| ***outline-style*** | **规定边框的样式** |
| ***outline-width*** | **规定边框的宽度** |
|**inherit**|**规定应该从父元素继承 outline 属性的设置。**|

###### 动画

- animation  简写属性，用于设置六个动画属性
	- animation-name  规定需要绑定到选择器的 keyframe 名称。
	- animation-duration  规定完成动画所花费的时间，以秒或毫秒计。
	- animation-timing-function  规定动画的速度曲线。
	- animation-delay  规定在动画开始之前的延迟。
	- animation-iteration-count  规定动画应该播放的次数。
	- animation-direction  规定是否应该轮流反向播放动画。
###### 属性继承
- initial	将属性的初始（或默认）值应用于元素，将所有CSS属性恢复到其初始状态。
- inherit	获取其父元素的计算值，它可以应用于任何CSS属性
- unset	如果CSS关键字 unset 从其父级继承，则将该属性重新设置为继承的值，如果没有继承父级样式，则将该属性重新设置为初始值。在第一种情况下（继承属性）它的行为类似于inherit ，在第二种情况下（非继承属性）类似于initial
###### 样式重置
- -webkit-scrollbar	css滚动条选择器(伪类)，该伪类选择器影响了一个元素的滚动条的样式，详情见MDN文档 https://developer.mozilla.org/zh-CN/docs/Web/CSS/::-webkit-scrollbar
- input样式重置
```css
input, button, select, textarea {
outline: none; /*去除chrome浏览器自带点击input出现边框的情况*/
-webkit-apperance: button; /*使元素看起来像按钮*/
-webkit-apperance: none; /*去除样式*/
border-radius: 0; /*去除圆角*/
}
```
###### matrix()函数

`matrix()` 指定了一个由指定的 6 个值组成的 2D 变换矩阵。这种矩阵的常量值是隐含的，而不是由参数传递的；其他的参数是以列优先的顺序描述的。

```css
transform: matrix(1, 2, -1, 1, 80, 80); // matrix()在 transform 中的用法
```

###### filter滤镜

滤镜效果，定义元素的视觉效果，可以将模糊或颜色偏移等图形效果应用于元素，通常用于调整图像，背景和边框的渲染。例如

```css
filter: blur(px) 添加模糊效果
filter: brightness(%)  调整图像亮度
...
```

详情见 https://www.w3school.com.cn/cssref/pr_filter.asp

### 浏览器
#### BOM
- 全称`Browser Object Model`，浏览器对象模型
- 提供了独立于内容的、可以与浏览器窗口进行互动的对象结构
- `BOM` 由多个对象组成，其中代表浏览器窗口的 `Window` 对象是 `BOM` 的顶层（核心）对象，其他对象都是该对象的子对象。
##### BOM核心功能
- 弹出新浏览器窗口的能力
- 移动、关闭和更改浏览器窗口大小的能力
- 可提供 `WEB` 浏览器详细信息的导航对象
- 可提供浏览器载入页面详细信息的本地对象
- 可提供用户屏幕分辨率详细信息的屏幕对象
- 支持 `Cookies`
`BOM` 最有用的功能是提供了入口 `document` 对象(`DOM` 对象),通过这个入口可以访问/操作`Html` 文档
##### window对象的子对象
- `document` 对象
- `frames` 对象
- `navigator` 对象
- `screen` 对象
- `location` 对象
- `history` 对象
##### window对象
- 表示浏览器中打开的窗口，如果文档包含框架（`<frame>或<iframe>标签`）,浏览器会为 `HTML` 文档创建一个 `window` 对象,并为每个框架 `frame` 创建一个额外的 `window` 对象
##### Navigator对象
- `Navigator` 对象包含有关浏览器的信息
##### Screen对象
- `Screen` 对象存放着有关显示浏览器屏幕的信息
##### Location对象
- `Location` 对象包含有关当前URL的信息(当前窗口的 `Web` 地址)
##### History对象
- `History` 对象包含用户(在浏览器窗口中)访问过的 `URL`
- `History` 属于历史遗留对象，对于现代 `Web` 页面来说，由于大量使用 `AJAX` 和页面交互，调用 `history.back()` 可能会让用户愤怒！

### 网络协议
##### TCP/IP模型
###### 七层模型
物理层->数据链路层->网络层->传输层->会话层->表达层->应用层
###### 五层模型
物理层->数据链路层->网络层->传输层->应用层
应用层集成了七层模型的会话层、表达层、应用层的功能
##### http协议
###### 概念
协议是指计算机通信网络中两台计算机之间进行通信所必须共同遵守的规定或规则，HTTP协议，即超文本传输协议(Hypertext transfer protocol)。是一种详细规定了浏览器和万维网(WWW = World Wide Web)服务器之间互相通信的规则，通过因特网传送万维网文档的数据传送协议，它允许将超文本标记语言(HTML)文档从Web服务器传送到客户端的浏览器，处于网络七层模型的应用层。
###### 特点
- http协议是基于请求-响应式的协议，客户端发送请求，服务端响应请求
- HTTP协议是无状态协议，也就是服务器每次只处理一个连接，响应数据之后会自动断开连接
- 简单快速，客户端向服务端发送请求只需要传入请求方法和路径，常用请求方法有GET，HEAD，POST，每种方法规定了客户与服务器联系的类型不同，由于HTTP协议简单，使得HTTP服务器的程序规模小，因而通信速度很快。
- 灵活，HTTP允许传输任意类型的数据对象。正在传输的类型由Content-Type加以标记
- http1.1开始，默认都开启了Keep-Alive，保持连接特性，当一个网页打开完成后，客户端和服务器之间用于传输HTTP数据的TCP连接不会关闭，如果客户端再次访问这个服务器上的网页，会继续使用这一条已经建立的连接。
- Keep-Alive不会永久保持连接，它有一个保持时间，可以在不同的服务器软件（如Apache）中设定这个时间。
###### 工作流程
一次HTTP操作称为一个事务，其工作过程可分为四步:
- 首先客户机与服务器需要建立连接。只要单击某个超级链接，HTTP的工作开始。
- 建立连接后，客户机发送一个请求给服务器，请求方式的格式为：统一资源标识符（URL）、协议版本号，后边是MIME信息包括请求修饰符、客户机信息和可能的内容。
- 服务器接到请求后，给予相应的响应信息，其格式为一个状态行，包括信息的协议版本号、一个成功或错误的代码，后边是MIME信息包括服务器信息、实体信息和可能的内容。
- 客户端接收服务器所返回的信息通过浏览器显示在用户的显示屏上，然后客户机与服务器断开连接。
如果在以上过程中的某一步出现错误，那么产生错误的信息将返回到客户端，由显示屏输出。对于用户来说，这些过程是由HTTP自己完成的，用户只要用鼠标点击，等待信息显示就可以了。
###### 请求方法
HTTP/1.1协议中共定义了八种方法（有时也叫“动作”）来表明Request-URI指定的资源的不同操作方式：
- OPTIONS：返回服务器针对特定资源所支持的HTTP请求方法。也可以利用向Web服务器发送的请求来测试服务器的功能性。
- HEAD：向服务器索要与GET请求相一致的响应，只不过响应体将不会被返回。这一方法可以在不必传输整个响应内容的情况下，就可以获取包含在响应消息头中的元信息。该方法常用于测试超链接的有效性，是否可以访问，以及最近是否更新。
- GET：向特定的资源发出请求。注意：GET方法不应当被用于产生“副作用”的操作中，例如在web app.中。其中一个原因是GET可能会被网络蜘蛛等随意访问。
- POST： 向指定资源提交数据进行处理请求（例如提交表单或者上传文件）。数据被包含在请求体中。POST请求可能会导致新的资源的建立和/或已有资源的修改。
- PUT：向指定资源位置上传其最新内容。
- DELETE：请求服务器删除Request-URI所标识的资源。
- TRACE：回显服务器收到的请求，主要用于测试或诊断。
- CONNECT：HTTP/1.1协议中预留给能够将连接改为管道方式的代理服务器。
- PATCH：用来将局部修改应用于某一资源，添加于规范RFC5789。
###### 状态码
- 405：请求所针对的资源不支持对应的请求方法
- 501：服务器不认识或者不支持对应的请求方法
###### GET&POST
- GET提交的数据会放在URL之后，以?分割URL和传输数据，参数之间以&相连，如EditPosts.aspx?name=test1&id=123456. POST方法是把提交的数据放在HTTP包的body中。
- GET提交的数据大小有限制，最多只能有1024字节（因为浏览器对URL的长度有限制），而POST方法提交的数据没有限制。
- GET方式需要使用request.queryString来取得变量的值，而POST方式通过request.form来获取变量的值。
- GET方式提交数据，会带来安全问题，比如一个登录页面，通过GET方式提交数据时，用户名和密码将出现在URL上，如果页面可以被缓存或者其他人可以访问这台机器，就可以从历史记录获得该用户的账号和密码。

##### http历史版本

- http0.9：功能简陋，只支持GET方法，只能发送HTML格式字符串
- http1.0：支持多种数据格式，增加POST、HEAD等方法，增加头信息，每次只能发送一个请求（无持久连接）
- http1.1：默认持久连接、请求管道化、增加缓存处理、增加Host字段、支持断点传输分块传输等
- http2.0：二进制分帧、多路复用、头部压缩、服务器推送

# 高级知识

##### 柯里化

###### 概念

柯里化（currying）指的是将一个多参数的函数拆分成一系列函数，每个拆分后的函数都只接受一个参数（unary）。

###### 案例

原函数：接受两个参数 a 和 b

```js
function add (a, b) {
  return a + b;
}

add(1, 1) // 2
```

柯里化：将上面的函数拆分成两个函数，每个函数都只接受一个参数。

```js
function add (a) {
  return function (b) {
    return a + b;
  }
}

// 或者采用箭头函数写法
const add = x => y => x + y;

const f = add(1);
f(1) // 2
```

##### 函数合成

###### 概念

函数合成（function composition）指的是，将多个函数合成一个函数。

###### 案例

```js
const compose = f => g => x => f(g(x));

const f = compose (x => x * 4) (x => x + 3);
f(2) // 20
```

上面代码中，`compose`就是一个函数合成器，用于将两个函数合成一个函数。

可以发现，柯里化与函数合成有着密切的联系。**前者用于将一个函数拆成多个函数，后者用于将多个函数合并成一个函数。**



##### 参数倒置

###### 概念

参数倒置（flip）指的是改变函数前两个参数的顺序。

###### 案例

```js
var divide = (a, b) => a / b;
var flip = f.flip(divide);

flip(10, 5) // 0.5
flip(1, 10) // 10

var three = (a, b, c) => [a, b, c];
var flip = f.flip(three);
flip(1, 2, 3); // => [2, 1, 3]
```

上面代码中，如果按照正常的参数顺序，10 除以 5 等于 2。但是，参数倒置以后得到的新函数，结果就是 5 除以 10，结果得到 0.5。如果原函数有 3 个参数，则只颠倒前两个参数的位置。

模板：

```js
let f = {};
f.flip =
  fn =>
    (a, b, ...args) => fn(b, a, ...args.reverse());
```

##### 执行边界

###### 概念

执行边界（until）指的是函数执行到满足条件为止。

###### 案例

```js
let condition = x => x > 100;
let inc = x => x + 1;
let until = f.until(condition, inc);

until(0) // 101

condition = x => x === 5;
until = f.until(condition, inc);

until(3) // 5
```

上面代码中，第一段的条件是执行到`x`大于 100 为止，所以`x`初值为 0 时，会一直执行到 101。第二段的条件是执行到等于 5 为止，所以`x`最后的值是 5。

模板：

```js
let f = {};
f.until = (condition, f) =>
  (...args) => {
    var r = f.apply(null, args);
    return condition(r) ? r : f.until(condition, f)(r);
  };
```

上面代码的关键就是，如果满足条件就返回结果，否则不断递归执行。

##### 创建空对象

###### 传统方法

```js
var obj = {}
```

###### 高级方法

```js
var obj = Object.create(null)
```

###### 比较

后者创建空对象时不会创建Object.propotype委托，因此它比 {} 更“空”

##### Iterator接口
###### 概念
原有的表示集合的数据结构，主要是数组和对象，ES6又添加了Map跟Set，Iterator是一种统一的接口机制，用来处理不同的数据结构。**在解构赋值时，会默认调用Iterator接口。**
- Iterator是一种接口，为各种不同的数据结构提供统一的访问机制
- 任何数据结构只要部署Iterator接口，就称这种数据结构是可遍历的
- ES6规定，默认的Iterator接口部署在数据结构的Symbol.iterator属性上
###### 作用
- 为各种数据结构提供一个统一的，简便的访问接口
- 使得数据结构的成员能够按照某种次序排列
- ES6创造了一种新的遍历命令for...of 循环，Iterator接口主要提供for...of消费
###### 遍历过程
- 创建一个指针对象，指向当前数据结构的起始位置；也就是说，遍历器对象本质上就是一个指针对象
- 第一次调用指针对象的next方法，可以将指针指向数据结构的第一个成员
- 第二次调用指针对象的next方法，指针就指向数据结构的第二个成员
- 不断调用指针对象next方法，直到他指向数据结构的结束位置
###### 原生具有该接口的数据结构
Array、Map、Set、TypedArray、函数的arguments对象、NodeList对象
###### 调用场合
- 结构赋值：对数组和Set结构进行赋值时，会默认调用
- 扩展运算符：只要某个数据结构部署了Iterator接口，都可以使用扩展运算符转为数组
- yield：yield后面跟的是一个可遍历的结构，会调用接口的遍历器接口
- 其他场合：由于数组的遍历会调用遍历器接口，所以任何接受数组作为参数的场合，其实都调用了遍历器接口：
	- for...of
	- Array.from()
	- Map(),Set(),WeakMap(),WeakSet()
	- Promise.all()
	- Promise.race()
###### 详情地址 
[ES6-Iterator接口 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/82299041)

##### 特殊运算符
###### >>
有符号位移运算符
N >> 1 就代表N的二进制右移一位，二进制右移一位就能得到中间值，在计算中位数时非常常用，能准确地运算负数。
```js
console.log(4 >>> 1); // 2
console.log(-4 >>> 1); // -2
```
###### >>>
无符号位移运算符
N >>> 1 就代表N的二进制右移一位，二进制右移一位就能得到中间值，但不能运算负数。
```js
console.log(1 + 11 >>> 1) // 6
console.log(-4 >>> 1) // 2147483646
```

##### for in && for of循环
###### for in 
以任意顺序遍历一个对象的除Symbol以外的可枚举属性，包括继承的可枚举属性。**for in 循只会遍历属性名，而不会遍历属性值**，`for in` 还会查找到原型上的可枚举属性。
```js
const obj = {a:1, b:2}
for (let x in obj) {
	console.log(x) // a b
}
```
###### for of
for...of语句在可迭代对象（包括 Array，Map，Set，String，TypedArray，arguments 对象等等）上创建一个迭代循环，调用自定义迭代钩子，并为每个不同属性的值执行语句**只能作用于可迭代对象，不能作用于Object等不可迭代对象**
```js
const arr = [1, 2]
for (let c of arr) {
  console.log(c); // 1 2
}
```

##### sync && defer

`sync` 和 `defer` 都是异步加载的属性，使得加载 `JS` 时不会阻碍 `H5` 元素的加载，二者的区别：

- `defer` 的加载是按顺序顺序的，即一个 `JS` 2号文件异步加载好后，只要你前面的 `JS` 1号文件没有加载好，那么 `JS` 2号也会等一号 `JS` 文件加载好后在开始加载。
- `sync` 的异步加载是谁先好了谁先上。
- 在实际运用中，当各个 `JS` 包互相依赖时，不要使用 `sync` ，毕竟你没法确定当你的一个`JS` 包加载好时他所依赖的 `JS` 包是否加载好。而如果各个 `JS` 之间相互独立的话就可以用`sync`。最保险的方法就是用 `defer`。



​                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 
