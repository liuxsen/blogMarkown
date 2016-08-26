---
title: 'html5接口'
date: 2016-05-15 22:00:07
tags: js
---
# html5.md
> localStorage 本地存储接口

1. localStorage.getItem(keyName)

    ```js
    var aValue = localStorage.getItem(keyName);
    ```

2. localStorage.setItem(keyName, keyValue);

    ```js
    localStorage.setItem(keyName, keyValue);
    ```

3. localStorage.removeItem(keyName);
4. localStorage.clear();
5. localStorage.length;

> localStorage 与 sessionStorage 的区别：

-localStorage：
    + 即使浏览器关闭了，数据也会被保存下来并可用于所有来自同源（相同域名、协议和端口）窗口的加载。

    + 主要用于参数设置或者偏好设置的功能。

- sessionStorage：
    + 数据存储在窗口对象中，对于其他窗口或标签不可见，并且当窗口关闭时，数据丢失。

    + 主要用于特殊的窗口状态。

---

那么要怎么使用 Web Storage？

其实提供的接口很简单，localStorage 和 sessionStorage 的用法是一样的。

1. 设置数据：setItem(name, value)

2. 获取数据：getItem(name)

3. 删除键值：removeItem(name)

4. 删除所有键值：clear()

```js
localStorage.setItem('name', 'wenzhixin');
localStorage.getItem('name'); //'wenzhixin'
localStorage.removeItem('name');
localStorage.clear();
```

当然，你也可以使用普通的对象用法：
```js
localStorage.name = 'wenzhixin';
localStorage['name'] = 'wenzhixin';
localStorage.name; //'wenzhixin'
localStorage['name']; //'wenzhixin'
delete localStorage.name;//删除键值
delete localStorage['name'];//删除键值
```

在实际使用中，会先将数据转换为 JSON，作为字符存储，如：

```js
localStorage[name] = JSON.stringify(value); //存储
JSON.parse(localStorage[name]); //读取
```

如何判断一个浏览器是否支持 Web Storage 呢？

```js
function supportsLocalStorage() {
    try {
        return 'localStorage' in window && window['localStorage'] !== null;
    } catch (e) {
        return false;
    }
}
```

如何判断一个浏览器是否支持 Web Storage 呢？

```js
function supportsLocalStorage() {
    try {
        return 'localStorage' in window && window['localStorage'] !== null;
    } catch (e) {
        return false;
    }
}
```

> 存储事件与触发条件

当存储对象中的值发生变化后，会触发一个存储事件，事件的数据结构为：

```js
var StorageEvent = {
    key: 'key',
    oldValue: 'oldValue',
    newValue: 'newValue',
    url: 'url',
    storageArea: storage //更改的存储区域
};
```

> 通过 window 来添加事件监听：

```js
function addStorageEvent() {
    var handlerStorage = function(e) {
        console.log(e);
    };
    if (window.addEventListener) {
        window.addEventListener("storage", handlerStorage, false);
    } else {
        window.attachEvent("onstorage", handlerStorage); //IE浏览器
    };
}
```

当然，也可以使用 jQuery 来添加事件：
```js
function addStorageEvent() {
    var handlerStorage = function(e) {
        console.log(e.originalEvent); //使用 jQuery 需要用 originalEvent
    };
    $(window).on('storage', handlerStorage);
}
```
**当调用 setItem(), removeItem(), 和 clear() 方法的时候，都会触发 storage 事件。**

 **那么，下面的代码，是否会触发 StorageEent 呢？**

```js
addStorageEvent();
localStorage.setItem('name', 'wenyi');//是否会触发呢？
```

答案是 no，no～你一定会问为什么不会触发呢？

A storage event is fired on every window/tab except for the one that updated the localStorage object and caused the event.
没错，确实不会触发。因为同一窗口下不会触发事件，当打开新的窗口或者标签，才会触发 Storage Event。

**由此，我们可以知道，storage 事件主要是用于监听 localStorage 数据改变时，通知其他窗口或者标签。**

