---
layout: default
title: php入门学习(1)
---

## 基础 ##

*  <?php ... ?>所有代码都在这里面,分号表示一句  
*  注释三种//, /*...*/ #  
*  函数,类,关键字大小写不敏感, 即echo和EcHo是一样的  
* 变量以 $ 符号开头，其后是变量的名称; 变量名称必须以字母或下划线开头; 变量名称不能以数字开头; 变量名称只能包含字母数字字符和下划线（A-z、0-9 以及 _）;变量名称对大小写敏感（$y 与 $Y 是两个不同的变量  
这里的变量和shell中的变量不同,不用创建,用的时候就有  
* 变量也分local和globle,函数外为globle,内部则为local;函数内部如果有globle则表示的是一个全局  
* static和c中的static一样  
* echo和print 前者快, 后者不论如何返回1,前者不返回,print可格式化输出  
* 整数和浮点数,var_dump()会返回类型和值  
* 字符串函数,很多,基本常用的函数都具备,使用时查询手册  
strlen()  
strpos("hello world","world")返回6  
* define()类似#define可设置一个常量  
* 字符串接符  
$tx1=hello. $tx2=$tx1."world",则$tx2就是"helloworld",也可是.=  
* --,++也适用   
* <>不等于===全等(值和类型)!==不全等(值和类型都不同),>=,<=这个也可以表示关系型   
* 逻辑运算or,and,xor,&&,||,!  
* 数组操作  
+,==,===,!=,<>,!==  
* php有1000多个内建函数.  

### 命名规则 ###

* 常量名 类常量建议全大写，单词间用下划线分隔    // MIN_WIDTH  
* 变量名建议用下划线方式分隔            // $var_name  
* 函数名建议用驼峰命名法                // varName  
* 定界符建议全大写                 // <<<DING, <<<'DING'  
* 文件名建议全小写和下划线、数字        // func_name.php  
* 私有属性名、方法名建议加下划线        // private $_name _func  
* 接口名建议加I_                    // interface I_Name  

### 语言结构 ###

array(), echo(), empty(), eval(), exit(), isset(), list(), print(), unset()  
echo, print 可省略括号。  

### 预定义常量 ###

* PATH_SEPARATOR  //路径分隔符(Windows为分号，类Unix为冒号)  
* DIRECTORY_SEPARATOR //目录分隔符  
* PHP_EOL //当前系统的换行符  
* PHP_VERSION //PHP版本号  
* PHP_OS  //PHP服务操作系统  
* PHP_SAPI    //用来判断是使用命令行还是浏览器执行的，如果PHP_SAPI=='cli' 表示是在命令行下执行  
PHP_INT_MAX                    INT最大值，32位平台时值为2147483647  
PHP_INT_SIZE                   INT字长，32位平台时值为4（4字节）  
* M_PI    //圆周率值  
* M_E     //自然数  

#### PHP运行环境检测函数 ####  

php_sapi_name() //返回一个PHP与WEB服务器接口类型的小写字符串  
该函数返回值与常量PHP_SAPI一致！  
接口类型：SAPI(the Server API, SAPI)  
可能值：aolserver、apache、apache2filter、apache2handler、caudium、cgi、cgi-fcgi、cli、 continuity、embed、isapi、litespeed milter、nsapi、phttpd、pi3web、roxen、thttpd、tux、webjames  

### 大小写问题 ###

- 类名、方法名、属性名、函数名：不区分大小写  
- 变量名、常量名、元素下标：区分大小写  

### 可变标识符 ###

* 可变变量  $i = 3; $k = 'i'; echo $$k; //输出3  
* 可变函数  function func() {echo 'hello!';} $i = 'func'; $i(); //输出hello  
* 可变下标  $i = '1234'; $k = 3; echo $i[$k];   //输出4  
* 可变类名  class CLS{public $k = 'hello';} $i = 'CLS'; $j = new $i; echo $j->k;  
* 可变属性  class CLS{public $k = 'hello';} $i = 'k'; $j = new CLS; echo $j->$i;  
* 可变方法  class CLS{public function k(){echo 'hello';}} $i='k'; $j=new CLS; $j->$i();

### 可变变量 ###

用于业务逻辑判断得到某些具体信息  
	$var_name = "class_name";  
    $$var_name = "PHP0913";        // $class_name = "PHP0913";$class_name已存入内存中  
    var_dump($class_name);        // var_dump($$var_name);  

### 变量函数 ###

get_defined_vars    //返回由所有已定义变量所组成的数组(包括环境变量、服务器变量和用户定义的变量)  

### unset() ###

* unset()仅删除当前变量名和引用，其值并未被删除  
* 引用传递中，删除一个变量及其引用，其他变量及引用均存在，且值依然存在  
  
     echo "<br />";  
    $v3 = '值';  
    $v4 = &$v3;  
    unset($v4);  
    var_dump($v3, $v4);  

### 变量的最长有效期 ###

* 当前脚本的执行周期，脚本执行结束，变量即消失  

### 预定义变量/超全局变量 ###

* $GLOBALS  
* $_COOKIE  
* $_ENV  
* $_FILES  
* $_GET  
* $_POST  
* $_REQUEST  
* $_SERVER  
* $_SESSION
 
### 常量定义 ###

* define(常量名, 常量值, [区分大小写参数])        //true表示不区分/false表示区分大小写  
* const 常量名 = 常量值    // 新，建议  
* 常量名可以使用特殊字符  
* constant($name)        // 获取常量名  
*                    // 例：echo constant('-_-');  

### 常量相关函数 ###

* defined  
* get_defined_constants  

### 预定义常量 ##

* FILE__            所在文件的绝对路径  
* __LINE__            文件中的当前行号  
* __DIR__            文件所在目录  
* __FUNCTION__        函数名称  
* __CLASS__            类的名称  
* __METHOD__        类的方法名  
* __NAMESPACE__        当前命名空间的名称  

### 整型 ###

整型占用4字节，共4*8=32位，最大值为2147483647，最小值为-2147483648，最小值的绝对值比最大值的大1  
最高为表示正负，1表示负，0表示正  

### 进制转换函数 ###

只能十进制与其他进制进行转换，只有六种  
转换时，参数应是字符串（即不可含八进制的“0”或十六进制的“0x”）  
    dec  
     bin  
     oct  
    hex  
* hexdec()    十六进制转十进制        也可写hex2dec()  
* dechex()    十进制转十六进制        也可写dec2hex()  
* bindec()    二进制转十进制        也可写bin2dec()  
* decbin()    十进制转二进制        也可写dex2bin()  
* octdec()    八进制转十进制        也可写oct2dec()  
* decoct()    十进制转八进制        也可写dec2oct()  

### 浮点数  ###

浮点数不能比较大小 ！！！  
几乎所有小数，在保存时都是近似值而不是精确值！  
最大值：+/- 1.8E308  
PHP所能保存的最长小数位：14位  

### 单引号字符串 ###

单引号字符串中，只能转义反斜杠和单引号  

### 双引号字符串 ###

只解析字符串一次 ！！！  
eval     把字符串作为PHP代码执行  
大括号包裹变量，可确定变量名界限。如："aaa{$bbb}ccc"  
双引号中可以将ASCII码转换为字符  
"\x61" -> a    // 字符串中不需0，整型中才是0x前导  
"\x49\x54\x43\x41\x53\x54" -> ITCAST  
将ASCII转成字符函数chr()  
将字符转成ASCII函数ord()  
双引号转义列表  
* \n 换行  
* \r 回车  
* \t 水平制表符  
* \\ 反斜线  
* \$ 美元标记  
* \v 垂直制表符  
* \e Escape  
* \f 换页  
* \" 双引号"  
* \[0-7]{1,3} 符合该正则表达式序列的是一个以八进制方式来表达的字符    
* \x[0-9A-Fa-f]{1,2} 符合该正则表达式序列的是一个以十六进制方式来表达的字符    

### 定界符 ###  

herodoc - 功能同双引号，能解析  
$str = <<<AAA  
字符串内容  
AAA;  
  
nowdoc - 功能同单引号，不能解析  
只在开始位置有单引号  
$str = <<<'AAA'  
字符串内容  
AAA;  

### 字符串的使用 ###

可将字符串当作一个字符的集合来使用，可独立访问每个字符。仅适用于单字节字符（字母、数字、半角标点符号），像中文等不可用  
$str = "abcd";  
echo $str[3];   // d  
echo $str{0};   // a  

### 类型操作函数 ###

* 获取/设置类型  
gettype($var) //获取变量的数据类型  
settype($var, $type) //设置变量的数据类型  
  
* 类型判断  
is_int  
is_float  
is_null  
is_string  
is_resource  
is_array  
is_bool  
is_object         
is_numeric      检测变量是否为数字或数字字符串  
  
* 转换成指定的数据类型  
boolval  
floatval  
intval  
strval  
  
* 强制转换类型  
(int)  
(float)  
(string)  
(bool)  
(array)  
(object)  
(unset) //转换为NULL  
(binary) 转换和 b前缀转换  //转换成二进制  
  
var_dump        打印变量的相关信息。  
                显示关于一个或多个表达式的结构信息，包括表达式的类型与值。  
                数组将递归展开值，通过缩进显示其结构。  
var_export($var [,bool $return]) //输出或返回一个变量的字符串表示  
    $return：为true，则返回变量执行后的结果  
print_r         打印关于变量的易于理解的信息  
empty           检查一个变量是否为空  
isset           检测变量是否存在  
  
### 流程控制 ###
  
* if语句的替代语法  
if (条件判断) :  
   语句块;  
elseif (条件判断) :  
   语句块;  
else :  
   语句块;  
endif;  
  
* 流程控制的替代语法  
在嵌入HTML时常用  
将 { 换成 : , 将 } 换成 endif; 等  
endif  
endwhile  
endfor  
endforeach  
endswitch  

<center><strong>{{ page.date | date_to_string }}</strong></center>
