---
layout: default
title: php入门学习(2)
---

### switch ###

```
switch (条件) {  
   case 状态值1:  
       语句块;  
       [break;]  
   case 状态值2:  
       语句块;  
       [break;]  
   case 状态值3:  
   case 状态值4:  
       语句块;  
       [break;]  
   default:  
       语句块;  
       [break;]  
}  
```

switch是状态分支，特殊的循环  
先计算出状态值，再去与判断数作比较  
break退出流程  

### for循环 ###

for (条件初始化表达式; 条件判断表达式; 条件变化表达式) {  
循环体  
}  
  
假设循环体被执行了N次，则  
条件初始化表达式被执行1次  
条件判断表达式被执行N+1次  
条件变化表达式被执行N次  
  
注意：  
    1. 循环变量在for语句结束后还可以继续使用，值为第一次失败的值  
    2. 循环变量在for循环体内可以使用  
    3. 任何条件表达式均可省略，但分号不能省略  
        a. 条件初始化表达式被省略时，循环变量被赋值为null，在与条件判断时，  
            进行类型转换后再比较。也可以在for语句外进行初始化。  
        b. 条件判断表达式被省略时，表示循环为真，进入死循环  
        c. 条件变化表达式被省略时，可以在循环体内完成  
    4. 每个表达式均可由多条语句组成，每条语句之间使用逗号分割  
        如果条件判断表达式由多条语句组成，都会执行，但只有最后一条语句才作为判断条件  
    5. for只能遍历数值型索引下标数组  
        数组长度函数：count()  
    6. 应该将可以初始化的语句均放在条件初始化表达式内，这样可以省去很多执行次数  

### goto ###

用来跳转到程序中的某一指定位置  
该目标位置可以用目标名称 加上冒号来标记。  
PHP中的goto有一定限制，只能在同一个文件和作用域中跳转，  
    * 也就是说你无法跳出一个函数或类方法，也无法跳入到另一个函数。  
    * 你也无法跳入到任何循环或者switch结构中。  
    * 常见的用法是用来跳出循环或者switch，可以代替多层的break。   
可以从循环(switch)中跳出来，但不能从外部跳转进去。而函数或类方法，向外向内均不可。  
goto a;  
echo 'Foo';  
a:  
echo 'Bar';    

### 文件加载 ###

require / include / require_once / include_once  
文件载入只是载入目标文件内的代码并执行，与载入的文件类型无关  
  
文件载入属于执行阶段，当执行到require等语句时，才载入该文件的代码，  
    * 编译并执行，然后回到require等语句位置继续执行下面的语句  
【注意】  
    * 在载入开始时，先退出PHP模式；  
    * 再载入目标文件代码，执行该代码；  
    * 结束时，再进入PHP模式。  
require：处理失败，产生 E_COMPILE_ERROR 错误，脚本中止。  
include：处理失败，产生 E_WARNING 错误，脚本继续执行。  
  
* 不建议使用require_once/include_once  
  

#### 相对路径 ####  

当前浏览器请求的哪个脚本，当前位置就是属于哪个脚本。  
./file 和 file 都表示当前目录下的file文件  
file情况（嵌套载入文件时）：  
* 如果当前目录没找到该文件就在代码文件所在目录中继续找。  
* 如果当前目录找到有该文件，则不会再在代码文件所在目录去找也不会再加载。  
* __DIR__     脚本文件所在目录  
* __FILE__    脚本文件路径  
  
include_path    加载文件查找目录 
    * set_include_path()  设置include_path，可多个，用字符串作参数  
    * 该函数设置的path只针对该当前文件有效  
    * 该设置只针对查找未直接写文件路径方式有效  
    * 设置新的include_path会覆盖原来的  
  
    * get_include_path()  获取当前include_path设置项，无参数  
  
    * 路径分隔符，在Windows下是分号，在Linux下是冒号  
    * 利用预定义常量 PATH_SEPARATOR 来获得当前的分隔符  
  
如果直接写文件名：  
    1. include_path所设置的  
    2. 当前目录  
    3. 代码所在文件的目录  
如果文件名前带有路径，则会直接根据路径查找，include_path直接被忽略  

### return ###

* return与require结合，可返回文件的内容，return写在被载入的文件内  
* return可以终止所在脚本的执行，作为普通脚本语句  
* return可以返回函数的相应值  

### 终止和延迟脚本执行 ###

* die / exit   终止  
* return是终止所在脚本的执行  
* die和exit会立即终止脚本执行  
* die("到此为止");     该函数内的字符串可被输出  
* sleep()  延迟(单位：秒)
    *  默认最多可延迟30秒，PHP配置可以修改 max_execution_time  
     例：sleep(12);  
* usleep()    以指定的微秒数延迟执行  
* time_sleep_until    使脚本睡眠到指定的时间为止

### 函数 ###

用于业务逻辑判断得到某些具体信息  
	$var_name = "class_name";  
    $$var_name = "PHP0913";        // $class_name = "PHP0913";$class_name已存入内存中  
    var_dump($class_name);        // var_dump($$var_name);  

### 变量函数 ###

1. 函数的声明是在编译时，故先定义再调用，定义与调用无先后关系！  
2. 文件只是代码的载体，程序均在内存中执行！  
3. 如果函数的定义在需要载入的文件内，则需要先载入该文件，否则调用出错！  
4. 函数的定义可以出现在其他的代码段中，此时函数不会在编译阶段被执行  
    只有被执行到时才会被定义！只有独立定义时才会被编译在内存中！  
    如果出现在其他函数体内，也需要外层函数被调用时才被定义并生效！  
5. 函数名不区分大小写  
6. 不允许重名，包括系统函数  
7. 【可变函数】  
    	函数名可以用其他变量代替  
    	$func_name = "sayHello";  
    	$func_name();       //此时调用sayHello()函数  
    	注意：只有在调用时才能使用变量，定义时不允许！  
8. 变量可作为函数名调用函数，数组元素值也可以！  
9. 形式参数parameter，实际参数argument  
    	可以对参数传递 null，表示该形参不想传递值  
    	形参与实参之间既可值传递，也可引用传递。  
    	引用传递参数，应该在定义函数时就在形式参数前加上 & 符号，而此时调用函数实参必须为变量  
    	如何选择使用哪种传递方式？  
        a. 是否需要保证原始数据的完整性  
        b. 是否需要增加效率  
        c. 对大数据引用传递可节省内存  
10. 参数默认值  
        a. 函数的参数默认值必须是已经确定的值，不能是变量！  
            只要在调用之前定义该常量，则可以使用常量作为参数默认值  
        b. 函数默认值可以有多个，建议将有默认值的参数放在参数列表的最后面  
           这样可以在调用函数时，不赋予后面有默认值的参数值，否则会出错  
        c. 默认参数可以是非标量类型，比如数组、null  
        d. 任何默认参数必须放在任何非默认参数的右侧  
11. 参数数量  
    a. 形参数量多于实参数量  
        报告警告级别错误，并以NULL代替  
    b. 实参多于形参  
        不报告错误，依次为形参赋值  
    c. 不确定参数数量  
        1) 一个形参都不定义，永远都是实参多于形参  
        2) 【可变数量参数】  
            func_get_args() 获取当前函数被调用时所有实参的值，返回一个所有实参值组成的数组  
            func_get_arg()  获取某个实参的值，通过索引值标识，e.g: func_get_arg(0)  
            func_num_args() 获取所有实参的数量  
12. 【return】返回值  
    a. 函数只有一个返回值，可以通过返回一个数组来得到类似的结果，但可以有多条return语句  
    b. return语句会立即中止函数的运行，并将控制权交回调用该函数的代码行  
    c. 可以返回包括数组和对象的任意类型  
    d. 函数的返回也分值传递和引用传递（返回的是一个变量才可）  
        1) 默认是值传递方式  
        2) 引用传递方式：  
            - 定义函数时，函数名前加上& 表示该函数可以返回引用  
            - 调用函数时，函数名前加上& 表示取得函数返回的引用  
                此时，函数外修改返回值，会修改函数内的该返回变量的值  
            - 如果函数需返回引用，则需要返回一个变量才可以  
            - 从函数返回一个引用，必须在函数声明和指派返回值给一个变量时都使用引用操作符&  
                function &returns_reference(){return $someref;}  
                $newref =& returns_reference();  
        3) 返回引用的作用  

### 变量作用域 ###

a. 全局变量和局部变量  
    	1. 作用域之间不重叠，即不同作用域的变量，之间不可访问 
    	2. 全局作用域  - 函数之外的区域  
    	3. 局部作用域  - 函数内的区域，每个函数都是一个独立的作用域  
  
b. 超全局变量，既可以在全局也可在局部使用，仅能用系统自带的，均是数组变量。  
   		 * $GLOBALS    $_COOKIE    $_ENV       $_FILES $_GET  
   		 $_POST      $_REQUEST   $_SERVER    $_SESSION  
c. $GLOBALS  
    1. 不能存在超全局变量，但可以有超全局的数据！  
    2. 将需要的数据放到超全局变量的数组内，但统一使用$GLOBALS  
    3. $GLOBALS 特征  
        - 每个全局变量就是对应$GLOBALS内的一个元素！  
            每当增加一个全局，则自动在$GLOBALS内增加一个同名元素！  
            同理，每当增加元素，也会增加一个全局变量，一般在函数内增加  
        - 做的任何修改，也会映射到另一个，包括更新和删除  
            在函数内访问全局变量，只需使用$GLOBALS  
        - 出现过的全局变量，就可以通过$GLOBALS这个数组取得  
    4. PHP生命周期中，定义在函数体外部的所谓全局变量，函数内部是不能直接获得的  
4) global关键字（不建议使用）  
    1. 将局部变量声明为同名全局变量的一个'引用'！相当于常量的引用传递  
        global $var;    // $var = &$GLOBALS['var'];  
        不同于$GLOBALS！！！  
    global在函数产生一个指向函数外部变量的别名变量，而不是真正的函数外部变量。  
    $GLOBALS确确实实调用是外部的变量，函数内外会始终保持一致。  
    global的作用是定义全局变量，但是这个全局变量不是应用于整个网站，而是应用于当前页面，包括include或require的所有文件。  
d.   
    1. 作用域只针对变量，对常量无效  
    2. 被载入文件中定义的变量作用域取决于被载入的位置。  
        函数外被载入就是全局，函数内被载入就是局部！  

### 变量生命周期 ###

1. 脚本结束时，全局变量消失  
2. 函数执行完时，局部变量消失  
3. 静态变量  
    static关键字  
        静态变量仅在局部函数域中存在，但当程序执行离开此作用域时，其值并不丢失。  
        静态变量仅会被初始化一次，其他局部变量每次被调用时都会被重新赋值。  
        static声明的静态变量的生命周期会被一直延续。   

### 迭代和递归 ###

迭代比递归效率高！  
迭代是一种思想（算法），结构和使用上如同循环！  
递归是一种思想（算法），将大问题拆分成小问题，逐一解决小问题以解决大问题  
    * 要求大问题和小问题的解决方案是一致的！  
    递归的结构和语法体现如图函数。函数体内调用函数本身！  
    递归出口：当该问题可以解决时，则不用再递归  
 
### 匿名函数/闭包函数 ###

匿名函数，也叫闭包函数(closures)，允许临时创建一个没有指定名称的函数。  
  
1. 定义匿名函数时，不需增加函数名。  
2. PHP对匿名函数的管理，以一个对象的方式进行处理。  
3. 匿名函数应该存放到变量内。  
4. 匿名函数通过Closure类来实现  
5. 可以使用函数作为函数的参数和返回值  
6. 声明函数时可以使用 use($param) 来向函数中传入函数外的变量，结合变量引用来实现闭包  
7. 可以用变量引用函数  
$func = function ($e) {  
    echo $e;  
};   //结束时，需分号结束，如同变量赋值  
var_dump($func);     //使用匿名函数  
$func('ITCAST');     //函数的调用  
    这不是可变函数，而是对象。Closure闭包类  
* use语法  
匿名函数倾向于值的概念，可能出现在任何地方。  
use可以使得匿名函数使用其外部作用域的变量。非全局！  
use与全局的区别：  
    use使用其外部作用域的变量  

```
function out() {  
    $v = "in out";  
    $func = function () use (& $v) {  
        var_dump($v);  
    }  
}  
```

    use类似参数的自动传递，也支持值与引用的传递方式。  
* 作用  
    常作为'临时函数'被调用（只在某个地方被调用的函数）  
    例如：  
        PHP存在一个array_map()函数，功能是针对一个函数内每个元素，去调用某个函数  
        操作结果(array) = array_map(操作函数, 操作数组);  
        $result_arr = array_map(function ($v) {return $v3}, $arr);  
  
* 闭包用法实例  

```
function closureCreater() {  
    $x = 1;  
    return function($fun = null) use(&$x) {//按引用传值  
        echo "<br />" . $x++;  
        $fun and $fun();  
    };  
}  
  
$x = "hello world";  
$test = closureCreater();  
$test();  
$test(function(){ echo "closure test one"; });  
$test(function(){ echo "closure test two"; });  
$test(function() use($x){ echo "<br />".$x;});  
```
  
* 将函数保存为数组元素  

```
$x = 'outer param.';  
$arr = array();  
$arr[] = function($str)use($x){ return $str.$x; };  
echo $arr[0]('test fun in arr,');  
```

### 数组 ###

* 关联数组：键和值有关联，键表示值的逻辑含义。  
* 索引数组：键和值无关联，键表示值的位置。通常下标从0开始，递增元素  
count($var [,$mode]) //统计数组元素个数  
    	$mode可选，设为1或true时则递归统计  
    	$var非数组，返回1；$var未初始化或等于null或空数组，返回0 
* 键名的使用  
整型数字键不需加引号($arr[1])  
字符串数字键也不需加引号($arr = array('1'=>'abc'); $arr[1])  
关联数组，字符串键需加引号($arr = array('a'=>'aaa'); $arr['a'])  
关联数组，双引号中解析变量，可不加引号($arr = array('a'=>'aaa'); "$arr[a]")   

### 指针 ###

* current/pos    返回当前被内部指针指向的数组单元的值，并不移动指针。  
* key            返回数组中当前单元的键名，并不移动指针  
*         将数组中的内部指针向前移动一位，并返回移动后当前单元的值。先移动，再取值。  
* prev        将数组的内部指针倒回一位，并返回移动后当前单元的值先移动，再取值。  
* end            将数组的内部指针指向最后一个单元，并返回最后一个单元的值  
* reset        将数组的内部指针指向第一个单元，并返回第一个数组单元的值  
  
* each    返回数组中当前的键/值对并将数组指针向前移动一步。  
            返回的是一个由键和值组成的长度为4的数组，下标0和key表示键，下标1和value表示值  
            在执行each()之后，数组指针将停留在数组中的下一个单元  
            或者当碰到数组结尾时停留在最后一个单元。  
            如果要再用 each 遍历数组，必须使用 reset()。  
  
    1. 以上指针操作函数，除了key()，若指针移出数组，则返回false。而key()移出则返回null。  
    2. 若指针非法，不能进行next/prev操作，能进行reset/end操作  
    3. current/next/prev     若遇到包含空单元（0或""）也会返回false。而each不会！  
  
* list    把数组中的值赋给一些变量。list()是语言结构，不是函数  
            仅能用于数字索引的数组并假定数字索引从0开始  
            /* 可用于交换多个变量的值 */ list($a, $b) = array($b, $a);  
    		例：list($drink, , $power) = array('coffee', 'brown', 'caffeine');  
  
1. 复制数组，其指针位置也会被复制。  
    特例：如果数组指针非法，则拷贝的数组指针会重置，而原数组的指针不变。  
    【指针问题】  
        谁第一个进行写操作，就会开辟一个新的值空间。与变量(数组变量)值传递给谁无关。  
        数组函数current()被定义为写操作，故会出现问题。  
        foreach遍历的是数组的拷贝，当被写时，才会开辟一个新的值空间。  
        即，foreach循环体对原数组进行写操作时，才会出现指针问题。  
        如果开辟新空间时指针非法，则会初始化指针。  
2. 如果指针位置出现问题，则reset()初始化一下就可解决。  

### 遍历数组 ###

* 先找到元素，再获取键和值  
  
foreach  
    foreach (array_expression as [$key =>] & $value)  
      当foreach开始执行时，数组内部的指针会自动指向第一个单元。  
      获取元素信息后，移动指针，再执行循环体  
      1. foreach本身循环结构，break和continue适用于foreach  
      2. foreach支持循环的替代语法。  
      3. $value是保存元素值的变量，对其修改不会改变数组的元素值  
      4. $value支持元素值的引用拷贝，在$value前加上&即可  
      5. $key不支持引用传递  
      6. foreach遍历的是原数组的拷贝，而在循环体对数组的操作是操作原数组  
            即循环体对数组的操作，对原数组生效，对遍历不生效。  
            先拷贝一份数组用作遍历
  
```
while...list...each  
while (list($key, $val) = mysql_fetch_row($result)) = each($arr) {  
  echo "$key => $val\n";  
}  
```

### 数组函数 ###

* 统计计算  
		count        计算数组中的单元数目或对象中的属性个数  
		array_count_values  统计数组中所有的值出现的次数  
		array_product       计算数组中所有值的乘积  
		array_sum           计算数组中所有值的和  
		range        建立一个包含指定范围单元的数组  
  
* 获取数组内容  
		array_chunk        将一个数组分割成多个  
    	array array_chunk(array $input, int $size[, bool $preserve_keys])   
		array_filter    用回调函数过滤数组中的单元  
		array_slice     从数组中取出一段  
	    array array_slice($arr, $offset [,$len [,$preserve_keys]])  
		array_keys        返回数组中所有的键名  
    	array array_keys(array $input[, mixed $search_value[, bool $strict]] )  
    	如果指定了可选参数 search_value，则只返回该值的键名。否则input数组中的所有键名都会被返回。  
		array_values    返回数组中所有的值，并建立数字索引  
  
		array_merge        合并一个或多个数组  
   	一个数组中的值附加在前一个数组的后面。  
   	如果输入的数组中有相同的字符串键名，则该键名后面的值将覆盖前一个值。  
   	如果数组包含数字键名，后面的值将不会覆盖原来的值，而是附加到后面。  
   	如果只给了一个数组并且该数组是数字索引的，则键名会以连续方式重新索引。   
		array_merge_recursive    递归地合并一个或多个数组  
  
* 搜索  
		in_array            检查数组中是否存在某个值  
	    bool in_array(mixed $needle, array $haystack[, bool $strict])  
		array_key_exists    检查给定的键名或索引是否存在于数组中  
    	isset()对于数组中为NULL的值不会返回TRUE，而 array_key_exists()会  
		array_search        在数组中搜索给定的值，如果成功则返回相应的键名    
		array_combine    创建一个数组，用一个数组的值作为其键名，另一个数组的值作为其值  
    	如果两个数组的单元数不同或者数组为空时返回FALSE。  
		array_rand        从数组中随机取出一个或多个单元，返回键名或键名组成的数组，下标是自然排序的  
		array_fill      用给定的值填充数组  
    	array_fill($start, $num, $value)  
		array_flip      交换数组中的键和值  
		array_pad       用值将数组填补到指定长度  
		array_reverse   返回一个单元顺序相反的数组  
		array_unique    移除数组中重复的值  
		array_splice    把数组中的一部分去掉并用其它值取代    
		implode            将数组元素值用某个字符串连接成字符串  
		explode($delimiter, $str [,$limit])    //使用一个字符串分割另一个字符串  
	    $delimiter不能为空字符串""    
		array_map        将回调函数作用到给定数组的单元上，只能处理元素值，可以处理多个数组  
	    如果callback参数设为null，则合并多个数组为一个多维数组  
		array_walk        对数组中的每个成员应用用户函数，只能处理一个数组，键和值均可处理，与foreach功能相同  
	    bool array_walk ( array &$array , callback $funcname [, mixed $userdata ] )  
  
* 栈：后进先出  
入栈和出栈会重新分配索引下标  
array_push        将一个或多个单元压入数组的末尾（入栈）  
array_pop        将数组最后一个单元弹出（出栈）        使用此函数后会重置(reset())array 指针。  
  
* 队列：先进先出  
队列函数会重新分配索引下标  
array_unshift    在数组开头插入一个或多个单元  
array_shift        将数组开头的单元移出数组            使用此函数后会重置(reset())array 指针。  
  
* 排序函数  
		sort            对数组排序  
		rsort            对数组逆向排序  
		asort            对数组进行排序并保持索引关系  
		arsort            对数组进行逆向排序并保持索引关系  
		ksort            对数组按照键名排序  
		krsort            对数组按照键名逆向排序  
		usort            使用用户自定义的比较函数对数组中的值进行排序  
		uksort            使用用户自定义的比较函数对数组中的键名进行排序  
		uasort            使用用户自定义的比较函数对数组中的值进行排序并保持索引				关联  
		natsort            用用“自然排序”算法对数组排序  
		natcasesort        用“自然排序”算法对数组进行不区分大小写字母的排序  
		array_multisort 对多个数组或多维数组进行排序  
		shuffle            将数组打乱  
    引用传递参数，返回bool值。  
    重新赋予索引键名，删除原有键名  
  
* 差集  
		array_udiff_assoc   带索引检查计算数组的差集，用回调函数比较数据  
		array_udiff_uassoc  带索引检查计算数组的差集，用回调函数比较数据和索引  
		array_udiff         用回调函数比较数据来计算数组的差集  
		array_diff_assoc    带索引检查计算数组的差集  
		array_diff_key      使用键名比较计算数组的差集  
		array_diff_uassoc   用用户提供的回调函数做索引检查来计算数组的差集  
		array_diff_ukey     用回调函数对键名比较计算数组的差集  
		array_diff          计算数组的差集  
* 交集  
		array_intersect_assoc 带索引检查计算数组的交集  
		array_intersect_key 使用键名比较计算数组的交集  
		array_intersect_uassoc 带索引检查计算数组的交集，用回调函数比较索引  
		array_intersect_ukey 用回调函数比较键名来计算数组的交集  
		array_intersect 计算数组的交集  
		array_key_exists 用回调函数比较键名来计算数组的交集  
		array_uintersect_assoc 带索引检查计算数组的交集，用回调函数比较数据  
		array_uintersect 计算数组的交集，用回调函数比较数据  
  
extract($arr [,$type [,$prefix]])   从数组中将变量导入到当前的符号表(接受结合数组$arr作为参数并将键名当作变量名，值作为变量的值)  
compact($var [,...])   建立一个数组，包括变量名和它们的值(变量名成为键名而变量的内容成为该键的值)  

### 伪类型  ###

* mixed        说明一个参数可以接受多种不同的（但并不必须是所有的）类型。  
* number        说明一个参数可以是 integer 或者 float。  
* callback    回调函数  
* void        void作为返回类型意味着函数的返回值是无用的。  
            void作为参数列表意味着函数不接受任何参数。  

### 数据库操作 ###

* 连接认证  
mysql_connect        连接并认证数据库  
* 发送SQL语句，接收执行结果  
mysql_query            发送SQL语句  
        仅对select, show, explain, describe语句执行成功返回一个资源标识符，其他语句成功返回true。执行失败均返回false。  
* 处理结果  
mysql_fetch_assoc    从结果集中取得一行作为关联数组  
        每次只取回一条，类似each  
    结果集中记录指针  
mysql_fetch_row        从结果集中取得一行作为枚举数组  
mysql_fetch_array    从结果集中取得一行作为关联数组，或数字数组，或二者兼有  
    array mysql_fetch_array ( resource $result [, int $ result_type  ] )  
    可选参数result_type可选值为：MYSQL_ASSOC，MYSQL_NUM 和 MYSQL_BOTH(默认)  
mysql_free_result    释放结果内存  
* 关闭链接  
mysql_close            关闭连接


<center><strong>{{ page.date | date_to_string }}</strong></center>
