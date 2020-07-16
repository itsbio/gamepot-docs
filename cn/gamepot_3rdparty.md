# 3rd-party SDK

> ### 这是机器翻译的文档，可能在词汇，语法或语法上有错误。 我们很快会为您提供由专业翻译人员翻译的文档。
>
> #### 如有任何疑问，请[联系我们](https://www.ncloud.com/support/question)。
>
> 我们将尽一切努力进一步改善我们的服务。

这是将 GAMEPOT SDK 之外的第三者 SDK 应用于游戏项目的指南，该指南不会产生构建错误。

> 根据每个 SDK 的指南进行描述，并参考每个 SDK 的指南以了解如何应用 API。

## Naver cafe SDK

### Android

> 快来了。

### iOS

> 快来了。

### Unity \([Link](https://github.com/naver/cafe-sdk-unity)\)

⒈ 导入 Unity 软件包时，请排除以下文件。

![gamepot-3rdparty-01](./images/gamepot-3rdparty-01.png)

## Adjust

### Android \([Link](https://github.com/adjust/android_sdk/blob/master/doc/korean/README.md#qs-getting-started)\)

⒈ 在将软件包添加到`build.gradle`中时，请忽略以下两个软件包。

```java
implementation 'com.android.installreferrer:installreferrer:1.0'
implementation 'com.google.android.gms:play-services-analytics:16.0.4'
```

⒉ 请忽略已经添加到`AndroidManifest.xml`中的权限。

```java
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

### iOS\([Link](https://github.com/adjust/ios_sdk/blob/master/README.md)\)

- 与 Gamepot 没有冲突。

### Unity\([Link](https://github.com/adjust/unity_sdk#qs-get-sdk)\)

- 与 Gamepot 没有冲突。

## Adbrix

### Android

> 快来了。

### iOS

> 快来了。

### Unity \([Link](https://help.adbrix.io/hc/ko/articles/360007861793-%EC%95%A0%EB%93%9C%EB%B8%8C%EB%A6%AD%EC%8A%A4-Android-%EC%97%B0%EB%8F%99%ED%95%98%EA%B8%B0-Unity-#toc2)\)

⒈ 导入 Unity 软件包时，请排除以下文件。

![gamepot-3rdparty-02](./images/gamepot-3rdparty-02.png)

⒉ 请下载下一个补丁。 \([Download](https://kr.object.ncloudstorage.com/itsb/gamepot-bridge.aar.zip)\)

⒊ 请使用以下路径中的文件替换下载的"gamepot-bridge.aar"文件。

> /Assets/Android/libs/gamepot-bridge.aar

⒋ 您需要在/Assets/Plugins/Android/AndroidManifest.xml 中导入 Adbrix 所需的设置并将其插入。
有关详细信息，请参阅 Adbrix SDK 指南。 \([Guide](https://help.adbrix.io/hc/ko/articles/360007861793-%EC%95%A0%EB%93%9C%EB%B8%8C%EB%A6%AD%EC%8A%A4-Android-%EC%97%B0%EB%8F%99%ED%95%98%EA%B8%B0-Unity-#toc6)\)

## Singular

### Android \([Link](https://developers.singular.net/docs/android-sdk)\)

_`[sdk v9.2.0]`_

⒈ 将软件包添加到应用程序级别的`build.gradle`时，请忽略以下软件包，因为该软件包已包含在内。

```java
compile 'com.android.installreferrer:installreferrer:1.0'
```

⒉ 请忽略已经添加到`AndroidManifest.xml`中的权限。

```java
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

### iOS \([Link](https://developers.singular.net/docs/ios-sdk)\)

_`[sdk v9.2.0]`_

- 与 Gamepot 没有冲突。

### Unity \([Link](https://developers.singular.net/docs/unity-sdk)\)

_`[sdk v9.2.0]`_

- 请在以下路径中删除库文件。

> `Assets/Plugins/Android/libs/installreferrer-1.0.aar`

## Appsflyer

### Android

> 快来了。

### iOS

> 快来了。

### Unity

> 快来了。

## AdMob

**_`由于迁移到androidx软件包的问题，​​不能使用Google Play服务版本18.0.0或更高版本的sdk。`_**

### Android \([Link](https://firebase.google.com/docs/admob/android/quick-start?hl=ko)\)

- Gamepot 服务使用 Firebase Messaging 服务。 请通过 Admob 和 Firebase 进行设置。

### iOS \([Link](https://developers.google.com/admob/ios/quick-start?hl=ko)\)

- 与 Gamepot 没有冲突。

### Unity \([Link](https://github.com/googleads/googleads-mobile-unity/releases/tag/3.17.0)\)

_`[Google Mobile Ads v3.17.0]`_

⒈ 通过上面的链接将插件（v3.17.0）导入游戏项目。

⒉ 如下所示，在`mainTemplate.gradle`中添加 AdMob Android 项目。

![gamepot-3rdparty-03](./images/gamepot-3rdparty-03.png)

⒊ 对于 AdMob SDK（Unity），您需要导入 Unity 包并使用 Unity Play Services 解析器功能。 （请参阅 AdMob 指南）

- 应用解析功能时，还会复制现有 Gamepot SDK 中使用的库。

- 从/ Assets / Plugins / Android / libs /中删除与 AdMob SDK 重叠的库的列表。

- 要删除的库列表如下。

  |                                       |                                               |
  | :------------------------------------ | :-------------------------------------------- |
  | 1. core-common-1.1.0.jar              | 2. lifecycle-common-1.1.0.jar                 |
  | 3. lifecycle-runtime-1.1.0.aar        | 4. customtabs-27.1.1.aar                      |
  | 5. support-annotations-27.1.1.jar     | 6. support-compat-27.1.1.aar                  |
  | 7. support-core-ui-27.1.1.aar         | 8. support-core-utils-27.1.1.aar              |
  | 9. support-fragment-27.1.1.aar        | 10. support-media-compat-27.1.1.aar           |
  | 11. support-v4-27.1.1.aar             | 12. play-services-ads-identifier-16.0.0.aar   |
  | 13. play-services-basement-16.2.0.aar | 14. play-services-measurement-base-16.0.5.aar |
  |                                       |                                               |

## Admob Mediation

**_`由于迁移到androidx软件包的问题，​​不能使用Google Play服务版本18.0.0或更高版本的sdk。`_**

### Android\([Link](https://developers.google.com/admob/android/mediate)\)

_`[Google Play service Ads SDK 17.2.0]`_

#### - Vungle\([Link](https://developers.google.com/admob/android/mediation/vungle)\)

- 与 Gamepot 没有冲突。 \(Vungle sdk 6.3.24\)

#### - Unity Ads\([Link](https://developers.google.com/admob/android/mediation/unity)\)

- 将软件包添加到应用程序级别的`build.gradle`时，请将其与相应的软件包一起添加。

```java
compile 'com.google.ads.mediation:unity:3.1.0.0'
```

#### - Facebook\([Link](https://developers.google.com/admob/android/mediation/facebook)\)

- 将软件包添加到应用程序级别的`build.gradle`时，请将其与相应的软件包一起添加。

```java
compile 'com.google.ads.mediation:facebook:5.4.0.0'
```

### iOS \([Link](https://developers.google.com/admob/ios/mediate)\)

_`[Google Mobile Ads SDK 7.49.0]`_

#### - Vungle\([Link](https://developers.google.com/admob/ios/mediation/vungle)\)

- 与 Gamepot 没有冲突。 \(Vungle sdk 6.3.2\)

#### - Unity Ads\([Link](https://developers.google.com/admob/ios/mediation/unity)\)

- 与 Gamepot 没有冲突。 \(UnityAds sdk 3.2.0\)

#### - Facebook\([Link](https://developers.google.com/admob/ios/mediation/facebook)\)

- 与 Gamepot 没有冲突。 \(iOS Audience Network sdk 5.5.0\)

### Unity \([Link](https://github.com/googleads/googleads-mobile-unity/releases/tag/3.17.0)\)

_`[Google Mobile Ads Unity Plugin v3.17.0]`_

#### - Vungle\([Link](https://developers.google.com/admob/unity/mediation/vungle)\)

- 与 Gamepot 没有冲突。

#### - Unity Ads\([Link](https://developers.google.com/admob/unity/mediation/unity)\)

- 与 Gamepot 没有冲突。

#### - Facebook\([Link](https://developers.google.com/admob/unity/mediation/facebook)\)

- 与 Gamepot 没有冲突。

## Facebook SDK (Unity Plugin)

### Unity \([Link](https://developers.facebook.com/docs/unity/downloads)\)

_`[FB UnityPackage ver 7.18.0]`_

⒈ 导入 Unity 程序包后，应用 Unity Play 服务解析器。

![gamepot-3rdparty-04](./images/gamepot-3rdparty-04.png)

- 应用解析功能时，还会复制现有 Gamepot SDK 中使用的库。

- 从/ Assets / Plugins / Android / libs /中删除与 Facebook SDK 重叠的库列表。

- 要删除的库列表如下。

  |                                        |                                        |
  | :------------------------------------- | :------------------------------------- |
  | 1. animated-vector-drawable-27.1.1.aar | 2. appcompat-v7-27.1.1.aar             |
  | 3. bolts-android-1.4.0.jar             | 4. bolts-applinks-1.4.0.jar            |
  | 5. bolts-tasks-1.4.0.jar               | 6. cardview-v7-27.0.2.aar              |
  | 7. core-3.3.0.jar                      | 8. core-common-1.1.0.jar               |
  | 9. customtabs-27.1.1.aar               | 10. facebook-android-sdk-5.2.0.aar     |
  | 11. facebook-applinks-5.2.0.aar        | 12. facebook-common-5.2.0.aar          |
  | 13. facebook-core-5.2.0.aar            | 14. facebook-login-5.2.0.aar           |
  | 15. facebook-messenger-5.2.0.aar       | 16.facebook-places-5.2.0.aar           |
  | 17. facebook-share-5.2.0.aar           | 18. lifecycle-runtime-1.1.0.aar        |
  | 19. lifecycle-common-1.1.0.jar         | 20. support-compat-27.1.1.aar          |
  | 21. support-core-ui-27.1.1.aar         | 22. support-core-utils-27.1.1.aar      |
  | 23. support-fragment-27.1.1.aar        | 24. support-media-compat-27.1.1.aar    |
  | 25. support-v4-27.1.1.aar              | 26. support-vector-drawable-27.1.1.aar |
  | 27. support-annotations-27.1.1.jar     |                                        |

- （对于 iOS）从/ Assets / Plugins / IOS / Frameworks /中删除重叠的框架列表。

  |                            |
  | :------------------------- |
  | 1. FBSDKCoreKit.framework  |
  | 2. FBSDKLoginKit.framework |

⒉ U 在 UnityEditer 的 FacebookSettings 中输入 Facebook 应用 ID，然后单击红色按钮以重新生成 AndroidManifest。

![gamepot-3rdparty-05](./images/gamepot-3rdparty-05.png)

⒊ 在编辑器中打开/Assets/Plugins/Android/AndroidManifest.xml 并删除红线（Facebook 应用程序 ID）。

![gamepot-3rdparty-06](./images/gamepot-3rdparty-06.png)
