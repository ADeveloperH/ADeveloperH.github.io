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


### 5 Android 权限适配 ###

[Android M 运行时权限实践全解析](https://www.jianshu.com/p/33a31c967d5e)  

[一句代码搞定权限请求，从未如此简单](https://www.jianshu.com/p/c69ff8a445ed)  

[Android6.0动态权限shouldShowRequestPermissionRationale的含义](https://blog.csdn.net/wangpf2011/article/details/80589648)  

[官：在运行时请求权限](https://developer.android.com/training/permissions/requesting?hl=zh-cn)  

[官：系统权限](https://developer.android.com/guide/topics/security/permissions?hl=zh-cn#normal-dangerous)  

### 6 进程保活相关（应用锁需求） ###

[Android进程保活招数概览](https://www.jianshu.com/p/c1a9e3e86666)  

[Tinker隐藏Notification方案](https://github.com/Tencent/tinker/blob/master/tinker-android/tinker-android-lib/src/main/java/com/tencent/tinker/lib/service/TinkerPatchService.java)  

[android进程保活实践](https://www.jianshu.com/p/53c4d8303e19)  

[android进程保活实践：下篇](https://www.jianshu.com/p/7cdae4f7763a)  

[Android通过JobScheduler与设置前台服务实现进程保活](https://www.jianshu.com/p/f9322c15579a)  

[Android 进程常驻（0）----MarsDaemon使用说明](https://blog.csdn.net/marswin89/article/details/50917098)  

[后台执行限制](https://developer.android.google.cn/about/versions/oreo/background#broadcasts)  

[进程保活方案](https://www.jianshu.com/p/845373586ac1)  

[关于 Android 进程保活，你所需要知道的一切](https://www.jianshu.com/p/63aafe3c12af)  


[Android AppLock(应用锁)开发](https://www.jianshu.com/p/dff749ae2339)  

[通过 ANDROID 辅助功能「ACCESSIBILITY SERVICE」 检测任意前台界面](http://effmx.com/articles/tong-guo-android-fu-zhu-gong-neng-accessibility-service-jian-ce-ren-yi-qian-tai-jie-mian/)  

### 7 添加 Window 权限适配 ###

```java
总结：
API <= 24(7.0) 使用 TYPE_TOAST 漏洞可以不用申请权限，直接显示
API >= 25(7.1.1) TYPE_TOAST 漏洞已修复，需要申请“允许显示在其他应用上层”权限，使用 TYPE_SYSTEM_ALERT
API >= 26(8.0) 系统将会限制 TYPE_TOAST 的使用，会直接抛出异常，使用 TYPE_APPLICATION_OVERLAY

```

[Android 悬浮窗权限各机型各系统适配大全](https://blog.csdn.net/self_study/article/details/52859790)  

[FloatWindowPermission](https://github.com/zhaozepeng/FloatWindowPermission)  

[Android悬浮窗遇到的那些坑](https://www.jianshu.com/p/2229d4a12269)  

[FFloater](https://github.com/ChristianFF/FFloater)  

