---
layout: react
title: React Hooks 详解
date: 2019-12-20 15:39:54
tags: React Hooks
---

## React Hooks 

![](https://github.com/YjjTT/ImageFile/raw/master/img/20191220154342.png)



---



###  useState

- **使用状态**

```react
const [n, setN] = React.useState(0)
cosnt [user, setUser] = React.useState({name: 'F'})
```

- **示例代码**

  [sandbox]: https://codesandbox.io/s/snowy-snow-50flp

```react
import React, {useState} from "react";
import ReactDOM from "react-dom";

function App() {
  const [user,setUser] = useState({name:'Tony', age: 18})
  const onClick = ()=>{
    setUser({
      name: 'Jack'
    })
  }
  return (
    <div className="App">
      <h1>{user.name}</h1>
      <h2>{user.age}</h2>
      <button onClick={onClick}>Click</button>
    </div>
  );
}

const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);
```

- **注意事项**

  1. 不可局部更新

     > 问: 如果state是一个对象,能否部分setState?
     >
     > 答案: 不可以
     >
     > 如上方代码, `setUser({name: ''Jack})`, 并没有set`age`属性,点击`onClick`,页面上只显name示`Jack`,不会显示age`18`.
     >
     > 因为: setState不会帮我们合并属性, 需要自己合并属性`...user`, React的所有东西都不会合并属性,因为他觉得这不是他要做的事情.
     >
     > 解决方法:
     >
     > ```react
     > setUser({
     > 	...user, // 拷贝user的所有属性
     > 	name: 'Jack' // 覆盖拷贝user的name属性
     > })
     > ```

  2. 地址要变

     > ```react
     > const onClick = ()=>{
     > 	user.name = 'Jack';
     >   setUser(user); 
     > }
     > 上面代码, user的name属性并不会发生变化,因为setState(obj), 如果obj的地址不变,那么React就会认为数据没有变化.
     > ```

- **useState接受函数**

```react
const [state, setState] = useState(()=>{
	return initialState
})
该函数会返回初始state, 且只执行一次, 减少多余的计算过程.

上面代码可以修改为:
const [user, setUser] = useState(
  () => ({name: 'Jack', age: 18})
);

useState 不写成函数, 就会很浪费时间,每次执行都会被JS引擎解析一遍, 下面代码的9+9都会被算一遍.
const [user,setUser] = useState({name:'Tony', age: 9+9)})
```

















