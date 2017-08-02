---
layout: default
title: php入门学习(4)
---

## 类与对象相关函数 ##

```
class_alias([$original [,$alias]])  给类取别名  
class_exists($class [,$autoload])   检查类是否已定义  
interface_exists($interface [,$autoload])   检查接口是否已被定义  
method_exists($obj, $method)检查类的方法是否存在  
property_exists($class, $property)  检查对象或类是否具有该属性  
get_declared_classes(void)  返回由已定义类的名字所组成的数组  
get_declared_interfaces(void)   返回一个数组包含所有已声明的接口  
get_class([$obj])       返回对象的类名  
get_parent_class([$obj])    返回对象或类的父类名  
get_class_methods($class)   返回由类的方法名组成的数组  
get_object_vars($obj)   返回由对象属性组成的关联数组  
get_class_vars($class)  返回由类的默认属性组成的数组  
is_a($obj, $class) 如果对象属于该类或该类是此对象的父类则返回TRUE  
is_subclass_of($obj, $class)    如果此对象是该类的子类，则返回TRUE  
get_object_vars($obj)   返回由对象属性组成的关联数组  
``` 

### 常用类 ###

* PHP手册 -> 预定义类  
Closure        闭包类，匿名函数对象的final类  
stdClass    标准类，通常用于对象类保存集合数据  
__PHP_Incomplete_Class        不完整类，当只有对象而没有找到类时，则该对象被认为是该类的对象  
Exception    异常类  
PDO            数据对象类  

### 魔术常量 ###

__DIR__            文件所在的目录  
__LINE__        文件中的当前行号   
__FILE__        文件的完整路径（绝对路径）和文件名  
  
__CLASS__        类的名称  
__METHOD__        类的方法名，包含类名和方法名  
__FUNCTION__    函数名称，用在方法内只表示方法名 

### 反射机制 Reflection ###

作用：1. 获取结构信息        2. 代理执行  
ReflectionClass 报告一个类的有关信息  
ReflectionMethod 报告一个方法的有关信息  
ReflectionClass::export    输出类结构报告  
* 代理执行  
实例化 ReflectionFunction 类的对象 
``` 
    $f = new ReflectionFunction('func');    // func为函数func($p)  
    $f->invoke('param');   
```

## 页面跳转 ## 

- 可以用于访问静态成员、方法和常量，还可以用于覆盖类中的成员和方法。   
- 当在类的外部访问这些静态成员、方法和常量时，必须使用类的名字。   
- self 和 parent 这两个特殊的关键字是用于在类的内部对成员或方法进行访问的。

### 访问辨析 ###

* PHP
```  
header('Loacation: url')
```  
header()执行完毕后，后面的代码也会继续执行，故需在该语句后加die结束  
无法给出提示，直接跳转  
* JS方法
```  
location.href = url
```
  
* HTML
```  
<meta http-equiv="Refresh" content="表示时间的数值; url=要跳转的URI">
```

## Cookie ##

cookie是一种在远程浏览器端储存数据并以此来跟踪和识别用户的机制。
Cookie是完全保持在客户端的如：IE firefox 当客户端禁止cookie时将不能再使  
cookie是HTTP标头的一部分，因此setcookie()函数必须在其它信息被输出到浏览器前调用，这和对header()函数的限制类似。可以使用输出缓冲函数来延迟脚本的输出，直到按需要设置好了所有的cookie或者其它HTTP标头  

### 新增 ###

setcookie    新增一条cookie信息  
setcookie($name [,$value [,$expire [,$path [,$domain [,$secure [,$httponly]]]]]])  
	* 注意：setcookie()函数前不能有输出！除非开启ob缓存！  
* 参数说明  
* $name    - cookie的识别名称  
    使用$_COOKIE['name']抵用名为name的cookie  
* $value    - cookie值，可以为数值或字符串，此值保存在客户端，不要用来保存敏感数据  
    假定$name参数的值为'name'，则$_COOKIE['name']就可取得该$value值  
* $expire    - cookie的生存期限（Unix时间戳，秒数）  
    如果$expire参数的值为time()+60*60*24*7则可设定cookie在一周后失效。如果未设定该参数，则会话后立即失效。  
* $path    - cookie在服务器端的指定路径。当设定该值时，服务器中只有指定路径下的网页或程序可以存取该cookie。  
    如果该参数值为'/'，则cookie在整个domain内有效。  
    如果设为'/foo/'，则cookie就在domain下的/foo/目录及其子目录内有效。  
    默认值为设定cookie的当前目录及其子目录。  
* $domain    - 指定此cookie所属服务器的网址名称，预设是建立此cookie服务器的网址。  
    要是cookie能在如abc.com域名下的所有子域都有效，则该参赛应设为'.abc.com'。  
* $secure    - 指明cookie是否仅通过安全的HTTPS连接传送中的cookie的安全识别常数，如果设定该值则代表只有在某种情况下才能在客户端与服务端之间传递。  
    当设成true时，cookie仅在安全的连接中被设置。默认值为false。  
  
### 读取 ### 
- 浏览器请求时会携带当前域名下的所有cookie信息到服务器。  
- 任何从客户端发送的cookie都会被自动存入$_COOKIE全局数组。  
- 如果希望对一个cookie变量设置多个值，则需在cookie的名称后加[]符号。即以数组形态保存多条数据到同一变量。
```  
    //设置为$_COOKIE['user']['name']，注意user[name]的name没有引号  
    setcookie('user[name]', 'shocker');
```  
- $_COOKIE也可以为索引数组

### 删除 ###

方法1：将其值设置为空字符串  
    setcookie('user[name]', '');  
方法2：将目标cookie设为“已过期”状态。  
    //将cookie的生存时间设置为过期，则生存期限与浏览器一样，当浏览器关闭时就会被删除。  
    setcookie('usr[name]', '', time()-1);  
  
* 注意：  
1. cookie只能保存字符串数据  
2. $_COOKIE只用于接收cookie数据，不用于设置或管理cookie数据。  
    对$_COOKIE进行操作不会影响cookie数据。  
    $_COOKIE只会保存浏览器在请求时所携带的cookie数据。  
3. cookie生命周期：  
    临时cookie：浏览器关闭时被删除  
    持久cookie：$expire参数为时间戳，表示失效时间。  
4. 有效目录  
    cookie只在指定的目录有效。默认是当前目录及其子目录。  
    子目录的cookie在其父目录或同级目录不可获取。  
5. cookie区分域名  
    默认是当前域名及其子域名有效。  
6. js中通过document.cookie获得，类型为字符串  
7. 浏览器对COOKIE总数没有限制，但对每个域名的COOKIE数量和每个COOKIE的大小有限，而且不同浏览器的限制不同。  

cookies用法实例:

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

## session ##

1. 开启session机制  
    session_start()  
    注意：session_start()函数前不能有输出！除非开启ob缓存。  
2. 操作数据  
    对$_SESSION数组进行操作  
3. 浏览器端保存SessionID，默认为当前域名下的所有目录及其子目录生效。即默认设置cookie的path值为'/'  
4. 服务器保存session数据  
    默认保存方式：每个会话都会生成一个session数据文件，文件名为：sess_加SessionID  
5. session可以存储除了资源以外的任何类型数据。  
    数据被序列化后再保存到文件中。  
6. $_SESSION的元素下标不能为整型！  
    因为只对元素值进行序列化。  
    元素内的数组下标无此要求。  
7. 生存周期  
    默认是浏览器关闭  
        因为浏览器保存的cookie变量SessionID是临时的  
        但是服务器端的session数据文件不一定消失（需要等待session的垃圾回收机制来处理）  
    可以延长cookie中PHPSESSID变量的生命周期。（不推荐）  
    php.ini配置session.gc_maxlifetime  
8. 删除数据  
    $_SESSION变量在脚本结束时依然会消失。开启session机制时会造出$_SESSION变量。  
    $_SESSION与保存session数据的文件是两个空间。  
    unset($_SESSION['key'])只是删除数组内的该元素，不会立即相应到保存session数据的文件上。  
        等到脚本结束，才会将$_SESSION的数据写入到该文件中。  
    session_destroy()    销毁保存session数据的文件，也不会对该文件写入内容。  
        并不删除$_SESSION变量，unset或脚本结束才会删除该变量。  
    如何完全删除一个session？需删除3部分  
        unset($_SESSION);      
            删除$_SESSION变量后，数据文件并未被改动。如果单独使用unset，则需先置空$_SESSION = array()  
        session_destroy();  
        setcookie('PHPSESSID', '', time()-1); //保险做法是将其生命周期失效  
    整个脚本周期内，只对数据文件读一次、写一次。  

### 重写session的存储机制 ###

1. session存储方式  
session.save_handler = user|files|memcache  
2. 因数据文件过多导致的问题，可通过分子目录保存进行解决  
PHP配置文件下session.save_path选项，并需手动创建数据存放目录。  
在该配置选项前加层级。分布子目录的原则，利用会话ID的相应字母来分配子目录。仍需手动创建子目录。  
		session.save_path = "2; F:/PHPJob/Temp"  
3. 多服务器数据共享问题  
4. 数据存储操作：  
    	初始化$open、释放资源$close、读$read、写$write、销毁存储介质$destroy
		(调用session_destroy时触发该操作)、垃圾回收$gc  
5. 会话ID的长度可变。不同的设置方式导致不同长度的会话ID。  
		session.hash_function   允许用户指定生成会话ID的散列算法。  
    	'0' 表示MD5（128 位），'1' 表示SHA-1（160 位）。  
		session.hash_bits_per_character    
		允许用户定义将二进制散列数据转换为可读的格式时每个字符存放多少个比特。  
    	可能值为 '4'（0-9，a-f），'5'（0-9，a-v），
		以及 '6'（0-9，a-z，A-Z，"-"，","）。  
    	总hash长度为128bit，会话ID长度为128/可能值，4->32, 5->26, 6->22  
6. 自定义数据存储操作方法  
7. 注意：不用关心PHP如何序列化、反序列化、如何得到数据和写入数据，只做与数据存储相关的操作  
		session_set_save_handler    设置用户自定义的会话数据存储函数  
    	bool session_set_save_handler(callable $open, callable $close,
		callable $read, callable $write, callable $destroy, callable $gc)  
执行顺序：open,  close, read, write, destroy, gc  
8. 先设置处理器，再开启会话  
  
9. 常用函数  
session_start        开启或恢复会话机制  
session_id            获取或设置当前会话ID  
session_destroy        销毁当前会话的所有数据（销毁数据文件）  
session_name        获取或设置当前会话名称（cookie变量名，默认为PHPSESSID）  
session_save_path    获取或设置当前会话数据文件保存路径  
session_set_save_handler    设置用户自定义的会话数据存储函数  
session_unset        释放所有会话变量(清空$_SESSION数组元素)  
session_encode        将当前会话数据编码为一个字符串  
session_decode        将字符串解译为会话数据  
session_write_close    写入会话数据并关闭会话  
session_register_shutdown    关闭会话  
session_set_cookie_params    设置会话cookie变量，必须在session_start()前使用。  
session_set_cookie_params(0,"/webapp/"); //设置session生存时间  
session_get_cookie_params    获取会话cookie变量。返回包含当前会话cookie信息的数组  
  
10. 配置php.ini  
ini_set($varname, $newvalue);  
    //该函数的配置只对当前脚本生效  
    //并非所有php.ini设置均可用该函数设置  
ini_get($varname)   //获取某配置项信息  
ini_get_all([str $extension])   //返回所有配置项信息的数组  
  
11. session扩展配置  
* session.name    指定会话名以用作cookie的名字。只能由字母数字组成，默认为PHPSESSID。  
* session.save_path   定义了传递给存储处理器的参数。  
    如果选择了默认的files文件处理器，则此值是创建文件的路径。默认为/tmp。  
    可选的N参数来决定会话文件分布的目录深度。  
    要使用N参数，必须在使用前先创建好这些目录。在ext/session目录下有个小的shell脚本名叫mod_files.sh可以用来做这件事。  
    如果使用了N参数并且N大于0，那么将不会执行自动垃圾回收。  
* session.save_handler    定义了来存储和获取与会话关联的数据的处理器的名字。默认为files。  
    如果用户自定义存储器，则该值改为user。  
    ini_set('session.save_handler', 'user');//此设置只针对当前脚本生效。  
* session.auto_start  指定会话模块是否在请求开始时自动启动一个会话。默认为 0（不启动）。  
* session.gc_probability与session.gc_divisor合起来定义了在每个会话初始化时启动gc（garbage collection 垃圾回收）进程的概率。此概率用 gc_probability/gc_divisor 计算得来。例如 1/100 意味着在每个请求中有 1% 的概率启动gc进程。session.gc_divisor默认为100。session.gc_probability默认为1。

## 图片生成与处理 ##

1. 新建画布  
imagecreate             新建一个基于调色板的图像  
    resource imagecreate(int $x_size, int $y_size)  
imagecreatetruecolor    新建一个真彩色图像  
2. 基于已有文件或URL创建画布  
imagecreatefromgd2      从GD2文件或URL新建一图像  
imagecreatefromgd2part  从给定的GD2文件或URL中的部分新建一图像  
imagecreatefromgd       从GD文件或URL新建一图像  
imagecreatefromgif      由文件或URL创建一个新图象  
imagecreatefromjpeg     由文件或URL创建一个新图象  
imagecreatefrompng      由文件或URL创建一个新图象  
imagecreatefromstring   从字符串中的图像流新建一图像  
imagecreatefromwbmp     由文件或URL创建一个新图象  
imagecreatefromxbm      由文件或URL创建一个新图象  
imagecreatefromxpm      由文件或URL创建一个新图象  

### 颜色分配 ###

imagecolorallocate          为一幅图像分配颜色  
    int imagecolorallocate(resource $image, int $red, int $green, int $blue)  
imagecolorallocatealpha     为一幅图像分配颜色 + alpha  
imagecolordeallocate        取消图像颜色的分配  
imagecolortransparent       将某个颜色定义为透明色  
imagecolorat            取得某像素的颜色索引值  
imagecolorclosest       取得与指定的颜色最接近的颜色的索引值  
imagecolorclosestalpha  取得与指定的颜色加透明度最接近的颜色  
imagecolorclosesthwb    取得与给定颜色最接近的色度的黑白色的索引  
imagecolorexact         取得指定颜色的索引值  
imagecolorexactalpha    取得指定的颜色加透明度的索引值  
imagecolormatch         使一个图像中调色板版本的颜色与真彩色版本更能匹配  
imagecolorresolve       取得指定颜色的索引值或有可能得到的最接近的替代值  
imagecolorresolvealpha  取得指定颜色 + alpha 的索引值或有可能得到的最接近的替代值  
imagecolorset           给指定调色板索引设定颜色  
imagecolorsforindex     取得某索引的颜色  
imagecolorstotal        取得一幅图像的调色板中颜色的数目  
 
### 区域填充 ###

imagefill   区域填充  
    bool imagefill(resource $image, int $x, int $y, int $color)  
imagefilledarc          画一椭圆弧且填充  
imagefilledellipse      画一椭圆并填充  
imagefilledpolygon      画一多边形并填充  
imagefilledrectangle    画一矩形并填充  
imagefilltoborder       区域填充到指定颜色的边界为止  
imagesettile    设定用于填充的贴图  

### 静态延迟绑定 ###

* self::，代表本类(当前代码所在类)  
    	永远代表本类，因为在类编译时已经被确定。  
    	即，子类调用父类方法，self却不代表调用的子类。

```
class A  
{  
    public static function echoClass()  
    {  
        echo __CLASS__;  
    }  
  
    public static function test()  
    {  
        self::echoClass();        
    }  
}  
  
class B extends A  
{        
    public static function echoClass()  
    {  
         echo __CLASS__;  
    }  
}  
  
B::test(); //输出A  
```
  
* static::，代表本类(调用该方法的类)  
    	用于在继承范围内引用静态调用的类。  
    	运行时，才确定代表的类。  
    	static::不再被解析为定义当前方法所在的类，而是在实际运行时计算的。   

```
class A  
{  
    public static function echoClass()  
    {  
        echo __CLASS__;  
    }  
  
    public static function test()  
    {  
        static::echoClass();        
    }  
}  
  
class B extends A  
{        
    public static function echoClass()  
    {  
         echo __CLASS__;  
    }  
}  
  
B::test(); //输出B    
```

### 图形创建 ###

imagearc        画椭圆弧  
imagechar       水平地画一个字符  
imagecharup     垂直地画一个字符  
imagedashedline 画一虚线  
imageellipse    画一个椭圆  
imageline       画一条线段  
imagepolygon    画一个多边形  
imagerectangle  画一个矩形  
imagesetpixel   画一个单一像素  
imagesx         取得图像宽度  
imagesy         取得图像高度  

### 画笔设置 ###

imagesetbrush   设定画线用的画笔图像  
imagesetstyle   设定画线的风格  
imagesetthickness   设定画线的宽度   

### 图形拷贝 ###

imagecopy           拷贝图像的一部分  
imagecopymerge      拷贝并合并图像的一部分  
imagecopymergegray  用灰度拷贝并合并图像的一部分  
imagecopyresampled  重采样拷贝部分图像并调整大小  
imagecopyresized    拷贝部分图像并调整大小  

### 字符创建  ###

imagestring         水平地画一行字符串  
imagestringup       垂直地画一行字符串  
imagepsslantfont    倾斜某字体  
imagefontheight     取得字体高度  
imagefontwidth      取得字体宽度  
imagettfbbox        取得使用 TrueType 字体的文本的范围  
imageloadfont       载入一新字体  
imagepsencodefont   改变字体中的字符编码矢量  
imagepsextendfont   扩充或精简字体  

### 导出画布为图片 ###

imagegif    以GIF格式将图像输出到浏览器或文件  
imagepng    以PNG格式将图像输出到浏览器或文件  
imagejpeg   以JPEG格式将图像输出到浏览器或文件  
imagewbmp   以WBMP格式将图像输出到浏览器或文件  
通过header()发送 "Content-type: image/图片格式" 可以使PHP脚本直接输出图像。  
    header("Content-type: image/gif"); imagegif($im);  
imagegd     将 GD 图像输出到浏览器或文件  
imagegd2    将 GD2 图像输出到浏览器或文件  

### 释放画布资源 ###

imagedestroy    销毁图像  

### 图像信息 ###

image_type_to_extension     取得图像类型的文件后缀  
getimagesize                取得图像大小  
imagesx                     取得图像宽度  
imagesy                     取得图像高度  
imageistruecolor            检查图像是否为真彩色图像  
imagetypes                  返回当前 PHP 版本所支持的图像类型

### 图像设置 ###

imagerotate         用给定角度旋转图像  
imagealphablending  设定图像的混色模式  
imageantialias      是否使用抗锯齿（antialias）功能  
imagefilter         对图像使用过滤器  
imagegammacorrect   对 GD 图像应用 gamma 修正  
imageinterlace      激活或禁止隔行扫描  

<center><strong>{{ page.date | date_to_string }}</strong></center>
