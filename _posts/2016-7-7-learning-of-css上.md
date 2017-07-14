---
layout: default
title: css学习下
---

## position ##

如果没有定位，我们做出来的网页将会是按部就班的自上而下、自左而右的平铺在浏览器上，外加通

过margin和padding调整一下间距，还有就是通过float来浮动某些元素。

但是有些情况下，这种按部就班的网页排版满足不了我们的要求，我们需要某些元素跑出来，悬浮在

网页上面，而且需要给它指定一个位置。这时候我们就需要用到了position，而且是非用不可。

position一共有四个可选属性：static/relative/absolute/fixed。其中static（静态定位）

是默认值，即所有的元素如果不设置其他的position值，它的position值就是static，有它跟没有

它一样。

### relative ###

如果设定 position:relative，就可以使用 top,bottom,left 和 right 来相对于元素在文档

中应该出现的位置来移动这个元素。【意思是元素实际上依然占据文档中的原有位置，只是视觉上相

对于它在文档中的原有位置移动了

```
#div-1 {
 position:relative;
 top:20px;
 left:-40px;
}
```

### absolute ###

当指定 position:absolute 时，元素就脱离了文档【即在文档中已经不占据位置了】，可以准确

的按照设置的 top,bottom,left 和 right 来定位了。

```
#div-1a {
 position:absolute;
 top:0;
 right:0;
 width:200px;
}
```

### relative+absolute ###

如果我们给 div-1 设置 relative 定位，那么 div-1 内的所有元素都会相对 div-1 定位。如

果给 div-1a 设置 absolute 定位，就可以把 div-1a 移动到 div-1 的右上方。

```
#div-1 {
 position:relative;
}
#div-1a {
 position:absolute;
 top:0;
 right:0;
 width:200px;
}
```

两栏绝对定位

```
#div-1 {
 position:relative;
}
#div-1a {
 position:absolute;
 top:0;
 right:0;
 width:200px;
}
#div-1b {
 position:absolute;
 top:0;
 left:0;
 width:200px;
}

```

两栏绝对定位定高

```
#div-1 {
 position:relative;
 height:250px;
}
#div-1a {
 position:absolute;
 top:0;
 right:0;
 width:200px;
}
#div-1b {
 position:absolute;
 top:0;
 left:0;
 width:200px;
}

```

### fixed ###

其实fixed和absolute是一样的，唯一的区别在于：absolute元素是根据最近的定位上下文确定位

置，而fixed永远根据浏览器确定位置。

relative元素的定位永远是相对于元素自身位置的，和其他元素没关系，也不会影响其他元素。

fixed元素的定位永远是相对于浏览器边界的，和其他元素没有关系。但是它具有破坏性，会导致其

他元素位置的变化。

absolute的定位相对于前两者要复杂许多。如果为absolute设置了top、left，浏览器会根据什么

去确定它的纵向和横向的偏移量呢？答案是浏览器会递归查找该元素的所有父元素，如果找到一个设

置了position:relative/absolute/fixed的元素，就以该元素为基准定位，如果没找到，就以浏

览器边界定位。

## display ##

display 的属性值有：none|inline|block|inline-block|list-item|run-in|table|

inline-table|table-row-group|table-header-group|table-footer-group|table-row|

table-column-group|table-column|table-cell|table-caption|inherit

其中常用的的有none、inline、block、inline-block。分别的意思是：

1、none： 元素不会显示，而且改元素现实的空间也不会保留。但有另外一个 visibility: 

hidden， 是保留元素的空间的。

2、inline： display的默认属性。将元素显示为内联元素，元素前后没有换行符。我们知道内联元

素是无法设置宽高的，所以一旦将元素的display 属性设为 inline， 设置属性height和width是

没有用的。此时影响它的高度一般是内部元素的高度（font-size）和padding。

3、block： 将元素将显示为块级元素，元素前后会带有换行符。设置为block后，元素可以设置

width和height了。元素独占一行。

4、inline-block：行内块元素。这个属性值融合了inline 和 block 的特性，即是它既是内联元

素，又可以设置width和height。

```
.inline{
    display:inline; 
    width:100px; 
    height:100px; 
    padding:10px; 
    background-color:red;
}
.block{
    display:block; 
    width:100px; 
    height:100px; 
    padding:10px;
    background-color:green;
}
.inline-block{
    display:inline-block; 
    width:100px;
    height:100px; 
    padding:10px;
    background-color:blue;
}


<div class="wrap">
    <div class="inline">
    inline
    </div>inline
    <div class="block">
    block
    </div> block
    <div class="inline-block">
    inline-block
    </div>inline-block
</div>
```

list-item：     此元素会作为列表显示。

run-in：     此元素会根据上下文作为块级元素或内联元素显示。

table：     此元素会作为块级表格来显示（类似 table），表格前后带有换行符。

inline-table：     此元素会作为内联表格来显示（类似 table），表格前后没有换行符。

table-row-group：     此元素会作为一个或多个行的分组来显示（类似tbody）。

table-header-group：     此元素会作为一个或多个行的分组来显示（类似thead）。

table-footer-group：     此元素会作为一个或多个行的分组来显示（类似 tfoot）。

table-row：     此元素会作为一个表格行显示（类似 <tr>）。

table-column-group：     此元素会作为一个或多个列的分组来显示（类似 colgroup）。

table-column：     此元素会作为一个单元格列显示（类似 col）

table-cell：     此元素会作为一个表格单元格显示（类似 td 和 th）

table-caption：     此元素会作为一个表格标题显示（类似 caption）

inherit：     规定应该从父元素继承 display 属性的值。

### 内联元素 ###

和其他元素都在一行上；

元素的高度、宽度及顶部和底部边距不可设置；

元素的宽度就是它包含的文字或图片的宽度，不可改变。

a、span、br、i、em、strong、label、q、var、cite、code

### 块级元素 ###

每个块级元素都从新的一行开始，并且其后的元素也另起一行。（真霸道，一个块级元素独占一

行）；

元素的高度、宽度、行高以及顶和底边距都可设置。

元素宽度在不设置的情况下，是它本身父容器的100%（和父元素的宽度一致），除非设定一个宽度。

常用的块状元素有：

div、p、h1...h6、ol、ul、dl、table、address、blockquote 、form

### 内联块状元素 ###

和其他元素都在一行上；

元素的高度、宽度、行高以及顶和底边距都可设置。

常用的内联块状元素有：img、input

## float ##

float 属性定义元素在哪个方向浮动。以往这个属性总应用于图像，使文本围绕在图像周围，不过在 

CSS 中，任何元素都可以浮动。浮动元素会生成一个块级框，而不论它本身是何种元素。

如果浮动非替换元素，则要指定一个明确的宽度；否则，它们会尽可能地窄。

注释：假如在一行之上只有极少的空间可供浮动元素，那么这个元素会跳至下一行，这个过程会持续

到某一行拥有足够的空间为止。

默认值：none；

继承性：no；

left                    元素向左浮动。

right                   元素向右浮动。

none                    默认值。元素不浮动，并显示在其在文本中出现的位置。

inherit                 规定应该从父元素继承 float 属性的值。

比较常用的两个属性值是左浮动和右浮动。
 
### 文字环绕效果 ###

浮动的初衷就是为了文字环绕效果。

```
 <div class="container">
     <div class="content"></div>
     <p>
 Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!
         </p>
     </div>   
```

```
.container {
  width: 300px;
  height: 300px;
  border: 1px solid black;
}
.container .content {
  float: left;
  width: 150px;
  height: 150px;
  background-color: lightpink;
  margin: 5px;
}
```

content 元素设置了左浮动，使div元素脱离文档流，文字在其周围坏绕显示。

### 父元素高度塌陷 ###

以div元素为例。div元素的高度会通过内容自动撑开。也就是说，内容有多少，高度就有多高。但是

当内部元素设置了float属性之后，会是父元素高度塌陷。代码和实例如下。 

```
<div class="container">
    <p>
Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!
    </p>
</div>
```

```
.container {
  width: 300px;
  border: 1px solid black;
}
.container p {
  float: left;
}
```

### 清除浮动的方法 ###

1:父元素底部添加空div，然后在添加属性clear : both。

```
<div class="container">
            <p>
            Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!
            </p>
            <div class="clearfix"></div>
        </div>
```

```
.container {
  width: 300px;
  border: 1px solid black;
}
.container p {
  float: left;
}
.container .clearfix {
  overflow: hidden;
  *zoom: 1;
}
```

2：父元素设置伪类after

```
<div class="container">
            <p>
            Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!Hello World!
            </p>
        </div>
```

```
.container {
  width: 300px;
  border: 1px solid black;
  *zoom: 1;
}
.container p {
  float: left;
}
.container:after {
  content: "";
  display: table;
  clear: both;
}
```

### float元素去空格化 ###

在平时的编码中，为了要符合HTML编码规范，都会为html标签添加缩进，达到美观的效果。可是缩进

时就会产生空格，也就是&nbsp;。当给元素设置左浮动时，元素本身左浮动，剩余的空格会被挤到最

后，也就是上文所说的文字环绕效果。但是，要记住一点，&nbsp;和回车敲下的空格的效果略有不

同。

### float元素块状化 ###

在为内联元素设置浮动属性之后，display属性由inline变成block。并且可以为内联元素设置宽

高。使用float加width属性可以实现一些简单的固定宽度的布局效果。

### float流体布局 ###

1：单侧固定，右侧自适应的布局。

```
<div class="container">
    <div class="left">左浮动+固定宽度</div>
    <div class="right">右边自适应宽度+margin-left</div>
</div>
```

```
.container{
    max-width:90%;
    margin:0 auto;
}

.left{
    float:left;
    text-align:center;
    background-color: lightpink;
    width: 200px;
    height:300px;
}

.right{
    background-color: lightyellow;
    margin-left:200px;
    height:300px;
    padding-left:10px;
}
```

2：DOM与显示位置不同的单侧固定

```
.container {
  max-width: 90%;
  margin: 0 auto;
}
.container .right {
  float: right;
  width: 200px;
  height: 200px;
  background-color: lightpink;
}
.container .left {
  background-color: lightyellow;
  margin-right: 200px;
  height: 300px;
  padding-left: 10px;
}
```

3：DOM与显示位置相同的单侧固定 

```
<div class="container">
            <div class="left-content">
                <!-- 左浮动+width100% -->
                <div class="left">margin-right</div>
            </div>
            <div class="right">左浮动+固定宽度+margin-left负值</div>
        </div>
```

```
.container {
  max-width: 90%;
  margin: 0 auto;
}
.container .right {
  float: left;
  width: 200px;
  height: 200px;
  background-color: lightpink;
  margin-left: -200px;
  height: 300px;
}
.container .left {
  background-color: lightyellow;
  margin-right: 200px;
  height: 300px;
  text-align: center;
}
```

4：智能布局

```
<div class="container">
            <div class="left">
                float+margin-right+自适应宽度
            </div>
            <div class="right">
                display:table-cell  ---IE8+;
                display:inline-block   ---IE7+;
                自适应宽度
            </div>
        </div>
```

```
.container {
  max-width: 90%;
  margin: 0 auto;
}
.container .left {
  float: left;
  height: 300px;
  background-color: lightpink;
}
.container .right {
  display: table-cell;
  *display: inline-block;
  height: 300px;
  background-color: lightyellow;
}
```

1：当一个元素设置float属性时，会使元素块状化。

2：float属性的创造初衷就是为了文字环绕效果而生的。

3：float元素会使父元素高度塌陷。

4：float元素会除去换行带来的空格。

5：使用float可以实现两栏自适应的布局。



<center><strong>{{ page.date | date_to_string }}</strong></center>
