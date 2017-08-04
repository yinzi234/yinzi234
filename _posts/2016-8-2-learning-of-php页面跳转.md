---
layout: default
title: php页面跳转
---

## HTTP头信息 ## 

也就是用PHP的header函数。PHP里的header函数的作用就是向浏览器发出由HTTP协议规定的本来应该通过WEB服务器的控制指令，例如声明返回信

息的类型("Context-type: xxx/xxx")，页面的属性("No cache", "Expire")等等。 

用HTTP头信息重定向到另外一个页面的方法如下：

```
<? 
if (isset($url)) 
{ 
Header("HTTP/1.1 303 See Other"); 
Header("Location: $url"); 
exit; //from www.baidu.com
} 
?>
```

* 注意：
	1. location和“:”号间不能有空格，否则不会跳转。
	2. 在用header前不能有任何的输出。
	3. header后的PHP代码还会被执行。例如，将浏览器重定向到

## Meta标签 ##

Meta标签是HTML中负责提供文档元信息的标签，在PHP程序中使用该标签，也可以实现页面跳转。 若定义http-equiv为refresh,则打开该页面时

将根据content规定的值在一定时间内跳转到相应页面。

若设置content="秒数;url=网址"，则定义了经过多长时间后页面跳转到指定的网址。例如，使用meta标签实现疫苗后页面自动跳转到

```
<   meta   http-equiv = "refresh"  
content = "1;url=http:// bbs.lampbrother.net" >
```

例如，以下程序meta.php实现在该页面中停留一秒后页面自动跳转到www.baidu.com。 

代码如下:

```
<  ?php   
$ url  =  "http://www.baidu.com" ;  ?>  
<   html >    
<   head >    
<   meta   http-equiv = "refresh"   content ="1;  
url = <  ?php echo $url;  ?> " >    
<  /head >    
<   body >    
页面只停留一秒……   
<  /body >  
<  /html >
```

## 脚本实现 ##

1. 
```
<?php
$url="http://www.learnphp.cn"; 
echo "<!--<scrīpt LANGUAGE="Javascrīpt">"; 
echo "location.href='$url'"; 
echo "</scrīpt>-->"; 
?>
```

2. 
```
echo "< meta http-equiv=\\"Refresh\\" content=\\"秒数; url=跳转的文件或地址\\" > "; 
```

其中:XX是秒数,0为立即跳转.refresh 是刷新的意思.Url 是要跳转到的页面. 

## JavaScript ##

```
<  ?php  
$ url  =  "http://bbs.lampbrother.net" ;  
echo " <   script   language = 'javascript'  
type = 'text/javascript' > ";  
echo " window.location.href = '$url' ";  
echo " <  /script > ";  
?>
```

* 此代码可以放在程序中的任何合法位置。

### open() ###

可以限制原窗口还是父窗口,子窗口或者新窗口. 

```
<script>url="submit.php";window.open(\'url,\'\',\'_self\');</script> 
```

其中 更改\'_self\' 就可以实现跳转限制原窗口还是父窗口,子窗口或者新窗口.

## header()函数 ##

header()函数是PHP中进行页面跳转的一种十分简单的方法。header()函数的主要功能是将HTTP协议标头(header)输出到浏览器。

header()函数的定义如下：

```
void header (string string [,bool replace [,int http_response_code]])
```

可选参数replace指明是替换前一条类似标头还是添加一条相同类型的标头，默认为替换。

第二个可选参数http_response_code强制将HTTP相应代码设为指定值。 header函数中Location类型的标头是一种特殊的header调用，常用来实

现页面跳转。

* 注意：
	1. location和“:”号间不能有空格，否则不会跳转。
	2. 在用header前不能有任何的输出。
	3. header后的PHP代码还会被执行。例如，将浏览器重定向到

```
<  ?php 
//重定向浏览器 
header("Location: http://bbs. lampbrother.net"); 
//确保重定向后，后续代码不会被执行 
exit;
?>
```

速度最快,功能强大...但是有个问题必须指出:如果在使用这个函数前已经有html输出,哪怕是一个空格.那么在页顶会显示错误信息.
 

<center><strong>{{ page.date | date_to_string }}</strong></center>
