# iframe 问题集锦

+ jquery获取iframe内容

```
$( "#website_property" ).contents().find( ".publiclist-center-content" ).height(); //内容高度
```

+ ie8中获取高度需要注意

+ 加上
+ $("#website_property").load(function(){}

```
$("#website_property").load(function(){
    $( "#website_property" ).contents().find( ".publiclist-center-content" ).height(); //内容高度
}
```

+ [软件开发程序员博客文章收藏网](http://www.programgo.com/category/mysql/)