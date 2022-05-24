---
layout: post
title: "Android-Fragment-调研"
date: 2013-04-30 06:45
comments: true
categories: Android
---

Fragment是google由3.0开始加入SDK的界面解决方案.  
后续由谷歌团队维护并发行了support包以支持低版本SDK来使用Fragment

###谁在使用Fragment
------------------

 * 网易新闻
 * 网易云音乐
 * 百度音乐
 * 多米
 * 豌豆荚
 * 小米app
 * Path
 * Pocket
 * Fuubo
 
<!-- more -->
###Fragment的优点
----------------
 * adding and removing Fragment可以做动画的效果,平滑过度

 * 自动化堆栈管理,所以返回键可以删除动态添加的Fragment,最后销毁Activity,无需做过多判断

 * 集成ActionBar的标签,可以替代TabHost,ActivityGrounp,与谷歌设计风格紧密结合

 * 布局更加模块化.与原Activity中的Layout分块化,VCBase的分块化道理相同

 * 灵活准确的生命周期去管理当前View的状态记录以及横竖屏处理

 * Fragment管理的View,可同时使用在Phone和Pad上,一份代码两份机器,可重用性高

 * Is a View, More than View

 * 可以从startActivityForResult中接收到返回结果,但是View不能

 * 唯一Id标识,可以从FragmentManager中获取id对应的Fragment

###Fragment的缺点
----------------
与其说是Fragment的缺点,不如说是每个应用程序模块之间的通讯都面临地耦合问题

* Fragment之间的通讯依赖Activity使用接口管理并通知

###如何解决模块之间的通讯的耦合问题
------------------------------

####1.使用接口,让Activity扮演管理角色,负责分发消息到该窗口的子View

该方案的缺点

 * 不方便使用单元测试
 * 随着应用功能的增加,需要监听的事件越来越多,导致越来越多的接口声明以及绑定

####2.使用LocalBroadcastManager + IntentFilter解决不同组件通讯,Intent负责搭载数据
该方案的缺点

* 不方便单元测试,需要实例化Intent,填装Intent的数据,实现Broadcast receivers以及再次提取Intent中的数据
* receiver中不可做耗时操作,因为reciver是限时进程,10秒后会被系统kill掉,如果需要做耗时操作,需另外启Service来完成

####3.EventBus
 * 消息订阅者:Activity or Fragment等订阅类注册自己到EventBus中  
 * 消息发布者:只负责发布消息以及消息包装数据到EventBus
 * 回调基于命名约定以及消息包装对象
 * 方便的单元测试
