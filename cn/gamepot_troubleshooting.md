# Troubleshooting

> ### 这是机器翻译的文档，可能在词汇，语法或语法上有错误。 我们很快会为您提供由专业翻译人员翻译的文档。
>
> #### 如有任何疑问，请[联系我们]（https://www.ncloud.com/support/question）。
>
> 我们将尽一切努力进一步改善我们的服务。

## 在 64 位环境中构建时，尝试登录 Naver ID 时发生崩溃。 （Android 构建的 API 28 或更高版本）

⒈ `AndroidManifest.xml` 将以下代码添加到文件中

> 对于 Unity，请编辑/Assets/Plugins/Android/AndroidManifest.xml

```java
// TODO : <application> 请把它放在标签内。

<application>

...

   <uses-library android:name="org.apache.http.legacy" android:required="false" />

...

</application>
```

ref.) 可以通过替换已修补的库来替换它。 \[[gamepot-channel-naver.aar](https://kr.object.ncloudstorage.com/itsb/patch/gamepot-channel-naver.aar)\]

## 上载 Play 商店 APK 时，会出现 com.nhncorp.nelo2.android.util 加密模式安全通知

logging제与日志记录功能相关的过时库引起的问题

⒉（如果您不使用仪表板日志功能）从 Gamepot SDK 的库中删除下面列出的库

|                                        |     |
| :------------------------------------- | :-- |
| 1. gamepot-logger.aar                  |
| 2. nelo2-android-sdk-common-0.10.2.jar |
| 3. nelo2-android-sdk-https-0.10.2.jar  |
|                                        |     |

## Line i386 x86_64 IOS Archive 上传问题

이동在控制台（终端）中移至 LineSDK.framework 文件的位置后，一一输入以下命令。

文字
（此代码删除了不允许的体系结构。）

lipo -remove x86_64 ./LineSDK.framework/LineSDK -o ./LineSDK.framework/LineSDK
lipo -remove i386 ./LineSDK.framework/LineSDK -o ./LineSDK.framework/LineSDK
lipo -remove x86_64 ./LineSDKObjC.framework/LineSDKObjC -o ./LineSDKObjC.framework/LineSDKObjC
lipo -remove i386 ./LineSDKObjC.framework/LineSDKObjC -o ./LineSDKObjC.framework/LineSDKObjC

```

## Twitter i386 x86_64 IOS 建造问题

이동在控制台（终端）中移至TwitterCore.framework的位置后，一一输入以下命令。

文字
（此代码删除了不允许的体系结构。）

lipo -remove x86_64 ./TwitterCore.framework/TwitterCore -o ./TwitterCore.framework/TwitterCore
lipo -remove i386 ./TwitterCore.framework/TwitterCore -o ./TwitterCore.framework/TwitterCore
lipo -remove x86_64 ./TwitterKit.framework/TwitterKit -o ./TwitterKit.framework/TwitterKit
lipo -remove i386 ./TwitterKit.framework/TwitterKit -o ./TwitterKit.framework/TwitterKit
```

## AdbrixRM i386 x86_64 IOS 建造问题

이동移至控制台（终端）中的 AdBrixRM.framework 文件位置后，一一输入以下命令。

文字
（此代码删除了不允许的体系结构。）

lipo -remove x86_64 ./AdBrixRM.framework/AdBrixRM -o ./AdBrixRM.framework/AdBrixRM
lipo -remove i386 ./AdBrixRM.framework/AdBrixRM -o ./AdBrixRM.framework/AdBrixRM

````


## NaverThirdPartyLogin.framework i386 x86_64 이슈
```text
（此代码删除了不允许的体系结构。）

lipo -remove x86_64 ./NaverThirdPartyLogin.framework/NaverThirdPartyLogin -o ./NaverThirdPartyLogin.framework/NaverThirdPartyLogin
lipo -remove i386 ./NaverThirdPartyLogin.framework/NaverThirdPartyLogin -o ./NaverThirdPartyLogin.framework/NaverThirdPartyLogin
````

## Unity 2018.4.4 或更高版本，Unity 2019.2.0 或更高版本中的 Android 构建问题

⒈ 如下修改`mainTemplate.gradle`文件

> 参见待办事项。

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
                  // TODO : Android gradle plugin 将版本更改为3.4.0版本。
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

⒉ 修复 Firebase 相关文件

- ⒈ 通过[链接](https://kr.object.ncloudstorage.com/gamepot/Firebase_patch.zip)下载补丁文件

- ⒉ 复制文件如下

  ```java
  /Firebase_patch/Assets/Firebase/Editor
  将文件从上面的路径复制到下面的路径
  -> {unity project}/Assets/Firebase/Editor

  {unity project}/Assets/PlayServicesResolver/Editor
   删除上述路径中的所有文件后，将文件复制到以下路径
  -> /Firebase_patch/Assets/PlayServicesResolver/Editor
  ```

- ⒊ /Assets/Plugins/Android/Firebase/res 如果未创建文件夹，请重新启动 Unity

## （统一）在应用 Naver Plug SDK（plug_sdk_4_4_7.unitypackage.unitypackage 或更高版本）时，会发生 IOS 构建错误。

- 通过[链接]下载并提取补丁文件（https://kr.object.ncloudstorage.com/itsb/patch/Patch_GamePotNaverLogin_20200508.zip）（GamePotNaver.framework）

- 将下载的补丁（GamePotNaver.framework）替换为现有路径的框架。

## （IOS）应用 NAVER Plug SDK 时，无法通过 Web 视图登录 NAVER ID。

- 在 XCode 中打开 info.plist。

  - 如下所示，将 Naver Cafe 的 URLScheme 值上传并保存到相应 Array 的第一个索引，然后检查登录的正常操作。
    ![gamepot_troubleshooting_01](./images/gamepot_troubleshooting_01.png)
