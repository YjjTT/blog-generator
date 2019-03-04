---
title: 自己实现jQuery
date: 2019-03-04 14:13:09
tags: jQuery, JavaScript
---

## 自己封装两个函数

```html
 // 有三个div
  <div id="item1"></div>
  <div id="item2"></div>
  <div id="item3"></div>
```

```css
.red{
  background: red;
}
div{
  width:100px;
  height:100px;
  border: 1px solid green;
}
```

1. 第一个函数,查询一个节点的兄弟姐妹

首先,先实现以下怎么获取一个节点的兄弟姐妹,并将其全部放到一个伪数组中:

```javascript
var allChildren = item2.parentNode.children // 先找到item2的爸爸,然后在找到他所有的儿子
var array = {length: 0} // 初始化一个伪数组
for(let i=0;i<allChildren.length;i++){ // 遍历获取到的所有儿子
    if(allChildren[i] !== item2){ 
        array[array.length] = allChildren[i] // push到数组的一种方法,因为伪数组没有push方法
        array.length += 1
    }
}
console.log(array) // {0: div#item1, 1: div#item2, 2: script, length: 3}
```

封装上面的代码:

```javascript
// 封装一个函数,接受一个参数
function getSiblings(node){
    var allChildren = node.parentNode.children 
	var array = {length: 0} 
	for(let i=0;i<allChildren.length;i++){ 
    	if(allChildren[i] !== node){ 
       	 	array[array.length] = allChildren[i] 
        	array.length += 1
    	}
	}
    return array
}
```

2. 给一个节点添加一个或者多个class

```javascript
function addClass(node, classes){ // 接受两个参数,一个是需要添加class的节点,另一个是class名组成的数组
	for(let key in classes){
    var value = classes[key]
    if(value){
      node.classList.add(key)
    }else{
      node.classList.remove(key)
    }
  }
}
addClass(item3,{'a':true, 'b':false, 'c':true}) // 如果是true就添加,false就不添加
```

上面的代码可见,`node.classList`出现了两次, 如果出现类似的代码,就存在代码优化的可能

```javascript
function addClass(node, classes){
  for(let key in classes){
    var value = classes[key]
    var methodName = value ? 'add' : 'remove'
    node.classList[methodName](key)
  }
}
addClass(item3,{'a':true, 'b':false, 'c':true})
```

上面的两个函数,都是在操作节点,那么可以将两个函数,使用命名空间设计模式进行整合,使其存在关联性(例如`document.getElementById`,`document.querySelector`)

```javascript
window.xxx = {}
xxx.getSiblings = getSiblings
xxx.addClass = addClass

// 使用
xxx.getSiblings(item3)
xxx.addClass(item3, {'a':true, 'b':false, 'c':true})
```

3. 将两个函数(addClass, setText)封装成一个jquery函数

```javascript
window.jQuery = function(nodeOrSelector){ // 接受一个参数,可以是node,也可以是一个selector
  let nodes = {} // 声明一个对象nodes
  if(typeof nodeOrSelector === 'string'){ // 如果是一个selector string
    let temp = document.querySelectorAll(nodeOrSelector) // 伪数组
    for(let i=0; i<temp.length;i++){
      nodes[i] = temp[i]
    }
    nodes.length = temp.length
  }else if(nodeOrSelector instanceof Node){ // 如果是一个node
    nodes = {0: nodeOrSelector, length: 1}
  }
    
  nodes.addClass = function(classes){
      for(let i=0;i<nodes.length;i++){
        nodes[i].classList.add(value)
      }
  }
    
  nodes.setText = function(text){
      for(let i =0;i < nodes.length;i++){
        nodes[i].textContent = text
    }
  }
  return nodes
}

// 使用
window.$ = jQuery

var $div = $('div')
$div.addClass('red')
$div.setText('hi')
```

![](https://github.com/YjjTT/ImageFile/raw/master/img/20190304150102.png)

## 面试题

```javascript
var div = document.getElementById('x')
var $div = $('#x')
请说出div和$div的联系和区别?
```

答

```javascript
1.div 返回了一个HTML DOM 对象,$div 返回了一个jquery 对象.
2.$div是包装了dom对象后产生的,无法使用dom对象的任何方法,比如innerHTML
3.如果是jquery 对象,前面加$, 如果是html dom对象,就是普通的命名.
4.div变成$div, 只需要用jquery构造函数将dom对象包装起来就可以了.
5.$div变成div
- jquery对象是一个hash,分别包含了一个key对应所包装的dom 对象, length,还有__proto__原型 object(0), 里面包含了jquery的一个方法和属性.比如addClass,after,ajax等, 所以使用div[0]即可获取到div
- 使用jquery自身所提供的方法, 通过get(index), 也能得到相应的dom对象
6.div的属性方法:getElementById appendChild innerHTML 等
7.$div的属性方法: addClass after append等
```



