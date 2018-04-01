---
layout: post
title: java面试小知识
categories: 面试知识
---
### 1 java中==、equals、hashCode的区别  ###

[弄懂java中”==“、”equals“、”hashCode“](https://www.jianshu.com/p/efde145f0152)  

[Java 中的 ==, equals 与 hashCode 的区别与联系](http://blog.csdn.net/justloveyou_/article/details/52464440)  

[重写equal()时为什么也得重写hashCode()之深度解读equal方法与hashCode方法渊源](http://blog.csdn.net/javazejian/article/details/51348320) 

###  2 Java数据类型相关 ###

#### 2.1 int、char、long各占多少字节数 ####

[Java基本类型占用字节数](https://www.jianshu.com/p/fd560bc39adb)

#### 2.2 int与integer的区别 ####

[int和Integer的区别](http://blog.csdn.net/haovip123/article/details/52049856)  

[Integer.parseInt("") Integer.valueOf("")和new Integer("")之间的区别](http://blog.csdn.net/suifeng3051/article/details/52101411)

#### 2.3 String、StringBuffer、StringBuilder ####

[String，StringBuffer，StringBuilder的区别](https://www.jianshu.com/p/5435cdf1d52e)  

[深入理解java中的String](https://www.jianshu.com/p/8c161bb213c6)  

[在java中String类为什么要设计成final？](https://www.zhihu.com/question/31345592)  

[为什么String要设计成不可变的?](http://blog.csdn.net/renfufei/article/details/16808775)  

[String与Integer的相互转化](http://blog.csdn.net/u011983531/article/details/50888139)

[再解Java中的String（suprise）](http://cmsblogs.com/?p=863)

### 3 java 类相关 ###

#### 3.1 抽象类与接口  ####

[深入理解Java的接口和抽象类](https://www.cnblogs.com/dolphin0520/p/3811437.html)  

[接口和抽象类有什么区别？](https://www.zhihu.com/question/20149818)  

[Java抽象类与接口的区别](http://www.importnew.com/12399.html)  

[java提高篇（四）-----抽象类与接口](http://blog.csdn.net/chenssy/article/details/12858267)  

[JAVA的多态用几句话能直观的解释一下吗？](https://www.zhihu.com/question/30082151/answer/120520568)  

[java提高篇(四)-----理解java的三大特性之多态](https://www.cnblogs.com/chenssy/p/3372798.html)

#### 3.2 成员内部类、静态内部类、局部内部类和匿名内部类 ####

[java提高篇(八)----详解内部类](https://www.cnblogs.com/chenssy/p/3388487.html)  

[Java静态内部类、匿名内部类、成员式内部类和局部内部类](http://www.weixueyuan.net/view/6007.html)  

[Java内部类详解](https://www.jianshu.com/p/e385ce41ca5b)  
  
[深入理解 JAVA 内部类 - final 问题](https://www.jianshu.com/p/e310b56fd105)  

[java为什么匿名内部类的参数引用时final？](https://www.zhihu.com/question/21395848)  

[java提高篇(十)-----详解匿名内部类](https://www.cnblogs.com/chenssy/p/3390871.html)  

[Java匿名内部类访问外部变量，为何需被标志为final？](https://www.jianshu.com/p/609ca1c584ac)  

[闭包（计算机科学）是什么？](https://www.zhihu.com/question/24084277)

#### 3.3 静态属性和静态方法 ####

[ Java中子类是否可以继承父类的static变量和方法而呈现多态特性](http://blog.csdn.net/u010412719/article/details/49254017)  

[子类为什么不能重写父类的静态方法](http://blog.csdn.net/fg2006/article/details/6703529)  

[关于java中静态属性、静态方法的继承问题](https://www.jianshu.com/p/c2f64b94de20)  

#### 3.4 泛型 ####

[Java泛型的实现原理](http://blog.csdn.net/aoxida/article/details/50774459)  

[Java中的泛型 (上) - 基本概念和原理](http://www.cnblogs.com/yxh1008/p/6012050.html#_labelTop)  

[Java 泛型 <? super T> 中 super 怎么 理解？与 extends 有何不同？](https://www.zhihu.com/question/20400700)  
 
[Java泛型通配符extends与super](http://www.cnblogs.com/sharewind/archive/2012/11/26/2788698.html)   

[java泛型（二）、泛型的内部原理：类型擦除以及类型擦除带来的问题](http://blog.csdn.net/lonelyroamer/article/details/7868820)   

#### 3.5 final finally finalize 的区别 ####

[final finally finalize 的区别](http://www.cnblogs.com/xwdreamer/archive/2012/04/17/2454178.html) 

#### 3.6 序列化的方式 Serializable 和Parcelable 的区别 ####

[序列化与反序列化之Parcelable和Serializable浅析](http://blog.csdn.net/javazejian/article/details/52665164)  

[Android 进阶6：两种序列化方式 Serializable 和 Parcelable](http://blog.csdn.net/u011240877/article/details/72455715)  

[Parceable和Serializable都有啥区别？](https://zhuanlan.zhihu.com/p/27193528) 

### 4 java容器类 ###

[java容器类框架详解](https://adeveloperh.github.io/2017/11/java_collections_framework/)  

[java容器类](http://alexyyek.github.io/2015/04/06/Collection/)  

[java 集合类Array、List、Map区别和联系](http://justcode.ikeepstudying.com/2017/06/java-%E9%9B%86%E5%90%88%E7%B1%BBarray%E3%80%81list%E3%80%81map%E5%8C%BA%E5%88%AB%E5%92%8C%E8%81%94%E7%B3%BB/)  

#### 4.1 HashMap 原理详解 ####

[Java 8系列之重新认识HashMap](https://tech.meituan.com/java-hashmap.html)  

[HashMap内部原理解析](https://juejin.im/entry/5a5cad9b518825734978e5f4)

[Java HashMap工作原理及实现](https://yikun.github.io/2015/04/01/Java-HashMap%E5%B7%A5%E4%BD%9C%E5%8E%9F%E7%90%86%E5%8F%8A%E5%AE%9E%E7%8E%B0/)  

[HashMap实现原理分析](http://fhaoer.com/20171127-HashMap/)  

[HashMap的工作原理](http://www.androidchina.net/5561.html)  

[HashMap常见面试问题](http://www.importnew.com/7099.html)    

[HashMap的死循环(HashMap infinite loop)](http://pettyandydog.com/2016/08/28/HashMap_infinite_loop/#more)    

#### 4.2 LinkedHashMap 原理详解 ####

[Java集合-LinkedHashMap工作原理](https://www.jianshu.com/p/3650bf13f09b)

[LinkedHashMap 源码详细分析（JDK1.8）](https://segmentfault.com/a/1190000012964859)    

[Java LinkedHashMap源码解析](http://liujiacai.net/blog/2015/09/12/java-linkedhashmap/)    

#### 4.3 HashSet 原理详解 ####

[Java HashSet工作原理及实现](https://yikun.github.io/2015/04/08/Java-HashSet%E5%B7%A5%E4%BD%9C%E5%8E%9F%E7%90%86%E5%8F%8A%E5%AE%9E%E7%8E%B0/)    

[HashSet实现原理及源码分析](https://blog.csdn.net/itmyhome1990/article/details/76212556)    

[ java-Transient关键字、Volatile关键字介绍和序列化、反序列化机制、单例类序列化](https://blog.csdn.net/u010156024/article/details/48345257)    

#### 4.4 LinkedHashSet 原理详解 ####

[Java LinkedHashSet工作原理及实现](http://yikun.github.io/2015/04/09/Java-LinkedHashSet%E5%B7%A5%E4%BD%9C%E5%8E%9F%E7%90%86%E5%8F%8A%E5%AE%9E%E7%8E%B0/)    

[jdk HashSet, LinkedHashSet工作原理分析](https://fangjian0423.github.io/2016/03/30/jdk_hashset_linkedhashset/)    

#### 4.5 TreeMap 原理详解 ####

[Java提高篇（二七）-----TreeMap](https://www.jianshu.com/p/526970086e4e)

[TreeMap 源码分析](https://segmentfault.com/a/1190000012775806)    

[Java TreeMap工作原理及实现](http://yikun.github.io/2015/04/06/Java-TreeMap%E5%B7%A5%E4%BD%9C%E5%8E%9F%E7%90%86%E5%8F%8A%E5%AE%9E%E7%8E%B0/)    

[TreeMap实现原理及源码分析](https://blog.csdn.net/itmyhome1990/article/details/76213883)      
  
#### 4.6 TreeSet 原理详解 ####

[Java TreeSet工作原理及实现](http://yikun.github.io/2015/04/10/Java-TreeSet%E5%B7%A5%E4%BD%9C%E5%8E%9F%E7%90%86%E5%8F%8A%E5%AE%9E%E7%8E%B0/)      

[java TreeSet原理与应用](https://www.jianshu.com/p/342bb16d4c6c)      

#### 4.7 HashTable 原理详解 ####

[HashMap、HashTable、HashSet、concurrentHashMap 线程安全，区别，实现原理](https://zhuanlan.zhihu.com/p/34793183)

[HASHMAP、HASHTABLE、CONCURRENTHASHMAP的原理与区别](http://www.yuanrengu.com/index.php/2017-01-17.html)    

[Java集合-Hashtable实现原理源码分析](https://www.jianshu.com/p/526970086e4e)    

[Hashtable 的实现原理](https://www.beibq.cn/book/sjsa262-9221)    

#### 4.8 ConcurrentHashMap 原理详解 ####

[ConcurrentHashMap底层原理](https://juejin.im/post/5aba1030f265da23961269c6)      

[ConcurrentHashMap 原理解析（JDK1.8）](https://www.jianshu.com/p/d10256f0ebea)      

[ConcurrentHashMap总结](http://www.importnew.com/22007.html)      

#### 4.9 WeakHashMap 原理详解 ####

[WeakHashMap实现原理及源码分析](https://blog.csdn.net/itmyhome1990/article/details/77651165)      

[Java WeakHashMap 源码解析](http://liujiacai.net/blog/2015/09/27/java-weakhashmap/)      

[WeakHashMap](https://github.com/CarpenterLee/JCFInternals/blob/master/markdown/9-WeakHashMap.md)      

[WeakHashMap 注意事项](http://www.baitouwei.com/2017/06/07/WeakHashMap-%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9/)      