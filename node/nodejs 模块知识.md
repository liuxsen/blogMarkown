# nodejs 模块知识.md

> 全局函数

| 函数名称 | 使用方法 | 功能 | 注意事项 |
|----|-----|------|----|
|require.main|if(module == require.main){}|检测当前模块是否是主模块||
| require.resolve| require.resolve("./testMoudle.js")| 返回加载模块的绝对路径| 这种方法访问模块，不会执行模块的方法|
|require.cache|require.cache[模块名]/require.chache|返回缓存区中已经被加载的模块||
|delete| delete require.cache[模块名]|**删除缓存区中对应的模块**，再次require进来的时候，会再次执行模块中的代码||
|setTimeout||||
|clearTimeout||||
|setInterval||||
|cleatInterval||||

> 全局变量

|变量名字|功能|
|--|--|
|__filename|返回带有完整路径的文件名|
|__dirname|返回模块的完整路径|

> 事件处理机制与事件环机制

+ EventEmitter 类

|方法名与参数| 描述功能|
|addListenr(event,listener)| 对指定事件绑定事件处理函数|
|on(event,listener)} | 对指定事件绑定事件处理函数，addListener的别名|
|once(event,listener)| 对指定事件只执行一次的时间处理函数|




