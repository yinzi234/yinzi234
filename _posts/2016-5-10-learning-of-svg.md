---
layout: default
title: svg学习
---

##SVG学习##

SVG 指可伸缩矢量图形，用来定义用于网络的基于矢量的图形。

SVG 文件必须使用 .svg 后缀来保存

SVG 代码以svg元素开始，包括开启标签svg和关闭标签/svg。这是根元

素。width 和 height 属性可设置此 SVG 文档的宽度和高度。version

 属性可定义所使用的 SVG 版本，xmlns 属性可定义 SVG 命名空间。

###SVG优势###

SVG 可被非常多的工具读取和修改（比如记事本）

SVG 与 JPEG 和 GIF 图像比起来，尺寸更小，且可压缩性更强。

SVG 是可伸缩的

SVG 图像可在任何的分辨率下被高质量地打印

SVG 可在图像质量不下降的情况下被放大

SVG 图像中的文本是可选的，同时也是可搜索的

SVG 可以与 Java 技术一起运行

SVG 是开放的标准

SVG 文件是纯粹的 XML

与 Flash 相比，SVG 最大的优势是与其他标准（比如 XSL 和 DOM）相兼容。而 Flash 则是未开源的私有技术。


###SVG使用方法###

###1.直接写入html文档###

```
<body>
<svg width="100%" height="100%">
<rect x="20" y="20" rx="20" ry="20" width="200" height="200"style="fill:red;stroke:black;stroke-width:4;opacity:0.5"/>
</svg>
</body>
```

###2.embed###

所有主流浏览器支持，允许使用脚本

```
<embed src="test.svg" width="200" height="200" 
type="image/svg+xml"
pluginspage="http://www.adobe.com/svg/viewer/install/" />

```

###3.object###

新浏览器支持，不允许使用脚本

```
<object data="test.svg" width="200" height="200" type="image/svg+xml" codebase="http://www.adobe.com/svg/viewer/install/" />
```

###4.iframe###

大部分浏览器支持

```
<iframe src="test.svg" width="200" height="200">
</iframe>

```

###SVG元素属性###

公共属性： 

style(stroke, stroke-width, fill), transform, id, class 等

私有属性：

<path>："d"  eg: d="M20 20L30 27L40 58Z"

<rect>:"x y width height rx ry"  注：其中设置 rx，ry 可形成圆角框

<circle>:"cx cy r"

<ellipse>:"cx cy rx ry"

<line>:"x y x1 y1"

<polyline>:"points"

<polygon>:"points"

###SVG基本形状###

SVG 有已经定义可以直接使用的形状元素：

###1.圆形circle###

```
<svg id="mypath" width="400" height="400" style="border:1px solid #00F5FF;">
      <circle cx="50" cy="50" r="50">
</svg>
```

其中cx，cy定义圆点坐标，未定义时默认圆点坐标（0，0）；

r为半径

<svg id="mypath" width="400" height="400" style="border:1px solid #00F5FF;">
<circle cx="50" cy="50" r="50">
</svg>

###2.矩形rect###


```
<svg id="mypath" width="400" height="400" >
    <rect x="10" y="10" width="100" height="100" stroke="red" fill="#ccc" >
 </svg>

```

其中fill填充色；stroke-width边框宽度；stroke边框颜色

<svg id="mypath" width="400" height="400" >
    <rect x="10" y="10" width="100" height="100" stroke="red" fill="#ccc" >
 </svg>

###3.椭圆ellipse###


```
<svg id="mypath" width="400" height="400" >
  <ellipse cx="100" cy="100" rx="100" ry="50" fill="#fff" stroke="#f00"/>  
</svg>
```

其中rx，ry横向纵向半径

###4.直线line###


```
<svg id="mypath" width="400" height="400" >
  <line x1="0" y1="0" x2="100" y2="100" stroke="#f00" stroke-width="5"/> 
</svg>

```

其中x1,y1 起点的位置；x2,y2 终点的位置


###5.折线polyline###

```
<svg id="mypath" width="400" height="400" >
  <polyline points="0,0 0,20 20,20 20,40 40,40 40,60" style="fill:white;stroke:red;stroke-width:2" />
</svg>
```

格式points"xi,yi"

###5.路径path###

```
<path d="M250 150 L150 350 L350 350 Z" />
```

这是开始于位置 250 150，到达位置 150 350，然后从那里开始到 350 

350，最后在 250 150 关闭的路径。

路径的属性有：

M = moveto

L = lineto

H = horizontal lineto

V = vertical lineto

C = curveto

S = smooth curveto

Q = quadratic Belzier curve

T = smooth quadratic Belzier curveto

A = elliptical Arc

Z = closepath

由于绘制路径的复杂性，因此强烈建议您使用 SVG 编辑器来创建复杂的图形。

###SVG滤镜###

可用滤镜：

feBlend

feColorMatrix

feComponentTransfer

feComposite

feConvolveMatrix

feDiffuseLighting

feDisplacementMap

feFlood

feGaussianBlur

feImage

feMerge

feMorphology

feOffset

feSpecularLighting

feTile

feTurbulence

feDistantLight

fePointLight

feSpotLight
//在单个svg元素上可以使用多个滤镜

###高斯模糊###

```
<defs>
<filter id="Gaussian_Blur">
<feGaussianBlur in="SourceGraphic" stdDeviation="20"/>
</filter>
</defs>

<ellipse cx="200" cy="150" rx="70" ry="40"
style="fill:#ff0000;stroke:#000000;
stroke-width:2;filter:url(#Gaussian_Blur)"/>
```

<filter> 用来定义 SVG 滤镜。；<filter> 必须嵌套在 <defs> 标签内。

<filter> 标签的 id 属性可为滤镜定义一个唯一的名称（同一滤镜可被文档中的多个元素使用）

filter:url 把元素链接到滤镜。当链接滤镜 id 时，必须使用 # 字符,
滤镜效果是 <feGaussianBlur> 定义的。fe 后缀可用于所有的滤镜

<feGaussianBlur> 的 stdDeviation 定义模糊的程度

in="SourceGraphic" 定义了由整个图像创建效果

###渐变###

线性渐变 linearGradient

```
<defs>
<linearGradient id="orange_red" x1="0%" y1="0%" x2="100%" y2="0%">
<stop offset="0%" style="stop-color:rgb(255,255,0);
stop-opacity:1"/>
<stop offset="100%" style="stop-color:rgb(255,0,0);
stop-opacity:1"/>
</linearGradient>
</defs>

<ellipse cx="200" cy="190" rx="85" ry="55"
style="fill:url(#orange_red)"/>
```

当 y1 和 y2 相等，而 x1 和 x2 不同时，可创建水平渐变

当 x1 和 x2 相等，而 y1 和 y2 不同时，可创建垂直渐变

当 x1 和 x2 不同，且 y1 和 y2 不同时，可创建角形渐变

<linearGradient> 必须嵌套在 <defs> 的内部

<linearGradient> 的 id 为渐变定义一个唯一的名称

fill:url(#orange_red) 把 ellipse 链接到此渐变

<linearGradient> 的 x1、x2、y1、y2 可定义渐变的开始和结束位置

渐变的颜色范围可由两种或多种颜色组成。每种颜色通过一个 <stop> 标签来规定。offset 属性用来定义渐变的开始和结束位置。

放射性渐变 radialGradient

```
<defs>
<radialGradient id="grey_blue" cx="50%" cy="50%" r="50%"
fx="50%" fy="50%">
<stop offset="0%" style="stop-color:rgb(200,200,200);
stop-opacity:0"/>
<stop offset="100%" style="stop-color:rgb(0,0,255);
stop-opacity:1"/>
</radialGradient>
</defs>

<ellipse cx="230" cy="200" rx="110" ry="100"
style="fill:url(#grey_blue)"/>
```

<radialGradient> 的 id 可为渐变定义一个唯一的名称

fill:url(#grey_blue) 把 ellipse 元素链接到此渐变

cx、cy 和 r 定义外圈， fx 和 fy 定义内圈 渐变的颜色范围可由两种或多种颜色组成。

每种颜色通过一个 <stop> 标签来规定。

offset 定义渐变的开始和结束位置

<center><strong>{{ page.date | date_to_string }}</strong></center>
