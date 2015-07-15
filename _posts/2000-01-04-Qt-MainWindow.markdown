---
layout: post
title: "Qt-MainWindow简介" 
comments: true
share: true
tags: Qt
---


QMainWindow是 Qt 框架带来的一个预定义好的主窗口类。所谓主窗口，就是一个普通意义上的应用程序（不是指游戏之类的那种）最顶层的窗口。


它实际上分成了几个部分：
![](http://files.devbean.net/images/2012/08/mw-struct-600x365.png)


通常，各个图形界面框架都会使用操作系统本地代码来生成一个窗口。如果你不喜欢本地样式，比如 QQ 这种，它其实是自己将标题栏绘制出来，这种技术称为 DirectUI，也就是无句柄绘制。

Qt 的主窗口支持多个工具条。你可以将工具条拖放到不同的位置，因此这里说是 Area。

在工具条区域内部是 Dock Widget Area，这是停靠窗口的显示区域。所谓停靠窗口，就像 Photoshop 的工具箱一样，可以停靠在主窗口的四周，也可以浮动显示。

