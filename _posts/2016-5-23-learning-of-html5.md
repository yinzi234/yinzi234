---
layout: default
title: HTML5学习
---

## HTML5声明 ##

```
<!DOCTYPE html>
```

### HTML5兼容问题 ###

HTML5提出的新的元素不被IE6-8识别，这些新元素不能作为父节点包裹子

元素，并且不能应用CSS样式。可以在head标签中引入htmltshiv.js解决;

```
<!--[if lt IE 9]>
<script sec="http://apps.bdimg.com/libs/html5shiv/3.7/
html5shiv.min.js"></script>
<![endif]>
```

### HTML5新元素 ###

### 新块级元素 ###

HTML5提供了新的语义元素来证明Web页面的不同部分：

header;nav;section;article;aside;figcaption;figure;footer

header: 标签定义文档的页眉;

section:定义文档中的节;

footer:定义文档或节的页脚;

aside:定义其所处内容之外的内容;//可用作文章的侧栏;

nav:定义导航链接的部分;//果文档中有“前后”按钮，则应该把它放到 

nav元素中;

main:规定文档的主要内容;//在一个文档中，不能出现一个以上的 

main元素。<main元素不能是以下元素的后代：article、

aside、footer、header或 nav;

article:规定独立的自包含内容;

figure:规定独立的流内容（图像、图表、照片、代码等等）;//使用

figcaption为figure定义标题，置于 "figure" 元素的第一个或最

后一个子元素的位置

```
<figure>  
    <img src=“miaov.png”/>  
    <figcaption>文字</figcaption>  
</figure> 
```

### 新元素 ###

time：用来表现时间或日期

```
<p> 每天晚上 <time>19:00</time> 结束营业。 </p>  
<p> 在<time datetime="2017-08-15">中秋</time> 那天。 </p>  
```

datalist：选项列表。与text文本框配合使用

```
<input type="text" list="valList" />  
<datalist id="valList">  
    <option value="javascript">javascript</option>  
    <option value="html">html</option>  
    <option value="css">css</option>  
</datalist>    
```

details：用于描述文档或文档某个部分的细节

summary： details元素的标题

```
<details>  
　　　<summary>妙味课堂</summary>  
　　　<p>国内将知名的IT培训机构</p>  
</details>      
```

address：定义文章 或页面作者的详细联系信息

mark：需要标记的词或句子

progress定义进度条

```
<progress max="100"value="76">  
     <span>76</span>%  
</progress>      
```

针对IE6-8这些不支持HTML5语义化标签的浏览器解决办法：

用js创建元素，然后样式中display:block:

```
<script>  
    document.createElement(“header”);  
    document.createElement(“nav”);  
    document.createElement(“footer”);  
</script>  
<style>  
header,nav,footer{display:block}  
</style>      
```

### 新多媒体元素 ###

audio:音频内容

video:视频

source:多媒体资源

embed:嵌入的内容，比如插件

track:为音频视频之类的媒介规定外部文本轨道

audio:[{src:"/URL",Desc:"音频URL地址,也可以用<audio>内设置

<source src="" type="audio/mpeg(.mp3)|audio/ogg|audio/

wav">标签的src;"},{autoplay:"autoplay",Desc:"音频在就绪后马上

播放"},{controls:"controls",Desc:"向用户显示控件，比如播放按

钮"},{loop:"loop",Desc:"每当音频结束时重新开始播放"},

{muted:"muted",Desc:"默认为静音"},{preload:"auto/meta/

none",Desc:"音频在页面加载时进行加载，并预备播放"}];

video:同audio相似，可以播放的格式：video/mp4、video/webm、video/ogg

embed:可以直接指定src路径输出插件

track:用于规定字幕文件或其他包含文本的文件，当媒体播放时，这些文件

是可见的

### FORMs ###

### 输入型控件 ###

email :  电子邮箱文本框，跟普通的没什么区别

   –当输入不是邮箱的时候，验证通不过

   –移动端的键盘会有变化

tel  :   电话号码

url  :   网页的URL

search :  搜索引擎

   –chrome下输入文字后，会多出一个关闭的X

range :  特定范围内的数值选择器

   –min、max、step(步数 )

number  : 只能包含数字的输入框

color  : 颜色选择器

datetime :  显示完整日期

datetime-local :  显示完整日期，不含时区

time  : 显示时间，不含时区

date  :   显示日期

week  : 显示周

month  : 显示月

### 表单特性 ###

placeholder  : 输入框提示信息

   –例子 : 微博的密码框提示

autocomplete :  是否保存用户输入值

   –默认为on，关闭提示选择off

autofocus  : 指定表单获取输入焦点

list和datalist :  为输入框构造一个选择列表

   –list值为datalist标签的id

required  : 此项必填，不能为空

Pattern: 正则验证 pattern="\d{1,5}“

Formaction在submit里定义提交地址

### 新的选择器 ###

querySelector：选择满足条件的第一个元素。

querySelectorAll：选择满足条件的一组元素。

getElementsByClassName：根据class选择元素，参数为元素的class

名。

新的Selectors API不仅更方便，而且也更高效，推荐使用。 

例如：页面上有一个表格，获取鼠标悬浮下的单元格：

```
var hovered=document.querySelector("td:hover");        
```

### classList ###

–length:  class的长度

–add()  :  添加class方法

–remove()  :  删除class方法

–toggle():  切换class方法

元素的classList属性返回的是一个{}对象－类数组。

### window.JSON新方法 ###

JSON.parse():把字符串转成json（字符串中的属性要严格的加上引号）

JSON.stringify() :把json转化成字符串（解析完的字符串会自动加上

引号）

JSON.parse()和eval()的区别：

eval()能解析任意的字符串，JSON.parse()只能解析ｊｓｏｎ格式的字符

串，且字符串中的属性要严格的加上引号。所以JSON.parse()安全性会更

高，更适用。

应用：克隆新对象，之前我们利用ｊｓ克隆一个对象时候，需要考虑深拷贝

和浅拷贝，这里就不再需要区分：

```
var a={"m":{"n":"hello"}};  
var aStr=JSON.stringify(a) ;  
var b=JSON.parse(aStr); //实现ｂ对ａ的拷贝         
```

### 内联SVG ###

VG和Canvas的区别：一种使用 XML 描述 2D 图形的语言，Canvas 通过 

JavaScript 来绘制 2D 图形;

canvas：依赖分辨率

不支持事件处理器

弱的文本渲染能力

能够以.png或.jpg格式保存结果图像

最适合图像密集型的游戏，其中的许多对象会被频繁重绘

SVG：不依赖分辨率

支持事件处理器

最适合带有大型渲染区域的应用程序

复杂度高会减慢渲染速度

不合适游戏应用

### 新的input ###

color、date、datetime、datetime-local、email、month、

number、range、search、tel、time、url、week

### WEB存储 ###

localStorage - 没有时间限制的数据存储;//对象存储的数据没有时间限

制。第二天、第二周或下一年之后，数据依然可用。

sessionStorage - 针对一个 session 的数据存储;//针对一个 

session 进行数据存储。当用户关闭当前页面后，数据会被删除

```
if(typeof(Storage)!=="undefined"){//判断是否可以使用web存储
　　localStorage.Name="one";
}       
```

### 应用程序缓存 ###

离线浏览 - 用户可在应用离线时使用它们，速度 - 已缓存资源加载

得更快，减少服务器负载 - 浏览器将只从服务器下载更新过或更改过的资

源。

使用时需要在<html>标签中添加manifest属性，并配置manifest文件;


### Web Worker ###

运行在后台的 JavaScript，不会影响页面的性能;

<center><strong>{{ page.date | date_to_string }}</strong></center>
