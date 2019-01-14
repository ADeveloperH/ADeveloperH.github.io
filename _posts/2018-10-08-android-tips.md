---
layout: post
title: 常用小知识
categories: android知识
---

### 1 系统语言切换相关 ###

[Android 7.0多语言支持开发浅析](https://blog.csdn.net/cekiasoo/article/details/53012646)  

[Android 项目开发填坑记 - 获取系统语言(兼容7.0)](https://likfe.com/2017/05/10/android-sys-language/)  

[Android中监听语言变化的两种方式](https://blog.csdn.net/yin1031468524/article/details/75208859)  

改变系统语言后，重新进入处于后台的APP，会重走onCreate方法：
[Android如何去处理运行时配置的改变？](https://www.jianshu.com/p/fdf368fd1ecc)  

#### 1.1 阿拉伯语适配（RTL） ####

[双向性](https://www.mdui.org/design/usability/bidirectionality.html#)  

[Android RTL 及小语种 适配](https://nomasp.com/2017/12/05/Android-RTL-Language/)  

[Android阿拉伯适配rtl](https://www.jianshu.com/p/4ada88074ce4)  


### 2 SharedPreference 导致 ANR  ###

ANR 如下(主要集中在 5.0 和 5.1 三星等手机上)：

```java
"main" prio=5 tid=1 Waiting
  | group="main" sCount=1 dsCount=0 obj=0x77751000 self=0xb4427800
  | sysTid=3377 nice=-4 cgrp=default sched=0/0 handle=0xb6fdebec
  | state=S schedstat=( 0 0 0 ) utm=94718 stm=70129 core=2 HZ=100
  | stack=0xbe4f6000-0xbe4f8000 stackSize=8MB
  | held mutexes=
  at java.lang.Object.wait! (Native method)
- waiting on <0x0bbd135f> (a java.lang.Object)
  at java.lang.Thread.parkFor (Thread.java:1220)
- locked <0x0bbd135f> (a java.lang.Object)
  at sun.misc.Unsafe.park (Unsafe.java:299)
  at java.util.concurrent.locks.LockSupport.park (LockSupport.java:157)
  at java.util.concurrent.locks.AbstractQueuedSynchronizer.parkAndCheckInterrupt (AbstractQueuedSynchronizer.java:813)
  at java.util.concurrent.locks.AbstractQueuedSynchronizer.doAcquireSharedInterruptibly (AbstractQueuedSynchronizer.java:973)
  at java.util.concurrent.locks.AbstractQueuedSynchronizer.acquireSharedInterruptibly (AbstractQueuedSynchronizer.java:1281)
  at java.util.concurrent.CountDownLatch.await (CountDownLatch.java:202)
  at android.app.SharedPreferencesImpl$EditorImpl$1.run (SharedPreferencesImpl.java:363)
  at android.app.QueuedWork.waitToFinish (QueuedWork.java:88)
  at android.app.ActivityThread.handleStopActivity (ActivityThread.java:4615)
  at android.app.ActivityThread.access$1300 (ActivityThread.java:211)
  at android.app.ActivityThread$H.handleMessage (ActivityThread.java:1734)
  at android.os.Handler.dispatchMessage (Handler.java:102)
  at android.os.Looper.loop (Looper.java:145)
  at android.app.ActivityThread.main (ActivityThread.java:6946)
  at java.lang.reflect.Method.invoke! (Native method)
  at java.lang.reflect.Method.invoke (Method.java:372)
  at com.android.internal.os.ZygoteInit$MethodAndArgsCaller.run (ZygoteInit.java:1404)
  at com.android.internal.os.ZygoteInit.main (ZygoteInit.java:1199)

```

[SharedPreference如何阻塞主线程](https://www.jianshu.com/p/63ee8587de3f)  

[How to analyze ANR in sharedPreferences](https://stackoverflow.com/questions/36905415/how-to-analyze-anr-in-sharedpreferences#)  

[SharedPreferences的apply和Commit方法的那些坑](http://www.cloudchou.com/android/post-988.html)  

[SharedPreferences调用导致的ANR分析](https://blog.csdn.net/u010335298/article/details/72865451)  

[对 SharedPreferences 再多一点了解](https://extremej.itscoder.com/shared_preferences_source/)  

[Android SharedPreferences的理解与使用](https://juejin.im/post/5adc444df265da0b886d00bc)  

[深入理解 Android 中的 SharedPreferences](https://juejin.im/entry/57dfa5fa8ac24700616ce971)  

[彻底搞懂 SharedPreferences](https://juejin.im/entry/597446ed6fb9a06bac5bc630)  

[官：SharedPreferences.Editor](https://developer.android.com/reference/android/content/SharedPreferences.Editor.html#apply())  


### 3 Manifest 中属性相关 ###

[AndroidManifest.xml文件--Application详解](https://www.jianshu.com/p/f535c0f6f65f)  

[(转) Android 让应用手动管理应用的数据目录](http://light3moon.com/2015/01/26/[%E8%BD%AC]%20Android%20%E8%AE%A9%E5%BA%94%E7%94%A8%E6%89%8B%E5%8A%A8%E7%AE%A1%E7%90%86%E5%BA%94%E7%94%A8%E7%9A%84%E6%95%B0%E6%8D%AE%E7%9B%AE%E5%BD%95/)  

[Android Activity标签属性](https://www.jianshu.com/p/8598825222cc)  


### 4 Glide 相关 ###

#### 4.1 Glide 加载应用图标 ####

[Manage all your Glides in a single class with GlideAppModule on Android](https://medium.com/@nuhkocaa/manage-all-your-glides-in-a-single-class-with-glidemodule-on-android-4856ee4983a1)  

[Glide4.x加载应用图标](https://blog.csdn.net/jallv/article/details/83618504)  


#### 5 Dialog 相关 ####

#### 5.1 自定义的AlertDialog无法弹出键盘 ####

[自定义的AlertDialog无法弹出键盘](https://blog.csdn.net/zxyyohou/article/details/80338222)  

