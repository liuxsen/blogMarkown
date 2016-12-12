# rem.js 使用方法

+ [移动端适配方案(上)](https://github.com/riskers/blog/issues/17)
+ [移动端适配方案(下)](https://github.com/riskers/blog/issues/18)

## 将方案rem.js加入项目中，

> 所有的尺寸用成rem来替换；

> rem替换快捷方法

### sublime 的插件
> 安装 步骤

+ 下载本项目，cssrem

+ 进入packages目录：Sublime Text -> Preferences -> Browse 打开packges目录
复制下载的cssrem目录到packges目录里。
+ 重启Sublime Text。
+ 进入sublime Preferences -> packge settings -> cssrem -> setting-default 复制
进入 setting-user 将复制的文本粘贴到里面(因为webapp一般尺寸设计按照iphone6 (750px) 来设计，所以，将"px_to_rem" 值改为 75 )修改如下

```json
{
    "px_to_rem": 75,
    "max_rem_fraction_length": 6,
    "available_file_types": [".css", ".less", ".sass"]
}
```

#### 方案用法

+ 比如 ui 给的一张 750 x 1334 的效果图（贴心的ui会直接标记尺寸大小，好喜欢有没有）
没有尺寸就自己量喽；有一张图片100px x 100px ；因为有 cssrem 插件所以直接按照真是的px宽度来写，插件会自己编译计算出750px宽度 对应的rem尺寸；
![sdf](aa.jpg)