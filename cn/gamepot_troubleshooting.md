# 故障排除

## 在64-bit环境下的构建过程中，尝试使用NAVER ID登录时发生崩溃（构建API 28以上的Android） <a name="64bit환경에서빌드할때네아로네이버아이디로그인시도시크래시발생API28이상의Android빌드"></a>

1. `AndroidManifest.xml` 请在文件中添加以下代码。 
    * 如为Unity，则修改/Assets/Plugins/Android/AndroidManifest.xml
    ```java
    // TODO：请置于<application>标签内。

    <application>

    ...

       <uses-library android:name="org.apache.http.legacy" android:required="false" />

    ...

    </application>
    ```
    
:::(Info) (参考)

这部分可通过更换已打补丁的库作为代替。 \[[gamepot-channel-naver.aar](https://kr.object.ncloudstorage.com/itsb/patch/gamepot-channel-naver.aar)\]
:::

## 上传Play Store APK时，会发出com.nhncorp.nelo2.android.util加密模式安全通知 <a name="플레이스토어APK업로드시comnhncorpnelo2androidutil암호화패턴보안알림발생"></a>

从GAMEPOT SDK 3.3.0开始搭载了nelo2-android-sdk-https-0.12.0.aar / nelo2-android-sdk-common-0.12.0.aar，上述问题已解决。
但考虑到已更改的NAVER Cloud ELSA库，minSDK应为19以上版本。

[以GAMEPOT SDK 3.2.0以下版本为准]

1. logging记录功能相关库因obsolete而引发的问题
2. （不使用仪表盘日志功能时）在GAMEPOT SDK的库中删除以下列表中的库
    * gamepot-logger.aar 
    * nelo2-android-sdk-common-0.10.2.jar 
    * nelo2-android-sdk-https-0.10.2.jar 

## 构建iOS时发生错误 <a name="IOS빌드시오류발생"></a>

错误示例：

error: Building for iOS, but the linked and embedded framework 'XXXXXX.framework' was built for iOS + iOS Simulator.

因“XXXXXX.framework”包含i386 x86_64 Archive信息而出现上述情况。 

```text
（该代码可删除不被允许的架构。）  

NaverThirdPartyLogin.framework还有问题时，请如下操作去除后进行构建。

lipo -remove x86_64 ./NaverThirdPartyLogin.framework/NaverThirdPartyLogin -o ./NaverThirdPartyLogin.framework/NaverThirdPartyLogin
lipo -remove i386 ./NaverThirdPartyLogin.framework/NaverThirdPartyLogin -o ./NaverThirdPartyLogin.framework/NaverThirdPartyLogin
```

## ine i386 x86_64 IOS Archive上传问题 <a name="Linei386x8664IOSArchive업로드이슈"></a>

在控制台（终端）进入LineSDK.framework文件位置后，请逐一输入以下命令。

```text
（该代码可删除不被允许的架构。） 

lipo -remove x86_64 ./LineSDK.framework/LineSDK -o ./LineSDK.framework/LineSDK
lipo -remove i386 ./LineSDK.framework/LineSDK -o ./LineSDK.framework/LineSDK
lipo -remove x86_64 ./LineSDKObjC.framework/LineSDKObjC -o ./LineSDKObjC.framework/LineSDKObjC
lipo -remove i386 ./LineSDKObjC.framework/LineSDKObjC -o ./LineSDKObjC.framework/LineSDKObjC
```

## Twitter i386 x86_64 IOS构建问题 <a name="Twitteri386x8664IOS빌드이슈"></a>

在控制台（终端）进入TwitterCore.framework文件位置后，请逐一输入以下命令。

```text
（该代码可删除不被允许的架构。）  

lipo -remove x86_64 ./TwitterCore.framework/TwitterCore -o ./TwitterCore.framework/TwitterCore
lipo -remove i386 ./TwitterCore.framework/TwitterCore -o ./TwitterCore.framework/TwitterCore
lipo -remove x86_64 ./TwitterKit.framework/TwitterKit -o ./TwitterKit.framework/TwitterKit
lipo -remove i386 ./TwitterKit.framework/TwitterKit -o ./TwitterKit.framework/TwitterKit
```

## AdbrixRM i386 x86_64 iOS构建问题 <a name="AdbrixRMi386x8664IOS빌드이슈"></a>

在控制台（终端）进入AdBrixRM.framework文件位置后，请逐一输入以下命令。

```text
（该代码可删除不被允许的架构。） 

lipo -remove x86_64 ./AdBrixRM.framework/AdBrixRM -o ./AdBrixRM.framework/AdBrixRM
lipo -remove i386 ./AdBrixRM.framework/AdBrixRM -o ./AdBrixRM.framework/AdBrixRM
```


## 使用NAVER ID登录时出现的NaverThirdPartyLogin.framework i386 x86_64问题 <a name="네아로NaverThirdPartyLoginframeworki386x8664이슈"></a>

```text
（该代码可删除不被允许的架构。） 

lipo -remove x86_64 ./NaverThirdPartyLogin.framework/NaverThirdPartyLogin -o ./NaverThirdPartyLogin.framework/NaverThirdPartyLogin
lipo -remove i386 ./NaverThirdPartyLogin.framework/NaverThirdPartyLogin -o ./NaverThirdPartyLogin.framework/NaverThirdPartyLogin
```


## Unity 2018.4.4以上、Unity 2019.2.0以上版本中的Android构建问题 <a name="Unity201844이상Unity201920이상에서Android빌드이슈"></a>

1. 请按照以下方法修改`mainTemplate.gradle`文件。 

    * 请参考TODO项目。

    ```java
    // TODO：删除所有使用GradleVersion的位置。

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
                      // TODO：将Android gradle插件版本改为3.4.0。
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

2. 请修改Firebase相关文件。

- 1. 请通过 [链接](https://kr.object.ncloudstorage.com/gamepot/Firebase_patch.zip) 下载补丁文件。

- 2, 请按照如下方法复制文件。

    ```java
    /Firebase_patch/Assets/Firebase/Editor
     将上面路径下的文件复制到以下路径
    -> {unity project}/Assets/Firebase/Editor

    {unity project}/Assets/PlayServicesResolver/Editor
     将上面路径下的文件全部删除后复制文件到以下路径
    -> /Firebase_patch/Assets/PlayServicesResolver/Editor
    ```

- 3. 若未创建/Assets/Plugins/Android/Firebase/res文件夹，请重新运行Unity。 

## （Unity）应用NAVER Lounge SDK（以NaverSDK Ver 1.1.1为例进行说明） <a name="Unity네이버라운지SDK적용NaverSDKVer111기준설명"></a>

参考URL：https://navergame.gitbook.io/naver-game/naver-game-sdk-faq-1#unity-android-class-duplication-exception

- 应用Unity插件时，不包含或删除navergame-sdk-1.1.1.aar文件

../Assets/NGSDK/Plugins/Android/navergame-sdk-1.1.1.aar

- 搭载Android Native NAVER Lounge SDK库

../Assets/Plugins/Android/navergame-sdk-gradle-1.1.1.aar 

- 修改mainTemplate.gradle文件（添加在NAVER Lounge SDK中使用的库）

```text
dependencies {
..
implementation 'androidx.multidex:multidex:2.0.1'
implementation "androidx.recyclerview:recyclerview:1.2.0"
implementation "androidx.viewpager2:viewpager2:1.0.0"
implementation "com.squareup.retrofit2:retrofit:2.6.4"
```

- 删除../Assets/Plugins/Android/libs文件夹中重复的库（删除列表）

```text
../Assets/Plugins/Android/libs/activity-1.0.0.aar
../Assets/Plugins/Android/libs/annotation-1.1.0.jar
../Assets/Plugins/Android/libs/collection-1.1.0.jar
../Assets/Plugins/Android/libs/core-1.3.0.aar
../Assets/Plugins/Android/libs/core-common-2.1.0.jar
../Assets/Plugins/Android/libs/core-runtime-2.0.0.aar
../Assets/Plugins/Android/libs/customview-1.0.0.aar
../Assets/Plugins/Android/libs/fragment-1.1.0.aar
../Assets/Plugins/Android/libs/lifecycle-common-2.1.0.jar
../Assets/Plugins/Android/libs/lifecycle-livedata-2.0.0.aar
../Assets/Plugins/Android/libs/lifecycle-livedata-core-2.0.0.aar
../Assets/Plugins/Android/libs/lifecycle-runtime-2.1.0.aar
../Assets/Plugins/Android/libs/lifecycle-viewmodel-2.1.0.aar
../Assets/Plugins/Android/libs/loader-1.0.0.aar
../Assets/Plugins/Android/libs/okhttp-4.9.1.jar
../Assets/Plugins/Android/libs/okio-2.8.0.jar
../Assets/Plugins/Android/libs/savedstate-1.0.0.aar
../Assets/Plugins/Android/libs/versionedparcelable-1.1.0.aar
../Assets/Plugins/Android/libs/viewpager-1.0.0.aar
../Assets/Plugins/Android/libs/retrofit-2.5.0.aar
```

- 从NaverSDK Ver 1.2.X版本开始，由于库与GAMEPOT SDK NAVER登录冲突，无法使用NAVER登录功能。

- 反映NaverSDK Ver 1.3.2版本时 

1.  删除../Assets/Plugins/Android/libs文件夹中重复的库（删除列表）：根据相应项目应用的环境，可能需要在构建时删除重复的库。 

```text
../Assets/Plugins/Android/libs/retrofit-2.5.0.jar
../Assets/Plugins/Android/libs/vectordrawable-animated-1.1.0.aar
../Assets/Plugins/Android/libs/vectordrawable-1.1.0.aar
../Assets/Plugins/Android/libs/savedstate-1.0.0.aar
../Assets/Plugins/Android/libs/media-1.0.0.aar
../Assets/Plugins/Android/libs/browser-1.0.0.aar
../Assets/Plugins/Android/libs/appcompat-resources-1.2.0.aar
../Assets/Plugins/Android/libs/appcompat-1.2.0.aar
../Assets/Plugins/Android/libs/activity-1.0.0.aar
../Assets/Plugins/Android/libs/okio-1.14.0.jar
../Assets/Plugins/Android/libs/okhttp-3.10.0.jar
```

2. 变更NAVER Lounge SDK库的位置

```text
现有
Assets/NGSDK/Plugins/Android/navergamesdk.androidlib/libs/navergame-sdk-gradle-1.3.2.aar 
->
变更位置 
/Assets/Plugins/Android/navergame-sdk-gradle-1.3.2.aar
```

3. 在以下路径中创建NaverGameDependencies.xml文件（文件内容参考下方）后 

请在Unity的Assets > Play Services Resolver > Android Resolver > Settings菜单中选择Use Jetifier项目。

请在取消选择的状态下，对Enable Resolution On Build / Enable Auto-Resolution / Patch gradle Template.properties项目进行Resolver。

/Assets/Firebase/Editor/NaverGameDependencies.xml

```text
<dependencies>
  
  <androidPackages>  
    <androidPackage spec="com.squareup.retrofit2:retrofit:2.9.0">
    </androidPackage>
    <androidPackage spec="androidx.viewpager2:viewpager2:1.0.0">
    </androidPackage>

  </androidPackages>
</dependencies>
```

4. com.naver.nid.naveridlogin-android-sdk-4.2.6.aar 파일을 하기 경로에 넣어 빌드시 포함되도록 해주십시오 

/Assets/Plugins/Android/libs/com.naver.nid.naveridlogin-android-sdk-4.2.6.aar

Download : [com.naver.nid.naveridlogin-android-sdk-4.2.6.aar](https://xyuditqzezxs1008973.cdn.ntruss.com/patch/com.naver.nid.naveridlogin-android-sdk-4.2.6.aar)

5. /Assets/NGSDK/Plugins/iOS/NCSDKUnityManager.mm 파일 수정

```text
기존 :

(NSString *)getAuthSettingDescription {
    return NNGSDKManager.shared.authSettingDescription;
}

수정 : 

- (NSString *)getAuthSettingDescription {
    return NNGSDKManager.shared.authSettingDescription;
}

```

6. launcherTemplate.gradle 내에  하기 부분 추가

```text
    packagingOptions {
	…..
	// 20230322Add cause More than one file was found with OS independent path 'META-INF/kotlin-stdlib-common.kotlin_module'.
	exclude("META-INF/*.kotlin_module") //-> 추가
```    

## （Unity）应用GoogleMobileAds SDK（以GoogleMobileAds-v6.1.2为例进行说明） <a name="UnityGoogleMobileAdsSDK적용GoogleMobileAdsv612기준설명"></a>

AdMob SDK（Unity）须在导入Unity包后使用Unity Play Services Resolver功能。

请在Unity的Assets > Play Services Resolver > Android Resolver > Settings菜单中选择Use Jetifier项目。
请在取消选择的状态下，对Enable Resolution On Build / Enable Auto-Resolution / Patch gradle Template.properties项目进行Resolver。

如为Unity的Assets > Play Services Resolver > IOS Resolver > Settings菜单中的
Add use_frameworks! to podfile / Always add the main target to Podfile项目，请在取消选择的状态下进行iOS构建。

此后若出现重复库的相关错误，请删除一处库。  

重复的库文件目录： 
```text
..Assets/Plugins/Android/libs/annotation-1.1.0.jar
..Assets/Plugins/Android/libs/browser-1.0.0.aar
..Assets/Plugins/Android/libs/core-common-2.1.0.jar
..Assets/Plugins/Android/libs/core-runtime-2.0.0.aar
..Assets/Plugins/Android/libs/core-1.3.0.aar
..Assets/Plugins/Android/libs/coordinatorlayout-1.0.0.aar
..Assets/Plugins/Android/libs/collection-1.1.0.jar
..Assets/Plugins/Android/libs/asynclayoutinflater-1.0.0.aar
..Assets/Plugins/Android/libs/fragment-1.1.0.aar
..Assets/Plugins/Android/libs/drawerlayout-1.0.0.aar
..Assets/Plugins/Android/libs/documentfile-1.0.0.aar
..Assets/Plugins/Android/libs/customview-1.0.0.aar
..Assets/Plugins/Android/libs/cursoradapter-1.0.0.aar
..Assets/Plugins/Android/libs/loader-1.0.0.aar
..Assets/Plugins/Android/libs/lifecycle-viewmodel-2.1.0.aar
..Assets/Plugins/Android/libs/lifecycle-runtime-2.1.0.aar
..Assets/Plugins/Android/libs/lifecycle-livedata-2.0.0.aar
..Assets/Plugins/Android/libs/lifecycle-common-2.1.0.jar
..Assets/Plugins/Android/libs/legacy-support-core-utils-1.0.0.aar
..Assets/Plugins/Android/libs/legacy-support-core-ui-1.0.0.aar
..Assets/Plugins/Android/libs/interpolator-1.0.0.aar
..Assets/Plugins/Android/libs/viewpager-1.0.0.aar
..Assets/Plugins/Android/libs/versionedparcelable-1.1.0.aar
..Assets/Plugins/Android/libs/swiperefreshlayout-1.0.0.aar
..Assets/Plugins/Android/libs/sqlite-framework-2.0.1.aar
..Assets/Plugins/Android/libs/sqlite-2.0.1.aar
..Assets/Plugins/Android/libs/slidingpanelayout-1.0.0.aar
..Assets/Plugins/Android/libs/print-1.0.0.aar
..Assets/Plugins/Android/libs/localbroadcastmanager-1.0.0.aar
..Assets/Plugins/Android/libs/lifecycle-livedata-core-2.0.0.aar
..Assets/Plugins/Android/libs/play-services-basement-17.5.0.aar
..Assets/Plugins/Android/libs/play-services-ads-identifier-17.0.0.aar
..Assets/Plugins/Android/libs/play-services-measurement-sdk-api-18.0.1.aar
..Assets/Plugins/Android/libs/play-services-measurement-impl-18.0.1.aar
..Assets/Plugins/Android/libs/play-services-measurement-base-18.0.1.aar
..Assets/Plugins/Android/libs/play-services-tasks-17.2.0.aar
..Assets/Plugins/Android/libs/play-services-measurement-18.0.1.aar

..Assets/Plugins/Android/libs/play-services-measurement-sdk-18.0.1.aar
..Assets/Plugins/Android/libs/play-services-measurement-api-18.0.1.aar

..Assets/Plugins/IOS/Frameworks/nanopb.framework
```

## （Unity）应用Appsflyer/Singular SDK（以appsflyer-v6.3.2为例进行说明） <a name="UnityAppsflyerSingularSDK적용appsflyerv632기준설명"></a>

与其他的SDK相同，UnityAppController class应只能从构建的项目中的一个文件中继承。 

若搭载GAMEPOT的Unity插件，默认在GamePotAppDelegate.h中继承。 

针对appsflyer或Singular等类似广告工具，相应库也会继承UnityAppController，从而导致GAMEPOT SDK可能无法运行。 

应当修改为仅在一个文件中继承后使用。 

<示例>
[appsflyer-v6.3.2补丁](https://xyuditqzezxs1008973.cdn.ntruss.com/patch/fixed_appsflyer632.zip)



## （Unity）单独应用Firebase SDK时（以Firebase Unity 8.7.0为例进行说明） <a name="UnityFirebaseSDK별도로적용할때FirebaseUnity870기준설명"></a>

若Unity编辑器版本低于2019.X版本，请优先使用以下补丁。 

下载补丁：[下载补丁](https://xyuditqzezxs1008973.cdn.ntruss.com/patch/unity_2020_X.zip)

```
    [替换文件夹和文件]

    ../Assets/ExternalDependencyManager

    ../Assets/Firebase

    - 替换Firebase库后修改文件夹名称 
    
    修改前：../Assets/Plugins/Android/Firebase
    
    修改后：../Assets/Plugins/Android/FirebaseApp.androidlib

    - 修改mainTemplate.gradle（因变更文件夹名导致的修改）
    
    修改前： 
    
    dependencies {
        ...
    	implementation project('Firebase')
    
    修改后：
    
    dependencies {
        ...
    	implementation project('FirebaseApp.androidlib')
        ...
```

- GAMEPOT Unity插件包中有一些Firebase SDK，搭载单独的Firebase SDK时，会由于库重复而导致错误。
导入Firebase Unity SDK（FirebaseAnalytics.unitypackage/FirebaseMessaging.unitypackage + 计划添加的Firebase SDK）后，应使用Unity Play Services Resolver功能。
请在Unity的Assets > Play Services Resolver > Android Resolver > Settings菜单中选择Use Jetifier项目。
请在取消选择的状态下，对Enable Resolution On Build / Enable Auto-Resolution / Patch gradle Template.properties项目进行Resolver。 
针对Unity的Assets > Play Services Resolver > IOS Resolver > Settings菜单中的Add use_frameworks! to podfile/Always add the main target to Podfile项目，请在取消选择的状态下进行iOS构建。


1. 需要删除重复的库文件： 
```text
../Assets/Plugins/Android/libs/viewpager-1.0.0.aar 
../Assets/Plugins/Android/libs/versionedparcelable-1.1.0.aar 
../Assets/Plugins/Android/libs/transport-runtime-2.2.5.aar 
../Assets/Plugins/Android/libs/transport-backend-cct-2.3.3.aar 
../Assets/Plugins/Android/libs/transport-api-2.2.1.aar 
../Assets/Plugins/Android/libs/swiperefreshlayout-1.0.0.aar 
../Assets/Plugins/Android/libs/slidingpanelayout-1.0.0.aar 
../Assets/Plugins/Android/libs/print-1.0.0.aar 
../Assets/Plugins/Android/libs/play-services-tasks-17.2.0.aar 
../Assets/Plugins/Android/libs/play-services-stats-17.0.0.aar 
../Assets/Plugins/Android/libs/play-services-measurement-sdk-api-18.0.1.aar 
../Assets/Plugins/Android/libs/play-services-measurement-sdk-18.0.1.aar 
../Assets/Plugins/Android/libs/play-services-measurement-impl-18.0.1.aar 
../Assets/Plugins/Android/libs/play-services-measurement-base-18.0.1.aar 
../Assets/Plugins/Android/libs/play-services-measurement-api-18.0.1.aar 
../Assets/Plugins/Android/libs/play-services-measurement-18.0.1.aar 
../Assets/Plugins/Android/libs/play-services-cloud-messaging-16.0.0.aar 
../Assets/Plugins/Android/libs/play-services-basement-17.5.0.aar 
../Assets/Plugins/Android/libs/play-services-base-17.5.0.aar 
../Assets/Plugins/Android/libs/play-services-ads-identifier-17.0.0.aar 
../Assets/Plugins/Android/libs/localbroadcastmanager-1.0.0.aar 
../Assets/Plugins/Android/libs/loader-1.0.0.aar 
../Assets/Plugins/Android/libs/lifecycle-viewmodel-2.1.0.aar 
../Assets/Plugins/Android/libs/lifecycle-runtime-2.1.0.aar 
../Assets/Plugins/Android/libs/lifecycle-livedata-core-2.0.0.aar 
../Assets/Plugins/Android/libs/lifecycle-livedata-2.0.0.aar 
../Assets/Plugins/Android/libs/lifecycle-common-2.1.0.jar 
../Assets/Plugins/Android/libs/legacy-support-core-utils-1.0.0.aar 
../Assets/Plugins/Android/libs/legacy-support-core-ui-1.0.0.aar 
../Assets/Plugins/Android/libs/javax.inject-1.jar 
../Assets/Plugins/Android/libs/interpolator-1.0.0.aar 
../Assets/Plugins/Android/libs/fragment-1.1.0.aar 
../Assets/Plugins/Android/libs/firebase-messaging-21.0.1.aar 
../Assets/Plugins/Android/libs/firebase-measurement-connector-18.0.0.aar 
../Assets/Plugins/Android/libs/firebase-installations-interop-16.0.1.aar 
../Assets/Plugins/Android/libs/firebase-installations-16.3.5.aar 
../Assets/Plugins/Android/libs/firebase-iid-interop-17.0.0.aar 
../Assets/Plugins/Android/libs/firebase-iid-21.0.1.aar 
../Assets/Plugins/Android/libs/firebase-encoders-json-17.1.0.aar 
../Assets/Plugins/Android/libs/firebase-encoders-16.1.0.jar 
../Assets/Plugins/Android/libs/firebase-datatransport-17.0.10.aar 
../Assets/Plugins/Android/libs/firebase-core-18.0.1.aar 
../Assets/Plugins/Android/libs/firebase-components-16.1.0.aar 
../Assets/Plugins/Android/libs/firebase-common-19.5.0.aar 
../Assets/Plugins/Android/libs/firebase-annotations-16.0.0.jar 
../Assets/Plugins/Android/libs/firebase-analytics-18.0.1.aar 
../Assets/Plugins/Android/libs/drawerlayout-1.0.0.aar 
../Assets/Plugins/Android/libs/documentfile-1.0.0.aar 
../Assets/Plugins/Android/libs/customview-1.0.0.aar 
../Assets/Plugins/Android/libs/cursoradapter-1.0.0.aar 
../Assets/Plugins/Android/libs/core-runtime-2.0.0.aar 
../Assets/Plugins/Android/libs/core-common-2.1.0.jar 
../Assets/Plugins/Android/libs/core-1.3.0.aar 
../Assets/Plugins/Android/libs/coordinatorlayout-1.0.0.aar
../Assets/Plugins/Android/libs/collection-1.1.0.jar 
../Assets/Plugins/Android/libs/asynclayoutinflater-1.0.0.aar 
../Assets/Plugins/Android/libs/annotation-1.1.0.jar
../Assets/Plugins/IOS/Frameworks/nanopb.framework 
../Assets/Plugins/IOS/Frameworks/FirebaseNanoPB.framework 
../Assets/Plugins/IOS/Frameworks/FirebaseMessaging.framework 
../Assets/Plugins/IOS/Frameworks/FirebaseInstanceID.framework 
../Assets/Plugins/IOS/Frameworks/FirebaseCoreDiagnostics.framework 
../Assets/Plugins/IOS/Frameworks/FirebaseCore.framework 
../Assets/Plugins/IOS/Frameworks/FirebaseAnalytics.framework
```


2. 确认../Assets/Plugins/Android/AndroidManifest.xml内是否应用FCM相关代码

```text
....
</activity>

<!-- FCM [start]-->
       <service
            android:exported="false"
            android:name="io.gamepot.common.GamePotFCMIDService">
            <intent-filter>
                <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
            </intent-filter>
        </service>
        <service
            android:exported="false"
            android:name="io.gamepot.common.GamePotFCMService">
            <intent-filter>
                <action android:name="com.google.firebase.MESSAGING_EVENT"/>
            </intent-filter>
        </service>
<!-- FCM [End]-->

...
<meta-data android:name="android.max_aspect" android:value="2.1" />
```
3. 应用Firebase Unity 9.4.0以上版本的情况下，构建iOS时的追加更改操作

在Unity编辑器中，从构建iOS后得到的结果中找到Podfile文件，并修改为如下格式（如存在其他库，则添加:modular_headers => true部分）
Firebase/FirebaseCore/GoogleUtilities应按照示例进行添加。

```text
示例）

[现有]
...
target 'UnityFramework' do
  pod 'Firebase/Analytics', '9.4.0'
  pod 'Firebase/Core', '9.4.0'
  pod 'Firebase/Messaging', '9.4.0'
end

[修改]

target 'UnityFramework' do
  pod 'Firebase/Analytics', '9.4.0' , :modular_headers => true
  pod 'Firebase/Core', '9.4.0' , :modular_headers => true
  pod 'Firebase/Messaging', '9.4.0' , :modular_headers => true

  pod 'Firebase', :modular_headers => true
  pod 'FirebaseCore', :modular_headers => true
  pod 'GoogleUtilities', :modular_headers => true
end
```

打开终端后，进入Podfile文件所在路径执行pod install命令，生成Unity-iPhone.xcworkspace文件后，使用该项目进行构建

```text
$ pod install
```

##  升级到android、targetsdkversion 31以上时，出现以下错误和应用无法安装的问题 <a name="androidtargetsdkversion을31로올렸을때다음에러와함께앱이설치되지않는문제"></a>

```text
示例）
Failure [INSTALL_PARSE_FAILED_MANIFEST_MALFORMED: Failed parse during installPackageLI: /data/app/XXXXXXXX.tmp/base.apk (at Binary XML file line #445): io.gamepot.common.GamePotFCMIDService: Targeting S+ (version 31 and above) requires that an explicit value for android:exported be defined when intent filters are present]
```

需要在AndroidManifest.xml内定义android:exported。 
需要添加下列语句。/（下列外部使用activty / service / receiver的部分应当按照相关用途进行定义。）

示例）

```text
       <service
            android:exported="false"
            android:name="io.gamepot.common.GamePotFCMIDService">
            <intent-filter>
                <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
            </intent-filter>
        </service>
        <service
            android:exported="false"
            android:name="io.gamepot.common.GamePotFCMService">
            <intent-filter>
                <action android:name="com.google.firebase.MESSAGING_EVENT"/>
            </intent-filter>
        </service>
        
        <!-- 若不使用ELSA服务，则删除下方语句/构建时不得包含gamepot-logger.aar [start]-->
        <receiver
            android:exported="false"
            android:name="com.navercorp.nelo2.android.util.NetworkStatusReceiver">
            <intent-filter>
                <action android:name="android.net.conn.CONNECTIVITY_CHANGE"/>
            </intent-filter>
        </receiver>
        <!-- 若不使用ELSA服务，则删除下方语句/构建时不得包含gamepot-logger.aar [end]-->
        
        
        <!-- 若不使用NAVER登录，则删除下方语句 [start]-->
        <activity android:exported="true" android:configChanges="orientation|screenSize" android:launchMode="singleTask" android:name="com.nhn.android.naverlogin.ui.OAuthCustomTabActivity" android:theme="@android:style/Theme.Translucent.NoTitleBar">
            <intent-filter>
                <action android:name="android.intent.action.VIEW"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <category android:name="android.intent.category.BROWSABLE"/>
                <data android:host="authorize" android:path="/" android:scheme="naver3rdpartylogin"/>
            </intent-filter>
        </activity>
        <!-- 若不使用NAVER登录，则删除下方语句 [end]-->
```

## 在Android OS 13设备上无法接收推送设置时

从Android OS 13开始，需要获得**android.permission.POST_NOTIFICATIONS**权限后才能显示推送通知。
如果是使用Targetsdk 31版本所构建，当应用在前台状态下收到推送时，OS内部会弹出一次权限获取弹窗。

获得**android.permission.POST_NOTIFICATIONS**权限的功能在GAMEPOT SDK中不受支持。
开发相关功能时，需保证开发商在单独的特点时间（例如）同意条款之时或应用启动之时）获得**android.permission.POST_NOTIFICATIONS**权限。
如果玩家拒绝，需要将“如果不在应用设置中手动重新激活通知权限，则不会显示推送通知”这一内容进行告知。

## GAMEPOT SDK中收集的个人信息类型 <a name="게임팟SDK에서수집하는개인정보유형"></a>

### Google store应用程序内容项目标准 <a name="구글스토어앱콘텐츠항목기준"></a>

应用通信采用HTTPS通信方式进行加密，如有注销会员功能，注销完成后会删除会员信息。 请勾选应用功能项目。 但是，仅作为应用的功能性元素使用，不用作账户管理功能。

```text
[个人信息]
    邮件地址
    用户ID

[设备或其他ID]
    设备或其他ID

[照片和视频]
    图片
    视频
```

### Apple store应用程序收集的个人信息项目标准<a name="애플스토어앱이수집하는개인정보항목기준"></a>

```text
[标识符]
    用户ID（账户信息）
    设备ID (IDFA, auto generated)
    购买项目
[用户内容]
    图片或者影像
    客户支持
```
如为用户内容，则适用于使用GAMEPOT Pro以上商品的顾客中使用GAMEPOT顾客咨询UI的情况。 使用Object Storage功能时，可以在客户咨询中上传图像文件。
