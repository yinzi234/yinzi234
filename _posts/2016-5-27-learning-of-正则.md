---
layout: default
title: 正则学习
---

##正则##

正则表达式是被用来匹配字符串中的字符组合的模式。在JavaScript中，正则表达式也是对象。这种模

式可以被用于RegExp的exec和test方法以及 String的match、replace、search和split方法。

###JavaScript RegExp对象###

RegExp 对象表示正则表达式，它是对字符串执行模式匹配的强大工具。

创建正则表达式两种方式：

正则表达式字面量

```
/pattern/attributes
var re = /ab+c/;

```

调用RegExp对象的构造函数，如下所示：

```
new RegExp(pattern, attributes);
var re = new RegExp("ab+c");

```

###参数###

参数 pattern 是一个字符串，指定了正则表达式的模式或其他正则表达式。

参数 attributes 是一个可选的字符串，包含属性 "g"、"i" 和 "m"，分别用于指定全局匹配、区分

大小写的匹配和多行匹配。ECMAScript 标准化之前，不支持 m 属性。如果 pattern 是正则表达

式，而不是字符串，则必须省略该参数。

###RegExp对象属性###

global：RegExp 对象是否具有标志 g。

ignoreCase：RegExp 对象是否具有标志 i。

lastIndex：一个整数，标示开始下一次匹配的字符位置。

multiline：RegExp 对象是否具有标志 m。

source：正则表达式的源文本。

###RegExp对象方法###

compile：编译正则表达式。

exec：检索字符串中指定的值。返回找到的值，并确定其位置。

test：检索字符串中指定的值。返回 true 或 false。

compile方法：

compile() 方法用于在脚本执行过程中编译正则表达式。

compile() 方法也可用于改变和重新编译正则表达式。

exec方法：

exec() 方法用于检索字符串中的正则表达式的匹配。返回一个数组，其中存放匹配的结果。如果未找

到匹配，则返回值为 null。

```
<script type="text/javascript">

var str = "Visit W3School, W3School is a place to study web technology."; 
var patt = new RegExp("W3School","g");
var result;

//返回匹配到的结果
while ((result = patt.exec(str)) != null)  {
  document.write(result);
  document.write("<br />");
  document.write(patt.lastIndex);
  document.write("<br />");
 }
</script>

```

结果：W3School
　　　　　　14
　　　　　W3School
　　　　　　24

test方法：

test() 方法用于检测一个字符串是否匹配某个模式。匹配返回 true，否则返回 false。

```
RegExpObject.test(string)
```


```
<script type="text/javascript">
var str = "Visit W3School";
var patt1 = new RegExp("W3School");

var result = patt1.test(str);

document.write("Result: " + result);
</script>
```

结果  ：Result: true

exec方法是使用正则表达式的最强大和最慢的方法。如果它成功地匹配regexp和字符串String，它会

返回一个数组。数组中下标为0的元素将包含正则表达式regexp匹配的字符串。下标为1的元素是分组1

捕获的文本，下标为2的元素是分组2捕获的文本，以此类推。如果匹配失败，它会返回null。

test方法是使用正则表达式的最简单和最快的方法。如果该regexp匹配string，它返回true；否则，

它返回false。

###支持正则表达式的String对象的方法###

search：检索与正则表达式相匹配的值。

match：找到一个或多个正则表达式的匹配。

replace：替换与正则表达式匹配的子串。

split：把字符串分割为字符串数组。

###string.search(regexp)###

search方法和indexOf方法类似，只是它接收一个正则表达式对象作为参数而不是一个字符串。如果找

到匹配，它返回第1个匹配的首字符位置，如果没有找到匹配，则返回-1。此方法会忽略g标识，且没有

position参数。它同时忽略 regexp 的 lastIndex 属性，并且总是从字符串的开始进行检索，这意

味着它总是返回 stringObject 的第一个匹配的位置。

注释：要执行忽略大小写的检索，请追加标志 i。

```
var text = 'and in it he says "Any damn fool could';
var pos = text.search(/["']/)
结果为18
```

###strng.match(regexp)和stringObject.match(searchvalue)###

match方法让字符串和一个正则表达式进行匹配。它依据g标识来决定如何进行匹配。如果没有g标识，

那么调用string.match(regexp)的结果与调用regexp.exec(string)的结果相同。然而，如果带有

g标识，那么它生成一个包含所有匹配（除捕获组之外）的数组。

```
var str="Hello world ll world!"
alert(str.match("world!"));     //结果world
console.log(str.match(/world/g));  //结果[world,world]
```

###string.split(separator,limit)###

split方法把这个string分割成片段来创建一个字符串数组。可选参数limit可以限制被分割的片段数

量。separator参数可以是一个字符串或者一个正则表达式。

```
var digits = '0123456789';
        var a = digits.split('',5);  //a是['0,'1','2','3','4','5'];
```

###stringObject.replace(regexp/substr,replacement)###

replace方法对string进行查找和替换操作，并返回一个新的字符串。参数searchValue可以是一个字

符串或者一个正则表达式对象。

返回值
一个新的字符串，是用 replacement 替换了 regexp 的第一次匹配或所有匹配之后得到的。
　　
说明
　　
字符串 stringObject 的 replace() 方法执行的是查找并替换的操作。它将在 stringObject 中

查找与 regexp 相匹配的子字符串，然后用 replacement 来替换这些子串。如果 regexp 具有全局

标志 g，那么 replace() 方法将替换所有匹配的子串。否则，它只替换第一个匹配子串。

replacement 可以是字符串，也可以是函数。如果它是字符串，那么每个匹配都将由字符串替换。但

是 replacement 中的 $ 字符具有特定的含义。如下表所示，它说明从模式匹配得到的字符串将用于

替换。

1、1、 2、...、$99：与 regexp 中的第 1 到第 99 个子表达式相匹配的文本。

$&：与 regexp 相匹配的子串。

$`：位于匹配子串左侧的文本。

$'：位于匹配子串右侧的文本。

$$：直接量符号。

用使用这些组号，则有个问题就是正则表达式要存在组号，关于组则相应的分组匹配自表达式，一个误

区：

(...)捕获型分组，又可以叫字表达式，捕获型分组会复制它所匹配的文本，并将其放到result数组

里，每个捕获分组都会被指定一个编号。

(?:)非捕获性分组，仅做简单的匹配，并不会捕获所匹配的文本，性能比捕获性分组效率高，非捕获性

分组不会干扰捕获型分组的编号。

把 "Doe, John" 转换为 "John Doe" 的形式：

```
name = "Doe, John";
name.replace(/(\w+)\s*, \s*(\w+)/, "$2 $1");
```

把所有的花引号替换为直引号：

```
name = '"a", "b"';
name.replace(/"([^"]*)"/g, "'$1'");
```

把字符串中所有单词的首字母都转换为大写：

```
name = 'aaa bbb ccc';
uw=name.replace(/\b\w+\b/g, function(word){
  return word.substring(0,1).toUpperCase()+word.substring(1);}
  );　　
```

###replace例子###

一：

```
<script type="text/javascript">

name = "Doe, John,12344";

document.write(name.replace(/(\w+)\s*, \s*(\w+),\d+/, function($1,$2){return $2}));
//弹出结果为John
</script>　
```

二：

```
<script type="text/javascript">

name = "Doe, John";

document.write(name.replace(/(\w+)\s*, \s*(\w+)/, "$2 $1"));
//结果为 John,Doe
</script>
```

三：

```
<script type="text/javascript">

name = "Doe, John,12344";

document.write(name.replace(/(\w+)\s*, \s*(\w+),\d+/, function($2){return $2}));
//弹出结果为Doe, John,12344
</script>
```

要想返回匹配的单个组元素，必须将匹配的组都作为参数。


###表单特性###

placeholder  : 输入框提示信息

   –例子 : 微博的密码框提示

autocomplete :  是否保存用户输入值 –默认为on，关闭提示选择off

autofocus  : 指定表单获取输入焦点

list和datalist :  为输入框构造一个选择列表  –list值为datalist

标签的id

required  : 此项必填，不能为空

Pattern: 正则验证 pattern="\d{1,5}“

Formaction在submit里定义提交地址

###元字符表###

元字符是正则表达式的一部分，当我们要匹配正则表达式本身时，必须对这些元字符转义.下面是正则表

达式用到的所有元字符

正则转义，如果对特殊字符转义拿捏不准时，可以给任何特殊字符都添加一个\前缀来使其字面化，注意

\前缀不能使字母或数字字面化。常见的需要转义的字符 -( [ { \ ^ $ | ) ? * + .等

.：查找单个字符，除了换行和行结束符。

\w：查找单词字符。

\W：查找非单词字符。

\d：查找数字。

\D：查找非数字字符。

\s:查找空白字符。

\S:查找非空白字符。

\b:匹配单词边界。

\B:匹配非单词边界。

\0:查找 NUL 字符。

\n:查找换行符。

\f:查找换页符。

\r:查找回车符。

\t:查找制表符。

\v:查找垂直制表符。

\xxx:查找以八进制数 xxx 规定的字符。

\xdd:查找以十六进制数 dd 规定的字符。

\uxxxx:查找以十六进制数 xxxx 规定的 Unicode 字符。


正则懒惰/贪婪规则：

　　*？重复任意次，但尽可能少重复。

　　+？重复1次或更多次，但尽可能少重复。

　　？？重复0次或1次，但尽可能少重复。

　　{n,m}?重复n到m次，但尽可能少重复。

　　{n,}?重复n次以上，但尽可能少重复。

<center><strong>{{ page.date | date_to_string }}</strong></center>
