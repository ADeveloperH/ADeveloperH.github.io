---
layout: post
title: Android 适配相关
categories: android知识
---

### 1 Android Icon 设置 ###

[Android应用图标微技巧，8.0系统中应用图标的适配](https://blog.csdn.net/guolin_blog/article/details/79417483)  
  
[Android O 新特性介绍：自适应图标（Adaptive Icons）](https://sspai.com/post/38431)  
  
[Android O 自适应图标的意义何在？Google 设计师给你答案 | 科普](https://sspai.com/post/40230)  
  
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

[Android应用保活四步曲](https://blog.csdn.net/joye123/article/details/79644567)  

[Android 进程保活--无限播放音乐](https://blog.csdn.net/u013933720/article/details/78277772)  

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

[Android判断应用或Activity是否存在](https://blog.csdn.net/u013205165/article/details/53607939)  

[根据机型适配跳转到权限设置页面](https://stackoverflow.com/questions/44383983/how-to-programmatically-enable-auto-start-and-floating-window-permissions-how-t)  

[根据机型适配跳转到权限设置页面2](https://stackoverflow.com/questions/48945300/how-to-open-window-of-autostart-application-for-all-devices)  

[根据机型适配跳转到权限设置页面3](https://stackoverflow.com/questions/36035284/how-to-enable-auto-start-for-an-app-in-xiaomi-programmatically)  

[根据机型适配跳转到权限设置页面4](https://www.ctolib.com/article/comments/26861)  


#### 7.1 Window 全屏设置 ####

```java

实现：当手机开启导航栏时仍然全屏

 public WindowManager.LayoutParams getWindowParams() {
        WindowManager.LayoutParams layoutParams;
        if (!PermissionUtil.isOverMarshmallow()) {
            // < 6.0 使用 TYPE_TOST
            if (RomUtils.checkIsOppoRom()) {
                layoutParams = new WindowManager.LayoutParams(-1, -1, WindowManager.LayoutParams.TYPE_PRIORITY_PHONE, 263176, TRANSLUCENT);
            } else {
                layoutParams = new WindowManager.LayoutParams(-1, -1, WindowManager.LayoutParams.TYPE_TOAST, 263176, TRANSLUCENT);
            }
        } else {
            if (PermissionUtil.isOverO()) {
                // >= 8.0
                layoutParams =  new WindowManager.LayoutParams(-1, -1, WindowManager.LayoutParams.TYPE_APPLICATION_OVERLAY, 263176, TRANSLUCENT);
            } else {
                layoutParams = new WindowManager.LayoutParams(-1, -1, WindowManager.LayoutParams.TYPE_SYSTEM_ALERT, 263176, TRANSLUCENT);
            }
        }
        layoutParams.screenOrientation = ActivityInfo.SCREEN_ORIENTATION_PORTRAIT;
		//布局不受限制
        layoutParams.flags |= WindowManager.LayoutParams.FLAG_LAYOUT_NO_LIMITS;
        layoutParams.x = 0;
        layoutParams.y = 0;
        NoxApplication context = NoxApplication.getInstance();
        WindowManager mWm = (WindowManager) context.getSystemService(Context.WINDOW_SERVICE);
        Display display = mWm.getDefaultDisplay();
        Point p = new Point();
        display.getRealSize(p);
        int statusHeight = ScreenUtil.getStatusHeight(NoxApplication.getInstance());
        Log.d("hj", "WindowPermissionHelper.getWindowParams: statusHeight:" + statusHeight);
        int navigationHeight = ScreenUtil.getNavigationHeight(NoxApplication.getInstance());
        Log.d("hj", "WindowPermissionHelper.getWindowParams: navigationHeight:" + navigationHeight);
        layoutParams.width = p.x;
        layoutParams.height = p.y + navigationHeight;
        Log.d("hj", "WindowPermissionHelper.getWindowParams: height:" + p.y);
        Log.d("hj", "WindowPermissionHelper.getWindowParams: width:" + p.x);
        return layoutParams;
    }

	
	View childAt = topBar.getChildAt(0);
    LinearLayout.LayoutParams layoutParams = (LinearLayout.LayoutParams) childAt.getLayoutParams();
    layoutParams.topMargin = ScreenUtil.getNavigationHeight(this);

```


[Android 如何让悬浮窗口覆盖显示在导航栏之上？](https://blog.csdn.net/wangjicong_215/article/details/72629126)  

[像360悬浮窗那样，用WindowManager实现炫酷的悬浮迷你音乐盒（上）](https://www.jianshu.com/p/95ceb0a2ed27)  

#### 7.2 Window 中监听返回键 ####

[在Activity，Service，Window中监听Home键和返回键的一些思考，如何把事件传递出来的做法！](https://blog.csdn.net/qq_26787115/article/details/52260393)  

[官网：Window 各种 Flag 详解](https://developer.android.com/reference/android/view/WindowManager.LayoutParams)

```java

注意：主要的限制在 FLAG_NOT_FOCUSABLE，WindowManager.LayoutParams.flags 中不能设置该 flag，否则监听不到返回键
可以使用：windowParams.flags &= ~FLAG_NOT_FOCUSABLE 消除该 flag

```  


### 8 Android 7.0 FileProvider 适配 ###

[Android 7.0 行为变更 通过FileProvider在应用间共享文件吧](https://mp.weixin.qq.com/s/0BFFoyJdrzkfk6k66tHtyA)  

[解决 Android N 7.0 上 报错：android.os.FileUriExposedException](https://blog.csdn.net/yy1300326388/article/details/52787853)  

[使用FileProvider解决file:// URI引起的FileUriExposedException](http://gelitenight.github.io/android/2017/01/29/solve-FileUriExposedException-caused-by-file-uri-with-FileProvider.html)  

[Android打开指定文件实践 工具类](https://juejin.im/post/5a39e330518825258b742867)  

### 9 AlarmManager 使用 ###

[关于android的alarmmanager使用过程中的坑(包括魅族手机休眠后无法启动闹钟的问题)](https://www.jianshu.com/p/6be84993d2f7)  

[定时任务，AlarmManager使用](https://www.cnblogs.com/ProtectedDream/p/6351447.html)  


### 10 AccessibilityService 使用 ###

[Android辅助功能AccessibilityService的使用](https://blog.csdn.net/u011965040/article/details/53257005)  

[Android辅助功能原理与基本使用详解-AccessibilityService](https://www.cnblogs.com/popfisher/p/7455754.html)  

[AccessibilityService 从入门到出轨](https://juejin.im/post/584bd285a22b9d0058d7713e)  

[Android自动化测试中AccessibilityService获取控件信息（1）](https://blog.csdn.net/itfootball/article/details/21953763)  

[AccessibilityService分析与防御](https://lizhaoxuan.github.io/2018/01/27/AccessibilityService%E5%88%86%E6%9E%90%E4%B8%8E%E9%98%B2%E5%BE%A1/)  


### 11 Android 自定义应用选择器 ###

[Android-自定义应用选择器](https://www.jianshu.com/p/3f65576f89b7)  



### 12 迎接 Androidx ###

问题：

[Androidx和Android support库共存问题解决](https://www.jianshu.com/p/f7a7a8765294)  

[Android:你好,androidX！再见,android.support](https://www.jianshu.com/p/41de8689615d)  


参考：

[support 库官网](https://developer.android.com/topic/libraries/support-library/revisions)  

[AndroidX Overview 官网](https://developer.android.com/jetpack/androidx/)  

[原包转换为androidx（Migrating to AndroidX）](https://developer.android.com/jetpack/androidx/migrate)  




### 13 Notification 监听 ###

[NotificationListenerService的那些事儿](https://www.jianshu.com/p/981e7de2c7be)  

[NotificationListenerService不能监听到通知，研究了一天不知道是什么原因？](https://www.zhihu.com/question/33540416)  

[NotificationCollectorMonitorService.java](https://gist.github.com/xinghui/b2ddd8cffe55c4b62f5d8846d5545bf9)  

[一次 NotificationListenerService 体验](https://blog.csdn.net/u013836857/article/details/82732906)  

[Android利用NotificationListenerService实现消息盒子功能](https://blog.csdn.net/Vanswells/article/details/81033280)  


#### 13.1 通知栏适配 ####

[Android通知栏介绍与适配总结](https://iluhcm.com/2017/03/12/experience-of-adapting-to-android-notifications/)  

[Android推送通知权限判断及跳转到权限设置界面(完善兼容8.0)](https://zhuanlan.zhihu.com/p/46313532)  

[android 8.0 获取通知栏开关状态](https://www.jianshu.com/p/28b8c0391c8d)  










