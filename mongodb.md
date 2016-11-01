---
title: mongodb
date: 2016-10-31 12:38:59
tags: mongodb
---

# mongodb安装
[mongodb](https://www.mongodb.com/download-center?jmp=nav#community)

> mongodb 数据库启动

+ 在文件夹bin下，打开控制台；
+ 输入
```
mongod -dbpath d:/install/mongodb
//启动mongo服务
```
+ 另启动一个控制台，（将bin/mongo.exe 路径加入到环境变量）
+ 输入mongo 链接mongo；

> mongoose 存储数据

```js
var mongoose = require('mongoose');
mongoose.connect('mongodb://localhost/blog');
var db = mongoose.connection;

db.on('error', console.error.bind(console, 'connection error:'));
db.once('open', function callback() {
    // schema class
    var kittySchema = mongoose.Schema({
            name: String
        })
        // 可以在schema上面自定义方法
    kittySchema.methods.speak = function() {
        var greeting = this.name ? '小猫的名字是:' + this.name : "i don't have a name";
        console.log(greeting);
    };
    // model
    var kittyModel = mongoose.model('kitty', kittySchema);

    // 通过model查看所有的documents
    kittyModel.find(function(err, kitties) {
        if (err) console.log(err);
        console.log(kitties);
        console.log('这里是分界线')
    });
    // 查询单个document
    kittyModel.find({ name: '小猫1' }, function(err, kitty) {
        if (err) console.log(err);
        console.log(kitty);
    });
    // document
    var kitty = new kittyModel({ name: '小猫2' });
    kitty.save(function(err) {
        if (err) console.log(err)
        kitty.speak();
    });
});
```

```js
var Schema = mongoose.Schema;
    var animalSchema = new Schema({
        name: String,
        type: String
    });
    // 分发一个方法给schema 所有的document会都有这个方法
    animalSchema.methods.findSimilarTypes = function(cb) {
        return this.model('Animal').find({ type: this.type }, cb)
    };
    // 分发一个方法到schema的statics属性上面，所有的model都有这个方法
    animalSchema.statics.findByName = function(name, cb) {
        return this.find({ name: name }, cb);
    };
    var Animal = mongoose.model('Animal', animalSchema);
    Animal.findByName('小狗1', function(err, dog) {
        if (err) console.log(err);
        console.log('static方法查找')
        console.log(dog);
        console.log('static方法查找')
    })

    var dog = new Animal({ type: 'dog', name: '小狗1' });
    var cat = new Animal({ type: 'cat', name: '小猫1' });
    // dog.save(function(err) {
    //     if (err) console.log(err);
    // });
    // cat.save(function(err) {
    //     if (err) console.log(err);
    // });
    dog.findSimilarTypes(function(err, dogs) {
        console.log(dogs)
    });
}
```

# mongodb 命令行

> 插入数据 && 查询 
+ show dbs （列出所有的数据库）
+  use blog （切换到相应的数据库）
+  db.blog.insert({name:'zhangsan'}) 插入数据
+  db.blog.find(); 查询数据

> 删除数据库

+ use blog
+ db.dropDatabase(); //删除数据库
+ show dbs //查看数据库是否删除成功

# mongoose 操作数据库
## schema 

> minimize 
+ schema属性如果是对象的话，查询的时候，如果查询不到值，那么就不会返回任何的东西
+ (设置minimize) 设置minimize属性值为false，那么在查询不到的时候，就会返回一个空对象

```js
// define a schema 数据结构
    var schema = new Schema({
        name: String,
        friends: [{
            name: String,
            age: Number
        }],
        feature: {
            hair: String
        }
    },{
        minimize:false
        })
    // compile a model
    var TodoModel = mongoose.model('Todo', schema);
    // create a document 
    var todo = new TodoModel({ name: 'zhangsan', feature: { hair: 'heide' } });
    // 保存到数据库
    todo.save({ name: 'xiaohei' }, function(err, todo) {
        if (err) console.log(err);
        console.log(todo);  
        // { __v: 0,name: 'zhangsan',_id: 581861abef24e345a8c7aa93,feature: { hair: 'heide' },friends: []}
        // { __v: 0,name: 'zhangsan',_id: 581861abef24e345a8c7aa93,friends: []}
        // { __v: 0,name: 'zhangsan',_id: 5818636c95599641f08bdb2e,feature: {},friends: [] }

    })
```

> strict

+ 默认值是true 当保存的数据 在schema中没有定义的时候；不会保存到db
+ false 没有定义的数据会被保存到db
+ 也可以定义在model的第二个参数；他会覆盖 schema中设置的strict
```js
var schema = new Schema({
            name: String,
            friends: [{
                name: String,
                age: Number
            }],
            feature: {
                hair: String
            }
        }, {
            minimize: false,
            strict: false
        });
var todo = new TodoModel({ name: 'zhangsan', age: 12 }, true);
//最后的strict值是true（没有定义的数据不会被插入到db）
```