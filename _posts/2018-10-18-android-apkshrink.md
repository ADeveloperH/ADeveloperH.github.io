---
layout: post
title: APK 瘦身
categories: android知识
---

### 1 国内应用市场 ###

[那些你不知道的 APK 瘦身，让你的 APK 更小](https://juejin.im/entry/57cbb192bf22ec006c24ed00)  

[如何将 APK 大小减少 6M 的](https://juejin.im/entry/56c13ad7a633bd00587845e3)  

[我的Android进阶之旅------>Android APP终极瘦身指南](https://blog.csdn.net/ouyang_peng/article/details/51136635)  

[Android 瘦身之道 ---- so文件](https://segmentfault.com/a/1190000008995593)  

[【腾讯Bugly干货分享】Redex初探与Interdex：Andorid冷启动优化](https://blog.csdn.net/tencent_bugly/article/details/53375240)  

[压缩代码和资源](https://developer.android.com/studio/build/shrink-code)  

### 2 Google Play Store ###

#### 2.1 split apk (Build multiple APKs) ####

[Build multiple APKs 官网](https://developer.android.com/studio/build/configure-apk-splits)  

[ABI 管理](https://developer.android.com/ndk/guides/abis)  

根据 abi 进行分包，最终配置如下：
```java

import com.android.build.OutputFile

android {
    compileSdkVersion project.compileSdkVersion as int
    buildToolsVersion '27.0.3'

    defaultConfig {
        applicationId "com.noxgroup.app.cleaner"
        minSdkVersion 19
        multiDexEnabled true
        targetSdkVersion project.targetSdkVersion as int
        versionCode 5
        versionName "1.5.3"
        
		//注意：这里和 split 冲突，如果配置了 split 了，这里就不用配置 filter 了
//        ndk {
//            abiFilters 'armeabi-v7a','x86'
//        }

    }

    splits {
        abi {
			//如果将此元素设置为true，Gradle将根据您定义的ABI生成多个APK。默认值为false
            enable true
			//清除ABI的默认列表。仅在与include元素组合时使用 才能指定要添加的ABI。以下代码段将ABI列表设置为just，
			//x86并x86_64 通过调用reset()清除列表，然后使用include：
            reset()
			//指定Gradle应为其生成APK的以逗号分隔的ABI列表。仅与组合使用reset()以指定ABI的确切列表。
            include 'armeabi-v7a', 'x86'//'armeabi-v7a', 'x86', 'arm64-v8a'
			//如果true，Gradle除了per-ABI APK之外还会生成通用APK。通用APK包含单个APK中所有ABI的代码和资源。
			//默认值为false。请注意，此选项仅在splits.abi块中可用。在根据屏幕密度构建多个APK时，
			//Gradle始终会生成一个通用APK，其中包含所有屏幕密度的代码和资源。
            universalApk false
        }
    }

	//注意：这个顺序不能改变。兼容性高的版本需要小于兼容性低的，Google play 默认会从高的开始找是否符合
    ext.abiCodes = ['armeabi-v7a':1, 'arm64-v8a':2, x86:3, x86_64:4]
    android.applicationVariants.all { variant ->
        variant.outputs.each { output ->
            def baseAbiVersionCode =
                    project.android.ext.abiCodes.get(output.getFilter(OutputFile.ABI))
            if (baseAbiVersionCode != null) {
                output.versionCodeOverride =
                        baseAbiVersionCode * 10000 + variant.versionCode
            }
            output.outputFileName = "yourappname_" + defaultConfig.versionName + "_" + buildType.name + "_"  + output.versionCodeOverride + "_" + output.getFilter(OutputFile.ABI).replace("-", "") + "_" + new Date().format("yyyyMMddHHmm")+".apk"
        }
    }
}



```


#### 2.2 Android App Bundles ####

[Android App Bundle探索](https://juejin.im/entry/5b13644a6fb9a01e842b0779)  

[Android组件化 Android app Bundle](https://juejin.im/post/5b51d06cf265da0f96288ad1)  

[Android动态化框架App Bundles](https://zhuanlan.zhihu.com/p/38481475)  

[Android App Bundle 使用流程（codelabs）](https://codelabs.developers.google.com/codelabs/your-first-dynamic-app/index.html?index=..%2F..index#0)  

[Android App Bundle Demo](https://github.com/coderEvolve/Android-App-Bundle-Demo)  

[使用 Android App Bundle 提供应用和用户所需功能](https://support.google.com/googleplay/android-developer/answer/9006925)  

[Android App Bundle 官网](https://developer.android.com/platform/technology/app-bundle/)  

[About Android App Bundles 官网](https://developer.android.com/guide/app-bundle/)  

```java

常见错误：  
1.<fusing> element is missing the 'include' attribute  
解决方案：https://stackoverflow.com/questions/50869694/android-app-bundle-build-error-fusing-element-is-missing-the-include-attrib  
just add "dist:" 如：dist:include="false"


````