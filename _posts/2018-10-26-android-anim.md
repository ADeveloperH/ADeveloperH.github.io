---
layout: post
title: 动画相关
categories: android知识
---

### 1 View 切换之 ViewFlipper 使用 ###

[ViewFlipper(翻转视图)使用详解](https://blog.csdn.net/my_rabbit/article/details/71170524)  

[Android：ViewFlipper实现的View切换](http://www.dengzhr.com/others/mobile/703)  


### 2 View 切换之 ViewSwitcher 使用 ###

[Android ViewSwitcher简介和使用](https://blog.csdn.net/zhangphil/article/details/48312811)  


### 3 自定义 View 实现动画 ###

#### 3.1 自定义控件 ####

[专家博客：自定义控件集合](https://blog.csdn.net/harvic880925)  

[Android 自定义 View 常见效果集合](https://www.kancloud.cn/digest/wingscustomview/129798)  

#### 3.2 贝塞尔曲线妙用动画效果实现 ####

[三次贝塞尔曲线练习之弹性的圆](http://www.jcodecraeer.com/a/anzhuokaifa/androidkaifa/2015/0915/3457.html)  

[Android 自定义 View 常见效果集合](https://www.kancloud.cn/digest/wingscustomview/129798)  

[Android开发之贝塞尔曲线进阶篇（仿直播送礼物，饿了么购物车动画）](https://cloud.tencent.com/developer/article/1032544)  

[Bezier曲线在Android动画中的应用](https://www.jianshu.com/p/fea4d1f6512a)  

[贝塞尔曲线开发的艺术](https://www.jianshu.com/p/55c721887568)  

[安卓自定义View进阶 - 贝塞尔曲线](https://blog.csdn.net/u013831257/article/details/51281136)  

[Path从懵逼到精通（2）——贝塞尔曲线](https://juejin.im/post/58ce7f0461ff4b006c9a5e66)  

[Android-贝塞尔曲线](https://blog.csdn.net/z82367825/article/details/51599245)  

[wing带你玩转自定义view系列（1） 仿360内存清理效果](https://blog.csdn.net/wingichoy/article/details/50500479)  

#### 3.3 等速螺线（阿基米德螺线） 动画效果实现 ####

[极坐标系和直角坐标系](https://wenku.baidu.com/video/course/v/b3aacc6c03cca6b554559b997a4596b2)  

[等速螺线（阿基米德螺线)](http://xuxzmail.blog.163.com/blog/static/251319162009739937397/)  

[有趣的螺线](https://www.jianshu.com/p/11bdec703c9a)  

[高等数学图形与动画：目录 ](http://xuxzmail.blog.163.com/blog/static/251319162009614101444586/)  


### 4 九宫格手势锁实现  ###

#### 4.1 参考 ####

[PatternLocker](https://github.com/ihsg/PatternLocker)  

#### 4.2 发光效果实现 ####

[自定义View-第十四步：setShadowLayer阴影与SetMaskFilter发光效果](https://www.jianshu.com/p/2f1024f9c554)  

[Android 画笔Paint](http://wuxiaolong.me/2016/08/20/Paint/)  

[Android 画布Canvas](http://wuxiaolong.me/2016/08/27/Canvas/)  

[Android Canvas 方法总结](https://www.jianshu.com/p/f69873371763)  

[Android 圆角、圆形 ImageView 实现](https://juejin.im/post/5b305f73f265da59b653b08d)  

#### 4.3 判断九宫格两点直线间是否包含其他点，判断三点共线 ####

[三点共线判断](http://yiminghe.iteye.com/blog/568666)  

[三点共线判断算法](http://oofoof.blog.163.com/blog/static/192924037201111882549437/)  

[海伦公式](https://baike.baidu.com/item/%E6%B5%B7%E4%BC%A6%E5%85%AC%E5%BC%8F)  

```java

判断九宫格两点直线间是否包含其他点总结：
1、九宫格点较少，直接使用穷举法
2、满足一下条件(两点分别为S(x1,y1),E(x2,y2),x = id / 3 , y = id % 3))：
a.|x1-x2| > 1 || |y1-y2|>1
b.在两点的范围内遍历[S,E]
c.三点共线，利用海伦面积公式：p=a || p=b || p=c
d.找到一个点遍历即可结束

````


### 5 拖拽删除动画 ###

#### 5.1 RecyclerView 之 SnapHelper 实现 ViewPager 效果 ####

[使用 RecyclerView 实现 Gallery 画廊效果，并控制 Item 停留位置](http://godcoder.me/2017/02/06/%E4%BD%BF%E7%94%A8%20RecyclerView%20%E5%AE%9E%E7%8E%B0%20Gallery%20%E7%94%BB%E5%BB%8A%E6%95%88%E6%9E%9C%EF%BC%8C%E5%B9%B6%E6%8E%A7%E5%88%B6%20Item%20%E5%81%9C%E7%95%99%E4%BD%8D%E7%BD%AE/)  

[Android中使用RecyclerView + SnapHelper实现类似ViewPager效果](https://www.jianshu.com/p/ef3a3b8d0a77)  

[仿微信朋友圈发表图片拖拽和删除功能](https://www.jianshu.com/p/373010a9f759)  


#### 5.2 RecyclerView 之 ItemTouchHelper 实现拖拽####

[仿微信朋友圈发表图片拖拽和删除功能](https://www.jianshu.com/p/373010a9f759)  

[DragPhotoView](https://github.com/githubwing/DragPhotoView)  


### 6 Shape 相关 ###

#### 6.1 Shape 实现三角形气泡背景效果 ####

[Android 通过 shape 实现三角形气泡效果](https://blog.csdn.net/hust_twj/article/details/78600789)  

### 7 Shimmer 微光效果实现 ###


[facebook 开源地址](https://github.com/facebook/shimmer-android)  

[shimmer 官方文档](http://facebook.github.io/shimmer-android/)  

[shimmer Text 开源地址](https://github.com/RomainPiel/Shimmer-android)  


```java  

引入 shimmer build 失败需要执行的命令（在上边的官方文档里）：
Install the latest code to your local repository
gradlew shimmer:installArchives

Install the sample app
gradlew sample:installDebug

````


### 8 lottie 实现 ###

[lottie 开源地址](https://github.com/airbnb/lottie-android)  

[lottie 官方文档](http://airbnb.io/lottie/android/android.html)  

[lottie 支持的 UI 特性](http://airbnb.io/lottie/supported-features.html)  

#### 8.1 AE 安装及使用教程 ####

[AE 安装](http://www.dayanzai.me/after-effects-cc-2014.html)  
