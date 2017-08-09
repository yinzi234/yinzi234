---
layout: default
title: php之cookie
---

## cookie ## 

* cookie是一种在远程浏览器端储存数据并以此来跟踪和识别用户的机制。

* Cookie是完全保持在客户端的如：IE firefox 当客户端禁止cookie时将不能再使。  

* cookie是HTTP标头的一部分，因此setcookie()函数必须在其它信息被输出到浏览器前调用，这和对header()函数的限制类似。可以使用输出缓冲函数来延迟脚本的输出，直到按需要设置好了所有的cookie或者其它HTTP标头。  

### Cookie和Session ###

在非常多时候，我们需要跟踪浏览者在整个网站的活动，对他们身份进行自动或半自动的识别（也就是平时常说的网站登陆之类的功能），这时候，我们常采用Cookie与 Session来跟踪和判断。

区别：

	Session信息是存放在server端
	session id是存放在client cookie的
	php的session存放方法是多样化的，这样就算禁用cookie一样可以跟踪

Cookie是完全保持在客户端的如：IE firefox 当客户端禁止cookie时将不能再使用

cookie是面向路径的.缺省path属性时,WEB服务器页会自动传递当前路径给浏览器.指定路径会强制服务器使用设置的路径. 

在一个目录页面里设的cookie在另一个目录的页面里是看不到的. 


### 设置cookie ###

使用cookie前必须设置cookie. 
函数原型:

```
int setcookie(string name,string value,int expire,string path,string domain,int secure) 
```

其中,除name外,所有的参数都是可选的,可以用空的字符串表示未设置. 
		* 属性value: 用来指定值. 
		* 属性path: 用来指定cookie被发送到服务器的哪一个目录路径下. 
		* 属性domain:能够在浏览器端对cookie的发送进行限定. 
		* expire参数:用来指定cookie的有效时间,它是一个标准的Unix时间标记. 
		* 可以用time()或者mktime()函数取得,以秒为单位. 
		* secure参数:表示这个cookie是否通过加密的HTTPS协议在网络上传输. 

* 注意：
	* 在同一个页面中设置cookie,实际上是按从后往前的顺序进行的.如果要先删除一个cookie,再写入一个cookie,则必须先写写入语句,再写删除语句.否则会出现错误. 

## setcookie ##

简单的:

```
 setcookie("mycookie","value_of_mycookie"); 
```

带失效时间的: 

```
setcookie("withExpire","Expire_in_1_hour",time()+3600); 
```

什么都有的:

```
setcookie("FullCookie","Full_cookie_value",time+3600,"/forum","www.123.com",1); 
```


### 接收和处理 ###

PHP对cookie的处理是全自动的,和处理FORM变量的原则一样.当然也可以使用PHP全局变量,$HTTP_COOKIE_VARS数组. 
例: 

```
echo $mycookie; 
echo $cookie Array[0]; 
echo count($cookie Array); 
echo $HTTP_COOKIE_VARS["mycookie"]; 
```

### 删除 ###

要删除一个已经存在的Cookie，有两个办法：

```
1、SetCookie("Cookie", "");
2、SetCookie("Cookie", "value" , time()-1 / time() );
```

### 使用限制 ###

1. 必须在HTML文件的内容输出之前设置; 
2. 不同的浏览器对cookie的处理不一致,使用时一定要考虑; 
3. 客户端的限制,比如用户设置禁止cookie,则cookie不能建立; 
 
### 用法实例 ###

```
if($_GET['out'])
{   //用于注销cookies
    setcookie('id',"");
    setcookie('pass',"");
    echo "<script>location.href='login.php'</script>"; //因为cookies不是及时生效的，只有你再次刷新时才生效，所以，注销后让页面自动刷新。
}

if($_POST['name']&&$_POST['password']) //如果变量用户名和密码存在时，在下面设置cookies
{   //用于设置cookies
    setcookie('id',$_POST['name'],time()+3600);
    setcookie('pass',$_POST['password'],time()+3600);
    echo "<script>location.href='login.php'</script>"; //让cookies及时生效
   
}
if($_COOKIE['id']&&$_COOKIE['pass'])
{   //cookies设置成功后，用于显示cookies
    echo "登录成功！<br />用户名：".$_COOKIE['id']."<br/>密码：".$_COOKIE['pass'];
    echo "<br />";
    echo "<a href='login.php?out=out'>注销cookies</a>";  //双引号内，如果再有引号，需要用单引号。
}

?>
<form action="" method="post">
用户ID：
<input type="text" name="name" /><br/><br/>
密码：
<input type="password" name="password" /><br/><br />
<input type="submit" name="submit">
</form>
```

## Session的配置与应用 ##

```
session_start();                    //初始化session.需在文件头部

$_SESSION[name]=value;  //配置Seeeion

echo $_SESSION[name];    //使用session

isset($_SESSION[name]);   // 判断

unset($_SESSION[name]);   //删除

session_destroy()；             //消耗所有session
```

* 注意：session_register()，session_unregister，session_is_registered在php5下不再使用

### 用法实例 ###

```
<?php
//session用法实例
session_start();//启动session，必须放在第一句，否则会出错。
if($_GET['out'])
{
      

    unset($_SESSION['id']);
    unset($_SESSION['pass']);
}

if($_POST['name']&&$_POST['password'])
{   
   //用于设置session
    $_SESSION['id']=$_POST['name'];
    $_SESSION['pass']=$_POST['password'];
}

if($_SESSION['id']&&$_SESSION['pass'])
{
    echo "登录成功！<br/>用户ID：".$_SESSION['id']."<br />用户密码：".$_SESSION['pass'];
    echo "<br />";
    echo "<a href='login.php?out=out'>注销session</a>";
}


?>
<form action="login.php"  method="post">
用户ID：
<input type="text" name="name" /><br/><br/>
密码：
<input type="password" name="password" /><br/><br />
<input type="submit" name="submit">
</form>
``` 



<center><strong>{{ page.date | date_to_string }}</strong></center>
