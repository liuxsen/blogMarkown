## nodejs-helloworld

```js
var http = require('http');
http.createServer(function(req,res){
res.writeHead(200, { 'Content-Type': 'text/plain' });
res.end('Hello world!');
}).listen(3000);
console.log('Server started on localhost:3000; press Ctrl-C to terminate....');
```

+ Node 的核心理念是事件驱动编程。(意味着你必须知道有哪些事件，以
及如何响应这些事件)
+ 路由(路由是指向客户端提供它所发出的请求内容的机制。)

> 路由相关代码示例

```js
var http = require('http');
http.createServer(function(req,res){
// 规范化 url，去掉查询字符串、可选的反斜杠，并把它变成小写
var path = req.url.replace(/\/?(?:\?.*)?$/, '').toLowerCase();
switch(path) {
case '':
res.writeHead(200, { 'Content-Type': 'text/plain' });
res.end('Homepage');
break;
case '/about':
res.writeHead(200, { 'Content-Type': 'text/plain' });
res.end('About');
break;
default:
res.writeHead(404, { 'Content-Type': 'text/plain' });
res.end('Not Found');
break;
}
}).listen(3000);
```

+ 静态资源服务

> 如果你用过 Apache，可能习惯于只是创建一个 HTML 文件，访问它，然后让它自动
发送到客户端。
* Node 不是那样的：我们必须打开文件，读取其中的内容，然后将这些内容
发送给浏览器。*

> 所以我们要在项目里创建一个名为 public 的目录（在这个目录下创建文件 home.html、about.html、notfound.html，
子目录 img，以及一个名为 img/logo.jpg 的图片。以上这些工作就由你自己来完成了：既然
你在阅读这本书，那么你应该知道怎么编写 HTML 文件和找张图片。在你的 HTML 文件中
这样引用 logo： 

```html
<img href="/img/logo.jpg" alt="logo">
```

## 静态文件路由代码

```js
var http = require('http'),
	fs = require('fs');
function serveStaticFile(res, path, contentType, responseCode) {
if(!responseCode) responseCode = 200;
fs.readFile(__dirname + path, function(err,data) {
if(err) {
res.writeHead(500, { 'Content-Type': 'text/plain' });
res.end('500 - Internal Error');
} else {
res.writeHead(responseCode,
{ 'Content-Type': contentType });
res.end(data);
}
});
}
http.createServer(function(req,res){
// 规范化 url，去掉查询字符串、可选的反斜杠，并把它变成小写
var path = req.url.replace(/\/?(?:\?.*)?$/, '').toLowerCase();
switch(path) {
case '':
serveStaticFile(res, '/public/home.html', 'text/html');
break;
case '/about':
serveStaticFile(res, '/public/about.html', 'text/html');
break;
case '/img/logo.jpg':
serveStaticFile(res, '/public/img/logo.jpg',
'image/jpeg');
break;
default:
serveStaticFile(res, '/public/404.html', 'text/html',
404);
break;
}
}).listen(3000);
console.log('Server started on localhost:3000; press Ctrl-C to terminate....');
```
> __dirname 会被解析为正在执行的脚本所在的目录

# Express

1. npm install --save express

> npm install  包名  (指定名称的包安装到 node_modules 目录下)
> 如果用了 npm install 包名 --save (会更新 package.json 文件)
> 因为 node_modules 随时都可以用 npm 重新生成，所以我们不会把这个目录保存在我们的代码库中

>> 为了确保不把它添加到代码库中,我们可以创建一个 .gitignore 文件：

.gitignore
```
# ignore packages installed by npm
node_modules
# put any other files you don't want to check in here,
# such as .DS_Store (OSX), *.bak, etc.
```

```js
// app.js
var express = require('express');
var app = express();
app.set('port', process.env.PORT || 3000);
// 定制 404 页面
app.use(function(req, res){
res.type('text/plain');
res.status(404);
res.send('404 - Not Found');
});
// 定制 500 页面
app.use(function(err, req, res, next){
console.error(err.stack);
res.type('text/plain');
res.status(500);
res.send('500 - Server Error');
});
app.listen(app.get('port'), function(){
console.log( 'Express started on http://localhost:' +
app.get('port') + '; press Ctrl-C to terminate.' );
});
```

> 建议将项目的入口文件命名为 项目英文.js 而不是 app.js (想象一下如果有一堆的app.js文件。。。)
> 注意我们指定程序端口的方式： app.set(port, process.env.PORT || 3000) 。
这样我们可以在启动服务器前通过设置环境变量覆盖端口。如果你在运行这
个案例时发现它监听的不是 3000 端口，检查一下是否设置了环境变量 PORT 
> 能显示 HTTP 请求状态码和所有重定向的浏览器插件。 Redirect Path



