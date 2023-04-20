# JS

# 1:基础

## 1.1:变量赋值

let 声明的变量可以被多次赋值

const 修饰的叫常量，只能赋值一次

- const 并不意味着它引用的内容不可修改
- 比如 const arr = [1,2,3]
- arr[0] = 100
- 其实跟Java类似，引用地址不可变，但是内部的值可以变

var 声明的变量可以被多次赋值

let 和 var 声明的变量的范围不同，了解即可，一般现在都直接使用 let 即可



## 1.2:undefined 和 null

执行表达式或函数，没有返回结果，出现 undefined

访问数组不存在的元素，访问对象不存在的属性，出现 undefined

定义变量，没有初始化，出现 undefined

```js
console.log(1) 	// 函数没有返回值, 结果是  undefined

let a = 10;	 	// 表达式没有返回值, 结果是 undefined
let b = [1,2,3]

console.log(b[10])   // 数组未定义元素是 undefined
let c = {"name":"张三"}

console.log(c.age)   // 对象未定义属性是 undefined
let d
console.log(d)		// 变量未初始化是 undefined
```

二者共同点

1：都没有属性、方法

2：二者合称 Nullish



二者区别

1：undefined 由 js 产生

2：null 由程序员提供

## 1.3:string

JS 字符串三种写法

```js
let a = "hello";  // 双引号
let b = "world";  // 单引号
let c = hello;  // 反引号
```

主要学会这种写法

```js
let name = 'ZZX'
let age = 20
let uri = /test?name=${name}&age=${age};
```

## 1.4:number 和 bigint

number 类型标识的是双精度浮动小数，例如

```js
10 / 3;   // 结果 3.3333333333333335
```

既然是浮点小数，那么可以除零

```js
10 / 0;	  // 结果 Infinity 正无穷大
-10 / 0;  // 结果 -Infinity 负无穷大
```

浮点小数有运算精度问题，例如

```js
2.0 - 1.1; // 结果 0.8999999999999999
```

字符串转数字

```js
parseInt("10"); 	// 结果是数字 10 
parseInt("10.5");	// 结果是数字 10, 去除了小数部分
parseInt("10") / 3; // 结果仍视为 number 浮点数, 因此结果为 3.3333333333333335

parseInt("abc");	// 转换失败，结果是特殊值 NaN (Not a Number)
```

要表示真正的整数，需要用 bigint，数字的结尾用 n 表示它是一个 bigint 类型

```js
10n / 3n;			// 结果 3n, 按整数除法处理
```

## 1.5:boolean

下面的几种情况在 IF 里面都是 falsy

* false
* Nullish (null，undefined)
* 0，0n，NaN
* ""  ''    即长度为零的字符串【这个容易记成true】



剩余的值绝大部分都是 truthy

有几个容易被当作 falsy 实际是 truthy 的

* "false"，"0" 即字符串的 false 和 字符串的零
* [] 空数组
* {} 空对象
* 注意：空字符串却不是

## 1.6:?? 和 ?.

### 1:??

需求：如果参数 n 没有传递或是 null，给它一个【男】

也就是当 参数是 nullish 的时候，就赋值默认男

如果用传统办法

```js
function test(n) {
    if(n === undefined || n === null) {
        n = '男';
    }
    console.log(n);
}
```

使用 ?? 的语法：值1 ?? 值2

值1 是 nullish，返回 值2

值1 不是 nullish，返回 值1

```js
function test(n) {
    n = n ?? '男';
    console.log(n);
}
```



### 2:?.

需求：函数参数是一个对象，可能包含有子属性

例如，参数可能是

```js
let stu1 = {
    name:"张三",
    address: {
        city: '北京'
    }
};

let stu2 = {
    name:"李四"
}

let stu3 = {
    name:"李四",
    address: null
}
```

现在要访问子属性（有问题）

当 address 不存在【undefined】或者 address 为 null【null】则会报错

```js
function test(stu) {
    console.log(stu.address.city)
}
```

现在希望当某个属性是 nullish 时，短路并返回 undefined，可以用 ?.

```js
function test(stu) {
    console.log(stu.address?.city)
}
```

用传统办法 

```js
function test(stu) {
    if(stu.address === undefined || stu.address === null) {
        console.log(undefined);
        return;
    }
    console.log(stu.address.city)
}
```

# 2:常用

## 2.1:箭头函数

也是一个没有名字的函数，一般用在某个事件要执行的时候直接写即可

```js
(参数) => {
    // 函数体
    return 结果;
}
```

* 如果没有参数，() 还是要保留
* 如果只有一个参数，() 可以省略
* 如果函数体内只有一行代码，{} 可以省略
* 如果这一行代码就是结果，return 可以省略

```js
document.getElementById("p1").onclick = () =>  console.log("666");
```

## 2.2:数组API

1：push、shift、splice

```js
let arr = [1,2,3] 

arr.push(4)    	     // 向数组尾部(右侧)添加元素, 结果 [1,2,3,4]
arr.shift()		    // 从数组头部(左侧)移除元素, 结果 [2,3,4]
arr.splice(1,1) 	// 删除【参数1】索引位置的【参数2】个元素，结果 [2,4]
```

2：join

```js
let arr = ['a','b','c'];

arr.join(); 		// 默认使用【,】作为连接符，结果 'a,b,c'
arr.join('');		// 结果 'abc'
arr.join('-');		// 结果 'a-b-c'
```

3：map、filter、forEach

```js
let arr = [1,2,3,6];

arr.map( (i) => {return i * 10} )   // 箭头函数
arr.map( i => i * 10 )              // 箭头函数
```

传给 map 的函数，参数代表旧元素，返回值代表新元素

```js
let arr = [1,2,3,6]
arr.filter( (i) => {return i%2 == 1} )
```

传给 filter 的函数，参数代表旧元素，返回 true 表示要留下的元素

```js
let arr = [1,2,3,6];
arr.forEach( (i) => console.log(i) );
```

## 2.3:JSON

Json 这种数据格式，它的语法看起来与 JS 对象非常相似，例如：

一个 Json 对象长这样：

```json
{
    "name":"张三",
    "age":18
}
```

一个 JS 对象长这样：

```js
{
    name:"张三",
    age:18
}
```

那么他们的区别在哪儿呢？总结了这么几点

1. 本质不同
   * json 对象本质上是个字符串，它的职责是作为客户端和服务器之间传递数据的一种格式，它的属性只是样子货
   * js 对象是切切实实的对象，可以有属性方法
2. 语法细节不同
   * json 中只能有 null、true|false、数字、字符串（只有双引号）、对象、数组
   * json 中不能有除以上的其它 js 对象的特性，如方法等
   * json 中的属性必须用双引号引起来

json 字符串与 js 对象的转换

```js
JSON.parse(json字符串);  // 返回js对象
JSON.stringify(js对象);  // 返回json字符串
```

## 2.4:[]  {}  ...

### 1: ...

叫做展开运算符

作用1：打散数组，把元素传递给多个参数

```js
let arr = [1,2,3]
function test(a,b,c) {
    console.log(a,b,c)
}
test(...arr)
```

打散可以理解为【去掉了】数组外侧的中括号，只剩下数组元素

作用2：复制数组或对象

```js
let arr1 = [1,2,3]
let arr2 = [...arr1]		// 复制数组
```

```js
let obj1 = {name:'张三', age: 18}
let obj2 = {...obj1}		// 复制对象
```

作用3：合并数组或对象

合并数组

```js
let a1 = [1,2]
let a2 = [3,4]

let b1 = [...a1,...a2]		// 结果 [1,2,3,4]
let b2 = [...a2,5,...a1]	// 结果 [3,4,5,1,2]
```

合并对象

```js
let o1 = {name:'张三'}
let o2 = {age:18}
let o3 = {name:'李四'}
let n1 = {...o1, ...o2}	       // 结果 {name:'张三',age:18}
let n2 = {...o3, ...o2, ...o1} // 结果{name:'李四',age:18}
```

复制对象时出现同名属性，后面的会覆盖前面的

反正 ... 的含义就是把数组或者对象的 [] 或者 {} 拆开

### 2: []

解构赋值

用在声明变量时

```js
let arr = [1,2,3]
let [a, b, c] = arr	  // 结果 a=1, b=2, c=3
```

用在声明参数时

```js
let arr = [1,2,3]

function test([a,b,c]) {
    console.log(a,b,c) 	// 结果 a=1, b=2, c=3
}

test(arr)				
```



### 3: {}

用在声明变量时

```js
let obj = {name:"张三", age:18}

let {name,age} = obj	   // 结果 name=张三, age=18
```

用在声明参数时

```js
let obj = {name:"张三", age:18}
function test({name, age}) {
    console.log(name, age)  // 结果 name=张三, age=18
}
test(obj)
```

## 2.5:继承关系

语法：Object.create(父对象)

```js
let father = {name:'张三', age:18, study:function(){}}
let son = Object.create(father)
```

## 2.6: for in

主要用来遍历对象

```js
let father = {name:'张三', age:18, study:function(){}}
for(const n in father) {
    console.log(n)
}
```

其中 const n 代表遍历出来的属性名

注意1：方法名也能被遍历出来（它其实也算一种特殊属性）

注意2：遍历子对象时，父对象的属性会跟着遍历出来

```js
let son = Object.create(father);
son.sex = "男";

for(const n in son) {
    console.log(n);
}
```

注意3：在 for in 内获取属性值，要使用 [] 语法，而不能用 . 语法

```js
for(const n in son) {
    console.log(n, son[n]);
}
```

## 2.7:for of

主要用来遍历数组，也可以是其它可迭代对象，如 Map，Set 等

```js
let a1 = [1,2,3]

for(const i of a1) {
    console.log(i)
}

let a2 = [
    {name:'张三', age:18},
    {name:'李四', age:20},
    {name:'王五', age:22}
]

for(const obj of a2) {
    console.log(obj.name, obj.age);
}

for(const {name,age} of a2) {
    console.log(name, age)
}
```

## 2.8:try catch

```js
let stu1 = {name:'张三', age:18, address: {city:'北京'}}
let stu2 = {name:'张三', age:18}

function test(stu) {
    try {
        console.log(stu.address.city)   
    } catch(e) {
        console.log('出现了异常', e.message)
    } finally {
        console.log('finally')
    }
}
```

