---
layout: default
title: Vue学习
---

## Vue ##

数据驱动的组件，为现代化的 Web 界面而生。

Vue.js（读音 /vjuː/, 类似于 view）是一个构建数据驱动的 web 界面

的库。Vue.js 的目标是通过尽可能简单的 API 实现响应的数据绑定和组

合的视图组件。

Vue.js 自身不是一个全能框架——它只聚焦于视图层。因此它非常容易学

习，非常容易与其它库或已有项目整合。另一方面，在与相关工具和支持库

一起使用时，Vue.js 也能完美地驱动复杂的单页应用。

### Vue的使用教程 ###

### Reactive Directives（响应式指令） ###
Reactive Directives可以绑定在Vue实例或者在Vue实例上下文中求值的表达式上，当绑定的对象发生改变时，指令中的update()会在下一个系统单位时间发生异步响应，我们来看看具体的用法：

v-text:更新元素的textContent，事实上在html中{{mustache}}形式的插入值也会被编译为针对一个textNode的v-text指令。

 

v-html:更新元素的innerHTML，由于可能插入恶意代码，使用时要注意保证来源安全。

 

v-show:根据绑定值的true或false来决定所在元素在网页中正常显示还是显示为空。

 

v-class：这个指令有一个可选参数，无参数时将绑定值（一般为class名）添加到所在元素的classlist当中，并且一旦检测绑定值有改动，便随之改变classlist里对应的class；提供参数时参数的true或false将决定绑定值（class）是否被添加到所在元素的classlist中，示例如下：

```
<span v-class="
  red    : hasError,
  bold   : isImportant,
  hidden : isHidden
"></span>
```

v-attr:更新所在元素的某些属性（由参数表示）。

```
<canvas v-attr="width:w, height:h"></canvas>
``` 

v-style:更新所在元素的样式，会智能添加浏览器供应商前缀，方便我们书写样式。这个指令有一个可选参数，无参数时，若绑定值为String则将绑定值设置为元素的style.cssText，若绑定值为Object则将Object中的样式键值对放入元素的style object当中；

```
<div v-style="myStyles"></div>
```

```
// myStyles can either be a String:
"color:red; font-weight:bold;"
// or an Object:
{
  color: 'red',
  // both camelCase and dash-case works
  fontWeight: 'bold',
  'font-size': '2em'
}
```

提供参数时，参数指明了css属性的对应值:

```
<div v-style="
  top: top + 'px',
  left: left + 'px',
  background-color: 'rgb(0,0,' + bg + ')'
"></div>
```

v-on:为元素添加并更新事件监听器，参数可以是一个处理函数或者一个函数语句。

```
<div id="demo">
  <a v-on="click: onClick">Trigger a handler</a>
  <a v-on="click: n++">Trigger an expression</a>
</div>
```

我们可以为处理函数提供参数，其中this指的是当前的ViewModel，如下例中通过传入this参数改变元素的text值：

```
<ul id="list">
  <li v-repeat="items" v-on="click: toggle(this)">{{text}}</li>
</ul>
```

```
new Vue({
  el: '#list',
  data: {
    items: [
      { text: 'one', done: true },
      { text: 'two', done: false }
    ]
  },
  methods: {
    toggle: function (item) {
      item.done = !item.done
    }
  }
})
```

我们还可以传入$event表示触发处理函数的DOM事件，如下例传入$event阻止事件冒泡：

<button v-on="click: submit('hello!', $event)">Submit</button>
复制代码

```
{
  methods: {
    submit: function (msg, e) {
      e.stopPropagation()
    }
  }
}
```

在监听键盘事件时由于要判断按键值，可以结合filter写成如下两种形式：

```
<!-- only call vm.submit() when the keyCode is 13 -->
<input v-on="keyup:submit | key 13">
<!-- same as above -->
<input v-on="keyup:submit | key enter">
```

当ViewModel销毁时，v-on绑定的事件会自动消除，我们不必亲自去清理这些绑定事件，这也防止了内存的泄露。

 

v-model:为表单元素创建一个双向绑定

 

v-if:根据绑定值的true或false来插入或移除元素，如例子中我们将根据test的正确与否决定两个<p>元素是否插入<template>当中

```
<template v-if="test">
  <p>hello</p>
  <p>world</p>
</template>
``` 

v-repeat:为绑定数组或对象中的每一个item创建一个子ViewModel，或者为绑定的数字值创建对应数量的子ViewModel。并根据绑定值的改变随时更新。没有提供参数时子ViewModel会直接使用绑定数组中的分配单元作为它的$data，如果值不是一个对象，则会创建一个数据包装对象，而值会被设置在别名为$value的 key 上。

```
<ul>
  <li v-repeat="users">
    {{name}} {{email}}
  </li>
</ul>
```

如果提供了参数，我们将创建一个数据包装对象，将参数作为对象的key，从而访问对象模板中的属性：

```
<ul>
  <li v-repeat="user : users">
    {{user.name}} {{user.email}}
  </li>
</ul>
```

v-with：这个指令只能结合接下来讲到的v-component指令使用，作用是让子ViewModel可以继承父ViewModel的数据，我们可以传入父ViewModel的属性对象或单个属性，在子ViewModel中访问：

```
// parent data looks like this
{
  user: {
    name: 'Foo Bar',
    email: 'foo@bar.com'
  }
}
```

继承对象：

```
<my-component v-with="user">
  <!-- you can access properties without `user.` -->
  {{name}} {{email}}
</my-component>
```

继承单个属性：

```
<my-component v-with="myName: user.name, myEmail: user.email">
  <!-- you can access properties with the new keys -->
  {{myName}} {{myEmail}}
</my-component>
```

v-events：这个指令也只能结合接下来讲到的v-component指令使用，它使得父ViewModel能够监听子ViewModel上的事件，我们要注意区分v-on与v-events,v-events监听的是通过vm.$emit()创建的 Vue 组件系统事件，而不是 DOM 事件。我们举例说明：

```
<!-- inside parent template -->
<div v-component="child" v-events="change: onChildChange"></div>
```

当子ViewModel调用this.$emit('change', …)时会触发父ViewModel的onChildChange()方法，并且把emit函数中附加的参数传给onChildChange()方法。

### Literal Directives(字面指令) ###

字面指令并没有绑定到某一个对象上，字面指令是把它们的参数作为纯字符串传给bind()函数中执行一次，字面指令可以接受{{mustache}}表达式，但是该表达式只会在编译阶段执行一次，不会绑定数据的改变：

下面看一看具体的api：
v-component：之前提到过，这是使用我们提前声明并注册好的组件构造器将当前元素编译为子ViewModel，从而实现数据继承，之后的文章会详细介绍组件系统。

 

v-ref：在父ViewModel中创建子ViewModel的引用，方便父ViewModel中的$对象访问子组件：

```
<div id="parent">
  <div v-component="user-profile" v-ref="profile"></div>
</div>
var parent = new Vue({ el: '#parent' })
// 访问子组件
var child = parent.$.profile
```

这个指令只能与v-component和v-repeat一起使用，与v-repeat一起使用时，其value是与绑定数据数组对应的子组件数组。

 

v-el：为当前dom元素创建一个引用，供其自身vue实例使用，例如<div v-el="hi">可以使得vm.$$.hi访问到该dom元素

 

v-partial：将当前dom元素中的innerHTML替换为事先注册的partial，有两种写法，{{ mustache}}可以让dom元素随数据改变而更新:

 
```
<!-- content will change based on vm.partialId -->
<div v-partial="{{partialId}}"></div>
```

另一种写法则没有数据跟随更新的效果：

```
<div>{{> my-partial}}</div>
```

v-transition：为当前dom元素在指定参数值作用时添加动画效果
 
### Empty Directives(字面指令) ###
v-pre：这个指令是通知编译器跳过当前dom元素和其所有子元素，这是为了在我们编程过程中对无需编译的元素节省编译时间

 

v-cloak：在当前元素编译完成之前改指令都会存在，我们一般使用这个指令来在元素编译未完成时隐藏原始的 {{ Mustache }} 模板，可以在css中这样写：

```
[v-cloak] { display: none }
```


### computed计算属性函数中不能使用vm变量 ###

在计算属性的函数中，不能使用Vue构造函数返回的vm变量，因为此时vm还未返回，依然处于Vue内部构造函数过程中，遂只能使用this来代替vm。
若要使用typescript，可使用以下方法来实现代码智能感知

```
vm = vm || this;
```

另：其他不能用vm变量，只能使用this变量的地方，都可以通过此方法来获得Typescript的智能感知和代码语法检查，比如mounted生命周期系列函数等。
不过模板里的vm引用Typescript无能为力，只能等待ts支持vue的jsx语法了

### 计算属性中不能引用其他计算属性？ ###

官方教程中没有找到相关说明(应该是我没找到)，从使用角度而言大致可以总结出以下结论：

计算属性必须引用（依赖）非计算属性或固定值。（见demo1）
计算属性若引用（依赖）其他计算属性，则被引用的计算属性必须引用非计算属性或固定值（见demo2）
计算属性可循环依赖，但最终依赖链上的最上游的计算属性，必须引用非计算属性或固定值。
DEMO1：官方标准用法，计算属性引用非计算属性：

```
var vm = new Vue({
    el: "#app",
    data: {
        dataVal: "xxcanghai"
    },
    computed: {
        computedVal1: function () {
            //标准用法，计算属性引用非计算属性
            return this.dataVal + "_1";//输出 xxcanghai_1
        }
    }
});
```

DEMO2：计算属性链式依赖其他计算属性，则依赖链头必须引用非计算属性或固定值

```
var vm = new Vue({
    el: "#app",
    data: {
        dataVal: "xxcanghai"
    },
    computed: {
        computedVal1: function () {
            return this.dataVal + "_1";
        },
        computedVal2: function () {
            //合法，计算属性computedVal2引用computedVal1，computedVal1再引用dataVal
            return this.computedVal1 + "_2";//输出 xxcanghai_1_2
        }
    }
});
```

原因很容易理解，如果最终没有引用或依赖任何非计算属性，那么计算属性在计算时会陷入死循环。

### vue2.0中若使用组件嵌套，则在父组件执行\$forceUpdate()之前模板中\$children为空数组 ###

触发这个问题有以下几个前提：

vue版本为2.0版本，1.0无此问题。
使用组件嵌套，在父组件的模板中访问$children变量
在渲染完成后没有再将$children变量写入过父组件的data变量（或其他vm数据）
就会触发此问题。

```
<!--父组件HTML模板-->
<div id="app">
   <div>{{$children.length}}</div> <!--此处显示0，应该为3-->
   <child></child>
   <child></child>
   <child></child>
</div>

//子组件代码
Vue.component("child", {
    template: "<div>child</div>",
});

//父组件声明
new Vue({
    el: "#app",
});
```

如下：
0
child
child
child

解决方案1：使用\$forceUpdate()

注册父组件的mounted方法，执行$forceUpdate()

```
<div id="app">
   <div>{{$children.length}}</div>
   <child></child>
   <child></child>
   <child></child>
</div>

Vue.component("child", {
    template: "<div>child</div>",
});

new Vue({
    el: "#app",
    mounted: function () {
        this.$forceUpdate();//强制重新绘制
    }
});
```

$children正确了：
3
child
child
child

解决方案2：使用vm的变量代替\$children

注册父组件的mounted方法，将$children赋值给自定义的vm的变量。
同时模板中使用自定义的变量来代替默认的$children

```
<div id="app">
   <div>{{child.length}}</div> <!--使用自定义的child对象-->
   <child></child>
   <child></child>
   <child></child>
</div>

Vue.component("child", {
    template: "<div>child</div>",
});

var vm = new Vue({
    el: "#app",
    data: {
        child: []
    },
    mounted: function () {
        this.child = this.$children;//手动将$children对象赋值给自定义child变量
    }
});
```

如下：
3
child
child
child

至于导致此问题的原因只能通过阅读vue2.0版本的源码才能了解了。

### 若父组件的template或render函数中无引用slot元素，则\$children恒等于空数组 ###

此问题关联上面第3个问题。
触发此问题的前提：

vue2.0版本
父组件和子组件都直接写在调用方模板中
在模板中访问$children变量
已经解决在上述问题3中强制刷新的问题

```
<div id="app">
    <!--子组件直接写在调用方的模板中-->
   <parent>
       <child></child>
       <child></child>
       <child></child>
   </parent>
</div>

//父组件
Vue.component("parent", {
    template: "<p>parent child:{{$children.length}} </p>",//模板中无slot元素
    mounted(){
        this.$forceUpdate();
    }
});
Vue.component("child", {
    template: "<div>child</div>"
});

var vm = new Vue({
    el: "#app"
});
```

parent child:0

解决方案1:父组件模板包含slot元素

在父组件的模板中加入slot元素。或在render函数中引用了this.$slots.default变量

```
Vue.component("parent", {
    template: "<p>parent child:{{$children.length}} <slot></slot></p>",
    mounted(){
        this.$forceUpdate();
    }
});
```

parent child:3
child
child
child


解决方案2：在父组件模板中编写子组件定义

此解决方案要修改此问题的复现第2要素，即子组件定义从调用方改为写到父组件的模板中也可解决此问题。

```
<div id="app">
   <parent>
   </parent>
</div>

Vue.component("parent", {
    //直接在父组件中写明调用子组件标签
    template: "<p>parent child:{{$children.length}}\
                   <child></child>\
                   <child></child>\
              </p>",
    mounted(){
        this.$forceUpdate();
    }
});
Vue.component("child", {
    template: "<div>child</div>",
});

var vm = new Vue({
    el: "#app",
    data: {
        child: []
    }
});
```

parent child:2
child
child

此方法虽然可以解决问题，但是有时我们直接把子组件写在调用方会更方便更利于理解，比如Tab与TabPage组件。
如下Tab组件代码，可能更符合一般人的使用思维：

```
<div id="app">
   <tab>
       <tab-page>Page1</tab-page>
       <tab-page>Page2</tab-page>
       <tab-page>Page3</tab-page>
   </tab>
</div>
```

### Vue的组件化实践 ###

组件（Component）是 Vue.js 最强大的功能之一。组件可以扩展 HTML 元素，封装可重用的代码。在较高层面上，组件是自定义元素，Vue.js 的编译器为它添加特殊功能。在有些情况下，组件也可以是原生 HTML 元素的形式，以 is 特性扩展。

使用上文提到的官方命令行工具：
目前可供使用的模板包括（模板名-说明）：

webpack - A full-featured Webpack + vue-loader setup with hot reload, linting, testing & css extraction.（全功能的 Webpack + vue-loader 设置，包括热加载，静态检测，测试，css 提取）
webpack-simple - A simple Webpack + vue-loader setup for quick prototyping.（一个简易的 Webpack + vue-loader 设置，以便于快速开始）
browserify - A full-featured Browserify + vueify setup with hot-reload, linting & unit testing.（全功能的 Browserify + vueify 设置，包括热加载，静态检测，单元测试）
browserify-simple - A simple Browserify + vueify setup for quick prototyping.（一个简易的 Browserify + vueify 设置，以便于快速开始）
simple - The simplest possible Vue setup in a single HTML file

<center><strong>{{ page.date | date_to_string }}</strong></center>
