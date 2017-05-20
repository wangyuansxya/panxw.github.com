---
layout: post
category: "android"
title:  "Android性能优化之内存优化"
tags: [Android,性能，内存，优化]
---
<br>
**一、为什么要做性能优化**<br>
移动端开发过程中内存优化是很重要的一块，因为Android对于每个应用程序都有一个最大的内存限制，需要注意的一点是不同的Android手机设置的largeheap不完全相同，所以需要对常见的手机有一个大概的认识。
至于为什么要做限制，是由于移动端的手机运行内存是很珍贵的资源，是有限的，不能让一个APP占用过多的内存。否则会导致其他的应用无法正常运行。<br>
**二、Android内存优化的几个方面**<br>
1.不要在view的onDraw方法内创建对象。  <br>
原因是因为View刷新的时候，ondraw方法可能会执行多次，如果在这里创建对象，可能导致UI上的卡顿
2.加载图片的时候使用Option对图片进行压缩  <br>
3.字符串的拼接。使用StringBuilder(线程安全的)和StringBuffer(线程非安全的)。<br>
如果不存在多线程操作的情况下，使用StringBuffer。不要使用String+String的形式<br>
4.使用Android提供的ArrayMap和SpareArry代替使用HashMap。  <br>
因为前者更剩内存，效率更高。通常的HashMap的实现方式更加消耗内存，因为它需要一个额外的实例对象来记录Mapping操作。<br>
另外，SparseArray更加高效在于他们避免了对key与value的autobox自动装箱，并且避免了装箱后的解箱。<br>
5.防止出现内存抖动的情况。避免在短时间内频繁的创建和销毁相同的对象<br>
6.减少class数量。一个class最少占用2KB的内存。(这条可做参考)<br>
7.复用系统变量。尽量使用系统提供的变量和方法<br>
8.ListView和GridView，是否ViewHolder优化<br>
9.使用完成的或者是不再使用的bitmap，调用recycle方法回收。<br> 及时关闭指针对象。数据库使用完之后，关闭cursor对象和数据库连接 <br>
10.内存泄露：本该回收掉的对象，在其生命周期的结束之后，仍然不能被系统回收的对象<br>
11.对可能造成内存泄露的对象，使用weakReference和SoftReference引用<br>
12.使用非静态内部类(默认持有外部类的引用)，造成内存泄露。<br>
13.for循环优化，应在开始循环之前，只获取到len。而不是每次都获取<br>
14.Enums的内存消耗通常是static constants的2倍。你应该尽量避免在Android上使用enums。<br>
15.在Java中的每一个类(包括匿名内部类)都会使用大概500 bytes。<br>
16.每一个类的实例花销是12-16 bytes。<br>
17.往HashMap添加一个entry需要额一个额外占用的32 bytes的entry对象。<br>
18.谨慎使用第三方libraries。很多开源的library代码都不是为移动网络环境而编写的，如果运用在移动设备上，，这样的效率并不高<br>
19.布局优化，对于可以复用或者打开页面但是可能不需要使用的布局，可以使用include，viewStub，merge标签进行优化<br>
20.使用ProGuard来剔除不需要的代码。ProGuard能够通过移除不需要的代码，重命名类，域与方法等方对代码进行压缩，优化与混淆。使用ProGuard可以使得你的代码更加紧凑，这样能够使用更少mapped代码所需要的RAM。 　<br>
21.对最终的APK使用zipalign。在编写完所有代码，并通过编译系统生成APK之后，你需要使用zipalign对APK进行重新校准。如果你不做这个步骤，会导致你的APK需要更多的RAM，因为一些类似图片资源的东西不能被mapped。<br>
note:Google Play不接受没有经过zipalign的APK。<br>
22.一旦你获取到一个相对稳定的版本后，需要分析你的app整个生命周期内使用的内存情况，并进行优化.<br>
23.使用多进程<br>
如果合适的话，有一个更高级的技术可以帮助你的app管理内存使用：通过把你的app组件切分成多个组件，运行在不同的进程中。<br>
这个技术必须谨慎使用，大多数app都不应该运行在多个进程中。因为如果使用不当，它会显著增加内存的使用，而不是减少。<br>
当你的app需要在后台运行与前台一样的大量的任务的时候，可以考虑使用这个技术。<br>
一个典型的例子是创建一个可以长时间后台播放的Music Player。<br>
如果整个app运行在一个进程中，当后台播放的时候，前台的那些UI资源也没有办法得到释放。<br>
类似这样的app可以切分成2个进程：一个用来操作UI，另外一个用来后台的Service.<br>
你可以通过在manifest文件中声明'android:process'属性来实现某个组件运行在另外一个进程的操作。<br>
> <service android:name=".PlaybackService"
>          android:process=":background" />