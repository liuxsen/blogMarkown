# express.md

1. 什么是中间件？
-----

> 中间件(middleware)就是处理HTTP请求的函数，用来完成各种特定的任务，比如检查用户是否登录、分析数据、以及其他在需要最终将数据发送给用户之前完成的任务。 它最大的特点就是，一个中间件处理完，可以把相应数据再传递给下一个中间件。

+ 小商场项目开发

-------------

+ 数据库设计
+ 分别是user(用户)集合、commodity(商品)集合、cart(购物车)集合，

> user集合

```js
name: {type:String,required:true},
password: {type:String,required:true},
```

> commodity集合

```js
name:{type:String},
price:{type:Number},
imgSrc:{type:String}
```

> 购物车集合

+ uId 用户id
+ cId 商品id
+ cName 商品名称
+ cPrice 商品价格
+ cImgSrc 商品展示路径
+ cQuantity 商品数量
+ cStatus 商品结算状态 false 未结算 true 已结算

```js
uId:{type:String},
cId:{type:String},
cName:{type:String},
cPrice:{type:String},
cImgID:{type:String},
cQuantity:{type:Number},
cStatus:{type:Boolean,default:false}
```