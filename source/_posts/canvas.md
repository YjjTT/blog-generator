---
title: canvas
date: 2019-01-11 15:07:06
tags: canvas
---

## canvas

> `canvas`标签是HTML5新增的元素, 可用于通过JavaScript中的脚本来绘制图形, 可以用于绘制图形, 制作照片, 创建动画, 甚至可以进行实时视频处理和渲染.

#### 属性

`canvas`只有两个属性`width`和`height`, 这些都是可选的, 并且使用DOM properties来设置,当没有设置`canvas`的宽高时, 初始化宽高为300px和150px, 并且`canvas`的宽高不能通过css来设置, 会出现图形扭曲.

```html
<canvas id="canvas" width=300 height=300></canvas>
```

#### 渲染上下文

```javascript
var canvas = document.getElementById('canvas'); // 通过id获取当前canvas
if (canvas.getContext){ // 判断浏览器是否支持
    var ctx = canvas.getContext('2d'); // 创建上下文
}else{
    
}
```

#### 绘制形状

1. 绘制矩形

```javascript
var yyy = document.getElementById('canvas');
if (yyy.getContext){
  var ctx = canvas.getContext('2d');
  ctx.strokeRect(10, 10, 150, 150); // 绘制矩形边框
  ctx.fillRect(25, 25, 100, 100); // 绘制一个填充的矩形
  ctx.clearRect(50, 50, 50, 50); // 清除指定区域, 使其透明
}
```

![](https://github.com/YjjTT/ImageFile/raw/master/img/20190111134003.png)

1. 绘制路径

图形的基本元素都是路径,路径是通过不同颜色和宽度的线段或曲线相连形成的不同形状的点的集合。一个路径，甚至一个子路径，都是闭合的。使用路径绘制图形需要一些额外的步骤。

1. 首先，你需要创建路径起始点。
2. 然后你使用画图命令去画出路径。
3. 之后你把路径封闭。
4. 一旦路径生成，你就能通过描边或填充路径区域来渲染图形。

- **绘制三角形**

```javascript
var yyy = document.getElementById('canvas');
if (yyy.getContext){
  	var ctx = canvas.getContext('2d');
    
    // 绘制填充三角形
    ctx.beginPath(); // 新建一条路径,生成之后,图形绘制命令会被指向到路径上生成路径.
    ctx.moveTo(75,75); // 设置起点, 就是将鼠标移动到某个点准备开始绘制
    ctx.lineTo(100, 75); // 从起点(75,75)到该点(100,75),画一条线
    ctx.lineTo(100, 25); // 从上一个点(100,75)到该点(100,25),画一条线
    ctx.fill(); // 通过填充路径的内容区域生成实心的图形, 图一的红色虚线会自动闭合,形成一个三角形, 并填充颜色
    
    // 绘制描边三角形
    ctx.beginPath(); // 新建一条路径,生成之后,图形绘制命令会被指向到路径上生成路径.
    ctx.moveTo(75,75); // 设置起点, 就是将鼠标移动到某个点准备开始绘制
    ctx.lineTo(100, 75); // 从起点(75,75)到该点(100,75),画一条线
    ctx.lineTo(100, 25); // 从上一个点(100,75)到该点(100,25),画一条线
    ctx.closePath(); // 闭合路径之后图形绘制命令又重新指向到上下文中。
    ctx.stroke(); // 通过线条来绘制图形轮廓。
}
```

![未填充](https://github.com/YjjTT/ImageFile/raw/master/img/20190111135418.png)

![fill()](https://github.com/YjjTT/ImageFile/raw/master/img/20190111135007.png)

![stroke()](https://github.com/YjjTT/ImageFile/raw/master/img/20190111140106.png)

> fill, 会自动闭合路径, 并填充图形, stroke不会自动闭合路径,如果没有设置closePath(), 则只是绘制了两条直线.

- 绘制圆

  ```javascript
  arc(x, y, radius, startAngle, endAngle, anticlockwise)
  
  - x : 圆弧中心的x轴坐标
  - y : 圆弧中心的y轴坐标
  - radius : 圆弧的半径
  - startAngle : 圆弧的起始点, x轴方向开始计算, 单位以弧度表示
  - endAngle : 圆弧的终点, 单位以弧度表示
  - anticlockwise(可选) : boolean值, true逆时针绘制圆弧, false顺时针绘制圆弧
  ```

  ```javascript
  arcTo(x1, y1, x2, y2, radius)
  
  - x1 : 第一个控制点的x坐标
  - y1 : 第一个控制点的y坐标
  - x2 : 第二个控制点的x坐标
  - y2 : 第二个控制点的y坐标
  - radius : 圆弧的半径
  ```

  - 绘制圆弧

  ```javascript
  // 使用arc来绘制
  var yyy = document.getElementById('canvas');
  if(yyy.getContext){
      var ctx = yyy.getContext();
      
      ctx.beginPath();
      ctx.arc(120, 38, 30, 0, Math.PI*2);
      ctx.stroke();
  }
  ```

  ![](https://github.com/YjjTT/ImageFile/raw/master/img/20190111144907.png)

  - 绘制圆

  ```javascript
  var yyy = document.getElementById('canvas');
  if(yyy.getContext){
      var ctx = yyy.getContext('2d');
      
      ctx.beginPath();
      ctx.arc(150, 38, 30, 0, Math.PI*2);
      ctx.fill();
  }
  ```

  ![](https://github.com/YjjTT/ImageFile/raw/master/img/20190111145149.png)

















