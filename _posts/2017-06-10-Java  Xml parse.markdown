---
layout: post
category: "android"
title:  "Android XML解析"
tags: [xml, sax解析，pull解析，dom解析]
---
**Android xml解析**

1，SAX解析器 <br>

	基于事件的解析模式。解析速度快，占用内存小，适合在Android移动设备中使用
2，Dom解析器<br>

	基于对象的解析模式。由于DOM是在内存中以树形的结构存放的，因此检索和更新效率比较高，但是对于特别大的文档，解析和加载整个文档会很好资源
3，pull解析器<br>

	pull解析器和sax解析器类似均是基于事件的。
	pull解析器需要我们自己去触发事件，解析器小巧轻便，解析速度快，简单易用。
	Android系统内部使用的就是pull解析器
