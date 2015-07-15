---
layout: post
title: "VPS操作常见错误汇总" 
comments: true
share: true
tags: 笔记
---


使用环境：Ubuntu 14.04

1. 主义VPS之间的区别并不仅仅局限于操作系统版本的区别，有时候同样的操作系统但是提供商不同，就会有不同的目录和不同的默认配置。对于部分VPS而言，www目录下和usr/share/目录下都是可以通过ip访问的到的，然而对于部分vps只有www/html/目录才能被外部访问。

	正是这个原因，所以一开始我在搬瓦工的vps上面装puhsysinfo和phpmyadmin都出现了无法访问的情况，但是在host1plus的vps上是可行的。

	找到原因就是因为搬瓦工只支持访问html目录。但是不能把Phpmyadmin目录都移动过去，若都移动过去就会变成目录形式展示在网址上了。应该：

		
		sudo ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin

	把在html/下建立快捷方式！


