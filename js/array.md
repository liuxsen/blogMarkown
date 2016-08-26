---
title: '数组'
date: 2016-05-15 22:00:07
tags: js
---
# array.md
> 特点

| 特点 | 说明 |
|---|----|
|元素类型任意性| 数组元素可以是基础数据类型，对象，也可以是数组
|动态性| 根据需要它们会增长或缩减，并且在变化时无需重新分配内存空间
|稀疏性 |数组元素的索引不一定是连续的，它们之间可以有空缺，

> 创建方式

- 数组字面量方式 ： 元素用逗号隔开即可。

```js
var empty = [];//创建空数组
var num = [1,2,3,4,5];//创建5个数值类型元素的的数组
var mix = [1,'jozo',true,[1,2],{1:'jozo'}];//创建任意类型元素的数组
```

- 构造函数方式 : 

    调用构造函数Array()，根据参数不同，创建不同的数组
    
    - 不传递参数

```js
var a = new Arry();//创建一个空数组，但我们更常用下面的方式
var a = [];
```

- 传递一个数值参数，这个参数用来指定数组长度

```js
var a = new Arry(5);// 创建了一个长度为5的数组
```

- 传递多个参数，用这些参数作为数组元素初始化数组。

```js
var a = new Arry(1,'jozo',true,[1,2]);//构造函数的参数将会成为数组元素
```

- 添加与删除
    - 添加

        - 通过索引添加
        
```js
var a = [];
a[0] = 'jozo';//此时 a = ['jozo']
a[1] = 'blog';//此时 a = ['jozo','blog']
```

        - 通过数组方法添加

            push(),concat(),splice(),unshift()方法都可以为数组添加元素，后面将会详细介绍。

    - 删除

        - 删除数组元素

```js
var a = [1,2];
delet a[0];//删除第一个元素
console.log(a[0]);//undefined
console.log(a[1]);//2
console.log(a.length);//2
```

可以看出，通过delete运算符删除数组元素也有一些注意的地方。1.原数组长度不变。2.被删除的元素的值变为undefined.3.数组内的其他元素的索引没有改变。其实就是原数组变成了稀疏数组。

splice(),pop(),shift()数组方法也可以用于删除数组元素，后面讲解。

    - 删除整个数组对象

        - 第一种方式：直接操作数组对象（推荐用法）

```js
var a = [1,2];
a.length = 0;
console.log(a);//输出: []
```


        - 第二种方式：改变变量的引用 （不算真正的删除）

```js
var a = [1,2];
a = [];
console.log(a);//输出: []
```

> 常用方法属性详解

其实上面的知识点不讲我们都差不多都知道的。但是数组的一些方法属性我们虽然知道但是却不会用，或是总是忘记该怎么用，因为它的方法属性也很多，我们来分析下各个方法的特点：

|常用方法|    说明|  返回值| 影响原数组|
|------|-------|------|------|
|1.join()  |  使用不同的分隔符将数组转换成包含分隔符的字符串| 转换后的字符串| F|
|2.reverse()| 颠倒数组元素的顺序 |  重排序的数组 | T|
|3.sort()    |通常会接受一个比较函数将数组特定的顺序排序 |  重排序的数组 | T|
|4.concat()  |将传递给该方法的每一个参数添加到原数组中  |  修改后的数组副本  |  F|
|5.slice()   |获取当前数组中的一或多个元素创建一个新的数组 | 返回新的数组 | F|
|6.splice()  |通过传递参数不同，可实现数组的增删改 | 新的数组  |  T|
|7.push()/pop() | 两个数组的栈方法（后进先出），在数组的末尾增加或删除数组 |   pop()返回数组长度，push()返回被删除的元素 | T|
|8.unshift()/shift() |两个数组的堆方法（先进先出），在数组的前端增加或删除数组  |  unshift()| 返回数组长度，shift()返回删除的元素 | T |

join()方法
--------
将数组中的所有元素都转化为字符串链接在一起，可以指定一个可选的分隔符来分隔各个元素，若未指定分隔符，默认使用逗号：

```js
var boys = ['jozo','jozo1','jozo2'];
var newboy1 = boys.join();
var newboy2 = boys.join('+');
var newboy3 = boys.join(undefined);

console.log(newboy1); // jozo,jozo1,jozo2
console.log(newboy2); // jozo+jozo1+jozo2
console.log(newboy3); // jozo,jozo1,jozo2
console.log(boys); // ["jozo", "jozo1", "jozo2"]
```

从上面的代码可以看出一些问题：

    - 给join()方法传递undefined，也会默认使用逗号分隔符，但是IE7及一下版本会直接用'undefined'作为分隔符。
    - join()方法并没有改变原数组。

reverse()方法
--------------
将数组元素颠倒顺序(注意：并不是从大到小或者是从小到大)，返回逆序的数组，这个方法直接对原数组中排序。

```js
var a = [1,3,2];
console.log(a.reserse());// [2,3,1] 只是颠倒顺序，不是按大小排序
console.log(a);//[2,3,1] 改变了原数组
```

这个方法快速直观明了，但不够灵活，很多时候我们需要特定的排序，所以有了下面的更灵活的方法。

sort()方法
------------
默认情况下，sort()方法按从小到大的排序，但是如果是数值，sort()方法会调用每个元素的toString()方法转换为字符串后再比较：

```js
var num  = [1,5,10,15];
console.log(num.sort()); //[1,10,15,5]  按照字符串比较。

var num  = ['jozo','c','b','a'];
console.log(num.sort()); //['a','b','c','jozo']  按照字符串比较。
```

默认的sort()方法以字母表顺序进行排序，这有时也不是最佳方案，因此我们可以传递一个函数类型的参数作为比较函数，改变排序方式，以便我们确定哪个值在前面。
比较函数：接受两个参数，函数的返回值决定数组的排序方式。

|返回值 |排序方式|
|----|---|
|负数|  从小到大|
|正数|  从大到小|
|0 |  顺序无关紧要|

看下代码：

```js
// 为了直观一点，写个罗嗦的比较函数
var compare = function(a,b){
    if(a < b){
        return -1;
    }else if(a > b){
        return 1;
    }else{
        return 0;
    }
};
var num1  = [1,5,10,15];
console.log(num1.sort(compare)); //[1,5,10,15]  从小到大

var num2  = ['jozo','c','b','a'];
console.log(num2.sort(compare)); //['a','b','c','jozo']  从小到大

```

```js
// compare()函数可以改进下：
//从小到大的比较函数
var compare = function(a,b){
    return a - b;
};
//从大到小的比较函数
var compare = function(a,b){
    return b - a;
};
```

```js
//或者直接给sort()方法传递一个匿名比较函数：
num.sort(function(a,b){return a -b}); // 推荐用法
```

concat()方法
------------
这个方法先会创建当前数组的一个副本，然后将收到的参数添加到副本数组的末尾，返回重新构建的数组。

- 当没有传递参数时，只是返回当前数组的一个副本。

```js
var a = [1,2];
b = a.concat();
console.log(b);//[1,2] a 的副本
console.log(a);//[1,2]; a 未改变
```

- 当传递的参数为非数组时，将会把每个参数添加到副本中
```js
var a = [1,2];
b = a.concat(3,4);
console.log(b);//[1,2,3,4] 在a的副本上添加
console.log(a);//[1,2]; a 未改变
```

- 当传递的参数是数组时，将会把数组的每一个元素添加到副本中。

```js
var a = [1,2];
b = a.concat([3,4]);
console.log(b);//[1,2,3,4] 在a的副本上添加
console.log(a);//[1,2]; a 未改变
```

```js
//来看看参数的另一种形式
var a = [1,2];
b = a.concat([3,4，[5,6]]); //数组的数组
console.log(b);//[1,2,3,4,[5,6]]  //数组的数组直接添加到副本
console.log(a);//[1,2]; a 未改变
```

slice()方法
---------

这个方法返回指定数组的一个片段或子数组，接受一个或两个参数。

1.一个参数 ：返回该参数指定位置（包含）到数组末尾的元素的新数组

var a = [1,2,3,4,5];
a.slice(0);// 返回 [1,2,3,4,5]
a.slice(1);// 返回 [2,3,4,5]
a.slice(7);// 返回 [] 参数超过数组索引，返回空数组
a.slice(-1);//返回 [5] 用数组长度-1 相当于slice(4);
console.log(a);//返回 [1,2,3,4,5] 原数组不变
2.两个参数 ：参数作为始末位置，但不包含第二个参数指定的位置。

var a = [1,2,3,4,5];
a.slice(0,4);// 返回 [1,2,3,4]
a.slice(1,4);// 返回 [2,3,4]
a.slice(1,7);// 返回 [2,3,4,5] 参数超过数组索引，则到数组末尾
a.slice(1,-1);//返回 [2,3,4] 用数组长度-1 相当于slice(1,4);
a.slice(1,-7);//返回 [] 当结束位置小于起始位置，返回空数组
console.log(a);//返回 [1,2,3,4,5] 原数组不变
3.6 splice()方法

这个数组恐怕是数组里最强大的方法了，它有多种用法，主要用途是向数组中部插入元素，请不要和上面的slice()方法混淆了，这是两个完全不同的方法。由参数的不同，可实现下列三种方法：

1.删除 ：指定一个或两个参数，第一个参数是删除的起始位置，第二个参数是要删除的元素个数，若省略第二个参数，则从起始位置删除至末尾：

var a = [1,2,3,4,5];
a.splice(3,2);//返回 [4,5] 从索引3开始，删除2个元素，此时 a = [1,2,3]
a.splice(1);// 返回 [2,3] 此时 a = [1]
2.插入：指定3个及以上个参数，前两个参数和上面的一致，第二个参数一般为0，后面的参数表示要插入的元素：

var a = [1,2,3,4,5];
a.splice(4,0,6,7);//返回 [] 从索引4开始，删除0个元素，此时 a = [1,2,3,4,5,6,7]

//下面这种情况又和concat()不同，直接插入数组而非数组元素
a.splice(4,0,[6,7]);//返回 [] 从索引4开始，删除0个元素，此时 a = [1,2,3,4,5,[6,7]]
3.更新：指定3个及以上个参数，前两个参数和上面的一致，第二个参数指定要删除的元素个数，后面的参数表示要插入的元素：

var a = [1,2,3,4,5];
a.splice(3,2,6,7);//返回 [4,5] 从索引3开始，删除2个元素，此时 a = [1,2,3,6,7]
3.7 push()/pop()方法

补充下数据结构的知识，栈是一种LIFO(Last-In-First-Out，后进先出)的数据结构，也就是最新添加的项最早被移除。而栈中项的插入和移除只发生在栈顶部。数组的push(),pop()方法就为数组实现了类似栈的功能：

1.push()：该方法可以接受任意数量，任意类型的的参数，并将它们添加至数组的末尾（栈顶），最后返回修改后的数组的长度。

var a = [];// 创建空数组
var lng = a.push(1,2,3);// 添加数组元素
console.log(a);// 输出：[1,2,3]
console.log(lng);// 输出：3  返回数组长度3
var lng2 = a.push(4,[5,6]);//
console.log(lng2); // 输出：5  返回数组长度5
console.log(a);//输出：[1,2,3,4,[5,6]]
2.pop() ：相反，该方法删除数组的最后一个元素，减小数组长度，并返回删除的元素。不带参数。

var a = [1,2,3];
var last= a.pop();// 删除数组最后一个元素
console.log(a);// 输出：[1,2]
console.log(last);// 输出：3  被删除的元素是 3
可以看出，这两个方法都是直接修改原数组。

3.8 unshift()/shift()方法

上面提到了栈的数据结构，这里再提一个队列的数据结构，这是一种FIFO(First-In-First-Out,先进先出)的数据结构，队列添加元素是在末端，删除是在前端。很多同学就会猜测了，unshift()就是在末端添加元素，shift()就是在前端删除元素，其实不然：

1.shift()：用于在前端删除数组元素，返回被删除的元素，与push()方法结合便是一对队列方法。

var a = [1,2,3];
a.push(4,5);//此时 a = [1,2,3,4,5] 
var start = a.shift();//此时 a = [2,3,4,5] 删除最前端的元素
console.log(start);// 1 返回删除的元素
2.unshift()：用于在前端添加元素，返回修改后的数组的长度，与pop()方法结合便是一对反操作的队列。

var a = [1,2,3];
a.unshift(4,5);//此时 a = [4,5,1,2,3] 在前端添加元素
var end= a.pop();//此时 a = [4,5,1,2] 
console.log(end);// 3 返回删除的元素
这两个方法同样都是直接修改原数组。

4.ES5的数组方法
ECMAScript定义了9个操作数组的数组方法:

遍历：forEach()
映射：map()
过滤：filter()
检测：every(),some()
简化：reduce(),reduceRight()
搜索：indexOf(),lastIndexOf()

每个方法都接受两个参数：1.要在每个数组元素上运行的函数；2.运行函数的作用域对象 -- this指向 (可选参数)
第一个参数--函数又可传递三个参数（简化和搜索方法除外），分别代表：1.每个数组元素的值；2.元素的索引；3.数组本身

注意：所有这些方法都不会修改原始数组，但是传递的函数是可以修改的。

4.1 forEach()
该方法对数组的每一项运行给定的函数。这个方法没有返回值。

var nums = [1,2,3];
var sum = 0;
nums.forEach(function(value){sum += num;}); //没有对原数组进行修改
console.log(sum); // 6  1+2+3

nums.forEach(function(value,i,ary){ary[i] = value +1;}); //对数组进行了修改
console.log(nums);//[2,3,4]
4.2 map()
该方法对数组的每一项运行给定的函数，返回每次函数调用的结果组成的数组。

var nums = [1,2,3];
var squer = nums.map(function(value){return value*vlaue});
console.log(squer); // [1,4,9]
console.log(nums);// [1,2,3]
注意：这可能看起来有点像forEach()方法，但细看会发现 该方法有返回值，而前者没有，而且返回值是数组，这个数组是新数组，并没有对原始数组进行修改。如果原始数组是稀疏数组，返回的也是相同方式的数组，具有相同的长度和相同的缺失元素。

4.3 filter()
该方法对数组的每一项运行给定的函数，返回该函数会返回true的项组成的数组。

var a = [1,2,3,4,5];
smallValue = a.filter(function(value){return value < 3;});// [1,2]
注意：filter()会跳过稀疏数组中缺少的元素，他的返回数组总是稠密的。下面的方式可以压缩稀疏数组的看空缺：

var a = [1,,3,,5];//有两个空缺元素
Var uglify = a.filter(function(){return true;}); //[1,3,5]
还可以过滤undefined和null的元素：

var a = [1,undefined,3,,null,5];//有两个空缺元素
Var uglify = a.filter(function(value){
    return value != undefined && value != null;
}); //[1,3,5]
4.4 every(),some()
every()：对数组的每一项运行给定的函数，如果该函数对数组的每一项都返回true，则返回true,注意是每一项，有一项为false则为false.

var nums = [1,2,3,4,5];
var bigresult = nums.every(function(value){return value > 2}); // false 不全大于2
var result = nums.every(function(value){return value > 0}); //true 全部大于0
some()：对数组的每一项运行给定的函数，如果该函数对数组的任一项返回true，则返回true。

var nums = [1,2,3,4,5];
var bigresult = nums.every(function(value){return value > 2}); // true 有大于2的元素
var result = nums.every(function(value){return value < 0}); //false 全部大于0
注意：在数组是空数组时，every()返回true,some()返回false



4.5 reduce(),reduceRight()
这两个方法都会迭代数组的所有项，然后构建一个最终的返回值。reduce()从数组的第一项开始，逐个遍历到最后；reduceRight()从数组的最后一项开始，逐个遍历到第一项。

这两个方法都是接收两个参数，一个是在每项上调用的函数，另一个是作为遍历的初始值。调用的函数又接收四个参数，分别是：前一个值，当前值，索引，数组对象。这个函数的返回值都会自动作为下一次遍历的函数的第一个参数。若未指定初始值，第一次遍历发生在数组的第二项上，因此第一个参数就是数组第一项，第二个参数就是数组的第二项。我们来个求和运算：

var nums = [1,2,3,4,5];
nums.reduce(function(pre,cur,index,ary){return pre + cur;}); // 15 

//指定初始值,则第一个参数就是初始值，第二个参数就是数组第一项
nums.reduce(function(pre,cur,index,ary){return pre + cur;},10); 25
在简单的数字元算上，reduce()和reduceRight()除了顺序不同，其他的完全相同。

4.6 indexOf(),lastIndexOf()
这两个方法都接受两个参数：要查找的项，查找起点位置的索引（可选）；indexOf()从数组头部开始检索,lastIndexOf()则从数组尾部向前开始检索。
两个方法都都返回找到的元素的第一次出项的位置（索引），在没有找到的情况下返回 -1 。
要注意的是：在检索时会与数组的每一项进行全等的比较，也就是必须严格相等（===）。

var nums = [1,2,3,4,5,4,3,2,1];
console.log(nums.indexOf(3)); // 2  索引为2
console.log(nums.lastIndexOf(3)) // 6 从后面开始找，索引为6;

console.log(nums.indexOf(3,3)); // 6  从位置3开始向后找
console.log(nums.lastIndexOf(3,3)) // 2 从位置3开始向前找

console.log(nums.indexOf(6)); // -1  没有找到

var class= {name : 'ruanjian'};
var students = [{name : 'jozo'}];
console.log(students.indexOf(class)); //false  非严格相等(不是同一个对象)

var school = [class];
console.log(school.indexOf(class);); //true 严格相等(同一个对象)
5.总结
结合高级程序设计与权威指南两本书，内容比较多，写了好长，写的过程中有种觉得没必要的感觉，但是写完之后就会觉得很有价值，至少对我来说。不是我不会，而是记得不深刻，重新书写一遍之后感觉对数组这东西比较透彻了。我也建议各位多做一个学习总结，如有不正确的，请提醒修正。谢谢。下一篇文章继续介绍数组！关于ES6的一些扩展以及数组一些应用。
