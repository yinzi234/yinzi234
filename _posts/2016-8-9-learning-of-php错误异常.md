---
layout: default
title: php之错误异常处理
---

## 错误 ## 

PHP程序的错误发生一般归属于下列三个领域。

* 语法错误
		语法错误最常见，并且最容易修复。例如，遗漏了一个分号，就会
		显示错误信息。这类错误会阻止脚本执行。通常发生在程序开发
		时，可以通过错误报告进行修复，再重新运行。

* 运行时错误
		这种错误一般不会阻止PHP脚本的运行，但是会阻止脚本做希望它
		所做的任何事情。例如，在调用header()函数前如果有字符输
		出，PHP通常会显示一条错误消息，虽然PHP脚本继续运行，但
		header()函数并没有执行成功。

* 逻辑错误
		这种错误实际上是最麻烦的，不但不会阻止PHP脚本的执行，也不
		会显示出错误消息。例如，在if语句中判断两个变量的值是否相
		等，如果错把比较运行符号“＝＝”写成赋值运行符号“＝”就是一
		种逻辑错误，很难会被发现。

一个异常则是在一个程序执行过程中出现的一个例外，或是一个事件，它中

断了正常指令的运行，跳转到其他程序模块继续执行。所以异常处理经常被

当做程序的控制流程使用。无论是错误还是异常，应用程序都必须能够以妥

善的方式处理，并做出相应的反应，希望不要丢失数据或者导致程序崩溃。

### 错误类型 ###

运行PHP脚本时，PHP解析器会尽其所能地报告它遇到的问题。在PHP中错误

报告的处理行为，都是通过PHP的配置文件php.ini中有关的配置指令确定

的。另外PHP的错误报告有很多种级别，可以根据不同的错误报告级别提供对

应的调试方法。一旦把PHP设置成呈现出发生了哪些错误，你可能想调整错误

报告的级别。在表10-1中列出了PHP中大多数的错误报告级别。

* PHP的错误报告级别

```
E_ERROR 致命的运行时错误（它会阻止脚本的执行）

E_WARNING 运行时警告（非致命的错误）

E_PARSE 从语法中解析错误

E_NOTICE 运行时注意消息（可能是或者可能不是一个问题）

E_CORE_ERROR 类似E_ERROR，但不包括PHP核心造成的错误

E_CORE_WARNING 类似E_WARNING，但不包括PHP核心错误警告

E_COMPILE_ERROR 致命的编译时错误

E_COMPILE_WARNING 致命的编译时警告

E_USER_ERROR 用户导致的错误消息

E_USER_WARNING 用户导致的警告

E_USER_NOTICE 用户导致的注意消息

E_ALL 所有的错误、警告和注意

E_STRICT关于PHP版本移植的兼容性和互操作性建议
```

如果用户希望在PHP脚本中，遇到上表中的某个级别的错误时，将错误消息

报告给用户。则必须在配置文件php.ini中，将display_errors指令的值

设置为On，开启PHP输出错误报告的功能。也可以在PHP脚本中调用ini_set

()函数，动态设置配置文件php.ini中的某个指令。如果display_errors

被启用，就会显示满足已设置的错误级别的所有错误。当用户在访问时，看

到显示的这些消息不仅会感到迷惑，而且还可能会过多地泄露有关服务器的

信息，使服务器变得很不安全。所以在项目开发或测试期间启用此指令，可

以根据不同的错误报告更好的调试程序。出于安全性和美感的目的，让公众

用户查看PHP的详细出错消息一般是不明智的，所以在网站投入使用时要将

其禁用。

### 基本的调试方法 ###

当你正在开发站点时，你将希望PHP报告特定类型的错误，可以通过调整错

误报告的级别实现，可以通过以下两种方法设置错误报告级别。

1. 可以通过在配置文件php.ini中，修改配置指令error_reporting的值，修改成功后重新启动Web服务器，则每个PHP脚本都可以按调整后的错误级别输出错误报告。下面是修改php.ini配置文件的示例，列出几种为error_reporting指令设置不同级别值的方式，可以把位运算符［&（与）、|（或）、~（非）］和错误级别常量一起使用。
		; 可以抛出任何非注意的错误，默认值
		error_reporting = E_ALL & ~E_NOTICE
	
		; 只考虑致命的运行时错误、解析错误和核心错误
	
		; error_reporting = E_ERROR | E_PARSE | E_CORE_ERROR
	
		; 报告除用户导致的错误之外的所有错误
	
		; error_reporting = E_ALL & ~(E_USER_ERROR | 
	
		E_USER_WARNING | E_USER_NOTICE)

2. 或者可以在PHP脚本中使用error_reporting()函数，基于各个脚本来
调整这种行为。这个函数用于确定PHP应该在特定的页面内报告哪些类型的错误。该函数获取一个数字或上表中错误级别常量作为参数。
		error_reporting(0);                                 //设置为0会完全关闭错误报告

		error_reporting (E_ALL);                          //将会向PHP报告发生的每个错误

		error_reporting (E_ALL & ~E_NOTICE);           //可以抛出任何非注意的错误报告

我们在PHP脚本中分别创建出一个“注意”、一个“警告”和一个致命“错误”。并

通过设置不同的错误级别，限制程序输出没有被允许的错误报告。

* 创建一个名为error.php的脚本文件

```
<html>

         <head><title>测试错误报告</title></head>

         <body>

                   <h2>测试错误报告</h2>

                   <?php

                            /*开启php.ini中的display_errors指令，只有该指令开启如果有错误报告才能输出*/

                            ini_set('display_errors',1); 

                            /*通过error_reporting()函数设置在本脚本中，输出所有级别的错误报告*/

                            error_reporting(E_ALL);

                            /*“注意(notice)”的报告，不会阻止脚本的执行，并且可能不一定是一个问题 */

                            getType($var);             //调用函数时提供的参数变量没有在之前声明

                            /*“警告(warning)”的报告，指示一个问题，但是不会阻止脚本的执行 */

                            getType();                 //调用函数时没有提供必要的参数

                            /*“错误(error)”的报告，它会终止程序，脚本不会再向下执行 */

                            get_Type();                //调用一个没有被定义的函数

                   ?>

         </body>

</html>
```

为了确保配置文件中的display_errors指令开启，通过ini_set()函数强

制在该脚本执行中启动，并通过error_repoting()函数设置错误级别为

E_ALL，报告所有错误、警告和注意。并在脚本中分别创建出注意、警告和错

误，PHP脚本只有在遇到错误时才会终止运行

* “注意”和“警告”的错误报告并不会终止程序运行。如果在上面的输出结果中，不希望有注意和警告的报告输出，就可以在脚本error.php中修改error_repoting()函数

```
error_reporting(E_ALL&~(E_WARNING | E_NOTICE));        //报告除注意和警告之外的所有错误
```

脚本error.php被修改以后并重新运行，在输出的结果中就只剩下一条错误

报告了


### 配置指令 ###

除了使用error_reporting和display_error两个配置指令可以修改错误

报告行为以外，还有许多配置指令可以确定PHP的错误报告行为。

	display_startup_errors是否显示PHP引擎在初始化时遇到的所有错误Off

	log_errors确定日志语句记录的位置Off

	error_log设置错误可以发送到syslog中Null

	log_errors_max_len每个日志项的最大长度，以字节为单位，设置0表示指定最大长度1024

	ignore_repeated_errors是否忽略同一文件、同一行发生的重复错误消息Off

	ignore_repeated_source忽略不同文件中或同一文件中不同行上发生的重复错误Off

	track_errors启动该指令会使PHP在$php_errormsg中存储最近发生的错误信息Off



## 错误日志 ##

如果需要将程序中的错误报告写入错误日志中，只要在PHP的配置文件中，

将配置指令log_errors开启即可。错误报告默认就会记录到Web服务器的日

志文件里，例如记录到Apache服务器的错误日志文件error.log中。当然也

可以记录错误日志到指定的文件中或发送给系统syslog

### 使用指定的文件记录错误报告日志 ###

如果使用自己指定的文件记录错误日志，一定要确保将这个文件存放在文档根目录之外，以减少遭到攻击的可能。并且该文件一定要让PHP脚本的执行

用户（Web服务器进程所有者）具有写权限。假设在Linux操作系统中，将/usr/local/目录下的error.log文件作为错误日志文件，并设置Web服务

器进程用户具有写的权限。然后在PHP的配置文件中，将error_log指令的值设置为这个错误日志文件的绝对路径。需要将php.ini中的配置指令做如

下修改：

```
error_reporting  =  E_ALL                        ;将会向PHP报告发生的每个错误

display_errors = Off                            ;不显示满足上条指令所定义规则的所有错误报告

log_errors = On                                ;决定日志语句记录的位置

log_errors_max_len = 1024                        ;设置每个日志项的最大长度

error_log = /usr/local/error.log                      ;指定产生的错误报告写入的日志文件位置
```

PHP的配置文件按上面的方式设置完成以后，并重新启动Web服务器。这样，

在执行PHP的任何脚本文件时，所产生的所有错误报告都不会在浏览器中显

示，而会记录在自己指定的错误日志/usr/local/error.log中。此外，不

仅可以记录满足error_reporting所定义规则的所有错误，而且还可以使

用PHP中的error_log()函数，送出一个用户自定义的错误信息。该函数的

原型如下所示：

```
bool error_log ( string message [, int message_type [, string destination [, string extra_headers]]] )
```

此函数会送出错误信息到Web服务器的错误日志文件、某个TCP服务器或到指

定文件中。该函数执行成功则返回TRUE，失败则返回FALSE。第一个参数

message 是必选项，即为要送出的错误信息。如果仅使用这一个参数，会按

配置文件php.ini中所设置的位置处发送消息。第二个参数message_type为

整数值：0表示送到操作系统的日志中；1则使用PHP的Mail()函数，发送信

息到某E-mail处，第四个参数extra_headers亦会用到；2则将错误信息送

到TCP 服务器中，此时第三个参数destination表示目的地IP及Port；3

则将信息存到文件destination中。如果以登入Oracle数据库出现问题的处

理为例，该函数的使用如下所示：

```
<?php  

         if(!Ora_Logon($username, $password)){  

                   error_log("Oracle数据库不可用!", 0);               //将错误消息写入到操作系统日志中

         }

         if(!($foo=allocate_new_foo()){

                   error_log("出现大麻烦了!", 1, "webmaster@www.mydomain.com");   //发送到管理员邮箱中

         }

         error_log("搞砸了!",   2,   "localhost:5000");            //发送到本机对应5000端口的服务器中

         error_log("搞砸了!",   3,   "/usr/local/errors.log");        //发送到指定的文件中

?> 
```

### 错误信息记录到操作系统的日志里 ###

错误报告也可以被记录到操作系统日志里，但不同的操作系统之间的日志管理有点区别。在Linux上错误语句将送往syslog，而在Windows上错误将发

送到事件日志里。如果你不熟悉syslog，起码要知道它是基于UNIX的日志工具，它提供了一个API来记录与系统和应用程序执行有关的消息。Windows

事件日志实际上与UNIX的syslog相同，这些日志通常可以通过事件查看器来查看。如果希望将错误报告写到操作系统的日志里，可以在配置文件中将

error_log指令的值设置为syslog。具体需要在php.ini中修改的配置指令如下所示：

```

error_reporting  =  E_ALL                      ;将会向PHP报告发生的每个错误

display_errors = Off                                   ;不显示满足上条指令所定义规则的所有错误报告

log_errors = On                               ;决定日志语句记录的位置

log_errors_max_len = 1024                      ;设置每个日志项的最大长度

error_log = syslog                             ;指定产生的错误报告写入操作系统的日志里
```

除了一般的错误输出之外，PHP还允许向系统syslog中发送定制的消息。虽然通过前面介绍的error_log()函数，也可以向syslog中发送定制的消

息，但在PHP中为这个特性提供了需要一起使用的4个专用函数。分别介绍如下：

1.  define_syslog_variables()

	在使用openlog()、syslog及closelog()三个函数之前必须先调用该函数。因为在调用该函数时，它会根据现在的系统环境为下面三个函数初使用化一些必需的常量。

2.  openlog()

	打开一个和当前系统中日志器的连接，为向系统插入日志消息做好准备。并将提供的第一个字符串参数插入到每个日志消息中，该函数还需要指定两个将在日志上下文使用的参数，可以参考官方文档使用。

3.  syslog()

	该函数向系统日志中发送一个定制消息。需要两个必选参数，第一个参数通过指定一个常量定制消息的优先级。例如LOG_WARNING表示一般的警告，LOG_EMERG表示严重地可以预示着系统崩溃的问题，一些其他的表示严重程度的常量可以参考官方文档使用。第二个参数则是向系统日志中发送的定制消息，需要提供一个消息字符串，也可以是PHP引擎在运行时提供的错误字符串。

4.  closelog()

	该函数在向系统日志中发送完成定制消息以后调用，关闭由openlog()函数打开的日志连接。

如果在配置文件中，已经开启向syslog发送定制消息的指令，就可以使用前面介绍的四个函数发送一个警告消息到系统日志中，并通过系统中的

syslog解析工具，查看和分析由PHP程序发送的定制消息，如下所示：

```
<?php

         define_syslog_variables();

         openlog("PHP5", LOG_PID , LOG_USER);

         syslog(LOG_WARNING, "警告报告向syslog中发送的演示，警告时间：".date("Y/m/d H:i:s"));

         closelog();

?>
```

以Windows系统为例，通过右击“我的电脑”选择管理选项，然后到系统工具菜单中，选择事件查看器，再找到应用程序选项，就可以看到我们自己定

制的警告消息了。上面这段代码将在系统的syslog文件中，生成类似下面的一条信息，是事件的一部分：

```
PHP5[3084], 警告报告向syslog中发送的演示，警告时间：2009/03/26 04:09:11.
```

使用指定的文件还是使用syslog记录错误日志，取决于你所在的Web服务器环境。如果你可以控制Web服务器，使用syslog是最理想的，因为你能利用

syslog的解析工具来查看和分析日志。但如果你的网站在共享服务器的虚拟主机中运行，就只有使用单独的文本文件记录错误日志了。

## 异常处理 ##

异常（Exception）处理用于在指定的错误发生时改变脚本的正常流程，是PHP 5中的一个新的重要特性。异常处理是一种可扩展、易维护的错误处理

统一机制，并提供了一种新的面向对象的错误处理方式。在Java、C#及Python等

语言中很早就提供了这种异常处理机制，如果你对哪一种语言中的异常处理熟悉，那对PHP中提供的异常处理机制也不会陌生。

### 异常处理实现 ###

异常处理和编写程序的流程控制相似，所以也可以通过异常处理实现一种另类的条件选择结构。异常就是在程序运行过程中出现的一些意料之外的事

件，如果不对此事件进行处理，则程序在执行时遇到异常将崩溃。处理异常需要在PHP脚本中使用以下语句：

```
try {                     //所有需要进行异常处理的代码都必须放入这个代码块内

   … …                  //在这里可以使用throw语句抛出一个异常对象

}catch(ex1) {               //使用该代码块捕获一个异常，并进行处理

   … …                 //处理发生的异常，也可再次抛出异常

}
```

在PHP代码中所产生的异常可以被throw语句抛出并被catch语句捕获。需要进行异常处理的代码都必须放入try代码块内，以便捕获可能存在的异常。

每一个try至少要有一个与之对应的catch，也不能出现单独的catch，另外try和cache之间也不能有任何的代码出现。一个异常处理的简单实例如下

所示：

```
<?php

         try {

                   $error = 'Always throw this error';

                   throw new Exception($error);      //创建一个异常对象，通过throw语句抛出

                   echo 'Never executed';            //从这里开始，try代码块内的代码将不会再被执行

         } catch (Exception $e) {

                   echo 'Caught exception: ',  $e->getMessage(), "\n";  //输出捕获的异常消息

         }

         echo 'Hello World';                    //程序没有崩溃继续向下执行

?>
```

在上面的代码中，如果try代码块中出现某些错误，我们就可以执行一个抛出异常的操作。在某些编程语言中，例如Java，在出现异常时将自动抛出异

常。而在PHP中，异常必须手动抛出。throw关键字将触发异常处理机制，它是一个语言结构，而不是一个函数，但必须给它传递一个对象作为值。在最

简单的情况下，可以实例化一个内置的Exception类，就像以上代码所示那样。如果在try语句中有异常对象被抛出，该代码块不会再继续向下执行，

而直接跳转到catch中执行。并传递给catch代码块一个对象，也可以理解为被catch代码块捕获的对象，其实就是导致异常被throw语句抛出的对象。

在catch代码块中可以简单的输出一些异常的原因，也可以是try代码块中任务的另一个版本解决方案，此外，也可以在这个catch代码块中产生新的

异常。最重要的是，在异常处理之后，程序不会崩溃，而会继续执行。

### 扩展PHP内置的异常处理类 ###

在try代码块中，需要使用throw语句抛出一个异常对象，才能跳转到catch代码块中执行，并在catch代码块中捕获并使用这个异常类的对象。虽然在

PHP中提供的内置异常处理类Exception，已经具有非常不错的特性，但在某些情况下，可能还要扩展这个类来得到更多的功能。所以用户可以用自定

义的异常处理类来扩展PHP内置的异常处理类。以下的代码说明了在内置的异常处理类中，哪些属性和方法在子类中是可访问和可继承的：

```
<?php

         class Exception {

           protected $message = 'Unknown exception';              //异常信息

           protected $code = 0;                              //用户自定义异常代码

           protected $file;                                   //发生异常的文件名

           protected $line;                                  //发生异常的代码行号

 

           function __construct($message = null, $code = 0){}    //构造方法

 

           final function getMessage(){}                        //返回异常信息

           final function getCode(){}                           //返回异常代码

           final function getFile(){}                            //返回发生异常的文件名

       final function getLine(){}                            //返回发生异常的代码行号

         final function getTrace(){}                           //backtrace() 数组

          final function getTraceAsString(){}                    //已格成化成字符串的 getTrace() 信息

 

           /* 可重载的方法 */

           function __toString(){}                             //可输出的字符串

         }

?>
``` 

上面这段代码只为说明内置异常处理类Exception的结构，它并不是一段有实际意义的可用代码。如果使用自定义的类作为异常处理类，则必须是扩展

内置异常处理类Exception的子类，非Exception类的子类是不能作为异常处理类使用的。如果在扩展内置处理类Exception时重新定义构造函数的

话，建议同时调用parent::construct()来检查所有的变量是否已被赋值。当对象要输出字符串的时候，可以重载__toString()并自定义输出的样

式。可以在自定义的子类中，直接使用内置异常处理Exception类中的所有成员属性，但不能重新改写从该父类中继承过来的成员方法，因为该类的大

多数公有方法都是final的。

创建自定义的异常处理程序非常简单，和传统类的声明方式相同，但该类必须是内置异常处理类Exception的一个扩展。当PHP中发生异常时，可调用

自定义异常类中的方法进行处理。创建一个自定义的MyException类，继承了内置异常处理类Exception中的所有属性，并向其添加了自定义的方法。

代码及应用如下所示：

```
<?php

         /* 自定义的一个异常处理类，但必须是扩展内异常处理类的子类 */

         class MyException extends Exception{

                   //重定义构造器使第一个参数 message 变为必须被指定的属性

                   public function __construct($message, $code=0){

                            //可以在这里定义一些自己的代码

                            //建议同时调用 parent::construct()来检查所有的变量是否已被赋值

                            parent::__construct($message, $code);

                   }

                  

                   public function __toString() {             //重写父类方法，自定义字符串输出的样式

                            return __CLASS__.":[".$this->code."]:".$this->message."<br>";

                   }

                  

                   public function customFunction() {       //为这个异常自定义一个处理方法

                            echo "按自定义的方法处理出现的这个类型的异常<br>";

                   }

         }

        

         try {                                    //使用自定义的异常类捕获一个异常，并处理异常

                   $error = '允许抛出这个错误';      

                   throw new MyException($error);         //创建一个自定义的异常类对象，通过throw语句抛出

                   echo 'Never executed';                 //从这里开始，try代码块内的代码将不会再被执行

         } catch (MyException $e) {                 //捕获自定义的异常对象

                   echo '捕获异常: '.$e;                  //输出捕获的异常消息

                   $e->customFunction();                //通过自定义的异常对象中的方法处理异常

         }

         echo '你好呀';                             //程序没有崩溃继续向下执行

?>
```

在自定义的MyException类中，使用父类中的构造方法检查所有的变量是否已被赋值。而且重载了父类中的__toString()方法，输出自己定制捕获的

异常消息。自定义和内置的异常处理类，在使用上没有多大区别，只不过在自定义的异常处理类中，可以调用为具体的异常专门编写的处理方法。

### 捕获多个异常 ###

在try代码块之后，必须至少给出一个catch代码块，也可以将多个catch代码块与一个try代码块进行关联。如果每个catch代码块可以捕获一个不同

类型的异常，那么使用多个catch就可以捕获不同的类所产生的异常。当产生一个异常时，PHP将查询一个匹配的catch代码块。如果有多个catch代码

块，传递给每一个catch代码块的对象必须具有不同的类型，这样PHP可以找到需要进入哪一个catch代码块。当try代码块不再抛出异常或者找不到

catch能匹配所抛出的异常时，PHP代码就会在跳转到最后一个 catch 的后面继续执行。多个异常的捕获的示例如下：

```
<?php

         /* 自定义的一个异常处理类，但必须是扩展内异常处理类的子类 */

         class MyException extends Exception{

                   //重定义构造器使第一个参数 message 变为必须被指定的属性

                   public function __construct($message, $code=0){

                            //可以在这里定义一些自己的代码

                            //建议同时调用 parent::construct()来检查所有的变量是否已被赋值

                            parent::__construct($message, $code);

                   }

                   //重写父类中继承过来的方法，自定义字符串输出的样式

                   public function __toString() {

                            return __CLASS__.":[".$this->code."]:".$this->message."<br>";

                   }

 

                   //为这个异常自定义一个处理方法

                   public function customFunction() {

                            echo "按自定义的方法处理出现的这个类型的异常";

                   }

         }

        

         /* 创建一个用于测试自定义扩展的异常类MyException */

         class TestException {

                   public $var;                          //一个成员属性，用来判断对象是否创建成功被初始化

 

                   function __construct($value=0) {        //通过构造方法的传值决定抛出的异常

                            switch($value){                 //对传入的值进行选择性的判断

                                     case 1:                    //如果传入的参数值为1，则抛出自定义的异常对象

                                               throw new MyException("传入的值“1” 是一个无效的参数", 5);

                                               break;

                                     case 2:                      //如果传入的参数值为2，则抛出PHP内置的异常对象

                                               throw new Exception("传入的值“2”不允许作为一个参数", 6);

                                               break;

                                     default:                    //如果传入的参数值合法，则不抛出异常创建对象成功

                                               $this->var=$value;      //为对象中的成员属性赋值

                                               break;

                            }

                   }

         }

     //示例1，在没有异常时，程序正常执行，try中的代码全部执行并不会执行任何catch区块

         try{

                   $testObj=new TestException();              //使用默认参数创建异常的测试类对象

                   echo "***********<br>";                 //没有抛出异常这条语句就会正常执行

         }catch(MyException $e){                      //捕获用户自定义的异常区块

                   echo "捕获自定义的异常：$e <br>";        //按自定义的方式输出异常消息

                   $e->customFunction();                     //可以调用自定义的异常处理方法

         }catch(Exception $e) {                         //捕获PHP内置的异常处理类的对象

                   echo "捕获默认的异常：".$e->getMessage()."<br>";   //输出异常消息

         }     

         var_dump($testObj);          //判断对象是否创建成功，如果没有任何异常，则创建成功

 

    //示例2，抛出自定义的异常，并通过自定义的异常处理类捕获这个异常并处理

         try{

                   $testObj1=new TestException(1);           //传入参数1时，创建测试类对象抛出自定义异常

                   echo "
```


<center><strong>{{ page.date | date_to_string }}</strong></center>
