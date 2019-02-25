---
title: JavaScript里的Array
date: 2019-02-25 15:46:15
tags: JavaScript, Array
---

# Array

> 写之前巩固一下JS的七种数据类型:number, string, boolean, null, undefined, symbol, object,
>
> 由此可见, Array属于object.

> `Array`是JS的原生对象, 同时也是一个构造函数.

### 构造函数

```javascript
var arr = new Array(2); // 生成一个两个成员的数组,每个位置都是空值
//等同于
var arr = Array(2);
```

`Array`构造函数有个很大的缺陷, 就是不同的参数, 会导致不一致性,比如:

```javascript
var arr = new Array(2); // 第一个参数2代表数组的length

var arr = new Array(2,2); // 第一个参数2代表数组的第一个元素

var arr = new Array(); // 返回一个空数组

var arr = new Array('abc'); // 返回一个数组['abc']
```

因此,通常创建数组的时候,不建议使用构造函数创建, 使用数组字面量最好:

```javascript
var arr = [1,2];
```

### 遍历

```javascript
// 下面是两个数组 arr 和 obj

var arr = [1,2]; // 内存中 __proto__, 指向的是Array.prototype
var obj = {0:1, 1:2, 'length':2}; // 内存中 __proto__, 指向的是Object.prototype

// 遍历arr
for(let i = 0; i < arr.length; i++){
	console.log(i, arr[i])
}
// 0 1
// 1 2

// 遍历obj
for(let i = 0; i < obj.length; i++){
	console.log(i, obj[i])
}
// 0 1
// 1 2

obj.xxx = 'xxx';
// 得到obj为
obj = {0:1, 1:2, 'length':2, xxx:"xxx"}

// 再次遍历obj得到
// 0 1
// 1 2

// 换一种方法遍历
for(let key in obj){
    console.log(key, obj[key])
}
// 0 1
// 1 2
// 2 3
// length 3
// xxx xxx
```

由上面的例子可以总计出:

1. 所以遍历是是遍历, 和是不是数组无关, 有关的是有没有下标.
2. 数组之所以为数组, 是因为你觉得他是数组, 觉得是数组就使用`for(let i = 0;i<obj.length;i++)`进行遍历, 觉得不是就使用`for(let key in obj)`遍历.
3. 数组本质: ____proto____(原型)指向了`Array.prototype`.

### 静态方法

`Array.isArray` 方法返回一个bool值, 表示参数是否为数组.

```javascript
var arr = [1,2,3];

typeof arr // 'object'
Array.isArray(arr) // true
```

### 实例方法

讲实例方法之前,先看下`Array`创建之后的内存图:

![](https://github.com/YjjTT/ImageFile/raw/master/img/Arraty.png)

- valueOf(), toString()

所有对象都拥有的两个公用方法.

```javascript
var arr = [1,2,3];
arr.valueOf(); // [1,2,3]

arr.toString(); // "1,2,3"
```

- push(), pop()

`push`向数组添加一个或者元素, pop删除数组的最后一个元素, 两个方法都会改变原数组

```javascript
var arr = ['a', 'b', 'c'];

arr.push(1)
arr.push('d')
arr.push(true)

arr // ['a', 'b', 'c', 1, 'd', true]

var arr = ['a', 'b', 'c']
arr.pop() // ['a', 'b']
```

**push和pop结合使用, 构成了后进先出的stack结构.**

- shift(), unshift()

`shift`删除数组的第一个元素, unshift在数组第一个位置添加元素, 两个方法都会改变原数组

```javascript
var arr = ['a', 'b', 'c'];
a.shift() // ['b', 'c']
// 使用shift可以清空一个数组

var arr = ['a', 'b', 'c'];
a.unshift('x', 'd') // ['x', 'd', 'a', 'b', 'c']
```

**shift和unshift结合使用, 构成了先进先出的queue结构.**

- join()

`join`数组元素之间用指定参数作为分隔符拼接

```javascript
var arr = [1,2,3];
arr.join(',') // "1,2,3"
arr.join() // "1,2,3" 不加参数,默认用逗号拼接

arr.toString(arr) // "1,2,3" 与join不同, 只是巧合

arr + "" // "1,2,3" 与join不同, 只是巧合
```

- concat()

`concat`拼接两个数组,生成一个新数组, 原数组不变

```javascript
var a = [1,2,3];
var b = [4,5,6];

a.concat(b) // [1,2,3,4,5,6]

a.concat([]) // [1,2,3]
a.concat([]) !== a
```

- reverse()

`reverse`颠倒排列数组元素 , 改变原数组

```javascript
var arr = [1,2,3];
arr.reverse(); // [3,2,1]
```

- sort()

`sort`对数组成员进行排序, 快速排序方法, 需要接受一个函数, 函数返回排序依据, 改变原数组

```javascript
var a = [1,3,6,2,5];

a.sort(function(x,y){ return x-y }) // [1,2,3,5,6] 如果函数返回值小于等于0, 第一个元素排在第二个元素前面
a.sort(function(x,y){ return y-x }) // [6,5,3,2,1] 如果该函数的返回值大于0，表示第一个成员排在第二个成员后面

var students = ['小明','小红','小花'] ;
var scores = { 小明: 59, 小红: 99, 小花: 80 };
students.sort(function(x,y){
    return scores[x] - scores[y]
})
```

- map()

`map`将所有元素依次传入参数函数, 并将每一次的执行结果组成一个新数组返回, 不改变原数组.

```javascript
var a = [1, 2, 3];
a.map(function(n){
    return n + 1''
}) // [2, 3, 4]
```

- forEach()

`forEach`和`map`方法相似, 也是对数组的所有成员依次执行参数函数, 但是`forEach`不会有返回值,只用来操作数据.

```javascript
// forEach 有三个参数, 通常只写两个参数
1. 当前值
2. 当前位置
3. 数组本身

var out = [];
[1, 2, 3].forEach(function(elem) {
  this.push(elem * elem);
}, out); // 其中this 就是[1,2,3], 第一个参数是一个函数, 第二个参数是空数组out, 回调函数内部的this指向了out

out // [1, 4, 9]
```

- filter()

`filter`过滤数组元素, 它的参数是一个函数，所有数组成员依次执行该函数，返回结果为`true`的成员组成一个新数组返回。该方法不会改变原数组。

```javascript
var a = [1,2,3,4,5,6];
a.filter(function(value){
    return value % 2 === 0
})
// [2,4,6]
a.filter(function(value,index){
    return index % 2 !== 0
})
// [1,3,5]
```

- reduce()

`reduce`方法依次处理数组的每个成员，最终累计为一个值.下面是四个参数:

1. 累积变量，默认为数组的第一个成员 
2. 当前变量，默认为数组的第二个成员 
3. 当前位置（从0开始）(可选)
4. 原数组 (可选)

```javascript
var a = [1,2,3,4,5];
a.reduce(function(a,b){
    console.log(a,b);
    return a+b;
})
// 15
```

- 使用`reduce`表示`map`

```javascript
var a = [1,2,3];
a.reduce(function(arr,n){
    arr.push(n*2);
    return arr;
},[])
// [2,4,6]
```

- 使用`reduce`表示`filter`

```javascript
var a = [1,2,3,4,5,6];
a.reduce(function(arr,n){
    if(n % 2 === 0){
        arr.push(n)
    }
    return arr
}, [])
// [2, 4, 6]
```

