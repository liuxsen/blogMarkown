---
title: sublime
date: 2016-11-18 15:44:22
tags:  编辑器
---

>安装Package Control的方法如下：

点击菜单中的 “View”–“Show Console”（也可通过快捷键 Ctrl + ` 打开，不过可能因与系统其他软件快捷键冲突而打不开）调出 Console。然后把下面的代码粘贴进去后回车即可，需稍微等待一段时间。（以下代码可能会因更新而导致失效，请以官网代码为准。）


```
/*Sublime Text 2 代码*/
import urllib2,os,hashlib; h = '2915d1851351e5ee549c20394736b442' + '8bc59f460fa1548d1514676163dafc88'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); os.makedirs( ipp ) if not os.path.exists(ipp) else None; urllib2.install_opener( urllib2.build_opener( urllib2.ProxyHandler()) ); by = urllib2.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); open( os.path.join( ipp, pf), 'wb' ).write(by) if dh == h else None; print('Error validating download (got %s instead of %s), please try manual install' % (dh, h) if dh != h else 'Please restart Sublime Text to finish installation')
 
/*Sublime Text 3 代码*/
import urllib.request,os,hashlib; h = '2915d1851351e5ee549c20394736b442' + '8bc59f460fa1548d1514676163dafc88'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
```
> 重启Sublime Text即可。

> 干净的卸载sublime 删除下面路径的 sublime文件夹

```
C:\Users\Administrator\AppData\Roaming
```

> sublime 破解注册码

```
—– BEGIN LICENSE —–
Ryan Clark
Single User License
EA7E-812479
2158A7DE B690A7A3 8EC04710 006A5EEB
34E77CA3 9C82C81F 0DB6371B 79704E6F
93F36655 B031503A 03257CCC 01B20F60
D304FA8D B1B4F0AF 8A76C7BA 0FA94D55
56D46BCE 5237A341 CD837F30 4D60772D
349B1179 A996F826 90CDB73C 24D41245
FD032C30 AD5E7241 4EAA66ED 167D91FB
55896B16 EA125C81 F550AF6B A6820916
—— END LICENSE 
```

## sublime常用插件

> [近乎完美的 Markdown 写作体验 - Sublime Text 3 + OmniMarkupPreviewer](http://macplay.leanote.com/post/%E8%BF%91%E4%B9%8E%E5%AE%8C%E7%BE%8E%E7%9A%84-Markdown-%E5%86%99%E4%BD%9C%E4%BD%93%E9%AA%8C-Sublime-Text-3-OmniMarkupPreviewer)
>快捷键 ctrl-alt-o

+ [sublime格式化插件 CodeFormatter]
+  Emmet
+  html beautify
+ css3
+ DocBlockr
    * 一个真正简单的方式来轻松地创建许多语言包括JavaScript，PHP和CoffeeScript的文档块。只要在函数的上面输入/**，按Tab就可以了。DocBlockr会观察函数需要的变量名和类型，并创建文档块。
+ jquery
+ BracketHighlighter 高亮元素
+ AllAutocomplete  可以搜索全部打开的标签页进行提示
+ MarkdownEditing markdown 写作提示工具
+ AutoFileName 自动补全路径
+ ColorPicker    一个完整的选色工具可以直接在你的编辑器中使用     Ctrl/Cmd + Shift + C。
+ IMESupport 中文输入法跟随
+ SideBar Enhancements  顾名思义：增强左边导航栏的作用；
+ bootstrap snippets
+  Sublime​Code​Intel 
> 持所有 Komode Editor 支持的代码语言，如：JavaScript, Mason, XBL, XUL, RHTML, SCSS, Python, HTML, Ruby, Python3, XML, Sass, XSLT, Django, HTML5, Perl, CSS, Twig, Less, Smarty, Node.js, Tcl, TemplateToolkit, PHP等。
> 提供以下功能：

+ 打开并跳转到函数/类等的符号定义位置
+ 实时显示模块/符号的自动补全功能
+ 在状态栏显示当前函数的相关信息
> 插件相关:
> 
    + 适用版本：Sublime Text 2 / Sublime Text 3
    + 调用方法：跳转到定义位置（Alt+Click 或 Control+Windows+Alt+Up）、返回（Control+Windows+Alt+Left）

> sublime 主题
+ Monokai Extended


> sublime sass支持

1. [安装ruby](http://rubyinstaller.org/downloads/)
2. [ruby安装sass](http://www.w3cplus.com/sassguide/install.html)
3. [sublime 安装sass插件](http://blog.dimpurr.com/sublime-sass/)
4. sublime 安装插件 SublimeOnSaveBuild （每次保存的时候就进行编译）

> sublime js错误提示插件 (JSHint与JSHint Gutter)[http://jarontai.github.io/blog/2014/11/28/sublime-jshint/]

# webstorm 破解

```
43B4A73YYJ-eyJsaWNlbnNlSWQiOiI0M0I0QTczWVlKIiwibGljZW5zZWVOYW1lIjoibGFuIHl1IiwiYXNzaWduZWVOYW1lIjoiIiwiYXNzaWduZWVFbWFpbCI6IiIsImxpY2Vuc2VSZXN0cmljdGlvbiI6IkZvciBlZHVjYXRpb25hbCB1c2Ugb25seSIsImNoZWNrQ29uY3VycmVudFVzZSI6ZmFsc2UsInByb2R1Y3RzIjpbeyJjb2RlIjoiSUkiLCJwYWlkVXBUbyI6IjIwMTctMDItMjUifSx7ImNvZGUiOiJBQyIsInBhaWRVcFRvIjoiMjAxNy0wMi0yNSJ9LHsiY29kZSI6IkRQTiIsInBhaWRVcFRvIjoiMjAxNy0wMi0yNSJ9LHsiY29kZSI6IlBTIiwicGFpZFVwVG8iOiIyMDE3LTAyLTI1In0seyJjb2RlIjoiRE0iLCJwYWlkVXBUbyI6IjIwMTctMDItMjUifSx7ImNvZGUiOiJDTCIsInBhaWRVcFRvIjoiMjAxNy0wMi0yNSJ9LHsiY29kZSI6IlJTMCIsInBhaWRVcFRvIjoiMjAxNy0wMi0yNSJ9LHsiY29kZSI6IlJDIiwicGFpZFVwVG8iOiIyMDE3LTAyLTI1In0seyJjb2RlIjoiUEMiLCJwYWlkVXBUbyI6IjIwMTctMDItMjUifSx7ImNvZGUiOiJSTSIsInBhaWRVcFRvIjoiMjAxNy0wMi0yNSJ9LHsiY29kZSI6IldTIiwicGFpZFVwVG8iOiIyMDE3LTAyLTI1In0seyJjb2RlIjoiREIiLCJwYWlkVXBUbyI6IjIwMTctMDItMjUifSx7ImNvZGUiOiJEQyIsInBhaWRVcFRvIjoiMjAxNy0wMi0yNSJ9XSwiaGFzaCI6IjMzOTgyOTkvMCIsImdyYWNlUGVyaW9kRGF5cyI6MCwiYXV0b1Byb2xvbmdhdGVkIjpmYWxzZSwiaXNBdXRvUHJvbG9uZ2F0ZWQiOmZhbHNlfQ==-keaxIkRgXPKE4BR/ZTs7s7UkP92LBxRe57HvWamu1EHVXTcV1B4f/KNQIrpOpN6dgpjig5eMVMPmo7yMPl+bmwQ8pTZaCGFuLqCHD1ngo6ywHKIQy0nR249sAUVaCl2wGJwaO4JeOh1opUx8chzSBVRZBMz0/MGyygi7duYAff9JQqfH3p/BhDTNM8eKl6z5tnneZ8ZG5bG1XvqFTqWk4FhGsEWdK7B+He44hPjBxKQl2gmZAodb6g9YxfTHhVRKQY5hQ7KPXNvh3ikerHkoaL5apgsVBZJOTDE2KdYTnGLmqxghFx6L0ofqKI6hMr48ergMyflDk6wLNGWJvYHLWw==-MIIEPjCCAiagAwIBAgIBBTANBgkqhkiG9w0BAQsFADAYMRYwFAYDVQQDDA1KZXRQcm9maWxlIENBMB4XDTE1MTEwMjA4MjE0OFoXDTE4MTEwMTA4MjE0OFowETEPMA0GA1UEAwwGcHJvZDN5MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAxcQkq+zdxlR2mmRYBPzGbUNdMN6OaXiXzxIWtMEkrJMO/5oUfQJbLLuMSMK0QHFmaI37WShyxZcfRCidwXjot4zmNBKnlyHodDij/78TmVqFl8nOeD5+07B8VEaIu7c3E1N+e1doC6wht4I4+IEmtsPAdoaj5WCQVQbrI8KeT8M9VcBIWX7fD0fhexfg3ZRt0xqwMcXGNp3DdJHiO0rCdU+Itv7EmtnSVq9jBG1usMSFvMowR25mju2JcPFp1+I4ZI+FqgR8gyG8oiNDyNEoAbsR3lOpI7grUYSvkB/xVy/VoklPCK2h0f0GJxFjnye8NT1PAywoyl7RmiAVRE/EKwIDAQABo4GZMIGWMAkGA1UdEwQCMAAwHQYDVR0OBBYEFGEpG9oZGcfLMGNBkY7SgHiMGgTcMEgGA1UdIwRBMD+AFKOetkhnQhI2Qb1t4Lm0oFKLl/GzoRykGjAYMRYwFAYDVQQDDA1KZXRQcm9maWxlIENBggkA0myxg7KDeeEwEwYDVR0lBAwwCgYIKwYBBQUHAwEwCwYDVR0PBAQDAgWgMA0GCSqGSIb3DQEBCwUAA4ICAQC9WZuYgQedSuOc5TOUSrRigMw4/+wuC5EtZBfvdl4HT/8vzMW/oUlIP4YCvA0XKyBaCJ2iX+ZCDKoPfiYXiaSiH+HxAPV6J79vvouxKrWg2XV6ShFtPLP+0gPdGq3x9R3+kJbmAm8w+FOdlWqAfJrLvpzMGNeDU14YGXiZ9bVzmIQbwrBA+c/F4tlK/DV07dsNExihqFoibnqDiVNTGombaU2dDup2gwKdL81ua8EIcGNExHe82kjF4zwfadHk3bQVvbfdAwxcDy4xBjs3L4raPLU3yenSzr/OEur1+jfOxnQSmEcMXKXgrAQ9U55gwjcOFKrgOxEdek/Sk1VfOjvS+nuM4eyEruFMfaZHzoQiuw4IqgGc45ohFH0UUyjYcuFxxDSU9lMCv8qdHKm+wnPRb0l9l5vXsCBDuhAGYD6ss+Ga+aDY6f/qXZuUCEUOH3QUNbbCUlviSz6+GiRnt1kA9N2Qachl+2yBfaqUqr8h7Z2gsx5LcIf5kYNsqJ0GavXTVyWh7PYiKX4bs354ZQLUwwa/cG++2+wNWP+HtBhVxMRNTdVhSm38AknZlD+PTAsWGu9GyLmhti2EnVwGybSD2Dxmhxk3IPCkhKAK+pl0eWYGZWG3tJ9mZ7SowcXLWDFAk0lRJnKGFMTggrWjV8GYpw5bq23VmIqqDLgkNzuoog==
```