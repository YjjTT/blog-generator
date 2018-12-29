---
title: CSS布局
date: 2018-12-29 14:33:23
tags: CSS, Layout
---

### CSS布局



#### 盒模型(框模型)

CSS有一些表现不用的框类型分别为box和line-box, 可以通过设置`display`属性来设定元素的框类型, 其中最常见的三种类型为`block`, `inline`, `inline-block`.

`display` 是CSS中最重要的用于控制布局的属性, 决定了文档流的流动方向。每个元素都有一个默认的 display 值，这与元素的类型有关, 并且该属性的值是可以修改的。对于大多数元素它们的默认值通常是 `block` 或 `inline` 。一个 block 元素通常被叫做块级元素。一个 inline 元素通常被叫做行内元素。

------

**1. block box**

- 块框（ `block` box）是定义为堆放在其他框上的框（例如：其内容会独占一行），而且可以设置它的宽高，之前所有对于框模型的应用适用于块框 （ `block` box）

```html
<div>
    div就是一个标准的block元素, 一个块级元素会占据一行, 并从上至下流动布局, 其他常用块级元素有p, form, footer, section等
</div>
```

```html
<p>
    <div style="background: red">div block box</div>这是一行普通的文字，这里有个 <span style="display: block; background: red">盒模型</span> 标签。
</p>
```

上面代码演示了block box的特性:

1. 穿插在inline中的block box, 会独占一行.

![](https://user-gold-cdn.xitu.io/2018/12/18/167c145caacf8c81?w=782&h=119&f=png&s=10836)

------

**2. inline box**

- 行内框（ `inline` box）与块框是相反的，它随着文档的文字流动（例如：它将会和周围的文字和其他行内元素出现在同一行，而且它的内容会像一段中的文字一样随着文字部分的流动而打乱），对行内盒设置宽高无效，设置padding, margin 和 border都会更新周围文字的位置，但是对于周围的的块框（ `block` box）不会有影响。

```html
<span>span</span>是一个标准的行内元素, 从左至右流动布局,如果流动遇到阻碍, 宽度不够, 换行继续流, 一个行内元素可以在段落中包裹一些文字<span>而不会打乱布局</span>, 其他常用的行内元素, a也是最常用的行内元素, 被用作链接.
```

```html
<p>这是一行普通的文字，这里有个<em>em</em>标签</p>
```

上面的代码包含四个box:

1. 首先是`p`标签所在的block box, 此box包含了其他的boxes;
2. 第二个是inline box, inline box不会让内容成块显示,而是从左到右排成一排, 如果有`display: inline`的标签则属于inline box, 如果是纯文字, 则属于匿名inline box.

![](https://user-gold-cdn.xitu.io/2018/12/18/167c145caaf1df73?w=328&h=134&f=png&s=17845)

1. 第三个也是inline box, 在block box中, 一个一个的inline box 组成了line box.

![](https://user-gold-cdn.xitu.io/2018/12/18/167c145cab12b040?w=308&h=97&f=png&s=9708)

1. 第四个是content area, 是一种围绕文字并看不见的box, content area的大小与`font-size`, 或者`line-height(Chrome默认约为1.2)`大小相关.

------

**inline-block box** 

- 行内块状框（`inline-block` box） 像是上述两种的集合：它不会重新另起一行但会像行内框（ `inline` box）一样随着周围文字而流动，而且他能够设置宽高，并且像块框一样保持了其块特性的完整性，它不会在段落行中断开。
- `vertical-align` 属性会影响到 `inline-block` 元素，你可能会把它的值设置为 `top` 。
- 你需要设置每一列的宽度
- 如果HTML源代码中元素之间有空格，那么列与列之间会产生空隙

```

```

```html
常用的行内块级元素有, <button style="height: 100px; width: 100px">button</button> <span>从左至右流动布局， 并且可以设置宽高</span>
```

```html
<p style="background: red">
    展示一个inline block box，比如一个<button style="height: 50px">button</button>, 还有一个图片<img src="./img/avatar.jpg" alt="图片">，看吧
  </p>
```

上面代码演示了inline block box的特性:

![](https://user-gold-cdn.xitu.io/2018/12/18/167c145caba21d5f?w=778&h=148&f=png&s=10860)

上图中, 图片是`inline`类型, 文字是`inline`, button是`inline block`, 由于line box的高度是由其内部的元素最高点到元素最低点的距离, 由于图片和文字属于同一类型,所以会在同一行上并对齐.

------

**none**

```html
另一个常用的display值是 none 。一些特殊元素的默认 display 值是它，例如 script 。 display:none 通常被 JavaScript 用来在不删除元素的情况下隐藏或显示元素。
```

------

### 盒模型属性

文档的每个元素被构造成文档布局内的一个矩形框，框每层的大小都可以使用一些特定的CSS属性调整。相关属性如下:

![](https://user-gold-cdn.xitu.io/2018/12/18/167c145cab8ddcaf?w=1328&h=996&f=png&s=64942)



![](https://user-gold-cdn.xitu.io/2018/12/18/167c145cac4a32a6?w=431&h=182&f=png&s=16089)

- `width`和`height`: 设置**内容框（content box）**的宽度和高度。内容框是框内容显示的区域——包括框内的文本内容，以及表示嵌套子元素的其它框。只有block才能设置宽高, inline不能设置宽高.还有其他属性可以更巧妙地处理内容的大小——设置大小约束而不是绝对的大小。这些属性包括[`min-width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/min-width)、[`max-width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/max-width)、[`min-height`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/min-height) 和 [`max-height`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/max-height)。
- `padding`: **padding** 表示一个 CSS 框的**内边距** ——这一层位于内容框的外边缘与边界的内边缘之间。该层的大小可以通过简写属性[`padding`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/padding) 一次设置所有四个边，或用 [`padding-top`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/padding-top)、[`padding-right`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/padding-right)、[`padding-bottom`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/padding-bottom) 和 [`padding-left`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/padding-left) 属性一次设置一个边。

```css
body { padding: 36px;} //对象四边的内边距均为36px 
body { padding: 36px 24px; } //上下两边的内边距为36px，左右两边的补丁边距为24px 
body { padding: 36px 24px 18px; } //上、下两边的内边距分别为36px、18px，左右两边的内边距为24px 
body { padding: 36px 24px 18px 12px; } //上、右、下、左内边距分别为36px、24px、18px、12px
body { padding: auto;} // 浏览器自动
body { padding: 40%;} // 基于父元素的宽度的内边距的长度
```

- `border`: CSS 框的**边界**（border）是一个分隔层，位于内边距的外边缘以及外边距的内边缘之间。边界的默认大小为0——从而让它不可见——不过我们可以设置边界的厚度、风格和颜色让它出现。 [`border`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border) 简写属性可以让我们一次设置所有四个边，例如 `border: 1px solid red;`, 设置border是调试的最好方法.

1. [`border-top`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-top), [`border-right`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-right), [`border-bottom`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-bottom), [`border-left`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-left): 分别设置某一边的边界厚度／风格／颜色。

2. [`border-width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-width), [`border-style`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-style), [`border-color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-color): 分别仅设置边界的厚度／风格／颜色，并应用到全部四边边界。

3. 你也可以单独设置某一个边的三个不同属性，如 [`border-top-width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-top-width), [`border-top-style`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-top-style), [`border-top-color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-top-color)，等。 

- `margin`: 外边距（margin）代表 CSS 框周围的外部区域，称为**外边距**，它在布局中推开其它 CSS 框。其表现与 padding 很相似；简写属性为 [`margin`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/margin)，单个属性分别为 [`margin-top`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/margin-top)、[`margin-right`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/margin-right)、[`margin-bottom`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/margin-bottom) 和 [`margin-left`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/margin-left)。

  > **注意**: 外边距有一个特别的行为被称作[外边距塌陷（margin collapsing）](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Box_Model/Mastering_margin_collapsing)：当两个框彼此接触时，它们的间距将取两个相邻外边界的最大值，而非两者的总和。

```css
body { margin: 36px;} //对象四边的外边距均为36px 
body { margin: 36px 24px; } //上下两边的外边距为36px，左右两边的外边距为24px 
body { margin: 36px 24px 18px; } //上、下两边的外边距分别为36px、18px，左右两边的外边距为24px 
body { margin: 36px 24px 18px 12px; } //上、右、下、左外边距分别为36px、24px、18px、12px
body { margin: auto;} // 浏览器自动
body { margin: 40%;} // 基于父元素的宽度的内边距的长度
```

------

### 脱离文档流

> 什么是文档流?
>
> 就是文档内元素的流动方向.
>
> 浮动元素会脱离正常的文档布局流，并吸附到其父容器的左边或者右边。

1. `float`浮动: CSS属性指定一个元素应沿其容器的左侧或右侧放置，允许文本和内联元素环绕它。该元素从网页的正常流动中移除，尽管仍然保持部分的流动性.最初引入 [`float`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/float) 属性是为了能让 web 开发人员实现简单的布局，包括在一列文本中浮动的图像，文字环绕在它的左边或右边.

- `float: left`: 表明元素必须浮动在其所在的块容器左侧的关键字。
- `float: right`: 表明元素必须浮动在其所在的块容器右侧的关键字。
- `float: none`: 表明元素不进行浮动的关键字。
- 当一个元素浮动之后，它会被移出正常的文档流，然后向左或者向右平移，一直平移直到碰到了所处的容器的边框，或者碰到**另外一个浮动的元素**。
- 当给子元素`float`时, 需要给该子元素的顶级标签清除浮动, 使用`clearfix`.

```css
clearfix:after{
    content: '';
    clear: both;
    display: block;
}
```

- 关于浮动可以看下[张鑫旭的一篇关于浮动的深入研究](https://www.zhangxinxu.com/wordpress/2010/01/css-float%E6%B5%AE%E5%8A%A8%E7%9A%84%E6%B7%B1%E5%85%A5%E7%A0%94%E7%A9%B6%E3%80%81%E8%AF%A6%E8%A7%A3%E5%8F%8A%E6%8B%93%E5%B1%95%E4%B8%80/)



1. `position`定位

**position**属性用于指定一个元素在文档中的定位方式。[`top`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/top)，[`right`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/right)，[`bottom`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/bottom)和 [`left`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/left) 属性则决定了该元素的最终位置。

**定位类型**

- **相对定位元素（****relatively positioned element****）**是[计算后](https://developer.mozilla.org/zh-CN/docs/Web/CSS/computed_value)位置属性为 `relative `的元素。
- **绝对定位元素（absolutely positioned element）**是[计算后](https://developer.mozilla.org/zh-CN/docs/Web/CSS/computed_value)位置属性为 `absolute` 或 `fixed` 的元素。

**取值**

- static

该关键字指定元素使用正常的布局行为，即元素在文档常规流中当前的布局位置。此时 `top`, `right`, `bottom`, `left` 和 `z-index `属性无效。

- relative 相对定位

> 相对定位的元素是在文档中的正常位置偏移给定的值，但是不影响其他元素的偏移

该关键字下，元素先放置在未添加定位时的位置，再在不改变页面布局的前提下调整元素位置（因此会在此元素未添加定位时所在位置留下空白）。

![](https://user-gold-cdn.xitu.io/2018/12/18/167c145d41c7748e?w=1564&h=316&f=png&s=71248)

- absolute 绝对定位

> 相对定位的元素并未脱离文档流，而绝对定位的元素则脱离了文档流。在布置文档流中其它元素时，绝对定位元素不占据空间, 一般给父元素添加relative, 子元素添加absolute,结合使用.

不为元素预留空间，通过指定元素相对于最近的非 static 定位祖先元素的偏移，来确定元素位置。绝对定位的元素可以设置外边距（margins），且不会与其他边距合并。

![](https://user-gold-cdn.xitu.io/2018/12/18/167c145d6b221be5?w=1558&h=344&f=png&s=71871)

- fixed 固定定位

> 固定定位与绝对定位相似，但元素的包含块为 viewport 视口。该定位方式常用于创建在滚动屏幕时仍固定在相同位置的元素。

不为元素预留空间，而是通过指定元素相对于屏幕视口（viewport）的位置来指定元素位置。元素的位置在屏幕滚动时不会改变。打印时，元素会出现在的每页的固定位置。`fixed` 属性会创建新的层叠上下文。当元素祖先的 `transform`  属性非 `none` 时，容器由视口改为该祖先。

![](https://user-gold-cdn.xitu.io/2018/12/18/167c145d6af9ba84?w=1564&h=336&f=png&s=123825)

------

### position和float的区别

|                    | 脱离文档流 | 原占位保留 |    清除方式     | z-index属性 |
| :----------------: | :--------: | :--------: | :-------------: | :---------: |
|       float        |     是     |     否     |    clearfix     |   不支持    |
| position: relative |     否     |     是     | position:static |    支持     |
| position: absolute |     是     |     否     | position:static |    支持     |
|  position: static  |     否     |     否     |                 |    支持     |
|  position: fixed   |     是     |     是     | position:static |   不支持    |

float主要就是实现文字环绕图片显示.其他无法做到.浮动就是个带有方位的`display:inline-block`属性。字之所以会环绕含有`float`属性的图片时因为**浮动破坏了正常的line boxes**。



### box-sizing

**盒模型**。当你设置了元素的宽度，实际展现的元素却超出你的设置：这是因为元素的边框和内边距会撑开元素。看下面的例子，两个相同宽度的元素显示的实际宽度却不一样。

**盒模型尺寸有两种**

- content-box: 会计算border和padding, 盒模型的默认样式
- Border-box: 不会计算border和padding

![](https://user-gold-cdn.xitu.io/2018/12/18/167c145dc52f4884?w=1550&h=281&f=png&s=58469)

[`box-sizing`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/box-sizing) 通过更改盒模型来拯救我们，盒子的宽度取值为 content + padding + border，而不仅是之前的content——所以当增加内边距或边界的宽度时，不会使盒子更宽——而是会使内容调整得更窄。

你设置一个元素为 `box-sizing: border-box;` 时，此元素的内边距和边框不再会增加它的宽度。这里有一个与前一页相同的例子，唯一的区别是两个元素都设置了 `box-sizing: border-box;` ：

![](https://user-gold-cdn.xitu.io/2018/12/18/167c145dce83a837?w=1560&h=284&f=png&s=66001)

### z-index

`z-index` 属性指定了一个具有定位属性的元素及其子代元素的 z-order。 当元素之间重叠的时候，z-order 决定哪一个元素覆盖在其余元素的上方显示。 通常来说 z-index 较大的元素会覆盖较小的一个。

对于一个已经定位的元素（即position属性值是非static的元素），`z-index` 属性指定：

1. 元素在当前堆叠上下文中的堆叠层级。
2. 元素是否创建一个新的本地堆叠上下文

**取值**

- Auto

元素不会建立一个新的本地堆叠上下文。当前堆叠上下文中新生成的元素和父元素堆叠层级相同。

- integer

整型数字是生成的元素在当前堆叠上下文中的堆叠层级。元素同时会创建一个堆叠层级为0的本地堆叠上下文。这意味着子元素的 z-indexes 不与元素外的其余元素的 z-indexes 进行对比。这意味着其实 CSS 允许你在现有的渲染引擎上层叠的摆放盒模型元素。 所有的层都可以用一个整数( z 轴顺序)来表明当前层在 z 轴的位置。 数字越大， 元素越接近观察者。Z 轴顺序用 CSS 的 [`z-index`](https://developer.mozilla.org/en-US/docs/Web/CSS/z-index) 属性来指定。

------

### 左右布局

1. `float + margin`

```css
.one{
    ...
    float: left;
    display: inline-block;
}
.two{
    ...
    float: right;
    margin-right: 20px;
    display: inline-block;
}
或者
.two{
    margin-left: 100px;
    display: inline-block;
}
```

![](https://user-gold-cdn.xitu.io/2018/12/18/167c145e0eaa78fa?w=1564&h=435&f=png&s=85447)

1. `position`

```css
.father{
  ...
  height: 100px;
  position: relative;
}
.one{
  ...
  position: absolute;
}
.two{
  ...
  position: absolute;
  right: 10px;
}

```

![](https://user-gold-cdn.xitu.io/2018/12/18/167c145eb27f17d7?w=1567&h=344&f=png&s=98893)

### 左中右布局

1. `float: left, float: right`

```css
.father{
  height: 100px;
  border: 1px solid black;
}
.one{
  width: 50px;
  height: 50px;
  background: red;
  float: left;
}
.two{
  width: 50px;
  height: 50px;
  background: green;
  float: right;
}
.three{
  background: yellow;
}
```

![](https://user-gold-cdn.xitu.io/2018/12/18/167c145ece64164b?w=1568&h=345&f=png&s=86048)

1. `position: absolute`

```css
.father{
  height: 100px;
  border: 1px solid black;
  position: relative;
}
.one{
  width: 50px;
  height: 50px;
  background: red;
  position: absolute;
  left: 0;
}
.two{
  width: 50px;
  height: 50px;
  background: green;
  position: absolute;
  right: 0;
}
.three{
  background: yellow;
  position: absolute;
  left: 50px;
  right: 50px;
}
```

![](https://user-gold-cdn.xitu.io/2018/12/18/167c145ef4945a53?w=1559&h=439&f=png&s=94899)

### 水平居中

1. `margin auto` 

```css
.father{
  height: 100px;
  border: 1px solid black;
}
.one{
  width: 50px;
  height: 50px;
  background: red;
  margin: 25px 0;
}
```

1. `父元素display:inline-block,子元素text-align: center;`

```css
.father{
  width: 500px;
  border: 1px solid black;
  text-align: center;
}
.one{
  width: 50px;
  height: 50px;
  background: red;
  display: inline-block;
}
```

### 垂直居中

1. `margin auto`

```css
.father{
  height: 100px;
  border: 1px solid black;
}
.one{
  width: 70px;
  height: 50px;
  background: red;
  margin: 0 auto;
}
```

当浏览器窗口比元素的宽度还要窄时，浏览器会显示一个水平滚动条来容纳页面。这时在这种情况下使用 `max-width` 替代 `width` 可以使浏览器更好地处理小窗口的情况.

1. `position`

```css
.father{
  width: 500px;
  height: 100px;
  border: 1px solid black;
}
.one{
  width: 50px;
  height: 50px;
  background: red;
  position: absolute;
  left: 50%;
  margin-left: -25px;
}
```