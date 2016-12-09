#用nodejs实现json和jsonp服务

> 一、JSON和JSONP

      JSONP的全称是JSON with Padding，由于同源策略的限制，XmlHttpRequest只允许请求当前源（协议，域名，端口）的资源。如果要进行跨域请求，我们可以通过使用html的script标记来进行跨域请求，并在相应中返回要执行的script代码，其中可以直接使用JSON传递JavaScript对象。这种跨域的通讯方式成为JSONP。

      由此我们可以看出两者的区别：

      json： 一种轻量级的数据格式。

      jsonp：为实现跨域，而采用的一种脚本注入方法。

      备注：要了解更多json，可以参见我原先写的一篇介绍json的文章：《JSON那些事》


>    二、实现

为了简单起见，我们要读取数据都是

```js
var data = {'name': 'jifeng', 'company': 'taobao'};
```


##  服务器端代码

```js
var http = require('http');
var urllib = require('url');
var port = 10011;
var data = {'name': 'jifeng', 'company': 'taobao'};
http.createServer(function(req, res){
  var params = urllib.parse(req.url, true);
  console.log(params);
  if (params.query && params.query.callback) {
    //console.log(params.query.callback);
    var str =  params.query.callback + '(' + JSON.stringify(data) + ')';//jsonp
    res.end(str);
  } else {
    res.end(JSON.stringify(data));//普通的json
  }
}).listen(port, function(){
  console.log('server is listening on port ' + port);
})
```

## 客户端代码，为方便起见，我直接用了jQuery的方法

```html

<html>
<head>
  <script src="http://code.jquery.com/jquery-latest.js"></script>
  <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
</head>
<body>
<script type="text/javascript">
function get_jsonp() {
  $.getJSON("http://10.232.36.110:10011?callback=?",
  function(data) {
    $('#result').val('My name is: ' + data.name);
  });
}
</script>
<a href="javascript:get_jsonp();">Click me</a><br />
<textarea id="result" cols="50" rows="3"></textarea>
</body>
</html>

```