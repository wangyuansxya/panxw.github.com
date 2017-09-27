---
layout: post
category: "android"
title:  "Android 引用referenced基础"
tags: [LayoutTransition, 引用referenced]
---
**Android 强引用（strong referenced），弱引用（WeakReference），软应用（soft referenced），LruCache(内存缓存)区别和联系**

从上到下依次减弱：

1，强引用（strong referenced）：StrongReference 是 Java 的默认引用实现,  它会尽可能长时间的存活于 JVM 内， 当没有任何对象指向它时 GC 执行后将会被回收（只要存在垃圾回收器就无法回收）

2，软应用（soft referenced）：SoftReference 于 WeakReference 的特性基本一致， 最大的区别在于 SoftReference 会尽可能长的保留引用直到 JVM 内存不足时才会被回收(虚拟机保证), 这一特性使得 SoftReference 非常适合缓存应用（在即将要发生内存溢出的时候，将这些对象列为下次回收的范围内）

3，弱引用（WeakReference）：当所引用的对象在 JVM 内不再有强引用时, GC 后 weak reference 将会被自动回收 （一旦进行垃圾回收就会回收掉的引用方式）
 WeakHashMap 使用 WeakReference 作为 key， 一旦没有指向 key 的强引用, WeakHashMap 在 GC 后将自动删除相关的 entry

4,虚引用：有虚引用的对象不会对生命周期造成任何的影响，也无法获取对象的实例。只是希望在对象被垃圾回收器回收之后能够收到一个通知（java1.2之后使用phantomReferenced）

说明：以下不能认为是引用的方法，是数据存储的方式

5，内存缓存(LruCache)：常用于缓存bitmap,实现方式是[LinkedHashMap]保存最近引用的对象，并且在缓存超出设置大小的时候剔除（evict）最近最少使用到的对象。

6，Disk Cache(磁盘缓存)：
