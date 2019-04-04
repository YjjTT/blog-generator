---
title: JSONP
date: 2019-03-14 16:59:45
tags: JSONP
---

### JSONP是什么?

> JSONP的历史, 就是前端程序员为了优化用户体验而形成的

首先来看一下浏览器看见什么会马上进行请求?

1. `form`
2. `a`
3. `link`
4. `image`
5. `script`

前三个就不说了,很简单~, 重点说下`image`和`script`

####image发送请求

服务器端代码:

```javascript
response.setHeader('Content-Type', 'image/jpeg')
response.statusCode = 200
response.write(fs.readFileSync('./dog.jpeg'))
// 必须写入一个真实的图片,请求才会成功
```

前端代码:

```javascript
let image = document.createElement('img')
image.src = '/pay'
image.onload = function(){
	alert('打钱成功')
	window.location.reload() // 刷新页面
}
image.onerror = function(){
	alert('打钱失败')
}
// 利用图片的加载成功和失败,来判断请求是否成功.
```

#### script发送请求

`script`元素可以作为一种Ajax传输机制:只须设置`script`元素的`src`属性（假如它还没插入到`document`中，需要插入进去），然后浏览器就会发送HTTP请求下载src属性

所指向的URL。使用`script`元素进行Ajax传输的一个主要原因是，它不受同源策略的影响(不受域名限制)，因此可以使用它们从其他的服务器请求数据，第二个原因是包含JSON编码数据的响应体会解码。 这种使用`script`元素作为Ajax传输的技术称为JSONP

说道script就和JSONP有关了

**什么是JSONP?**

>全称 JSON with Padding，用于解决AJAX跨域问题的一种方案。
>
>由于同源策略的限制，浏览器只允许XmlHttpRequest请求当前源（域名、协议、端口）的资源，而对请求script资源没有限制。通过请求script标签实现跨域请求，然后在服务端输出JSON数据并执行回调函数，这种跨域的数据的方式被称为JSONP。
>
>JSONP是一种非正式传输协议，该协议的一个要点就是允许用户传递一个callback参数给服务端，然后服务端返回数据时会将这个callback参数作为函数名来包裹住JSON数据，这样客户端就可以随意定制自己的函数来自动处理返回数据了。

具体步骤为:

请求方: xxx.com 的前端程序员(浏览器)

响应方: yyy.com 的后端程序员(服务器)

1. 请求方创建 script, src指向响应方, 同时传递一个查询参数 `?callback=xxx`

2. 响应方根据查询参数 callback, 构造形如

   1. xxx.call(undefined, '你要的数据')
   2. xxx('你要的数据')

   这样的响应

3. 浏览器接受到响应, 就会执行 xxx.call(undefined, '你要的数据')

4. 那么请求方就知道了他要的数据

**JSONP的行业要求**

1. callback
2. 上面的xxx换成xxx+随机数(), 例如xxx23231321, 防止污染全局变量

#### JSONP代码

`服务器代码`: 域名为jack.com:8002

```javascript
var http = require('http')
var fs = require('fs')
var url = require('url')
var port = process.env.PORT || 8888

if (!port) {
    console.log('请指定端口号好不啦？\nnode server.js 8888 这样不会吗？')
    process.exit(1)
}
var server = http.createServer(function (request, response) {
    var parsedUrl = url.parse(request.url, true)
    var pathWithQuery = request.url
    var queryString = ''
    if (pathWithQuery.indexOf('?') >= 0) {
        queryString = pathWithQuery.substring(pathWithQuery.indexOf('?'))
    }
    var path = parsedUrl.pathname
    var query = parsedUrl.query
    var method = request.method

    if (path === '/') { // 当请求路径为 '/' 时, 返回一个index.html
        var string = fs.readFileSync('./index.html', 'utf8')
        var amount = fs.readFileSync('./db', 'utf8')
        string = string.replace('&&&amount&&&', amount)
        response.setHeader('Content-Type', 'text/html;charset=utf-8')
        response.end(string)
    } else if (path === '/pay') { // 当请求路径问 '/pay'时
        var amount = fs.readFileSync('./db', 'utf8')
        var newAmount = amount - 1
        fs.writeFileSync('./db', newAmouznt)
        response.setHeader('Content-Type', 'application/javascript')
        response.statusCode = 200
        response.write(`
            ${query.callback}.call(undefined,'success')
        `)
        response.end()
    } else {
        response.statusCode = 404
        response.setHeader('Content-Type', 'text/html;charset=utf-8')
        response.end()
    }
})
server.listen(port)
```

上面的代码

response.write(`
${query.callback}.call(undefined,'success')
`)

第二个参数为string, 也可以叫做StringP, 如果换成JSON,就是JSONP.

```javascript
${query.callbackName}.call(undefined,{
	"success": true,
	"left": ${newAmount}
})
// JSON: { "success": true,"left": ${newAmount}}
// 左padding: ${query.callbackName}.call(undefined,
// 右padding: )
```

`前端代码`: 域名为frank.com:8001

```html
<h5>您的账户余额是 <span id='amount'>&&&amount&&&</span></h5>
    <button id="button">付款</button>
    <script>
    button.addEventListener('click', function (e) {
        let script = document.createElement('script')
		let functionName = 'frank' + parseInt(Math.random() * 100000, 10)
        // 前端声明一个函数, 给后端调用, 函数名通过callback传递给后端
		window[functionName] = function (result) {
            // 后端返回result, 可以是json, 可以是string
			if (result === 'success') {
				alert(`我得到的结果是${result}`)
				amount.innerText = amount.innerText - 1
			} else {
				alert('fail')
			}
		}
		script.src = 'http://jack.com:8001/pay?callback=' + functionName
		document.body.appendChild(script)
		script.onload = function (e) {
            e.currentTarget.remove() // 移除script
			delete window[functionName]
		}
		script.onerror = function () {
			alert('打钱失败')
			e.currentTarget.remove()
			delete window[functionName]
		}
     })
    </script>
```

#### 问题: JSONP为什么不支持 POST 请求?

因为JSONP是通过动态创建script来实现的, 动态创建的script只能用GET,不能用POST.











