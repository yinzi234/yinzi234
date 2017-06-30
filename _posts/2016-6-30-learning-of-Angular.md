---
layout: default
title: AngularJS学习
---

##AngularJS##

AngularJS[1]  诞生于2009年，由Misko Hevery 等人创建，后为

Google所收购。是一款优秀的前端JS框架，已经被用于Google的多款产品

当中。AngularJS有着诸多特性，最为核心的是：MVVM、模块化、自动化双

向数据绑定、语义化标签、依赖注入等等。

AngularJS使用了不同的方法，它尝试去补足HTML本身在构建应用方面的缺

陷。AngularJS通过使用我们称为标识符(directives)的结构，让浏览器

能够识别新的语法。例如：

使用双大括号{{}}语法进行数据绑定；

使用DOM控制结构来实现迭代或者隐藏DOM片段；

支持表单和表单的验证；

能将逻辑代码关联到相关的DOM元素上；

能将HTML分组成可重用的组件。

AngularJS主要考虑的是构建CRUD应用，不适合游戏，图形界面编辑器，这

种DOM操作很频繁也很复杂的应用。

###js文件目录###

###app.js###

项目的配置文件，路由的配置，模块的依赖可以写在这里。demo：

```
var phonecatApp = angular.module('phonecatApp', [  'ngRoute',  'phonecatAnimations',
  'phonecatControllers',  'phonecatFilters',  'phonecatServices','phonecatDirectives']);
  
//路由
phonecatApp.config(['$routeProvider',
function($routeProvider) {
$routeProvider.
when('/phones', {
templateUrl: 'partials/phone-list.html',//模板的相对路径
controller: 'PhoneListCtrl' //使用的控制器名
}).
when('/phones/:phoneId', {
templateUrl: 'partials/phone-detail.html',
controller: 'PhoneDetailCtrl'
}).
otherwise({
redirectTo: '/phones'
});
}]);
```

使用angular.moudle('phonecatApp',[...])进行模块化，

phonecatApp 就是ng－app的值，ng－app指的是从拥有该指令的html标

签开始，将整个控制权交给angular.js去管理，［...］是对模块的依赖，

通俗地讲，就比如［］里面的 'phonecatControllers'，那么之后在

controller.js（后面有讲）就可以直接

```
var phonecatControllers = angular.module('phonecatControllers', []); //'phonecatControllers'此处在app.js有进行模块依赖了，所以这里就这样写
phonecatControllers.controller("控制器名",function($scope){...})
``` 

以往的套路是这样的，

var phonecatApp = angular.moudle("phonecatApp",[]);

然后phonecatApp.controller("控制器名",function(){...})，这样

的话那么我们指令、服务、过滤器都需要写在同一个js文件。当然也是可以

没有错的，但是把所有js代码写在同一个js文件里面，太臃肿了，管理起来

也难！
 
路由的设置也在这里写，路由的知识以后再详细讲，这里只是讲整个项目的

目录。

###controller.js###

项目的控制器文件，所有控制器写在这里。demo：

```
var phonecatControllers = angular.module('phonecatControllers', []);
phonecatControllers.controller("控制器名",['$scope' ,'$http',function($scope,$http){...}]);
```

###services.js###

项目的服务文件，根据angualr的依赖注入机制，可以自己写服务，然后在

写控制器代码时传入，如：phonecatControllers.controller("控制器

名",['$scope' ,'myservice',function($scope,myservice)

{...}]); myservice是自定义的服务，这样就可以注入，在不同控制器调

用同个业务（引入$http等来异步获取数据，因为不同控制器操作的源是一

样的，所以可以封装成一个服务供调用），可以使用自定义服务来进行封

装，供不同控制器注入调用，尽量不要使用$命名，以免冲突出现错误。

demo：

```
var phonecatServices = angular.module('phonecatServices', [...]); //同上所述，［...］为依赖
 
phonecatServices.factory('Phone', function(){
 
　　return ['1882345555','123453222'];
 
});
```

编写服务js，分别有factory、provider、service方法，这里使用

factory，这样的话在controller.js写控制器的时候，就可以注入使用了

###filters.js###

项目过滤器文件，看过大概看了一下angular.js内置的一些过滤器（如

date、curreny等，因为是初学，所有只是大概看了一下，之后会继续学习

深入的），那往往是不够用的，往往我们需要自己自定义一些过滤器，这样

的话我们就可以在我们的模板文件（.html）中引入了，如<input ng-

model='xxx' type="text" onlyNum />或是<span>{{XxXX | 

touuper }}</span>,onlyNum（限制只能输入数字）、touuper（转换成

大写字母）就是我们自定义的过滤器。demo：

```
var phonecatFilter = angular.module('phonecatFilters', []); //同上所述，［...］为依赖
phonecatFilter.filter('touuper', function() {
   return function(input) {
       return input.toUpperCase();
   };
});
```

###directives.js###

项目的指令文件，这里写的是项目中，我们自己自定义的标签，制定的标签

可以引入到模板文件里面使用，其代表含义，我们在directives.js中去定

义，这个也是angualr.js比较有特点的功能，原本的html标签已经很丰富

的了，但是这样的自定义标签可以使htmldom结构中更能自定义话，ng-*就

是指令，可以去打开源码去看，它们都会被编译我们熟悉的属性、html标

签，而指令有着四种形式AEMC,分别是attrs、element、注释、class，

demo：

```
angular.module('phonecatDirectives', []).directive("hello", function() {
return {
 
scope: {} ,//是否具有独立作用域
restrict: 'AEMC',   //定义类型
template: '<div>Hi everyone!</div>',  //模板
replace: true  //是否替换原来的节点
 
link: function(scope,element,attrs,[controller]){　
 
//定义指令的行为，如果不需要则不需引入
 
}
 
compile:function(){
 
//编译指令时的函数
 
}
 
templateUrl: ""  //模版路径
}
});
```

###测试###

写hello world：

```
<!doctype html>
<html ng-app>
    <head>
        <script src="http://code.angularjs.org/angular-1.0.1.min.js"></script>
    </head>
    <body>
        Hello {{'World'}}!
    </body>
</html>
```

就这样hello world就简单地写好了，{{'world'}}这里面就是一个表达

式，这里这个表达式是个字符串，但我们要把它改成Hello * ，World可以

动态改变任意字符串，可以这样写：

```
<!doctype html>
<html ng-app>
    <head>
        <script src="http://code.angularjs.org/angular-1.0.1.min.js"></script>
    </head>
    <body>    
        Your name: <input type="text" ng-model="yourname" placeholder="World">
        <hr>
        Hello  {{ yourname ||'World'}}!
    </body>
</html>
```

ng-model绑定了一个yourname的变量（双向数据绑定），这样'World'即

可以改变成其他的字符串了！那我们还想说把它得到的字符串用alert弹出

来，可以怎么做：

html：

```
<!doctype html>
<html ng-app>
  <head>
    <script src="http://code.angularjs.org/angular-1.0.1.min.js"></script>
    <script src="script.js"></script>
  </head>
  <body>
    <div class="example2" ng-controller="Cntl1">
　　　　<h1>{{init}}</h1>

      Name: <input ng-model="name" type="text"/>
      <button ng-click="greet()">Greet</button>
    </div>
  </body>
</html>

```

js:

```
function Cntl1($window, $scope){
  $scope.name = 'World';//实现数据双向绑定
　$scope.init = 'Hello xiaobin';
  $scope.greet = function() {
    ($window.mockWindow || $window).alert('Hello ' + $scope.name);
  }
}
<!--补充：表达式计算是发生在作用域中的。Javascript默认是以window为作用域的。AngularJS要使用window作用域的话得用$window来指向全局window对象。 比如说，你使用window中定义的alert()方法，在AngularJS表达式中必须写成$window.alert()才行。这是为了防止意外进入全局作用域（各种bug的来源）而设计的。 -->
```

这里可以看到html的模板里面ng-model绑定了一个变量name，js里面的

Cntl1控制器在scope作用域中也定义了一个那么变量$scope.name，这里

就可以很深刻体现出数据的双向绑定了，两处的值的改变都会影响另外一个

的值变化。上面给button绑定了一个ng-click指令，没错，里面的greet

（）函数正是我们在控制器文件里面定义的函数，通过这种方式我们实现了

视图和控制器的交互，至于谁是模板，谁是控制器，上面的代码已经很详

细！

那么如果是有这样的另外要求，需要在视图遍历某个数组，那可以这样做：

html:

```
<!doctype html>
<html ng-app>
  <head>
    <meta charset='utf8'/>
    <script src="http://code.angularjs.org/angular-1.0.1.min.js"></script>
    <script src="script.js"></script>
  </head>
  <body>
    <div ng-controller="Cntl2" class="expressions">
      {{hello}}
      <br>
      Expression:
      <input type='text' ng-model="expr" size="80"/>
      <button ng-click="addExp(expr)">Evaluate</button>
      <ul>
       <li ng-repeat="exprd in exprs">
         [ <a href="" ng-click="removeExp($index)">X</a> ]
         <tt>{{exprd}}</tt> => <span ng-bind="$parent.$eval(exprd)"></span>
        </li>
      </ul>
    </div>
  </body>
</html>
```

js:

```
function Cntl2($scope) { //$scope注入的作用域
  var exprs = $scope.exprs = [];  //这是通过$scope.创建的数组
  $scope.expr = '3*10|currency'; //添加默认模型属性，对应模板的input框中相对应有模型变量的默认值
  $scope.hello = '小斌开始学习angularJs拉！';
  $scope.addExp = function(expr) {
     exprs.push(expr);//压入数组(push)
  };

  $scope.removeExp = function(index) {
    exprs.splice(index, 1); //删除某个数组项(splice)
  };
}

//模型和视图分离，但是他们两者确实是同步的
```

###实例：遍历排序###

这里实现的功能是这样的，在前台遍历phones的对象数组，然后可以按照年

龄和名字排序，也可以通过输入字符串过滤检索。代码如下：

html：

```
<!doctype html>
<html ng-app ng-controller="PhoneListCtrl">
<head>
<meta charset='utf8' />
<title ng-bind="'Google Phone Gallery:' + query"></title> 
<!-- <title ng-bind-template="Google Phone Gallery:{{query}}"></title> -->
<script src="http://code.angularjs.org/angular-1.0.1.min.js"></script>
<script src="script.js"></script>
</head>
<body>
<div class="example2">
Select: 
<select name="select" id="select" ng-model='order'>
<option value="name">名字</option>
<option value="age">年龄</option>
</select>	
Search: <input name="search" type="text" ng-model='query' />
<ul>
<!--迭代器-->
<li ng-repeat='phone in phones | filter:query | orderBy:order'>
{{phone.name}}
<p>{{phone.number}}</p>
</li>
</ul>
</div>
</body>
</html>
```

js：

```
function PhoneListCtrl($scope){
$scope.phones = [
{'name':'xioabin','number':'18824863682','age':'12'},
{'name':'xioalong','number':'18824863683','age':'19'},
{'name':'xiaohua','number':'18824863684','age':'5'},
{'name':'xiaoMING','number':'18824863685','age':'1'},
{'name':'xiaoTU','number':'18824863686','age':'2'},
{'name':'xiaoKE','number':'18824863687','age':'40'},
];
$scope.order = 'name';

}
```

代码不多，但是也有挺多知识点在里面的，首先我们使用no-repeat遍历js

文件里面的phones对象数组，于是后面在html中出现了ng-

repeat='phone in phones | filter:query | orderBy:order'，那

这是这样解释的，遍历phones，按照query过滤，order排序，而filter

和orderBy则是angularJs的迭代器，相应的自带迭代器还有：currency

（货币转换）、json（json格式转换）、date（日期转换）、

lowercase、uppercase（大小写转换）等。而query和order是input中

ng-model绑定的数据，那这样就可以实时拿着条件检索数据。这里有几点

是要讲的：

ng-app    标识以下内容就归angularjs管理

ng-controller 指得是包裹的内容中是在控制器PhoneListCtrl的控制

下，在其作用域下去操作变量和函数

<title ng-bind="'Google Phone Gallery:' + query"></title> 

<title ng-bind-template="Google Phone Gallery:

{{query}}"></title>

这里是两种数据绑定的形式，ng-bind和ng-bind-template，异同上面已

经很明显地体现出来了！当然还有其他的用途，就是有时候我们是这样写的

<span>{{bind}}</span>的，然后在拼命刷新页面的时候，会经常看到

{{bind}}的闪现，那么用ng-bind和ng-bind-template就可以解决了，

像这样<span ng-bind="bind"></span>。

###定义数组###

在控制器文件中直接定义一个数组，让其在模版文件中用ng-repeat指令构

造一个迭代器，定义的数组http://t.cn/RUbL4rP如同以下：

```
$scope.phones = [
        {'name':'xioabin','number':'18824863682','age':'12'},
        {'name':'xioalong','number':'18824863683','age':'19'},
        {'name':'xiaohua','number':'18824863684','age':'5'},
        {'name':'xiaoMING','number':'18824863685','age':'1'},
        {'name':'xiaoTU','number':'18824863686','age':'2'},
        {'name':'xiaoKE','number':'18824863687','age':'40'},
    ];
```

这种形式往往不是我们所要的，我们通常会使用常用ajax技术去获取数据，

在angular也有类似的服务来实现XHR，那就是 $http，使用怎么一个服

务，需要将代码放置在本地服务器或是web站点上，首先先准备phone.json

文件，如下：

```
[

        {"name":"xioabin","number":"18824863682","age":"12"},

        {"name":"xioalong","number":"18824863683","age":"19"},

        {"name":"xiaohua","number":"18824863684","age":"5"},

        {"name":"xiaoMING","number":"18824863685","age":"1"},

        {"name":"xiaoTU","number":"18824863686","age":"2"},

        {"name":"xiaodfs","number":"18824863687","age":"46"},

        {"name":"xiaodfE","number":"18824863682","age":"46"},

        {"name":"xiaobh","number":"18824863680","age":"48"},

        {"name":"xiaogg","number":"18824863687","age":"10"},

        {"name":"xiaouu","number":"18824863686","age":"20"},

        {"name":"xiaoKds","number":"18824863682","age":"30"},

        {"name":"xiaoKEdad","number":"18824863689","age":"60"},

        {"name":"xiaoKb","number":"18824863683","age":"90"},

        {"name":"xiaofa","number":"18824863685","age":"17"}

    ]
```

内容可以自己设置，模版文件代码与之前大同小异：

```
<!doctype html>

<html ng-app ng-controller="PhoneListCtrl">

  <head>

      <meta charset='utf8' />

      <title ng-bind="'Google Phone Gallery:' + query"></title>  

      <!-- <title ng-bind-template="Google Phone Gallery:{{query}}"></title> -->

    <script src="http://code.angularjs.org/angular-1.0.1.min.js"></script>

    <script src="script.js"></script>

  </head>

  <body>

    <div class="example2">

        Select:  

        <select name="select" id="select" ng-model='order'>

            <option value="name">名字</option>

            <option value="age">年龄</option>

        </select>                        

        Search: <input name="search" type="text" ng-model='query' />

         <ul>

         <!--迭代器-->
    <li>
      <span>序号</span>&nbsp;&nbsp; 
      <span>姓名</span>&nbsp;&nbsp; 
      <span>号码</span>&nbsp;&nbsp; 
      <span>年龄</span>
    </li>
         <li ng-repeat='phone in phones | filter:query | orderBy:order'>

               <span>{{$index+1}}</span>&nbsp;&nbsp;  <span>{{phone.name}}</span>&nbsp; &nbsp; <span>{{phone.number}}</span>&nbsp; &nbsp; <span>{{phone.age}}</span>

         </li>

         </ul>

    </div>

  </body>

</html>

```

不同的就是控制器文件的不同，如下：

```
//注入服务$http
function PhoneListCtrl($scope,$http){
      $http.get("phone.json").success(function(data, status, headers, config) {
          if(status==200){ $scope.phones = data;  }
        console.log(status+","+headers+","+config);
        // alert(JSON.stringify(data));
      });
        $scope.order = 'name';
}
```

这里传入了一个$http，那么我们就可以通过$http.get(路径).success

(function(data,status){/*成功获取数据，之后该干嘛？*/})，data

是返回的数据，status是状态码，header和config可以打印出来看一下，

应该是一些配置和头部吧！这样$scope.phones就与之前一样是一个数组

了！

官网的$http是这样的形式，可以参考着写：

```
$http({  
        url:'...',
           method:'...',
           data:'...',
          params:'...',
          cache:'...'
      })
         .success(function(){....})
         .error(function() {.....});
```

如果我们的控制器按上面那样写的话，在压缩代码时候会出错，那么有这两

种方法可以解决这个问题：

为了克服压缩引起的问题，只要在控制器函数里面给$inject属性赋值一个

依赖服务标识符的数组，就像被注释掉那段最后一行那样：

PhoneListCtrl.$inject = ['$scope', '$http'];

另一种方法也可以用来指定依赖列表并且避免压缩问题——使用Javascript

数组方式构造控制器：把要注入的服务放到一个字符串数组（代表依赖的名

字）里，数组最后一个元素是控制器的方法函数：

var PhoneListCtrl = ['$scope', '$http', function($scope, 

$http) { /* constructor body */ }];

这就是angularjs的依赖注入了！当控制器构造的时候，AngularJS的依赖

注入器会将这些服务注入到你的控制器中。当然，依赖注入器也会处理所需

服务可能存在的任何传递性依赖（一个服务通常会依赖于其他的服务）。

注意不要使用‘$’前缀来命名你自己的服务和模型（就是自己可以定义自己

的服务，像$http），否则可能会产生名字冲突。


<center><strong>{{ page.date | date_to_string }}</strong></center>
