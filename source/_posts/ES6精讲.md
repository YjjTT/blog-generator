---
title: ES6精讲
date: 2019-06-15 14:51:08
tags: ES6, JS
---

ES6 精讲

ES5->ES6 — JS打脸史

a = 1
var a = 1
// 上面两种是ES 3，下面两种是ES 6
let a = 1
const a = 1

a = 1含义不明, 不确定是全局变量还是局部变量 - 不要用

var a = 1 变量提升, 会出现问题 - 不要用

let a = 1 不会变量提升

const a = 1 只能赋值一次



Let:

1. Let的作用域在最近的{}之间
2. 如果你在let a 之前使用a, 那么报错
3. 如果你重复let a , 那么报错

Const:

1.2.3 // 同上

4.只有一次赋值机会, 而且必须在声明的时候立马赋值



function fn(){
    if(true){
        console.log(a)
    }else{
        var a // 声明var a 不会报错, 不声明就报错, 无论支不执行,都会变量提升
        console.log(2)
    }
}
fn()



解决js全局变量提升, 用函数包起来

(function(){
   var a = 1
   window.xx = function (){
       console.log(a)
   } 
}()) // 匿名函数立即执行





{
    let a = 1
    console.log(a) // 1
    {
        console.log(a) // 报错, Temp Dead Zone
        let a = 2
        console.log(a)  // 2
        {
            let a = 3
            console.log(a) // 3

```
    }
}
```

}
console.log(a) // 1



{
    const a = 1
    console.log(a)
    a = 2 // 报错 const 常量只能赋值一次
    console.log(a)
}

面试题:

```var a = 1
function fn(){
    console.log(a) // 1
}
a = 2 ////// 这里有一行代码不给你看
fn()
// 能确定a 一定打印出1么？ 答案：不能 代码执行顺序```
```

```
for (var i=0; i<6; i++){

}
console.log(i) // i = 6
```

```
var i
for(i=0; i<6; i++){
    function fn(){
        console.log(i)
    }
    fn() // 会执行 fn 0,1,2,3,4,5
}

var i
for(i=0; i<6; i++){
    function fn(){
        console.log(i)
    }
    XXXXXXXX  // 会执行 fn
}
是否会打印0,1,2,3,4,5?
答案不一定, 写fn()时, 会打印0,1,2,3,4,5
当写成button.onclick = fn 打印出6 刻舟求剑
```

```
for (let i=0; i<6; i++){
	// 块里面的i = 圆括号里面i的值
	let i = _i // JS自动加的, 正常里面是访问不到i的
	console.log(i)
	// 圆括号里面i的值 = 块里面的i
}

以上一共有7个i, 圆括号里的一个i, 块级里面自动生成6个i
```

