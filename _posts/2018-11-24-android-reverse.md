---
layout: post
title: 逆向基础篇
categories: android 逆向
---

### 1 Android 锁屏密码加密分析 ###

#### 1.1 uiautomatorview 的使用 ####

```java

工具路径：D:\SDK\tools\bin

```

[Android自动化测试工具 UiAutomator使用详解](https://www.jianshu.com/p/5b84dd220a92)  


#### 1.2 busybox 使用 ####

```java
busybox 安装命令：

E:\reversetool\busybox\busybox64.exe --install E:\reversetool\busybox\install

安装之后配置环境变量即可正常使用

```

[Windows 10 安装Busybox](https://becoder.org/using-windows-10-as-linux-with-busybox-w32-and-clink/)  

[官网地址](https://frippery.org/busybox/)  

[Android自动化测试工具 UiAutomator使用详解](https://www.jianshu.com/p/5b84dd220a92)  

## 2 JNI 开发 ##

#### 2.1 CMake 方式搭建环境 ####

[Android NDK 入门与实践之 CMake](https://zhuanlan.zhihu.com/p/32750723)  

[Android Studio配置CMake开发NDK](https://www.jianshu.com/p/1e14dcc81c3c)  

[Android NDK开发扫盲及最新CMake的编译使用](https://juejin.im/post/595da4e25188250d8b65ddbf)  

[官网](https://developer.android.com/studio/projects/add-native-code?utm_source=android-studio#ndkCompile)

```java

注意：
1.和 JNI 相关的文件生成目录在：.externalNativeBuild
2.执行步骤，创建 native 方法，Make Project 进入 \app\build\intermediates\classes\debug 目录，执行命令
javah com.adeveloperh.androidreversestudy.jni.JNIUtils，拿到 \app\build\intermediates\classes\debug 目录下对应生成的 .h 文件，copy 有用的信息 JNIEXPORT void JNICALL Java_com_adeveloperh_androidreversestudy_jni_JNIUtils_sayHello
  (JNIEnv *, jclass); 到 .cpp 文件，在里面写对应的逻辑，即可

3.增加的 .cpp 文件要添加到 CMakeLists.txt 的 add_library 中

4.在 .cpp 文件中需要包含如下内容（生成的 .h 文件中也有）：
	#include <jni.h> 和 extern "C"，需要有 extern "C"，否则会报错 No implementation found for ...
	千万注意：extern "C"{} 大括号需要包含所有的 native 方法，否则会报错 No implementation found for
```

[Android Studio NDK CMake 指定so输出路径以及生成多个so的案例与总结](https://blog.csdn.net/b2259909/article/details/58591898)

#### 2.2 基本知识点 ####

[JNI与NDK](https://www.jianshu.com/p/61b1bd2fa872)

[C++项目中的extern "C" {}](https://www.cnblogs.com/skynet/archive/2010/07/10/1774964.html)

[C++程序员如何向一个java工程师解释extern "C"的作用](https://blog.csdn.net/wangshubo1989/article/details/50784124)

  

### 3. ADB 常用命令 ###

```java

adb devices:查看当前连接的设备, 连接到计算机的android设备或者模拟器将会列出显示 

adb start-server:开启ADB服务

adb kill-server:关闭ADB服务

adb connect 192.168.1.61:通过局域网 IP 连接设备

adb disconnect 192.168.1.61:断开设备

adb install -r (APK路径):安装一个apk , -r 代表如果apk已安装，重新安装apk并保留数据和缓存文件。apk路径则可以直接将apk文件拖进cmd窗口

adb uninstall（apk包名):直接卸载

adb uninstall -k (apk包名):卸载 app 但保留数据和缓存文件

adb shell pm list packages:列出手机装的所有app的包名

adb shell pm list packages -s:列出系统应用的所有包名

adb shell pm list packages -3:列出除了系统应用的第三方应用包名

adb shell pm clear（apk包名）:清除应用数据与缓存

adb shell am start -n com.helloshan.demo/.MianActivity:启动应用

adb shell am force-stop （apk包名):强制停止应用 

adb remount:获取文件的读写权限(有些设备并不能直接adb remount，必须要先以root身份进入，先执行adb root，在执行adb remount )

adb logcat:查看日志

adb shell wm size :查看屏幕分辨率



```
### 4 文件解析 ###

#### 4.1 readelf 工具使用及 so 文件解析 ####

[windows 安装cygwin教程](https://blog.csdn.net/chunleixiahe/article/details/55666792)

#### 4.2 XML 解析 ####

```java

方法一：使用 SDK 提供的 aapt 来解析，命令如下：

命令1：输出所有的资源信息

D:\SDK\build-tools\28.0.3\aapt l -a E:\DEX\apk\zz.dela.cmcc.traffic_47.apk > E:\reversetool\aapt\result.txt

命令2：查看需要查看的资源文件xml

D:\SDK\build-tools\28.0.3\aapt dump xmltree E:\DEX\apk\zz.dela.cmcc.traffic_47.apk  res/layout/activity_set_gesturelock_explain.xml> E:\reversetool\aapt\result.txt

方法二：自己解析 xml 具体代码已上传 github

方法三：使用下边的 apktool 工具进行解析
```

#### 4.3 resource.arsc 文件解析 ####

#### 4.4 dex 文件解析 ####


### 5 工具集合 ###

#### 5.1 SDK 中 aapt 的使用 ####

```java

1.解析 xml 文件

命令1：输出所有的资源信息

D:\SDK\build-tools\28.0.3\aapt l -a E:\DEX\apk\zz.dela.cmcc.traffic_47.apk > E:\reversetool\aapt\result.txt

命令2：查看需要查看的资源文件xml

D:\SDK\build-tools\28.0.3\aapt dump xmltree E:\DEX\apk\zz.dela.cmcc.traffic_47.apk  res/layout/activity_set_gesturelock_explain.xml> E:\reversetool\aapt\result.txt

```

[aapt命令](https://blog.csdn.net/lujh06/article/details/82012103)

[Android aapt](https://elinux.org/Android_aapt)

#### 5.2 apktool 使用 ####
```java

作用：资源文件的获取，可以提取出图片文件和布局文件进行查看

```

[APKTool 官网](https://ibotpeaches.github.io/Apktool/)

[APKTool 源码](https://github.com/iBotPeaches/Apktool)

[Android APK反编译 apktool使用教程](https://blog.csdn.net/ysc123shift/article/details/52985435)

[Android逆向之旅---反编译利器Apktool和Jadx源码分析以及错误纠正](https://blog.csdn.net/jiangwei0910410003/article/details/51671019)

#### 5.3 dex2jar 及 jd-gui 的使用 ####

```java

dex2jar 作用：将apk反编译成java源码（classes.dex转化成jar文件）

jd-gui 作用：查看APK中的classes.dex转化成的jar文件，即源码文件

常用命令：
d2j-dex2jar.bat xxx.dex

```

[下载地址](https://sourceforge.net/projects/dex2jar/)

[apktool、dex2jar、jd-gui的区别及详解](https://blog.csdn.net/themelove/article/details/53126360)

[Android apk反编译之旅——（二）dex2jar-2.0和jd-gui1.4的使用](https://blog.csdn.net/renwudao24/article/details/79724600)

#### 5.4 jadx 使用 ####

```java

作用：相当于apktool+dex2jar+jd-gui

优点：
1.图形化的界面。
2.拖拽式的操作。
3.反编译输出 Java 代码。
4.导出 Gradle 工程。


下载：直接在 github 下 DownLoad 中下载即可

查看中文字符串：Resources -> resources.arsc -> res -> values-zh-rCN -> strings


````

[源码地址](https://github.com/skylot/jadx)

[Android 反编译利器，jadx 的高级技巧](https://segmentfault.com/a/1190000012180752)


