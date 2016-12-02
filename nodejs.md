---
title: nodejs
date: 2016-11-18 15:44:22
tags:  NODE
---

#  前端ajax上传文件，图片，后端nodejs接收文件；
> 学习了nodejs，就想实现一下有进度条的文件上传，

> 在做这个功能的时候遇到的问题

+ 用普通的ajax无法实现文件上传，只能post，get，一些json，string字符串；
+ 想要上传文件或者图片，可以添加form上传；注意需要在form上添加 标示  enctype="multipart/form-data"
    * 缺点，这样会倒置页面的刷新；很糟糕有没有
+ 还可以在页面中添加一个ifame,将表单提交到ifame中，不过，一听说有iframe就有点糟心有没有；


于是就有了下面的东西；
请自动忽略没有样式(只是为了实现功能)这个梗，啊哈哈；

好了废话少说直接上代码


## 前端部分代码

``` html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        .progressBar{
            width: 150px;
            height: 15px;
            border: 1px solid red;
            /*display: none;*/
            border-radius: 5px;
        }
        .bar {
            width: 0;
            height: 100%;
            background: #08d09a;
            border-radius: 5px;
            line-height: 0;
            margin: 0;
        }
    </style>
</head>
<body>
<button id="submit">提交</button>
<input type="file" name="file" id="fileInputElement"/>
<div class="progressBar" style="display: none;">
    <p class="bar"></p>
</div>
<script>
    var btn = document.getElementById('submit');
    var fileInputElement = document.getElementById('fileInputElement');
    var bar = document.getElementsByClassName('bar')[0];
    var progressBar = document.getElementsByClassName('progressBar')[0];

    btn.onclick =function(){
        progressBar.style.display = 'block';
        var oMyForm = new FormData();
        oMyForm.append("username", "Groucho");
        oMyForm.append("accountnum", 123456); 
        // 数字123456被立即转换成字符串"123456"

        // fileInputElement中已经包含了用户所选择的文件
        oMyForm.append("userfile", fileInputElement.files[0]);

        var oFileBody = '<a id="a"><b id="b">hey!</b></a>'; // Blob对象包含的文件内容
        var oBlob = new Blob([oFileBody], { type: "text/xml"});


        var oReq = new XMLHttpRequest();

        oReq.open("POST", "/formupload");
        // 文件上传过程的回调
        oReq.upload.onprogress = function(e) {
            console.log((e.loaded/e.total)*100+'%')
            bar.style.width = (e.loaded/e.total)*100+'%';
        }

        /**
         *   e.loaded 文件已经上传了的大小
         *   e.total  文件总大小
          e.loaded/e.total)*100+'%'  转化成比例；
         */
        // 文件上传完毕的回调
        oReq.upload.onloadend = function(e) {
            console.log('接收完成'+e.loaded+'/'+e.total);
            setTimeout(function(){
                progressBar.style.display = 'none';
                bar.style.width = 0;
            },1000)
        }
        oReq.send(oMyForm);
    }
</script>
</body>
</html>
```

### 用到了  *FormData* 类；

> 使用方法
+ 通过new FormData 创建一个form提交实例对象；此对象会有append方法，
    * 用法 oMyform.append(name,value) name是一个字段，value是对应的值(可以是字符串，数字，file文件（通过dom.files[0]获得）)

```js
    var oMyForm = new FormData();
    oMyForm.append("username", "Groucho");
    oMyForm.append("accountnum", 123456);
    oMyForm.append("userfile", fileInputElement.files[0]);
```

### 用到了XMLHttpRequest 的 onprogress  和  onloadend

*注意* onprogress、onloadend、需要通过xhr.upload 调用如下；

```js
oReq.upload.onprogress=function(e){
    console.log(e.loaded)
    console.log(e.total)
};
oReq.upload.onloadend=function(e){};
```

# nodejs 后端的处理

> 主要用到了formidable模块

## 主要代码逻辑


```  js
/**
 * [导出一个中间件，formupload，用于处理文件上传；]
 */
exports.formupload = function(req,res,next){
    //console.log(req);
    var form = new formidable.IncomingForm();
    var uploadDir = path.normalize(__dirname+'/'+"../avatar");
    form.uploadDir = uploadDir;
    console.log(uploadDir);
    form.parse(req, function(err, fields, files) {
        for(item in files){
            (function(){
                var oldname = files[item].path;
                var newname = files[item].name === 'blob' ? oldname+'.xml' : oldname+"."+files[item].name.split('.')[1];
                fs.rename(oldname,newname,function(err){
                    if(err) console.log(err);
                    console.log('修改成功');
                })
            })(item);
        }
        console.log(util.inspect({fields: fields, files: files}));
        res.send('2');
    });
```

## 遇到的问题

+ for 循环中有异步逻辑，导致异步逻辑出现问题；
+ formidable 的上传文件路径用相对路径会找不到所指定的路径

## 解决办法

+ 可以用闭包实现，每次传进到闭包的变量不会受到外界的影响；
+ 用牛逼的__dirname 变量；指向当前文件的绝对路径；

