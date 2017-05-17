---
layout: post
category: "android"
title:  "Android性能优化之内存优化"
tags: [Android,性能，内存，优化]
---
#### 性能和功能的取舍 ####

移动端开发过程中内存优化是很重要的一块，因为Android对于每个应用程序都有一个最大的内存限制，需要注意的一点是不同的Android手机设置的largeheap不完全相同，所以需要对常见的手机有一个大概的认识。
至于为什么要做限制，是由于移动端的手机运行内存是很珍贵的资源，是有限的，不能让一个APP占用过多的内存。否则会导致其他的应用无法正常运行。

#### Android内存优化的几个方面 ####

1.不要在view的onDraw方法内创建对象。  <br>
原因是因为View刷新的时候，ondraw方法可能会执行多次，如果在这里创建对象，可能导致UI上的卡顿
2.加载图片的时候使用Option对图片进行压缩  <br>
3.字符串的拼接。使用StringBuilder(线程安全的)和StringBuffer(线程非安全的)。<br>
如果不存在多线程操作的情况下，使用StringBuffer。不要使用String+String的形式
4.使用Android提供的ArrayMap和SpareArry代替使用HashMap。  <br>
因为前者更剩内存，效率更高<br>
5.防止出现内存抖动的情况。避免在短时间内频繁的创建和销毁相同的对象<br>
6.减少class数量。一个class最少占用2KB的内存。(这条可做参考)<br>
7.复用系统变量。尽量使用系统提供的变量和方法<br>
8.ListView和GridView，是否ViewHolder优化<br>
9.使用完成的或者是不再使用的bitmap，调用recycle方法回收。<br> 及时关闭指针对象。数据库使用完之后，关闭cursor对象和数据库连接 <br>
10.内存泄露：本该回收掉的对象，在其生命周期的结束之后，仍然不能被系统回收的对象<br>
11.对可能造成内存泄露的对象，使用weakReference和SoftReference引用<br>
12.使用非静态内部类(默认持有外部类的引用)，造成内存泄露。<br>
