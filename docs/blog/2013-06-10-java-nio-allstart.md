---
layout: post
title: "Java NIO 系列教程"
date: 2013-06-10 01:53
comments: true
categories: JavaNIO
---

本文章为转载，感谢并发编程网  

译文原文地址:[http://ifeve.com/java-nio-all/](http://ifeve.com/java-nio-all/)

英文原文地址:[http://tutorials.jenkov.com/java-nio/index.html](http://tutorials.jenkov.com/java-nio/index.html)  


作者：**Jakob Jenkov**   译者：**郭蕾**     校对：**方腾飞**


Java NIO(New IO)是一个可以替代标准Java IO API的IO API（从Java 1.4开始)，Java NIO提供了与标准IO不同的IO工作方式。


***Java NIO: Channels and Buffers（通道和缓冲区）***

标准的IO基于字节流和字符流进行操作的，而NIO是基于通道（Channel）和缓冲区（Buffer）进行操作，数据总是从通道读取到缓冲区中，或者从缓冲区写入到通道中。


***Java NIO: Asynchronous IO（异步IO）***

Java NIO可以让你异步的使用IO，例如：当线程从通道读取数据到缓冲区时，线程还是可以进行其他事情。当数据被写入到缓冲区时，线程可以继续处理它。从缓冲区写入通道也类似。

***Java NIO: Selectors（选择器）***

Java NIO引入了选择器的概念，选择器用于监听多个通道的事件（比如：连接打开，数据到达）。因此，单个的线程可以监听多个数据通道。

<!-- more -->

下面是Java NIO系列文章的目录：

1. Java NIO概述   (airu 已翻译)  
2. Java NIO Channel (airu 已翻译)  
3. Java NIO Buffer    (airu 已翻译)  
4. Java NIO Scatter / Gather（已翻译）  
5. Java NIO 通道之间的数据传输   （已翻译）  
6. Java NIO Selector（浪迹v 已翻译）  
7. Java NIO FileChannel（周泰 已翻译）  
8. Java NIO SocketChannel （布丁  已翻译）  
9. Java NIO ServerSocketChannel （布丁  已翻译）  
10. Java NIO DataGramChannel （布丁  已翻译）  
11. Java NIO Pipe （A黄忠 已翻译）  
12. Java NIO 与IO（已翻译）  
