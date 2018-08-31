---
layout: post
title: Android 适配相关
categories: android知识
---

### 1 Android Icon 设置 ###

[Android Asset Studio](https://romannurik.github.io/AndroidAssetStudio/index.html)  
  
[使用 Image Asset Studio 创建应用图标（官网）](https://developer.android.com/studio/write/image-asset-studio?hl=zh-cn)  

[图标在线生成工具Android Asset Studio的使用](http://www.jcodecraeer.com/plus/view.php?aid=7823)  

[Android神兵利器之Image Asset Studio](https://www.jianshu.com/p/e335581a6a23)  

[阿里巴巴矢量图库](http://www.iconfont.cn/)  

[Android O 新特性介绍：自适应图标（Adaptive Icons）](https://sspai.com/post/38431)  

### 2 Android 启动页适配 ###

冷启动设置的启动页的方案：

[Android APP启动优化](http://wuxiaolong.me/2017/03/13/appStart/)  

[用layer-list实现图片旋转叠加、错位叠加、阴影、按钮指示灯](http://www.cnblogs.com/tianzhijiexian/p/3889770.html)  

[resource xml 使用官方文档](https://developer.android.com/guide/topics/resources/drawable-resource#Scale)  

问题描述：  
启动页设置 "android:windowBackground" 后在部分宽高比下显示被拉伸。

解决方案：
[Android 启动背景图怎么适配？【已解决】](https://github.com/android-cn/android-discuss/issues/715)  

```java

<?xml version="1.0" encoding="utf-8"?>
<layer-list xmlns:android="http://schemas.android.com/apk/res/android"
    android:opacity="opaque">

    <item android:drawable="@color/black"/>

    <item>
        <bitmap android:src="@drawable/splash_bg" android:gravity="center"/>
    </item>
</layer-list>

注意：全屏的启动页建议使用.9图，否则使用 layer-list 显示效果仍然不佳。.9图文件大小过大，微信启动不设置 windowBackground ，通过设置 SplashActivity 的 ImageView scaletype 为 centerCrop 来适配

```

### 3 Android StatusBar 适配 ###

[StatusBarUtil](https://github.com/ADeveloperH/StatusBarUtil)  


问题：  
1. 状态栏遮挡 contentView 显示的内容

[解决Android Toobar与状态栏重叠](https://blog.csdn.net/zifeiyu12345/article/details/79000164)  

[Android沉浸状态栏(StatusBar)兼容方案](https://www.jianshu.com/p/648176c8b67e)  


### 4 Android 屏幕适配 ###

[Android 目前最稳定和高效的UI适配方案](https://www.jianshu.com/p/a4b8e4c5d9b0)  

[dimens_sw](https://github.com/ladingwu/dimens_sw)  

[一种极低成本的Android屏幕适配方式（头条）](https://mp.weixin.qq.com/s?__biz=MzI1MzYzMjE0MQ==&mid=2247484502&idx=2&sn=a60ea223de4171dd2022bc2c71e09351&scene=21#wechat_redirect)  

[支持多种屏幕（官方）](https://developer.android.com/guide/practices/screens_support)  

[Android 屏幕适配从未如斯简单（8月10日最终更新版）](https://juejin.im/post/5b6250bee51d451918537021)  

[屏幕适配问题汇总及解决 ](https://github.com/Blankj/AndroidUtilCode/issues/597)  

[骚年你的屏幕适配方式该升级了!-今日头条适配方案](https://juejin.im/post/5b7a29736fb9a019d53e7ee2)  