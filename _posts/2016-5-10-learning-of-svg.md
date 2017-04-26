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
<rect x="20" y="20" rx="20" ry="20" width="250" height="100"style="fill:red;stroke:black;stroke-width:5;opacity:0.5"/>
</svg>
</body>
```

###2.<embed>###

所有主流浏览器支持，允许使用脚本

```
<embed src="rect.svg" width="300" height="100" 
type="image/svg+xml"
pluginspage="http://www.adobe.com/svg/viewer/install/" />

```


<center><strong>{{ page.date | date_to_string }}</strong></center>
