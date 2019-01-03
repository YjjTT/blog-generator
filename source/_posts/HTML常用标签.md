---
title: HTML常用标签
date: 2019-01-03 13:11:19
tags: HTML
---

## HTML 常用标签

### Iframe标签

**HTML内联框架元素<iframe>**表示嵌套的浏览上下文, 有效地将另一个HTML页面嵌入到当前页面中。在HTML 4.01中，文档可能包含头部和正文，或头部和框架集，但不能包含正文和框架集。但是，<iframe>可以在正常的文档主体中使用。每个浏览上下文都有自己的会话历史记录和活动文档。包含嵌入内容的浏览上下文称为父浏览上下文。顶级浏览上下文（没有父级）通常是浏览器窗口。

> iframe目前用的比较少, 一些遗留项目会使用iframe

**属性**

1. `frameborder `, iframe默认会有一个很丑的边框, 所有在写iframe的时候, 加上属性`frameborder="0"`可以消除边框.
2. css写样式的时候, `width`可以是使用百分比或者像素, `height`只能是像素.
3. `name` , 通常与a标签结合使用.
4. `src`,  一般都是网址`src="http://www.baidu.com"`, 也可以是相对路径`src="./index.html"`, 嵌套空白页`src="about:blank"`或者是`src="#"`
5. `sandbox`, 如果指定了空字符串，该属性对呈现在iframe框架中的内容启用一些额外的限制条件。属性值可以是用空格分隔的一系列指定的字符串, 比如:`sandbox="allow-forms"`

- `allow-forms`:允许嵌入的浏览上下文可以提交表单。如果该关键字未使用，该操作将不可用。
- `allow-modals`: 允许内嵌浏览环境打开模态窗口。
- `allow-orientation-lock`: 允许内嵌浏览环境禁用屏幕朝向锁定

1. `srcdoc`, 该属性值可以是HTML代码，这些代码会被渲染到iframe中，如果同时指定了src属性，srcdoc会覆盖src所指向的页面。该属性最好能与sandbox和seamless属性一起使用。
2. `seamless`, 该布尔属性指示浏览器将iframe渲染成容器页面文档的一部分。例如，通过打被包含的文档的链接，在iframe页面的样式被渲染之前，父页面的CSS样式就可以应用在iframe中（除非被其他设置阻止）。

![](https://user-gold-cdn.xitu.io/2018/12/14/167aa9a68fd3ae49?w=914&h=708&f=png&s=145914)

------

### a标签

**HTML <a>** 元素  (或锚元素) 可以创建一个到其他网页、文件、同一页面内的位置、电子邮件地址或任何其他URL的超链接。

**属性**

1. `download`: 此属性指示浏览器下载URL或者文件而不是导航到它，因此将提示用户将其保存为本地文件。**此属性仅使用于[同源URL](https://developer.mozilla.org/zh-CN/docs/Web/Security/Same-origin_policy)**, 如果不是同源(同域), 将会导航到该URL, 例如:

- `<a href="http://127.0.0.1:8080/index.html" download="ss">下载</a>` 会下载同源的一个ss.html
- `<a href="http://qq.com" download="ss">下载</a>`, `download`无效, 导航到qq.com

1. `target`: 该属性指定在何处显示链接的资源。 取值为标签（tab），窗口（window），或框架（iframe）等浏览上下文的名称或其他关键词。

- `target="_self"`: 当前页面加载, 如果没有指定此属性的话, 该值是默认值.
- `target="_blank"`: 新窗口打开
- `target="_parent"`: 会加载到当前页面的父页面, 如果没有父页面,则等同于`_self`
- `targe="_top"`: 会加载到最上层页面, 祖先级页面, 当index1.thml包含index2.html, index2.html包含index3.html, 则index3.html中的跳转则会加载到index1.html上

1. `href`: 包含超链接指向的URL或URL片段。

- `<a href="qq.com">QQ</a>`: 点击QQ不会跳转到qq.com, 会把qq.com当成文件, **不是以.com为后缀就是网址,也可以是文件**
- `<a href="//qq.com">QQ</a>`, 不写协议的时候, 无协议绝对地址, 默认是当前页面协议, 是file协议, 就跳转file://qq.com, 是HTTP协议, 就跳转http://qq.com.
- `<a href="xxx.html">QQ</a>`, 相对路径, 路径只会以目录为参考, 如果在index.html中跳转, 并不会以index.html为前缀`index.html/xxx.html`, 会显示`xxx.html`
- `<a href="#1">QQ</a>`, 写锚点, 会自动加到后面, 不会发起请求, `index.html#1`, 虽然不会发起请求,但是页面会有变化.
- `<a href="?name=xxx">QQ</a>`, 写参数, 会自动加到后面, 并发起GET请求, `index.html?name=xxx`
- `<a href="javascript: alert(1)">QQ</a>`, 伪协议, 会执行js代码.
- `<a href="javascript:;">QQ</a>`, 伪协议, 使其标签点击不跳转
- `<a href="">QQ</a>`, 什么也不写, 页面会刷新, 跳转到了自己.

1. `name`: 和iframe配合使用

------

### form标签

**HTML <form>** **元素** 表示了文档中的一个区域，这个区域包含有交互控制元件，用来向web服务器提交信息。

> **a标签和form标签都是跳转, 区别就是a标签发起的是GET请求, form标签发起的是POST请求.**

**属性**

1. `action`: 提交(POST)数据所到的地方.`action="users"`, 就是提交到users, 一个处理这个form信息的程序所在的URL.
2. `autocomplete`: 用于指示 input 元素是否能够拥有一个默认值，这个默认值是由浏览器自动补全的。这个设定可以被属于这个form的子元素的 `autocomplete` 属性重载（覆盖）

- `off`: 在每一个用到的输入域里，用户必须显式的输入一个值，或者document 以它自己的方式提供自动补全；浏览器不会自动补全输入。
- `on`: 浏览器能够根据用户之前在form里输入的值自动补全。

1. `enctype`: 当 `method` 属性值为 `post 时`, enctype 是提交form给服务器的内容的 [MIME 类型](http://en.wikipedia.org/wiki/Mime_type)

- `application/x-www-form-urlencoded`: 如果属性未指定时的默认值
- `multipart/form-data`: 这个值用于一个 `type` 属性设置为 "file" 的 [``](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input) 元素。
- `text/plain (HTML5)`

1. `method`: 浏览器使用这种 [HTTP](https://developer.mozilla.org/en-US/docs/HTTP) 方式来提交 form, GET一般不用写, 如果是GET, 提交的数据会被作为查询参数, 并不会放到第四部分作为formdata, POST会把提交的数据放到formdata里, 如果要给POST加查询参数, 可以通过给URL加查询参数`?user=zzz`

- `post`: 指的是 HTTP [POST 方法](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html#sec9.5) ; 表单数据会包含在表单体内然后发送给服务器.
- `get`: 指的是 HTTP [GET 方法](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html#sec9.3); 表单数据会附加在 `action` 属性的URL中，并以 '?' 作为分隔符, 然后这样得到的 URI 再发送给服务器. 当这样做（数据暴露在URL里面）没什么副作用，或者表单仅包含ASCII字符时，再使用这种方法吧。

1. `target`: 和a标签相同
2. `name` : HTML5中，一个文档中的多个form当中，name必须唯一而不仅仅是一个空字符串. 也可以与**iframe标签**配合使用.

**如果form标签没有提交按钮, 则无法提交, html里只有form标签能提交数据**

------

### input标签

**HTML input 元素**用于为基于Web的表单创建交互式控件，以便接受来自用户的数据。使用input标签提交数据, 必须有name属性.

**属性**

1. `type` : 要呈现的控件类型

- `type="button"`: 普通按钮 <input type="button" value="提交" >
- `type="checkbox"`: 复选框。必须使用 value 属性定义此控件被提交时的值<input type="checkbox">
- `color`：[HTML5](https://developer.mozilla.org/zh-CN/docs/HTML/HTML5) 用于指定颜色的控件。<input type="color" >
- `date：`[HTML5](https://developer.mozilla.org/zh-CN/docs/HTML/HTML5) 用于输入日期的控件（年，月，日，不包括时间）。<input type="date">
- `datetime`：[HTML5](https://developer.mozilla.org/zh-CN/docs/HTML/HTML5) 基于 UTC 时区的日期时间输入控件（时，分，秒及几分之一秒）。<input type="datetime">
- `datetime-local`：[HTML5](https://developer.mozilla.org/zh-CN/docs/HTML/HTML5) 用于输入日期时间控件，不包含时区。<input type="datetime-local">
- `email`：[HTML5](https://developer.mozilla.org/zh-CN/docs/HTML/HTML5) 用于编辑 e-mail 的字段。 合适的时候可以使用 [`:valid`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:valid) 和 [`:invalid`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:invalid) CSS 伪类。<input type="email">
- `file`：此控件可以让用户选择文件。使用 accept 属性可以定义控件可以选择的文件类型。<input type="file">
- `hidden`：不显示在页面上的控件，但它的值会被提交到服务器。<input type="hidden">
- `image`：图片提交按钮。必须使用 src 属性定义图片的来源及使用 alt 定义替代文本。还可以使用 height 和 width 属性以像素为单位定义图片的大小。<input type="image" src="#">
- `month`：[HTML5](https://developer.mozilla.org/zh-CN/docs/HTML/HTML5) 用于输入年月的控件，不带时区。<input type="month">
- `number`: [HTML5](https://developer.mozilla.org/zh-CN/docs/HTML/HTML5) 用于输入浮点数的控件。<input type="number">
- `password`：一个值被遮盖的单行文本字段。使用 maxlength 指定可以输入的值的最大长度 。<input type="password">
- `radio`：单选按钮。必须使用 value 属性定义此控件被提交时的值。使用checked 必须指示控件是否缺省被选择。在同一个”单选按钮组“中，所有单选按钮的 name 属性使用同一个值； 一个单选按钮组中是，同一时间只有一个单选按钮可以被选择。<input type="radio" name="xxx"> <input type="radio" name="xxx">
- `reset`：用于将表单所内容设置为缺省值的按钮。<input type="reset">
- `search`：用于输入搜索字符串的单行文本字段。换行会被从输入的值中自动移除。<input type="search">
- `submit`：用于提交表单的按钮。<input type="submit">
- `tel`：[HTML5](https://developer.mozilla.org/zh-CN/docs/HTML/HTML5) 用于输入电话号码的控件；换行会被自动从输入的值中移除A，但不会执行其他语法。可以使用属性，比如 pattern 和 maxlength 来约束控件输入的值。恰当的时候，可以应用 [`:valid`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:valid) 和 [`:invalid`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:invalid) CSS 伪类。<input type="tel">
- `text`：单行字段；换行会将自动从输入的值中移除。<input type="text">
- `time`：[HTML5](https://developer.mozilla.org/zh-CN/docs/HTML/HTML5) 用于输入不含时区的时间控件。<input type="time">
- `url`：[HTML5](https://developer.mozilla.org/zh-CN/docs/HTML/HTML5) 用于编辑URL的字段。 The user may enter a blank or invalid address. 换行会被自动从输入值中移队。可以使用如：pattern 和 maxlength 样的属性来约束输入的值。 恰当的时候使可以应用 [`:valid`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:valid) 和 [`:invalid`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:invalid) CSS 伪类。<input type="url">
- `week`：[HTML5](https://developer.mozilla.org/zh-CN/docs/HTML/HTML5) 用于输入一个由星期-年组成的日期，日期不包括时区。<input type="week">

1. `accept`: 如果该元素的 **type** 属性的值`是file`,则该属性表明了服务器端可接受的文件类型；否则它将被忽略,该属性的值必须为一个逗号分割的列表,包含了多个唯一的内容类型声明：

   - 以 STOP 字符 (U+002E) 开始的文件扩展名。（例如：".jpg,.png,.doc"）

   - 一个有效的 MIME 类型，但没有扩展名
   - `audio/*` 表示音频文件 
   - `video/*` 表示视频文件
   - `image/*` 表示图片文件

2. `autocomplete`: 这个属性表示这个控件的值是否可被浏览器自动填充。如果**type**属性的值是hidden、checkbox、radio、file，或为按钮类型（button、submit、reset、image），则本属性被忽略。

3. `autofocus`: 这个布尔属性允许您指定的表单控件在页面加载时具有焦点（自动获得焦点），除非用户将其覆盖，例如通过键入不同的控件。文档中只有一个表单元素可以具有autofocus属性，它是一个布尔值。 如果type属性设置为隐藏则不能应用（即您不能自动获得焦点的属性设置为隐藏的控件）。

4. `disabled`: 这个布尔属性表示此表单控件不可用。 特别是在禁用的控件中， `click` 事件 [将不会被分发](http://www.whatwg.org/specs/web-apps/current-work/multipage/association-of-controls-and-forms.html#enabling-and-disabling-form-controls) 。 并且，禁用的控件的值在提交表单时也不会被提交。如果 **type** 属性为  hidden，此属性将被忽略。

5. [more](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Input)

------

### button标签

**HTML button 元素**表示一个可点击的按钮，可以用在[表单](https://developer.mozilla.org/en-US/docs/Learn/HTML/Forms)或文档其它需要使用简单标准按钮的地方

**input和button区别**: 是否是空元素, button有子元素, input没有

------

**属性**

1. `type`: button的类型

- `submit`:  此按钮将表单数据提交给服务器。如果未指定属性，或者属性动态更改为空值或无效值，则此值为默认值。
- `reset`:  此按钮重置所有组件为初始值。
- `button`: 此按钮没有默认行为。它可以有与元素事件相关的客户端脚本，当事件出现时可触发。
- menu: 此按钮打开一个由指定[``](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/menu)元素进行定义的弹出菜单。
- 如果form表单里只有一个button标签, 那么这个button标签会自动升级为提交submit按钮

1. `name`: button的名称，与表单数据一起提交。
2. `value`: button的初始值。它定义的值与表单数据的提交按钮相关联。当表单中的数据被提交时，这个值便以参数的形式被递送至服务器。
3. [more](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/button)

------

### 持续更新