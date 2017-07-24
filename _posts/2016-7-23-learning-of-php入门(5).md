---
layout: default
title: php入门学习(5)
---

## 缩略图-水印 ##

* imagecopyresampled  重采样拷贝部分图像并调整大小  
    	bool imagecopyresampled ( resource $dst_image , resource 
		$src_image , int $dst_x , int $dst_y , int $src_x , int $src_y , 
		int $dst_w , int $dst_h , int $src_w , int $src_h )  
* imagecopymerge      拷贝并合并图像的一部分  
    	bool imagecopymerge ( resource $dst_im , resource $src_im , int 
		$dst_x , int $dst_y , int $src_x , int $src_y , int $src_w , int 
		$src_h , int $pct )  
* getimagesize        取得图像大小  
    	array getimagesize ( string $filename [, array &$imageinfo ] )

## URL函数 ##

__get_headers__ — 取得服务器响应一个 HTTP 请求所发送的所有标头  
__get_meta_tags__ — 从一个文件中提取所有的 meta 标签 content 属性，返回一个数组  
__http_build_query__ — 生成 URL-encode 之后的请求字符串  
__urldecode__ — 解码已编码的URL字符串  
__urlencode__ — 编码URL字符串  
__parse_url__ — 解析URL，返回其组成部分
```  
    'http://username:password@hostname/path?arg=value#anchor'  
    scheme(如http), host, port, user, pass, path, query(在问号?之后), 
	fragment(在散列符号#之后) 
``` 

### 编码可用于交换多个变量 ###

$a = '中国';  
$b = '四川';  
$a = urlencode($a);  
$b = urlencode($b);  
$a = $a.'&'.$b;  
$b = explode('&', $a);  
$a = urldecode($b[1]);  
$b = urldecode($b[0]);  
echo $a, $b;  

### list()函数用于交换变量 ###

``` 
    list($a, $b) = array($b, $a);    
```

## 文件、目录 ## 

__dirname($path)__  返回路径中的目录部分  
__basename($path [,$suffix])__  返回路径中的文件名部分  
__pathinfo($path [,$options])__ 返回文件路径的信息(数组元素：					dirname,basename,extension) 
__realpath($path)__ 返回规范化的绝对路径名  

  
__copy($source, $dest)__    拷贝文件  
__unlink($file)__   删除文件  
__rename($old, $new)__  重命名或移动一个文件或目录  
__mkdir($path [,$mode [,$recursive]])__ 新建目录  
    	* $mode表示权限，默认0777  
    	* $recursive表示可创建多级目录，默认false  
__rmdir($dir)__     删除目录(目录必须为空，且具有权限)  
  
__file_exists($file)__  检查文件或目录是否存在  
__is_file($file)__      判断文件是否存在且为正常的文件  
__is_dir($file)__       判断文件名是否存在且为目录  
__is_readable($file)__  判断文件或目录是否可读  
__is_writable($file)__  判断文件或目录是否可写  
__is_executable($file)__    判断给定文件名是否可执行  
__is_link($file)__      判断给定文件名是否为一个符号连接  
  
__tmpfile(void)__   建立一个临时文件  
__tempnam($dir, $prefix)__  在指定目录中建立一个具有唯一文件名的文件  
  
__file($file)__ 把整个文件读入一个数组中
```  
fopen($filename, $mode [,$use_include_path])  
    $mode参数：(加入'b'标记解决移植性)  
        'r'     只读方式打开，将文件指针指向文件头。  
        'r+'    读写方式打开，将文件指针指向文件头。  
        'w'     写入方式打开，将文件指针指向文件头并将文件大小截为零。如果文件不存在则尝试创建之。  
        'w+'    读写方式打开，将文件指针指向文件头并将文件大小截为零。如果文件不存在则尝试创建之。  
        'a'     写入方式打开，将文件指针指向文件末尾。如果文件不存在则尝试创建之。  
        'a+'    读写方式打开，将文件指针指向文件末尾。如果文件不存在则尝试创建之。  
        'x'     创建并以写入方式打开，将文件指针指向文件头。  
        'x+'    创建并以读写方式打开，将文件指针指向文件头。
```  
__fclose($handle)__ 关闭一个已打开的文件指针  
__fread($handle, $length)__ 读取文件（可安全用于二进制文件）  
__fwrite($handle, $string [,$length])__ 写入文件（可安全用于二进制文件）  
__rewind($handle)__ 倒回文件指针的位置  
__ftell($handle)__  返回文件指针读/写的位置  
__fseek($handle, $offset [,$whence])__  在文件指针中定位  
__feof($handle)__   测试文件指针是否到了文件结束的位置  
__fgets__   从文件指针中读取一行  
__fgetss__  从文件指针中读取一行并过滤掉HTML标记  
__flock($handle, $opt)__ 轻便的咨询文件锁定  
    * $opt：LOCK_SH 取得共享锁定（读取的程序）；LOCK_EX 取得独占锁定（写入的程序）；LOCK_UN 释放锁定（无论共享或独占）  
  
  
__readfile($file) 读入一个文件并写入到输出缓冲  
__fflush($handle) 将缓冲内容输出到文件  
  
__touch($file [,$time [,$atime]])__   设定文件的访问和修改时间  
__fileatime__   取得文件的上次访问时间  
__filectime__   取得文件的inode修改时间  
__filegroup__   取得文件的组  
__fileinode__   取得文件的inode  
__filemtime__   取得文件修改时间  
__fileowner__   取得文件的所有者  
__fileperms__   取得文件的权限  
__filesize__    取得文件大小  
__filetype__    取得文件类型  

## 获取/设置文件信息 ##

1. 扩展Fileinfo，配置php.ini  
2. extension=php_fileinfo.dll
  
__finfo_open([$opt])__ //创建一个文件信息资源  
__finfo_file($finfo, $file [,$opt])__ //获取文件信息  
__finfo_set_flags($finfo, $opt)__ //设置文件信息项  
__finfo_close($finfo)__ //关闭文件信息资源  
  
__mime_content_type($file)__ //获取文件的MIME类型  
  
$opt参数选项：  
		* FILEINFO_MIME_ENCODING 文件编码类型  
		* FILEINFO_MIME_TYPE 文件MIME类型  

### 目录 ###

__chdir($dir)__         改变当前目录  
__chroot($dir)__        将当前目录改变为当前进程的根目录  
__closedir($handle)__   关闭目录句柄  
__dir($dir)__           返回一个目录的实例对象  
__getcwd()__            取得当前工作目录  
__opendir($path)__      打开目录句柄  
__readdir($handle)__    从目录句柄中读取条目  
__rewinddir($handle)__  倒回目录句柄  
__scandir($dir [,$order])__     列出指定路径中的文件和目录  
__glob($pattern [,$flags])__    寻找与模式匹配的文件路径  
    * $flags：  
        GLOB_MARK - 在每个返回的项目中加一个斜线    
        GLOB_NOSORT - 按照文件在目录中出现的原始顺序返回（不排序）    
        GLOB_NOCHECK - 如果没有文件匹配则返回用于搜索的模式    
        GLOB_NOESCAPE - 反斜线不转义元字符    
        GLOB_BRACE - 扩充 {a,b,c} 来匹配 'a'，'b' 或 'c'    
        GLOB_ONLYDIR - 仅返回与模式匹配的目录项   
    查找多种后缀名文件：glob('*.{php,txt}', GLOB_BRACE); 

## 解压缩 ##

1. 新建ZipArchive对象  
$zip = new ZipArchive;  
//打开ZIP文件  
$zip->open($file [,$flags]);  
    $flags：  
        ZIPARCHIVE::OVERWRITE 覆盖(不存在会自动创建)  
        ZIPARCHIVE::CREATE 添加(不存在会自动创建)  
        ZIPARCHIVE::EXCL  
        ZIPARCHIVE::CHECKCONS  
2. 关闭正在处理的ZIP文件  
3. 解压缩ZIP文件  
$zip->extractTo($dest, [$entries]);
```   
    $dest：解压到的文件夹，$entries：解压的条目
```   
4. 添加文件到ZIP文件  
``` 
$zip->addFile($file, [$newname]);     
    $newname可以为"dir/file"，这样可以将文件添加到压缩文件中的某个目录下。其他函数也如此。
```   
5. 添加文件到ZIP文件，而内容来自字符串  
``` 
$zip->addFromString($file, $str);  
``` 
6. 添加空文件夹到ZIP文件  
``` 
$zip->addEmptyDir($dir);  
``` 
7. 通过索引删除ZIP中的文件或文件夹  
``` 
$zip->deleteIndex($index);  
``` 
8. 通过名称删除ZIP中的文件或文件夹  
``` 
$zip->deleteName($name);  
``` 
9. 设置ZIP文件注释  
``` 
$zip->setArchiveComment($str);  
``` 
10. 获取ZIP文件注释  
``` 
$zip->getArchiveComment();  
``` 
11. 通过索引获取文件内容  
``` 
$zip->getFromIndex($index);  
``` 
12. 通过名称获取文件内容  
``` 
$zip->getFromName($name);  
``` 
13. 获取索引文件的文件名称  
``` 
$zip->getNameIndex($index);  
``` 
14. 通过索引重命名文件  
``` 
$zip->renameIndex($index, $newname);  
``` 
15. 通过名称重命名文件  
``` 
$zip->renameName($name, $newname);  
```   
//若将文件夹内容打包成ZIP文件，需循环文件夹的所有目录及文件
```  
function addFileToZip($path, $zip) {  
    //打开当前文件夹$path  
    $handle = opendir($path);  
    //循环读取子文件夹及文件  
    //为防止文件名本身可被转换为false的情况(比如为"0")，则需用不全等!==  
    while ($file = readdir($handle) !== false) {  
        //过滤假文件夹  
        if ($file != '.' && $file != '..') {  
            //对于子文件夹则递归调用本函数  
            if (is_dir($path . '/' . $file)) {  
                addFileToZip($path.'/'.$file, $zip);  
            } else {  
                //将文件添加到ZIP对象  
                $zip->addFile($path . '/' . $file);  
            }  
        }  
    }  
    //关闭文件夹$path  
    closedir($path);  
}  
// ----- END 解压缩 ----- //
```
  
## 文件上传 ## 
* enctype="multipart/form-data"   //FORM标签必须的属性  
* $_FILES 上传文件信息数组变量  
* error   上传错误信息  
  	无错误  
  	文件大小超过php.ini配置  
        1) upload_max_filesize 允许上传的最大文件大小  
        2) post_max_size 最大的POST数据大小  
        3) memory_limit 每个脚本能够使用的最大内存数量(默认128MB)  
  	文件大小超过浏览器表单配置  
        MAX_FILE_SIZE   表示表单数据最大文件大小，该元素需在文件上传域之前。(默认2M)  
        <input type="hidden" name="MAX_FILE_SIZE" value="102400">  
  	文件只有部分被上传  
  	文件没有被上传  
    	6,7 临时文件写入时失败  
  	找不到临时文件  
  	文件写入失败  
* name    文件名  
* type    文件类型  
* tmp_name    上传文件临时路径  
* size    文件大小  
* move_uploaded_file($path, $newpath);    //将上传的文件移动到新位置  
* is_uploaded_file($file) //判断是否为POST上传的文件

### 多文件上传 ###
```
<input type="file" name="updfile[]" /> //HTML中以数组提交  
$_FILES['updfile']['tmp_name'][0]   //服务器端可访问第一个文件的临时路径，其他属性类似 
``` 

### php.ini配置 ###

__file_uploads = On__ 是否允许HTTP上传文件  
__upload_max_filesize__ 上传文件大小限制，默认为2M  
__post_max_size__   post方式表单数据总大小限制，默认为8M  
__upload_tmp_dir__  上传文件临时目录，默认是系统临时目录  
   	* 需设置上传文件临时目录，给其最小权限  
* GET方式的最大传输量为2K  

## 批量提交 ##

FORM表单中的name值可用名称加中括号的形式，在$_POST获取表单数据时，可多项提交形成数组。  
比如多文件上传file，复选框提交checkbox等。 
``` 
<input type="checkbox" name="id[]" value="值1" />  
<input type="checkbox" name="id[]" value="值2" />  
$id = $_POST['id']; //则可获得全部被选中的复选框值，形成索引数组 
``` 
如果name值为：  
```
<input type="checkbox" name="id[one]" value="值1" />  
<input type="checkbox" name="id[two]" value="值2" />  
$id = $_POST['id'];  //则可获取所有name为id[...]的值，形成管理数组 
```

## iconv ##

php.ini配置iconv 
``` 
[iconv]  
;iconv.input_encoding = ISO-8859-1  
;iconv.output_encoding = ISO-8859-1  
;iconv.internal_encoding = ISO-8859-1  
iconv_set_encoding($type, $charset);  
    $type：input_encoding，output_encoding，internal_encoding  
iconv_get_encoding([$type = "all"])  
    $type：all，input_encoding，output_encoding，internal_encoding  
```  
  
  
* iconv($in_charset, $out_charset, $str) //将字符串转换为目标编码  
  * 指定编码，可解决中文字符的统计、查询、截取等！  
* iconv_strlen($str [,$charset]) //统计字符串的字符数  
* iconv_strpos($str, $needle, $offset [,$charset]) //查找子串首次出现的位置  
* iconv_strrpos($str, $needle [,$charset]) //查找子串最后一次出现的位置  
* iconv_substr($str, $offset [,$len [,$charset]]) //截取子串  

## 字符串函数 ##

* addslashes($str)    //使用反斜线转移字符串  
* stripcslashes($str) //反引用一个使用addcslashes转义的字符串  
* stripslashes($str)  //反引用一个引用字符串  
* chr($ascii) //返回ASCII码的字符  
* ord($char)  //返回字符的ASCII码  
* substr_count($haystack, $needle)    //计算子串出现的次数  
* count_chars($str [,$mode])  统计每个字节值出现的次数  
    	//0 - 以所有的每个字节值作为键名，出现次数作为值的数组。    
    	//1 - 与0相同，但只列出出现次数大于零的字节值。    
    	//2 - 与0相同，但只列出出现次数等于零的字节值。    
    	//3 - 返回由所有使用了的字节值组成的字符串。    
    	//4 - 返回由所有未使用的字节值组成的字符串。   
* crypt($str, [$salt])    //单向字符串散列  
* str_split($str [,$len]) //将字符串按长度分割为数组  
* explode($separ, $str)   //使用一个字符串分割另一个字符串  
* implode([$glue,] $arr)  //将数组元素的值根据$glue连接成字符串  
* chunk_split($str [,$len [,$end]])   //将字符串分割成小块  
    	$len：每段字符串的长度，$end：每段字符串末尾加的字符串(如"\r\n")  
* html_entity_decode($str [,$flags [,$encoding]]) //将HTML实体转成字符信息  
* htmlentities($str [,$flags [,$encoding]])   //将字符信息转成HTML实体  
* htmlspecialchars_decode($str)   //将特殊HTML实体转成字符信息  
* htmlspecialchars($str [,$flags [,$encoding]])   //将字符信息转成特殊HTML实体  
* lcfirst($str)   //将字符串首字母转成小写  
* ucfirst($str)   //将字符串首字母转成大写  
* ucwords($str)   //将字符串中每个单词的首字母转换为大写  
* strtolower($str)    //将字符串转化为小写  
* strtoupper($str)    //将字符串转化为大写  
* trim($str [,$charlist]) //去除字符串首尾处的空白字符（或者其他字符）  
* ltrim($str [,$charlist])    //去除字符串首段的空白字符（或者其他字符）  
* rtrim($str [,$charlist])    //去除字符串末端的空白字符（或者其他字符）  
* md5_file($file) //计算指定文件的MD5散列值  
* md5($str)   //计算字符串的MD5散列值  
* money_format($format, $num) //将数字格式化为货币形式  
* number_format($num) //格式化数字  
* nl2br($str) //在字符串所有新行之前插入HTML换行标记<br />  
* parse_str($str, [$arr]) //解析字符串  
* print($str) //输出字符串  
* printf      //输出格式化字符串  
* sprintf($format [,$args...])    //格式化字符串  
* sha1_file   //计算文件的sha1散列值  
* sha1        //计算字符串的sha1散列值  
* similar_text($first, $second [,$percent])   //计算两个字符串的相似度  
  	  返回在两个字符串中匹配字符的数目，$percent存储相似度百分比  
* str_replace($search, $replace, $str [,$count [,$type]])  //子字符串替换  
* str_ireplace    //字符串替换(忽略大小写)  
* str_pad($str, $len [,$pad [,$type]])  //使用另一个字符串填充字符串为指定长度  
  	  $type：在何处填充。STR_PAD_RIGHT，STR_PAD_LEFT 或 STR_PAD_BOTH  
* str_repeat($str, $num)  //重复一个字符串  
* str_shuffle($str)   //随机打乱一个字符串  
* str_word_count($str [,$format [,$charlist]])    //返回字符串中单词的使用情况  
* strcasecmp($str1, $str2)    //二进制安全比较字符串（不区分大小写）  
    	如果str1小于str2，返回负数；如果str1大于str2，返回正数；二者相等则返回0。  
* strcmp($str1, $str2)    //二进制安全字符串比较  
* strcoll($str1, $str1)   //基于区域设置的字符串比较(区分大小写，非二进制安全)  
* strcspn($str1, $str1 [,$start [,$len]])   //获取不匹配遮罩的起始子字符串的长度  
* strip_tags($str)    //从字符串中去除HTML和PHP标记  
* strpos($haystack, $needle [,$offset])   //查找字符串首次出现的位置  
* stripos($haystack, $needle [,$offset])    //查找字符串首次出现的位置（不区分大小写）  
* strripos($haystack, $needle [,$offset])   //计算指定字符串在目标字符串中最后一次出现的位置（不区分大小写）  
* strrpos($haystack, $needle [,$offset])   //计算指定字符串在目标字符串中最后一次出现的位置  
* strlen($str)    //获取字符串长度  
* strpbrk($haystack, $str)    //在字符串中查找一组字符的任何一个字符  
* strrev($str)    //反转字符串  
    	join('', array_reverse(preg_split("//u", $str))); //实现对UTF-8字符串的反转  
* strspn$subject, $mask)  //计算字符串中全部字符都存在于指定字符集合中的第一段子串的长度。  
* strstr($haystack, $needle)   //查找字符串的首次出现  
* stristr($haystack, $needle)   //查找字符串的首次出现(不区分大小写)  
* strrchr($haystack, $needle) //查找指定字符在字符串中的最后一次出现  
* strtok($str, $token)    //标记分割字符串  
* substr_compare($main_str, $str, $offset [,$len) //二进制安全比较字符串（从偏移位置比较指定长度）  
* substr_replace$str, $replace, $start [,$len]    //替换字符串的子串  
* strtr($str, $from, $to) //转换指定字符  
* substr($str, $start [,$len])    //返回字符串的子串  
* vfprintf$handle, $format, $args)    //将格式化字符串写入流  
* vprintf($format, $args) //输出格式化字符串  
* vsprintf($format, $args) //返回格式化字符串  
* wordwrap($str [,$width=75 [,$break='\n']])  //打断字符串为指定数量的字串  
  
* crc32($str) //计算一个字符串的crc32多项式  
    	crc32算法[循环冗余校验算法]  
    	生成str的32位循环冗余校验码多项式。将数据转换成整数。
 
## mbstring(多字节字符串) ##

需开启mbstring扩展  
* mb_strimwidth($str, $start, $width [,$trim [,$encoding]])   //保留指定的子串(并补充)  
* mb_stripos($str, $needle [,$offset [,$encoding]])   //查找子串首次出现的位置(忽略大小写)  
* mb_strpos($str, $needle [,$offset [,$encoding]])   //查找子串首次出现的位置  
* mb_strripos($str, $needle [,$offset [,$encoding]])   //查找子串最后一次出现的位置(忽略大小写)  
* mb_strrpos($str, $needle [,$offset [,$encoding]])   //查找子串最后一次出现的位置  
* mb_strstr($str, $needle [,$before [,$encoding]])    //返回子串首次出现位置之后(前)的字符串  
* mb_stristr($str, $needle [,$before [,$encoding]])    //返回子串首次出现位置之后(前)的字符串(忽略大小写)  
* mb_strrchr($str, $needle [,$before [,$encoding]])    //返回字符最后一次出现位置之后(前)的字符串  
* mb_strrichr($str, $needle [,$before [,$encoding]])    //返回字符最后一次出现位置之后(前)的字符串(忽略大小写)  
  
* mb_strtoupper($str [,$encoding])    //转换成大写  
* mb_strtolower($str [,$encoding])    //转换成小写  
  
* mb_strlen($str [,$encoding])    //获取字符串长度  
* mb_split($pattern, $str [,$limit])  //将字符串分割成数组  
* mb_substr($str, $start [,$len [,$encoding]])    //获取字符串的子串  
* mb_strcut($str, $start [,$len [,$encoding]])    //获取字符串的子串  
* mb_strwidth($str [,$encoding])  //获取字符串的宽度  
* mb_substr_count($str, $needle [,$encoding]) //子串在字符串中出现的次数     

## PCRE函数 ##

* preg_filter($pattern, $replace, $subject [,$limit [,&$count]])  执行一个正则表达式搜索和替换  
* preg_replace($pattern, $replace, $subject [,$limit [,&$count]])  执行一个正则表达式搜索和替换  
* preg_replace_callback($pattern, $callback, $subject [,$limit [,&$count]])   执行一个正则表达式搜索并且使用一个回调进行替换  
* preg_grep($pattern, $input [,$flags])   返回匹配模式的数组条目  
* preg_match($pattern, $subject [,&$matches [,$flags [,$offset]]]) 执行一个正则表达式匹配  
* preg_match_all($pattern, $subject [,&$matches [,$flags [,$offset]]]) 执行一个全局正则表达式匹配  
    	$matches存放返回的结果  
        $matches[0][n] (n>=0) 表示存放第n+1个匹配到的结果  
        $matches[m][n] (m>=1, n>=0) 表示存放第n+1个匹配到结果的第m个表达式的内容  
* preg_split($pattern, $subject [,$limit [,$flags]])  通过一个正则表达式分隔字符串  
    	$limit表示限制分隔得到的子串最多只有limit个，-1表示不限制  
    	$flags参数：  
        PREG_SPLIT_NO_EMPTY：将返回分隔后的非空部分  
        PREG_SPLIT_DELIM_CAPTURE：用于分隔的模式中的括号表达式将被捕获并返回  
        PREG_SPLIT_OFFSET_CAPTURE：对于每一个出现的匹配返回时将会附加字符串偏移量  
* preg_quote($str [,$delimiter])  转义正则表达式字符  
* preg_last_error()   返回最后一个PCRE正则执行产生的错误代码  

## Math函数 ##

__base_convert($number, $frombase, $tobase)__   //在任意进制之间转换数字  
__ceil($float)__    //向上取整  
__floor($float)__   //向下取整  
__exp($float)__ //计算e的指数  
__hypot($x, $y)__   //计算直角三角形的斜边长  
__is_nan($val)__    //判断是否为合法数值  
__log($arg [,$base=e])__  //自然对数  
__max($num1, $num2, ...)__  //找出最大值  
    * max($arr)   //找出数组中的最大值  
__min($num1, $num2, ...)__  //找出最小值  
__rand([$min], $max)__  //产生一个随机整数  
__srand([$seed])__  //播下随机数发生器种子  
__mt_rand([$min], $max)__   //生成更好的随机数  
__mt_srand($seed)__     //播下一个更好的随机数发生器种子  
__pi()__    //得到圆周率值  
__pow($base, $exp)__    //指数表达式  
__sqrt($float)__    //求平方根  
__deg2rad($float)__ //将角度转换为弧度  
__rad2deg($float)__ //将弧度数转换为相应的角度数  
__round($val [,$pre=0])__ //对浮点数进行四舍五入  
__fmod($x, $y)__ //返回除法的浮点数余数 


<center><strong>{{ page.date | date_to_string }}</strong></center>
