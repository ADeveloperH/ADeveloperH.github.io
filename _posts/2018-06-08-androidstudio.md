---
layout: post
title: AndroidStudio相关
categories: 开发工具总结
---

### 1、常用插件 ###

1、GsonFormat

2、查看数据库文件：SQLSOUT 插件

[SQLScout (SQLite Support) ](https://plugins.jetbrains.com/plugin/8322-sqlscout-sqlite-support-)  

### 2、常用模板及自定义模板 ###


[android studio自定义类和方法的注释](https://blog.csdn.net/u013168615/article/details/50073257)  


[AndroidStudio中代码模板的使用](https://blog.csdn.net/wubihang/article/details/51228752)  

### 3、AndroidStudio主题设置 ###

[IntelliJ IDEA主题网站](http://color-themes.com/?view=index)  

[Android Studio有哪些值得推荐的主题背景？](https://www.zhihu.com/question/38958773)  

[该为你的Android Studio 打造一个炫酷的个性化主题了](https://juejin.im/post/58ea37ae0ce46300586427b6)  


### 4、常用小知识 ###

- AndroidStudio基本使用教程（可下载pdf查看）：  

	[Android Studio 使用艺术](https://legacy.gitbook.com/book/quanke/android-studio/details)  

----------

- AndroidStudio运行翻译编辑器（可查看是否遗漏）：  
打开res文件夹，然后打开values文件夹找到string.xml文件夹，右键单击strings.xml（不是文件夹），选择Open Translations Editor管理String资源翻译编辑器提供了查看所有你的string资源的视图和当前的本地化翻译。可以在视图中进行操作。

### 5、编译打包相关、 ###

#### 5.1 Android Studio中Make Project，Clean Project，Rebuild Project区别  #### 

Make Project：编译Project下所有Module，一般是自上次编译后Project下有更新的文件，不生成apk。  

Make Selected Modules：编译指定的Module，一般是自上次编译后Module下有更新的文件，不生成apk。  

Clean Project：删除之前编译后的编译文件，并重新编译整个Project，比较花费时间，不生成apk。  

Rebuild Project：先执行Clean操作，删除之前编译的编译文件和可执行文件，然后重新编译新的编译文件，不生成apk，这里效果其实跟Clean Project是一致的，这个不知道Google搞什么鬼～～  

Build APK：前面4个选项都是编译，没有生成apk文件，如果想生成apk，需要点击Build APK。  

Generate Signed APK：生成有签名的apk。  

注意：
对于Clean和Rebuild看到最后的效果是一样的。平时小的改动直接用Make Project就可以，可以看到只有它有快捷方式，表明这个功能要经常用。对于一些大的改动比如更新lib，大功能修改等，用Clean或Rebuild，毕竟这两个编译起来要费时间。
如果有的时候死活编译不过，多试试Clean吧，会有意想不到的效果！

### 5.2 如何选择 compileSdkVersion, minSdkVersion 和 targetSdkVersion ###

[如何选择 compileSdkVersion, minSdkVersion 和 targetSdkVersion](https://chinagdg.org/2016/01/picking-your-compilesdkversion-minsdkversion-targetsdkversion/)  

[如何选择 compileSdkVersion, minSdkVersion 和 targetSdkVersion](https://github.com/yubenben/android_learning_notes/blob/master/src/Android%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0%EF%BC%9A%E5%A6%82%E4%BD%95%E9%80%89%E6%8B%A9compileSdkVersion%2CminSdkVersion%E5%92%8CtargetSdkVersion.md)  

[如何选择 compileSdkVersion, minSdkVersion 和 targetSdkVersion](https://blog.csdn.net/a_long_/article/details/77094237)  

[AndroidStudio、gradle、buildToolsVersion关系](https://blog.csdn.net/lixin88/article/details/61196274)  

#### 5.2 build.gradle 文件 ####
- Project:build.gradle是用来配置项目的构建任务.	默认的build.gradle内容如下:
```java
//项目构建文件，你可以到各子项目/模块添加常用的配置选项.
buildscript	{
//Android插件从这个仓库中下载
repositories	{
jcenter()	//	依赖仓库源的别名,兼容maven的远程中央仓库
}
//依赖
dependencies	{
//	android	gradle插件
classpath	'com.android.tools.build:gradle:2.2.0-alpha1'
//	提示:
//请不要在此处添加应用程序依赖;它们应该在单个Module(模块)build.gradle文件
//这里添加的应该只是Project的依赖
}
}
//此处配置Project中默认的仓库源,包括每个module的依赖
//这样每个module就不用单独配置仓库了
allprojects	{
	repositories	{
	jcenter()
	}
}
//buildscript中的repositories是指定Android插件的仓库源.
//allprojects中的repositories是指定整个Project中默认的仓库源.
//	任务类型是	Delete
//	clean任务就是删除项目根目录下的build目录(build为输出目录)
task	clean(type:	Delete)	{
	delete	rootProject.buildDir
}
//	打包前执行clean任务
```

- 模块构建配置文件:build.gradle.Module:build.gradle是用来配置模块的构建任务.默认的build.gradle文件内容如下:
```java
//插件:
//这个module是一个android程序,使用com.android.application
//如果是android库,应该使用com.android.library
apply	plugin:	'com.android.application'
android	{//android程序构建需要配置的参数
//编译使用的SDK版本
compileSdkVersion	23
//buildtool版本
buildToolsVersion	"23.0.2"
defaultConfig	{//默认配置
applicationId	"com.wirelessqa.basebuildsample"	//apk包名
//最小SDK版本
minSdkVersion	16
//目标SDK版本
targetSdkVersion	23
//version	code
versionCode	1
//应用程序的版本
versionName	"1.0"
//android单元测试test	runner
testInstrumentationRunner	"android.support.test.runner.AndroidJUnitRunner"
}
//构建类型,	此处配置debug和release版本的一些参数,像混淆、签名配置.
buildTypes	{
//release版本的配置
release	{
//是否开启混淆
minifyEnabled	false
//指定混淆文件及混淆规则配置文件的位置
proguardFiles	getDefaultProguardFile('proguard-android.txt'),	'proguard-rules.pro'
	}
	}
}
//模块依赖
dependencies	{
//编译依赖libs目录下所有jar包
compile	fileTree(dir:	'libs',	include:	['*.jar'])
//编译依赖appcompat库
compile	'com.android.support:appcompat-v7:23.4.0'
}
```
模块构建配置文件:build.gradle也可以在项目结构中配置