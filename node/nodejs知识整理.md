# nodejs知识整理.md

闭包
-----

```js
var generateClosure = function() {
var count = 0;
var get = function() {
count ++;
return count;
};
return get;
};
var counter1 = generateClosure();
var counter2 = generateClosure();
console.log(counter1()); // 输出 1
console.log(counter2()); // 输出 1
console.log(counter1()); // 输出 2
console.log(counter1()); // 输出 3
console.log(counter2()); // 输出 2
```

上面这个例子解释了闭包是如何产生的： counter1 和  counter2 分别调用了  generate-Closure()  函数，生成了两个闭包的实例，它们内部引用的  count  变量分别属于各自的运行环境。我们可以理解为，在 generateClosure() 返回 get  函数时，私下将  get 可能引用到的  generateClosure()  函数的内部变量（也就是  count  变量）也返回了，并在内存中生成了一个副本，之后 generateClosure()  返回的函数的两个实例 counter1和 counter2  就是相互独立的了。

闭包的用途
-----

+ 嵌套的回调函数
+ 实现私有成员

```js
var generateClosure = function() {
var count = 0;
var get = function() {
count ++;
return count;
};
return get;
};
var counter = generateClosure();
console.log(counter()); // 输出 1
console.log(counter()); // 输出 2
console.log(counter()); // 输出 3
```

我们可以把一个对象用闭包封装起来， 只返回一个 “访问器” 的对象， 即可实现对细节隐藏

bind
-----
```js
var someuser = {
name: 'byvoid',
func: function() {
        console.log(this.name);
    }
};
var foo = {
name: 'foobar'
};
foo.func = someuser.func;
foo.func(); // 输出 foobar
foo.func1 = someuser.func.bind(someuser);
foo.func1(); // 输出 byvoid  上下文环境是 someuser
func = someuser.func.bind(foo);
func(); // 输出 foobar
func2 = func;
func2(); // 输出 foobar
```

上面代码直接将  foo.func  赋值为  someuser.func ，调用  foo.func() 时， this 指
针为 foo ，所以输出结果是 foobar 。 foo.func1 使用了 bind  方法，将 someuser  作为 this 指针绑定到 someuser.func ，调用  foo.func1()  时， this 指针为 someuser ，所以输出结果是 byvoid 。全局函数 func 同样使用了 bind  方法，将 foo 作为 this  指针绑定到  someuser.func ，调用  func()  时， this 指针为  foo ，所以输出结果是 foobar 。而  func2  直接将绑定过的 func 赋值过来，与 func  行为完全相同。

> 理解  bind

尽管  bind 很优美，还是有一些令人迷惑的地方，例如下面的代码：

```js
var someuser = {
name: 'byvoid',
func: function () {
console.log(this.name);
}
};
var foo = {
name: 'foobar'
};
func = someuser.func.bind(foo);
func(); // 输出 foobar
func2 = func.bind(someuser);
func2(); // 输出 foobar
```

