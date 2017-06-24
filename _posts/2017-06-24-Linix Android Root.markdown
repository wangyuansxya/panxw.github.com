---
layout: post
category: "linux"
title:  "Linux Android Root"
tags: [Linix, Root, Android]
---
**Android Root解析**

判断操作系统的本质：系统内核+文件系统

1，Android就是linux系统，只是没有桌面系统的一些特征罢了。android的内核和文件系统都是Linux提供的。在ubuntu的终端命令行下，可以通过输入‘su’命令来获取最高权限。相当于windows系统的管理员权限

2，为什么我们需要管理员权限。做Linux驱动开发的时候可以在获取到root权限的情况下，直接使用android手机来测试驱动。最坏的情况下就是手机无法开机，直接刷一个新的rom包就行了。不会对机器的硬件有什么损伤。这样方便了开发。提升了效率

3，

