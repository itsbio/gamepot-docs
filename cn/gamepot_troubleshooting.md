# 故障排除

## 在64位环境中构建时，尝试NAVER ID登录（使用NAVER ID登录）时发生崩溃。（API 28以上的Android构建）

⒈ 在`AndroidManifest.xml`文件中添加以下代码

> 使用Unity时，修改/Assets/Plugins/Android/AndroidManifest.xml

```java
// TODO : <application> 请放入标签。

<application>

...

   <uses-library android:name="org.apache.http.legacy" android:required="false" />

...

</application>
```

参考）这部分可通过更换已打补丁的库作为代替。\[[gamepot-channel-naver.aar](https://kr.object.ncloudstorage.com/itsb/patch/gamepot-channel-naver.aar)\]


## 上传Play Store APK时，发生com.nhncorp.nelo2.android.util加密模式安全通知

⒈ 日志记录功能相关库因过时引发的问题

⒉ （不使用仪表盘日志功能时）在Gamepot SDK的库中删除以下列表中的库

 |||
 | :------  | :------  |
 | 1. gamepot-logger.aar |
 | 2. nelo2-android-sdk-common-0.10.2.jar |
 | 3. nelo2-android-sdk-https-0.10.2.jar |
 |||

## Line i386 x86_64 IOS Archive上传问题

⒈ 请在控制台（终端）中移动到LineSDK.framework文件位置后，逐一输入以下命令。

```text
（该代码可删除不被允许的架构。）

lipo -remove x86_64 ./LineSDK.framework/LineSDK -o ./LineSDK.framework/LineSDK
lipo -remove i386 ./LineSDK.framework/LineSDK -o ./LineSDK.framework/LineSDK
lipo -remove x86_64 ./LineSDKObjC.framework/LineSDKObjC -o ./LineSDKObjC.framework/LineSDKObjC
lipo -remove i386 ./LineSDKObjC.framework/LineSDKObjC -o ./LineSDKObjC.framework/LineSDKObjC
```

## Twitter i386 x86_64 IOS构建问题

⒈ 请在控制台（终端）中移动到TwitterCore.framework文件位置后，逐一输入以下命令。

```text
（该代码可删除不被允许的架构。）

lipo -remove x86_64 ./TwitterCore.framework/TwitterCore -o ./TwitterCore.framework/TwitterCore
lipo -remove i386 ./TwitterCore.framework/TwitterCore -o ./TwitterCore.framework/TwitterCore
lipo -remove x86_64 ./TwitterKit.framework/TwitterKit -o ./TwitterKit.framework/TwitterKit
lipo -remove i386 ./TwitterKit.framework/TwitterKit -o ./TwitterKit.framework/TwitterKit
```

## AdbrixRM i386 x86_64 IOS构建问题

⒈ 请在控制台（终端）中移动到AdBrixRM.framework文件位置后，逐一输入以下命令。

```text
（该代码可删除不被允许的架构。）

lipo -remove x86_64 ./AdBrixRM.framework/AdBrixRM -o ./AdBrixRM.framework/AdBrixRM
lipo -remove i386 ./AdBrixRM.framework/AdBrixRM -o ./AdBrixRM.framework/AdBrixRM
```


## NAVER ID登录NaverThirdPartyLogin.framework i386 x86_64问题
```text
（该代码可删除不被允许的架构。）

lipo -remove x86_64 ./NaverThirdPartyLogin.framework/NaverThirdPartyLogin -o ./NaverThirdPartyLogin.framework/NaverThirdPartyLogin
lipo -remove i386 ./NaverThirdPartyLogin.framework/NaverThirdPartyLogin -o ./NaverThirdPartyLogin.framework/NaverThirdPartyLogin
```


## Unity 2018.4.4以上、Unity 2019.2.0以上版本中的Android构建问题

⒈ 按以下方法修改`mainTemplate.gradle`文件

> 请参考TODO项目。

```java
// TODO : 删除所有使用GradleVersion的地方。

buildscript {
    repositories {
        // if (GradleVersion.current() >= GradleVersion.version("4.2")) {
            google()
            jcenter()
        // } else {
        //     jcenter()
        // }
    }
    dependencies {
        // if (GradleVersion.current() < GradleVersion.version("4.0")) {
        //     classpath 'com.android.tools.build:gradle:2.1.0'
        // } else if (GradleVersion.current() < GradleVersion.version("4.2")) {
        //     classpath 'com.android.tools.build:gradle:2.3.0'
        // } else {
                  // TODO : 请将Android gradle插件版本改为3.4.0。
            classpath 'com.android.tools.build:gradle:3.4.0'
        // }
        classpath 'com.google.gms:google-services:3.2.0'
    }
}

allprojects {
   repositories {
        flatDir {
            dirs 'libs'
        }

        // if (GradleVersion.current() >= GradleVersion.version("4.2")) {
            google()
            jcenter()
        // } else {
        //     jcenter()
        // }
   }
}


dependencies {
    // if (GradleVersion.current() >= GradleVersion.version("4.2")) {
        implementation fileTree(include: ['*.jar'], dir: 'libs')
        implementation project(":GamePotResources")
        implementation project(':Firebase')
    // } else {
    //     compile fileTree(include: ['*.jar'], dir: 'libs')
    //     compile project(":GamePotResources")
    //     compile project(':Firebase')
    // }
}

fileTree(dir: 'libs', include: ['*.aar'])
        .each { File file ->
    // println file.name
    // if (GradleVersion.current() >= GradleVersion.version("4.2")) {
        dependencies.add("implementation", [name: file.name.lastIndexOf('.').with { it != -1 ? file.name[0..<it] : file.name }, ext: 'aar'])
    // } else {
    //     dependencies.add("compile", [name: file.name.lastIndexOf('.').with { it != -1 ? file.name[0..<it] : file.name }, ext: 'aar'])
    // }
}
```

⒉ 修改Firebase相关文件

- ⒈ 通过[链接](https://kr.object.ncloudstorage.com/gamepot/Firebase_patch.zip)下载补丁文件

- ⒉ 按以下方法复制文件

    ```java
    /Firebase_patch/Assets/Firebase/Editor
     将上面路径下的文件复制到以下路径
    -> {unity project}/Assets/Firebase/Editor

    {unity project}/Assets/PlayServicesResolver/Editor
     将上面路径下的文件全部删除后复制文件到以下路径
    -> /Firebase_patch/Assets/PlayServicesResolver/Editor
    ```

- ⒊ /Assets/Plugins/Android/Firebase/res文件夹无法创建时，重新运行Unity


## （Unity）应用NAVER插件SDK（plug_sdk_4_4_7.unitypackage.unitypackage以上）时，发生IOS构建错误。

- 通过[链接](https://kr.object.ncloudstorage.com/itsb/patch/Patch_GamePotNaverLogin_20200508.zip)下载补丁文件并解压（GamePotNaver.framework）

- 请用下载的补丁文件（GamePotNaver.framework）替换当前路径下的框架。

## （IOS）应用NAVER插件SDK时，无法通过WebView登录NAVER ID。

- 请在XCode中打开info.plist。

 - 如下所示，将Naver Cafe的URLScheme值传入相应数组的第一个索引，保存以后再确认能否正常登录。
 
![gamepot_troubleshooting_01](./images/gamepot_troubleshooting_01.png)
