---
layout: default
title: Ajax学习
---

##Ajax##

Ajax 是 Asynchronous JavaScript and XML（以及DHTML 等）的缩写.

下面是 Ajax 应用程序所用到的基本技术：

• HTML 用于建立 Web 表单并确定应用程序其他部分使用的字段。 

• JavaScript 代码是运行 Ajax 应用程序的核心代码，帮助改进与服务

器应用程序的通信。 

• DHTML 或 Dynamic HTML，用于动态更新表单。我们将使用 div、

span 和其他动态 HTML 元素来标记 HTML。 

• 文档对象模型 DOM 用于（通过 JavaScript 代码）处理 HTML 结构和

（某些情况下）服务器返回的 XML。

从上面可以看出,Ajax不是什么新的技术,而是几个老的技术通过新的方法结

合起来,从而实现了新的效果!很多事物都是多元化的,可以说Ajax是一个新

技术，也可以说Ajax是一个新的思路，一个新的架构！

###Ajax的基本工作原理###

在一般的 Web 应用程序中，用户填写表单字段并单击 Submit 按钮。然后

整个表单发送到服务器，服务器将它转发给处理表单的脚本（通常是 PHP 

或 Java，也可能是 CGI 进程或者类似的东西），脚本执行完成后再发送

回全新的页面。该页面可能是带有已经填充某些数据的新表单的 HTML，也

可能是确认页面，或者是具有根据原来表单中输入数据选择的某些选项的页

面。当然，在服务器上的脚本或程序处理和返回新表单时用户必须等待。屏

幕变成一片空白，等到服务器返回数据后再重新绘制。这就是交互性差的原

因，用户得不到立即反馈，因此感觉不同于桌面应用程序。

Ajax 基本上就是把 JavaScript 技术和 XMLHttpRequest 对象放在 

Web 表单和服务器之间。当用户填写表单时，数据发送给一些 

JavaScript 代码而不是 直接发送给服务器。相反，JavaScript 代码捕

获表单数据并向服务器发送请求。同时用户屏幕上的表单也不会闪烁、消失

或延迟。换句话说，JavaScript 代码在幕后发送请求，用户甚至不知道请

求的发出。更好的是，请求是异步发送的，就是说 JavaScript 代码（和

用户）不用等待服务器的响应。因此用户可以继续输入数据、滚动屏幕和使

用应用程序。

然后，服务器将数据返回 JavaScript 代码（仍然在 Web 表单中），后

者决定如何处理这些数据。它可以迅速更新表单数据，让人感觉应用程序是

立即完成的，表单没有提交或刷新而用户得到了新数据。JavaScript 代码

甚至可以对收到的数据执行某种计算，再发送另一个请求，完全不需要用户

干预！这就是 XMLHttpRequest 的强大之处。它可以根据需要自行与服务

器进行交互，用户甚至可以完全不知道幕后发生的一切。结果就是类似于桌

面应用程序的动态、快速响应、高交互性的体验，但是背后又拥有互联网的

全部强大力量。


###XMLHttpRequest 对象###

open()：建立到服务器的新请求。

send()：向服务器发送请求.

abort()：退出当前请求。

readyState：提供当前 HTML 的就绪状态。

responseText：服务器返回的请求响应文本。

由于前两年的浏览器大战，使得各种浏览器获得 XMLHttpRequest 对象采

用的方法有所不同。

支持多种浏览器的方式创建 XMLHttpRequest 对象

```
var xmlHttp = false;
try {
xmlHttp = new ActiveXObject("Msxml2.XMLHTTP");
} catch (e) {
try {
    xmlHttp = new ActiveXObject("Microsoft.XMLHTTP");
} catch (e2) {
    xmlHttp = false;
}
}
if (!xmlHttp && typeof XMLHttpRequest != 'undefined') {
xmlHttp = new XMLHttpRequest();
}
```

1. 建立一个变量 xmlHttp 来引用即将创建的 XMLHttpRequest 对象。 

2. 尝试在 Microsoft 浏览器中创建该对象： 

   尝试使用 Msxml2.XMLHTTP 对象创建它。 

   如果失败，再尝试 Microsoft.XMLHTTP 对象。 

3. 如果仍然没有建立 xmlHttp，则以非 Microsoft 的方式创建该对

象。 

xmlHttp 应该引用一个有效的 XMLHttpRequest 对象，无论运行什么样

的浏览器。

###Ajax中的请求/响应###

发出请求：Ajax 应用程序中基本相同的流程：

1. 从 Web 表单中获取需要的数据。 

2. 建立要连接的 URL。 

3. 打开到服务器的连接。 

4. 设置服务器在完成后要运行的函数。 

5. 发送请求。

```
function callServer() {
// Get the city and state from the web form
var city = document.getElementById("city").value;
var state = document.getElementById("state").value;
// Only go on if there are values for both fields
if ((city == null) || (city == "")) return;
if ((state == null) || (state == "")) return;
// Build the URL to connect to
var url = "/scripts/getZipCode.aspx?city=" + escape(city) + "&state=" + escape(state);
// Open a connection to the server
xmlHttp.open("GET", url, true);
// Setup a function for the server to run when it's done
xmlHttp.onreadystatechange = updatePage;
// Send the request
xmlHttp.send(null);
}
```

处理响应：

readyState可能返回的值：

0：请求未初始化（还没有调用 open()）。

1：请求已经建立，但是还没有发送（还没有调用 send()）。

2：请求已发送，正在处理中（通常现在可以从响应中获取内容头）。

3：请求在处理中；通常响应中已有部分数据可用了，但是服务器还没有完成响应的生成。

4：响应已完成；您可以获取并使用服务器的响应了。

必须知道两点：

1.什么也不要做，直到 xmlHttp.readyState 属性的值等于 4。

2.服务器将把响应填充到 xmlHttp.responseText 属性中。

响应函数：

```
function updatePage() {
  if (xmlHttp.readyState == 4) {
    var response = xmlHttp.responseText;
    document.getElementById("zipCode").value = response;
  }
}
```

###创建一个XMLHttpRequest对象###

```
 var xhr =null;
        if(window.XMLHttpRequest){
            xhr = new XMLHttpRequest();
        }else{
            xhr = new ActiveXObject('Microsoft.XMLHTTP');

        }
//这里进行的是针对IE浏览器的兼容性处理,在IE中,我们的xmlhttprequest对象就变成了activeobject,而且里边的参数是不能少的,IE就是这样倔强

```


###ajax方法参数###

1.url: 

要求为String类型的参数，（默认为当前页地址）发送请求的地址。

2.type: 

要求为String类型的参数，请求方式（post或get）默认为get。注意其他

http请求方法，例如put和delete也可以使用，但仅部分浏览器支持。

3.timeout: 

要求为Number类型的参数，设置请求超时时间（毫秒）。此设置将覆盖

$.ajaxSetup()方法的全局设置。

4.async: 

要求为Boolean类型的参数，默认设置为true，所有请求均为异步请求。如

果需要发送同步请求，请将此选项设置为false。注意，同步请求将锁住浏

览器，用户其他操作必须等待请求完成才可以执行。

5.cache: 

要求为Boolean类型的参数，默认为true（当dataType为script时，默认

为false），设置为false将不会从浏览器缓存中加载请求信息。

6.data: 

要求为Object或String类型的参数，发送到服务器的数据。如果已经不是

字符串，将自动转换为字符串格式。get请求中将附加在url后。防止这种自

动转换，可以查看　　processData选项。对象必须为key/value格式，例

如{foo1:"bar1",foo2:"bar2"}转换为&foo1=bar1&foo2=bar2。如果

是数组，JQuery将自动为不同值对应同一个名称。例如{foo:

["bar1","bar2"]}转换为&foo=bar1&foo=bar2。

7.dataType: 

要求为String类型的参数，预期服务器返回的数据类型。如果不指

JQuery将自动根据http包mime信息返回responseXML或responseText，

并作为回调函数参数传递。可用的类型如下：

xml：返回XML文档，可用JQuery处理。

html：返回纯文本HTML信息；包含的script标签会在插入DOM时执行。

script：返回纯文本JavaScript代码。不会自动缓存结果。除非设置了

cache参数。注意在远程请求时（不在同一个域下），所有post请求都将转

为get请求。

json：返回JSON数据。

jsonp：JSONP格式。使用SONP形式调用函数时，例如myurl?

callback=?，JQuery将自动替换后一个“?”为正确的函数名，以执行回调

函数。

text：返回纯文本字符串。

8.beforeSend：

要求为Function类型的参数，发送请求前可以修改XMLHttpRequest对象

的函数，例如添加自定义HTTP头。在beforeSend中如果返回false可以取

消本次ajax请求。XMLHttpRequest对象是惟一的参数。

```
            function(XMLHttpRequest){
               this;   //调用本次ajax请求时传递的options参数
            }
```

9.complete：

要求为Function类型的参数，请求完成后调用的回调函数（请求成功或失

败时均调用）。参数：XMLHttpRequest对象和一个描述成功请求类型的字

符串。

```
          function(XMLHttpRequest, textStatus){
             this;    //调用本次ajax请求时传递的options参数
          }
```

10.success：

要求为Function类型的参数，请求成功后调用的回调函数，

有两个参数。
         (1)由服务器返回，并根据dataType参数进行处理后的数据。
         (2)描述状态的字符串。

```
         function(data, textStatus){
            //data可能是xmlDoc、jsonObj、html、text等等
            this;  //调用本次ajax请求时传递的options参数
         }
```

11.error:

要求为Function类型的参数，请求失败时被调用的函数。该函数有3个参

数，即XMLHttpRequest对象、错误信息、捕获的错误对象(可选)。ajax事

件函数如下：

```
       function(XMLHttpRequest, textStatus, errorThrown){
          //通常情况下textStatus和errorThrown只有其中一个包含信息
          this;   //调用本次ajax请求时传递的options参数
       }
```

12.contentType：

要求为String类型的参数，当发送信息至服务器时，内容编码类型默认

为"application/x-www-form-urlencoded"。该默认值适合大多数应用

场合。

13.dataFilter：

要求为Function类型的参数，给Ajax返回的原始数据进行预处理的函数。

提供data和type两个参数。data是Ajax返回的原始数据，type是调用

jQuery.ajax时提供的dataType参数。函数返回的值将由jQuery进一步处

理。

```
            function(data, type){
                //返回处理后的数据
                return data;
            }
```

14.dataFilter：

要求为Function类型的参数，给Ajax返回的原始数据进行预处理的函数。

提供data和type两个参数。data是Ajax返回的原始数据，type是调用

jQuery.ajax时提供的dataType参数。函数返回的值将由jQuery进一步处

理。

```
            function(data, type){
                //返回处理后的数据
                return data;
            }
```

15.global：

要求为Boolean类型的参数，默认为true。表示是否触发全局ajax事件。

设置为false将不会触发全局ajax事件，ajaxStart或ajaxStop可用于控

制各种ajax事件。

16.ifModified：

要求为Boolean类型的参数，默认为false。仅在服务器数据改变时获取新

数据。服务器数据改变判断的依据是Last-Modified头信息。默认值是

false，即忽略头信息。

17.jsonp：

要求为String类型的参数，在一个jsonp请求中重写回调函数的名字。该值

用来替代在"callback=?"这种GET或POST请求中URL参数里

的"callback"部分，例如{jsonp:'onJsonPLoad'}会导致

将"onJsonPLoad=?"传给服务器。

18.username：

要求为String类型的参数，用于响应HTTP访问认证请求的用户名。

19.password：

要求为String类型的参数，用于响应HTTP访问认证请求的密码。

20.processData：

要求为Boolean类型的参数，默认为true。默认情况下，发送的数据将被转

换为对象（从技术角度来讲并非字符串）以配合默认内容类

型"application/x-www-form-urlencoded"。如果要发送DOM树信息或

者其他不希望转换的信息，请设置为false。

21.scriptCharset：

要求为String类型的参数，只有当请求时dataType为"jsonp"或

者"script"，并且type是GET时才会用于强制修改字符集(charset)。通

常在本地和远程的内容编码不同时使用。

###XML和json###

当我们完成了发送请求并且从后端获取了数据后,我们应该再进一步的去思

考,那么我可以指定从后端传过来的数据吗?那么接下来就出现了我们的json

和XML数据格式,这两种都是我们进行前端和后端进行传送数据的格式,那么

我们先来看一下XML,XML数据其实你也可以看做我们的html标签,只不过它

是我们可以自定义的标签,你可以给它的标签名取的很有意义,那样就会很方

便你去使用:

```
<china>
    <province name='河南'>
     <city>郑州</city>
    </province>
    
</china>
//这就是一个简单的XML格式的数据,我们对于这样的数据进行操作的时候可以使用js操作DOM对象的方法,
//xml数据必须有一个根节点
```

另外一种经常使用的数据格式就是json了,json是一种独立于语言的数据格

式,就是说它是可以在很多种语言中使用的,不限定于某一个特定的语言,而

且它相较于xml来说代码量较小,而且易于解析,xml就有些数据量庞大解析

不便了,但是碍于json出现的较晚,所以现在大部分人还是使用的xml,无奈

与很多后端数据都是用xml存储,json的格式有些类似于我们的JavaScript

中的对象字面量:

```
{"name":"james",
  "hobby":"basketball",
    "son" : {"littleson":"er","bigson":"san"}
}//这种就是一个简单的json格式数据,json数据代码量较小,但是可读性来说

```
相较于xml有些dom一样的解析方法,xml的解析在js中最长用的解析方法就

是json.parse()了,而将js对象转化为json对象我们使用

json.stringify(),当然了,json和xml的区别还有很多

###ajax在jQuery中###

实例：

```
$.ajax({
                    type:"post",  //请求方式
                    url:"a.php", //服务器的链接地址
                    dataType:"json", //传送和接受数据的格式
                    data:{
                        username:"james",
                        password:"123456"
                    },
                    success:function(data){//接受数据成功时调用的函数
                       console.log(data);//data为服务器返回的数据
                    },
                    error:function(request){//请求数据失败时调用的函数
                        alert("发生错误:"+request.status);
                    }
});
```

###跨域请求###

使用ajax请求的都是在本地和我们同源的文件,因为JavaScript在设计时

出于安全方面的考虑,不允许跨域请求

JSONP(JSON with Padding)是 JSON 的一种“使用模式”，可用于解决主

流浏览器的数据访问问题,因为html的<script>元素标签可以从其他来源动

态的加载数据,所以我们可以利用<script>标签来实现跨域请求,这种方式

就成为jsonp,当然了,jsonp和json可不是一回事,json是数据的一种传输

格式,而jsonp是一种跨域请求方式

```
<html>
<body>
    <script src='test.js'></script>
</body>
</html>
//script中的src没有同源限制,它可以加载其他任意文件.而jsonp利用的就是这一个功能展开的
```

例子

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jsonp</title>
</head>
<body>
<script src="http://cdn.weather.hao.360.cn/api_weather_info.php?app=hao360&_jsonp=weather&code=131111"></script>
//这是360天气的一个天气预报的一个api接口,

</body>
</html>
```

jQuery中jsonp的使用:

```
   $.ajax({
                type:'get',
                url:天气预报接口,
                async:'true', // 是否为异步调用
                dataType:'jsonp', 指定数据传输方式
                jsonp:'jsoncallback',     //回调函数名的key值 可省略
                jsonpCallback:'XBox',       //回调函数的函数名 可省略
                success:function(data){
                   //成功后执行的函数,data就是我们要获取的函数值
                },
                error  :function(){
                     //失败时执行的函数
               }
```


<center><strong>{{ page.date | date_to_string }}</strong></center>
