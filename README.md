#编译环境
#### 由于reactNativeAndroid ndk支持版本必须为r10e，所以项目根目录下的local.properties文件ndk路径不能指向最新的默认ndk，而需指向android-ndk-r10e，需自己根据系统环境去下载，mac版大约1g，需翻墙，下载链接教程中有列出来。
* ndk环境[官方教程](http://facebook.github.io/react-native/docs/android-building-from-source.html)，附[mac版下载链接](http://dl.google.com/android/repository/android-ndk-r10e-darwin-x86_64.zip)。

# 配置
##### 1.项目build.gradle文件需加入，否则会导致reactAndroid中的build.gradle中的下载任务编译不成功
>  
    dependencies {
        ...
        classpath 'de.undercouch:gradle-download-task:3.3.0'
        ...
    }

##### 2.运行后React Native页面报错，找不到so文件，这个是因为你的项目没有默认支持"armeabi-v7a"，需在主module build.gradle中加上
> 
 	 defaultConfig {
        ...
        ndk {
            abiFilters "armeabi-v7a"        
        }
        ...
    }  
    
# build很慢
#### 这是因为reactAndroid module中的build.gradle配置中有五个下载任务，大约会下载150M左右的文件，这几个下载文件默认是下载在build目录下的，每次编译有可能会被删除，我现在放在了module根目录下，这样就不会默认被删除了。但是第一次下载你可能还是需要build大概5到10分钟，由你的网络情况而决定。

# 遇到的一些坑
>   
    Could not get unknown property 'repositoryUrl' for project
#### [解决方案](https://stackoverflow.com/questions/43967489/could-not-get-unknown-property-repositoryurl-for-project)



###附参考文档
* [React Native For Android 源码编译](https://www.jianshu.com/p/bd4bcdceba9b)
* [React Native Android源码编译](https://www.jianshu.com/p/fbd29a9799ee)
* [从源代码编译React Native](https://reactnative.cn/docs/0.24/android-buildingfromsource.html)


