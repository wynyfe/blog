---
title: React-Native 打包
date: 2018-06-27 16:57:43
tags:
---
#### Android

##### step1 生成签名密匙
在项目根目录下执行下列命令
>keytool -genkey -v -keystore my-release-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000

接着会让你输入你的姓氏、组织名称、密码……最后输入‘y’表示确认，否则会重新录入信息;一定要记住自己的密码，这类信息最好截图保存

然后会在根目录下生成一个`my-release-key.keystore`的`密匙库`文件，我们把它移动到`android/app／`路径下

##### step2 配置gradle
`android/app／`路径下的`build.gradle`文件，添加如下代码，注意添加位置
```
android { 
... 
defaultConfig { ... }
signingConfigs {
release {
storeFile file(MYAPP_RELEASE_STORE_FILE)
storePassword MYAPP_RELEASE_STORE_PASSWORD
keyAlias MYAPP_RELEASE_KEY_ALIAS
keyPassword MYAPP_RELEASE_KEY_PASSWORD
}
}
...
buildTypes {
release {
...
signingConfig signingConfigs.release
}
}
}
```
PS：`MYAPP_RELEASE_STORE_FILE`等变量可以在`android／gradle.properties`中查看，并且变量值必需与生成密钥时的一致

##### step3 打包应用
* 在 `android/app/src/main／` 路径下创建 `assets` 文件夹
* 回到项目根目录，执行如下命令
> react-native bundle --assets-dest ./android/app/src/main/res/ --entry-file ./index.android.js --bundle-output ./android/app/src/main/assets/index.android.bundle --platform android --dev false

然后就能在 `assets` 文件夹下看到新文件 `index.android.bundle`
* 进入 `android/` 路径下，执行
> ./gradlew assembleRelease

##### step4 成功！
现在等待编译大约1min后，在 `android/app/build/outputs/apk/` 下，找到打包生成的 `app-release.apk`
##### 报错的情况
* 在简书某一篇教程里，step3中的命令回报错 `option '--bundle-output' missing` ，他推荐的命令如下：
> react-native bundle --platform android --dev false --entry-file index.android.js \ --bundle-output android/app/src/main/assets/index.android.bundle \ --assets-dest android/app/src/main/res/

* 在编译打包时报错，原因是`android／gradle.properties`中的密码与我在step1中输入的``092901``不一致，所以必需记住自己的输入信息
