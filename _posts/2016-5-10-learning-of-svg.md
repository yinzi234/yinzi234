---
layout: default
title: svg学习
---

##SVG学习##

SVG 指可伸缩矢量图形，用来定义用于网络的基于矢量的图形。

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


<center><strong>{{ page.date | date_to_string }}</strong></center>
