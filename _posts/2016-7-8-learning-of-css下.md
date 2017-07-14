---
layout: default
title: css学习上
---

## 叠层 ##

概念：CSS中的层叠就是让多个来源的样式叠加在一起，然后结合样式的特殊性（后面详

细介绍）、继承性，确定最终应用的样式。

样式的来源分五种：

1、浏览器默认的样式；

2、用户自定义样式。一些页面中会提供一些让用户自定义字体大小颜色等的快捷键；

3、外部样式，即<link>引用的CSS后缀文件；

4、内部样式，即写在<style></style>标签内的样式；

5、内联样式，即直接写在style属性内的样式（现在的网页设计强调结构、表现、行为

三者分离，所以这个还是少用为好。我会强迫性移除内联样式的，哈哈）；

CSS权威指南中对样式来源的分类分成三种：

1、创作人员（上面提到的第3、4、5点都可归到这一点）

2、读者（用户自定义样式）

3、用户代理（这个就是上面所说的浏览器默认样式了）

例子：

```
<!DOCTYPE html>
<html>
<head>
<link rel="stylesheet" href="style.css" type="text/css">
<style>
    #p1 #p2{
        color:yellow;
    }
    .div1 .div2 #p1{
        color:green;
    }
    .div1 .div2 p{
        color:gray;
    }
    .div1 .div2 .impo{
        color:green;
    }
    .impo{
        color: brown !important;
    }
</style>
</head>
<body>
    <div class="div1">
        <div class="div2">
            <p id="p1">Hello  world</p>
            <p id="p2" style="color: red">Hello, how are you!</p>
            <p class="impo">I'm important!</p>
        </div>
    </div>
</body>
</html>

Style.css文件的代码：
.div1 .div2 #p1{
    color: blue;
}
```

### 层叠规则 ###

1、找出所有相关的规则，这些规则都包含与一个给定元素匹配的选择器。

2、按显式权重对应用到该元素的所有声明进行排序，有!important标志的声明的权重

要高于不带!important标志的声明。

3、按来源对应用到给定元素的所有声明进行排序。正常情况下，创作人员的样式要胜过

读者的样式。有!important标志的的读者样式要强于所有其他样式，包括有!

important标志的创作人员样式。创作人员的样式和读者样式斗都比用户代理的默认样

式强。

4、按特殊性对应用到给定元素的所有声明进行排序，有较高特殊性的元素权重要大于有

较低特殊性的元素。

5、按出现顺序对应用到给定元素的所有声明进行排序，后面出现的声明权重要大于前面

出现的声明，即后定义的样式会覆盖前面定义的样式。

简单总结：找出一个给定元素的所有声明后，先按显式权重和来源进行排序。如果相

同，则比较特殊性。若再相同，则比较顺序。

根据以上的知识，我们很明确知道了上面的例子三行文字的颜色是什么了：

第一行是文字的颜色是green；第二行文字的颜色是red；第三行文字颜色是brown。

### 选择器的特殊性 ###

1、对于内联样式，特殊性首位加1，即1，0，0，0。

2、对于选择器中出现的ID属性值，加0，1，0，0， 有多少个ID值就在第二位加几位。

3、对于选择器中出现的类属性值，属性选择及伪类，加0，0，1，0，共出现多少个就

在第三位加几位。

4、对于选择器中出现的元素，以及伪元素，加0，0，0，1，共出现多少个就在第四位

加几位。

5、通配符对特殊性没有任何贡献，即特殊性是0，0，0，0。

6、结合符没有特殊性，连0特殊性也没有。

7、继承的CSS完全没有特殊性，连0特殊性也没有（CSS中的继承是有选择性的，并不是

全部CSS都继承，像边框属性就不会继承）。

注：伪元素选择器包含以下几种：

1、:first-line；  用于向文本的首行设置特殊样式；

2、:first-letter；  用于向文本的首字母设置特殊样式；

3、:before；   可以在元素的内容前面插入新内容；

4、:after；   可以在元素的内容之后插入新内容；

5、::selection 选择被用户选取的元素部分（CSS3中新加的选择器）；

例子：

```
<!DOCTYPE html>
<html>
<head>
<style type="text/css">
     #content #main-content h2{ 
     color:red; 
      } 
      
     #content #main-content>h2{ 
     color:blue ;
      } 
     body #content div[id="main-content"] h2{ 
     color:green; 
      }
     
     #main-content div.paragraph h2{
     color:orange;
      }
     #main-content [class="paragraph"] h2{
     color:yellow;
      }
     div#main-content div.paragraph h2.first{
     color:pink;
     
     }
</style>

</head>
<body>
<div id="content">
  <div id="main-content">
    <h2>学习HTML</h2>
    <div class="paragraph">
      <h2 class="first">学习CSS</h2>
    </div>
  </div>
</div>

</body>
</html>
```

用刚刚讲的特殊性规则计算下这六个样式的特殊性：

第一个规则特殊性的值是：0，2，0，1

第二个规则特殊性的值是：0，2，0，1

第三个规则特殊性的值是：0，1，1，3

第四个规则特殊性的值是：0，1，1，2

第五个规则特殊性的值是：0，1，1，1

第六个规则特殊性的值是：0，1，2，3

这样很明确知道了，特殊性最高的是第一和第二条规则，但第二条规则在后面，所以第

一个标题的颜色是blue，第二个标题的颜色是red.

0特殊性（通配符）和没有特殊性（结合符和继承）是有很大差别的，这种差别决不能忽

视。

```
<!DOCTYPE html>
<html>
<head>
<style type="text/css">
*{
    color:gray;
}
h1#page-title{
    color:red;
}
</style>
</head>
<body>
<div>
    <h1 id="page-title">Hello<em>world</em></h1>
</div>
</body>
</html>

```

这其中Meerkat的颜色是red，但Central的颜色是gray。因为通配符*的特殊性是0， 

而继承的CSS是没有特殊性的，连0也没有，所以，通配符的权重要大于继承。

## 浏览器默认样式 ##

我们在写表单的时候会发现一些浏览器对表单赋予了默认的样式，如在Chorme浏览器

下，文本框及下拉选择框当载入焦点时，都会出现发光的边框，并 且在火狐及谷歌浏览

器下，多行文本框textarea还可以自由拖拽拉大，另外还有在IE10下，当文本框输入

内容后，在文本框的右侧会出现一个小叉叉， 等等。不容置疑，这些效果是在用户体验

上得到了提升，但有些时候我们并不需要这些默认的样式

### 去除Chrome等浏览器文本框默认发光边框 ###

```
input:focus, textarea:focus {
    outline: none;
}
```

去掉高光样式：

```
input:focus{
    -webkit-tap-highlight-color:rgba(0,0,0,0);
    -webkit-user-modify:read-write-plaintext-only;
}
```

当然这样以来，当文本框载入焦点时，所有浏览器下的文本框的边框都不会有颜色上及

样式上的变化了，但我们可以重新根据自己的需要设置一下，如：

```
input:focus,textarea:focus {
    outline: none;
    border: 1px solid #f60;
}
```

这样的话，当文本框载入焦点时，边框颜色就会变为橙色，给用户一个反馈。

### 去除IE10+浏览器文本框后面的小叉叉 ###

```
input::-ms-clear {
    display: none;
}
```

### 禁止多行文本框textarea拖拽 ###

这样按下面添加属性多行文本框就不能拖拽放大缩小了：

```
textarea {
    resize: none;
}
```

在这里要提到一个属性resize，这个是CSS3属性，用于元素缩放，它可以取以下几个

值：

none 默认值

both 允许水平方向及垂直方向缩放

horizontal 只允许水平方向缩放

vertical 只允许垂直方向缩放

不仅可以针对textarea元素，对大多数元素都适用，如div等，在这里不一一列举，但

与textarea不同的是，对div使用时需要加上一句overflow: auto;，也就是这样才

有效果：

```
div {
    resize: both;
    overflow: auto;
}
```

## 选择器 ##

### 基础选择器 ###

*：通用元素选择器，匹配页面任何元素（这也就决定了我们很少使用）

<span>#id</span>：id选择器，匹配特定id的元素

.class：类选择器，匹配class包含(不是等于)特定类的元素

element：标签选择器

```
*
        {
            /*页面所有元素都使用*/
            border:0;
        }

        #test
        {
            /*id=test 的元素*/
            background-color:#0e0;
        }

        .staus
        {
            /*含有类status的元素*/
            border:0;
        }

        div
        {
            /*页面所有div*/
             background-color:#0e0;
        }
```

### 组合选择器 ###

E,F	多元素选择器，用”,分隔，同时匹配元素E或元素F

E F	后代选择器，用空格分隔，匹配E元素所有的后代（不只是子元素、子元素向下递

归）元素F

E>F	子元素选择器，用”>”分隔，匹配E元素的所有直接子元素

E+F	直接相邻选择器，匹配E元素之后的相邻的同级元素F

E~F	普通相邻选择器（弟弟选择器），匹配E元素之后的同级元素F（无论直接相邻与

否）

.class1.class2	这个姑且也算一个吧，没什么名字，匹配类名中既包含class1又包

含class2的元素

### 属性选择器 ###

E[attr]	匹配所有具有属性attr的元素，div[id]就能取到所有有id属性的div

E[attr=value]	匹配属性attr值为value的元素，div[id=test],匹配id=test的

div

E[attr~=value]	匹配所有属性attr具有多个空格分隔、其中一个值等于value的元

素

E[attr|=value]	匹配所有att属性具有多个”-”分隔、其中一个值以value开头的元

素，主要用于lang属性，比如“en”、“en-us”

E[attr ^=value]	匹配属性attr的值以value开头的元素

E[attr $=value]	匹配属性attr的值以value结尾的元素

E[attr *=value]	匹配属性attr的值包含value的元素
 
### 伪类选择器 ###

E:first-child	匹配元素E的第一个子元素

E:link	匹配所有未被点击的链接

E:visited	匹配所有已被点击的链接

E:active	匹配鼠标已经其上按下、还没有释放的E元素

E:hover	匹配鼠标悬停其上的E元素

E:focus	匹配获得当前焦点的E元素

E:lang(c)	匹配lang属性等于c的E元素

E:enabled	匹配表单中可用的元素

E:disabled	匹配表单中禁用的元素

E:checked	匹配表单中被选中的radio或checkbox元素

E::selection	匹配用户当前选中的元素

E:root	匹配文档的根元素，对于HTML文档，就是HTML元素

E:nth-child(n)	匹配其父元素的第n个子元素，第一个编号为1

E:nth-last-child(n)	匹配其父元素的倒数第n个子元素，第一个编号为1

E:nth-of-type(n)	与:nth-child()作用类似，但是仅匹配使用同种标签的元素

E:nth-last-of-type(n)	与:nth-last-child() 作用类似，但是仅匹配使用同

种标签的元素

E:last-child	匹配父元素的最后一个子元素，等同于:nth-last-child(1)

E:first-of-type	匹配父元素下使用同种标签的第一个子元素，等同于:nth-of-

type(1)

E:last-of-type	匹配父元素下使用同种标签的最后一个子元素，等同于:nth-

last-of-type(1)

E:only-child	匹配父元素下仅有的一个子元素，等同于:first-child:last-child

或 :nth-child(1):nth-last-child(1)

E:only-of-type	匹配父元素下使用同种标签的唯一一个子元素，等同于:first-

of-type:last-of-type或 :nth-of-type(1):nth-last-of-type(1)

E:empty	匹配一个不包含任何子元素的元素，文本节点也被看作子元素

E:not(selector)	匹配不符合当前选择器的任何元素

### 伪元素选择器 ###

E:first-line	匹配E元素内容的第一行

E:first-letter	匹配E元素内容的第一个字母

E:before	在E元素之前插入生成的内容

E:after	在E元素之后插入生成的内容

### 优先级 ##

不同级别

1. 在属性后面使用 !important 会覆盖页面内任何位置定义的元素样式。

2.作为style属性写在元素内的样式

3.id选择器

4.类选择器

5.标签选择器

6.通配符选择器

7.浏览器自定义

同一级别

同一级别中后写的会覆盖先写的样式

## 盒子模型 ##

CSS css盒子模型 又称框模型 (Box Model) ，包含了元素内容（content）、内边

距（padding）、边框（border）、外边距（margin）几个要素。

最内部的框是元素的实际内容，也就是元素框，紧挨着元素框外部的是内边距

padding，其次是边框（border），然后最外层是外边距（margin），整个构成了框

模型。通常我们设置的背景显示区域，就是内容、内边距、边框这一块范围。而外边距

margin是透明的，不会遮挡周边的其他元素。

那么，元素框的总宽度 = 元素（element）的width + padding的左边距和右边距的

值 + margin的左边距和右边距的值 + border的左右宽度；

元素框的总高度 = 元素（element）的height + padding的上下边距的值 + 

margin的上下边距的值 ＋ border的上下宽度。

### css外边距合并 ###

两个上下方向相邻的元素框垂直相遇时，外边距会合并，合并后的外边距的高度等于两

个发生合并的外边距中较高的那个边距值

注意的是：只有普通文档流中块框的垂直外边距才会发生外边距合并。行内框、浮动框

或绝对定位之间的外边距不会合并。

css reset 中也会经常用到:

```
* {
  margin : 0;
  padding : 0;
}

```
### box-sizing属性  ###

box-sizing属性是用户界面属性里的一种，之所以介绍它，是因为这个属性跟盒子模型

有关，而且在css reset中有可能会用到它。

box-sizing : content-box|border-box|inherit;

(1) content-box ,默认值，可以使设置的宽度和高度值应用到元素的内容框。盒子的

width只包含内容。

　　即总宽度=margin+border+padding+width

(2) border-box , 设置的width值其实是除margin外的border+padding+element

的总宽度。盒子的width包含border+padding+内容

　　　　即总宽度=margin+width

很多CSS框架，都会对盒子模型的计算方法进行简化。

(3) inherit , 规定应从父元素继承 box-sizing 属性的值

关于border-box的使用：

1 一个box宽度为100%，又想要两边有内间距，这时候用就比较好

2 全局设置 border-box 很好，首先它符合直觉，其次它可以省去一次又一次的加加

减减，它还有一个关键作用——让有边框的盒子正常使用百分比宽度。

### 应用 ###

1:margin越界（第一个子元素的margin-top和最后一个子元素的margin-bottom的越

界问题）

以第一个子元素的margin-top 为例：

当父元素没有边框border时，设置第一个子元素的margin-top值的时候，会出现

margin-top值加在父元素上的现象，解决方法有四个：

（1）给父元素加边框border （副作用）

（2）给父元素设置padding值  （副作用）

（3）父元素添加 overflow：hidden （副作用）

（4）父元素加前置内容生成。（推荐）

以第四种方法为例：

```
.parent {
     width : 500px;
     height : 500px;
     background-color : red;       
}
.parent : before {
     content : " ";
     display : table;
}

.child {
     width : 200px;
     height : 200px;
     background-color : green;
     margin-top : 50px;
}


<div class="parent">
    <div class="child"></div> 
</div>
```

2 浏览器间的盒子模型。

（1）ul标签在Mozilla中默认是有padding值的，而在IE中只有margin有值。

（2）标准盒子模型与IE模型之间的差异：

　　标准的盒子模型就是上述介绍的那种，而IE模型更像是 box-sizing : border-

box; 其内容宽度还包含了border和padding。解决办法就是：在html模板中加

doctype声明。

3 用盒子模型画三角形

```
<!DOCTYPE html>
<html>
  <head>
    <style>
        .triangle {
            width : 0;
            height: 0;
            border : 100px solid transparent;
            border-top : 100px solid blue; /*这里可以设置border的top、bottom、left、right四个方向的三角*/
        }
    </style>
  </head>
  <body>
    <div class="triangle"></div>
  </body>
</html>
```

<center><strong>{{ page.date | date_to_string }}</strong></center>
