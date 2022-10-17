# Troubleshooting

> ###これは機械翻訳されたドキュメントで、語彙、構文、または文法に誤りがある可能性があります。 プロの翻訳者が翻訳したドキュメントをすぐに提供します。
>
> ####ご不明な点がございましたら、[お問い合わせ](https://www.ncloud.com/support/question)でお問い合わせください。
>
> 私たちは、サービスのさらなる向上に全力を尽くします。

## 4-bit 環境でビルドするとき、あなたのアロー（ネイバー ID をログイン）試行中にクラッシュが発生し。（API28 以上の Android ビルド）

⒈ `AndroidManifest.xml`ファイルに次のコードを追加

> Unity の場合、/Assets/Plugins/Android/AndroidManifest.xml を修正

```java
// TODO : <application>タグの中に入れてください。

<application>

...

   <uses-library android:name="org.apache.http.legacy" android:required="false" />

...

</application>
```

ref.) その部分がパッチされたライブラリの交換ではなく、することができます。 \[[gamepot-channel-naver.aar](https://kr.object.ncloudstorage.com/itsb/patch/gamepot-channel-naver.aar)\]

## プレイストア APK アップロード時に、com.nhncorp.nelo2.android.util 暗号化パターンのセキュリティ警告が発生

⒈ logging 機能関連のライブラリが obsolete なので発生する問題

⒉ （ダッシュボードログ機能を使用しない場合）Gamepot SDK のライブラリの中で、以下のリストのライブラリを削除

|                                        |     |
| :------------------------------------- | :-- |
| 1. gamepot-logger.aar                  |
| 2. nelo2-android-sdk-common-0.10.2.jar |
| 3. nelo2-android-sdk-https-0.10.2.jar  |
|                                        |     |

## Line i386 x86_64 IOS Archive アップロードの問題

⒈ コンソール（端末）から LineSDK.framework ファイルの場所に移動した後、次のコマンドを一つずつ入力してください。

```text
（許可されていないアーキテクチャを削除するコードです。）

lipo -remove x86_64 ./LineSDK.framework/LineSDK -o ./LineSDK.framework/LineSDK
lipo -remove i386 ./LineSDK.framework/LineSDK -o ./LineSDK.framework/LineSDK
lipo -remove x86_64 ./LineSDKObjC.framework/LineSDKObjC -o ./LineSDKObjC.framework/LineSDKObjC
lipo -remove i386 ./LineSDKObjC.framework/LineSDKObjC -o ./LineSDKObjC.framework/LineSDKObjC
```

## Twitter i386 x86_64 IOS ビルドの問題

⒈ コンソール（端末）から TwitterCore.framework ファイルの場所に移動した後、次のコマンドを一つずつ入力してください。

```text
（許可されていないアーキテクチャを削除するコードです。）

lipo -remove x86_64 ./TwitterCore.framework/TwitterCore -o ./TwitterCore.framework/TwitterCore
lipo -remove i386 ./TwitterCore.framework/TwitterCore -o ./TwitterCore.framework/TwitterCore
lipo -remove x86_64 ./TwitterKit.framework/TwitterKit -o ./TwitterKit.framework/TwitterKit
lipo -remove i386 ./TwitterKit.framework/TwitterKit -o ./TwitterKit.framework/TwitterKit
```

## AdbrixRM i386 x86_64 IOS ビルドの問題

⒈ コンソール（端末）から AdBrixRM.framework ファイルの場所に移動した後、次のコマンドを一つずつ入力してください。

```text
（許可されていないアーキテクチャを削除するコードです。）

lipo -remove x86_64 ./AdBrixRM.framework/AdBrixRM -o ./AdBrixRM.framework/AdBrixRM
lipo -remove i386 ./AdBrixRM.framework/AdBrixRM -o ./AdBrixRM.framework/AdBrixRM
```

## はいアロイ NaverThirdPartyLogin.framework i386 x86_64 問題

```text
（許可されていないアーキテクチャを削除するコードです。）

lipo -remove x86_64 ./NaverThirdPartyLogin.framework/NaverThirdPartyLogin -o ./NaverThirdPartyLogin.framework/NaverThirdPartyLogin
lipo -remove i386 ./NaverThirdPartyLogin.framework/NaverThirdPartyLogin -o ./NaverThirdPartyLogin.framework/NaverThirdPartyLogin
```

## Unity2018.4.4 以上、Unity2019.2.0 以上で Android ビルド問題

⒈`mainTemplate.gradle`ファイルを以下のように変更し

> TODO 項目を参照してください。

```java
// TODO：GradleVersionが使用されている場所をすべて削除します。

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
                  // TODO : Android gradle plugin versionを3.4.0バージョンに変更します。
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

⒉ Firebase 関連ファイルを修正

- ⒈ [リンク](https://kr.object.ncloudstorage.com/gamepot/Firebase_patch.zip)を介してパッチファイルをダウンロード

- ⒉ 以下のようにファイルのコピー

  ```java
  /Firebase_patch/Assets/Firebase/Editor
   上記のパスのファイルを下のパスにコピー
  -> {unity project}/Assets/Firebase/Editor

  {unity project}/Assets/PlayServicesResolver/Editor
   上記のパスのファイルをすべて削除した後、次のパスにファイルをコピーする
  -> /Firebase_patch/Assets/PlayServicesResolver/Editor
  ```

- ⒊ / Assets/ Plugins/ Android/ Firebase/ res フォルダが作成されていない場合 Unity やり直し

## （Unity）ネイバープラグ（SDK plug_sdk_4_4_7.unitypackage.unitypackage 以上）を適用する際、IOS ビルドエラーが発生。

- [リンク](https://kr.object.ncloudstorage.com/itsb/patch/Patch_GamePotNaverLogin_20200508.zip)を介してパッチファイルをダウンロードして解凍 (GamePotNaver.framework)

- ダウンロードしたパッチ（GamePotNaver.framework）を既存のパスの framework と交換してください。

## （IOS）ネイバープラグ SDK を適用する際、ウェプビュを介してネイバー ID をログイン不可。

- XCode の info.plist を開いてください。

- 次のように、Naver Cafe の URLScheme 値を、その Array の最も最初のインデックスに上げて保存し、ログイン正常動作を確認してください。
  ![gamepot_troubleshooting_01](./images/gamepot_troubleshooting_01.png)


##（Unity）ネイバーラウンジSDK適用（NaverSDK Ver1.1.1基準の説明）

参考URL：https://navergame.gitbook.io/naver-game/naver-game-sdk-faq-1#unity-android-class-duplication-exception

- ユニティプラグインパッケージ適用時navergame-sdk-1.1.1.aarファイルを含まない、または削除処理の進行

../Assets/NGSDK/Plugins/Android/navergame-sdk-1.1.1.aar

- AndroidのネイティブネイバーラウンジSDKライブラリ搭載

../Assets/Plugins/Android/navergame-sdk-gradle-1.1.1.aar 

-  mainTemplate.gradleファイルの変更（ネイバーラウンジSDKで使用されるライブラリの追加）

```text
dependencies {
..
implementation 'androidx.multidex:multidex:2.0.1'
implementation "androidx.recyclerview:recyclerview:1.2.0"
implementation "androidx.viewpager2:viewpager2:1.0.0"
implementation "com.squareup.retrofit2:retrofit:2.6.4"
```

- ../Assets/Plugins/Android/libsフォルダに重複したライブラリの削除（削除リスト）

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

## (Unity) GoogleMobileAds SDK の適用(GoogleMobileAds-v6.1.2 基準の説明)

AdMob Unity（SDK）の場合は、Unityパッケージをインポートした後にUnity Play Services Resolver機能を使用する必要があります。

Unity で Assets > Play Services Resolver > Android Resolver > Settings メニュー中

Use Jetifier を選択してください。

Enable Resolution On Build / Enable Auto-Resolution / Patch gradle Template.properties項目は、選択解除した状態でResolverを進めてください。

Unity で Assets > Play Services Resolver > IOS Resolver > Settings メニュー中

Add use_frameworks! to podfile / Always add the main target to Podfile 項目は選択解除した状態で IOS ビルドを進めてください。

その後、冗長ライブラリエラーの場合は、どちらか一方のライブラリを削除してください。

重複するライブラリファイルのリスト:

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

## （Unity）appsflyer SDKを適用します（appsflyer-v6.3.2に基づく）

他のSDKも同じですが、UnityAppControllerクラスは、ビルドするプロジェクト内の1つのファイルからのみ継承する必要があります。

GAMEPOT用のUnityプラグインパッケージをマウントする場合、デフォルトでGamePotAppDelegate.hから継承しています。

appflyerやSingularなどの広告ツールの場合、ライブラリはUnityAppControllerも継承するため、GAMEPOT SDKが機能しない可能性があります。

1つのファイルからのみ継承されるように変更して使用する必要があります。

예시)
[appsflyer-v6.3.2 기준 패치](https://xyuditqzezxs1008973.cdn.ntruss.com/patch/fixed_appsflyer632.zip)


## (Unity) Applying Firebase SDK separately (guide for Firebase Unity 8.7.0)

- If you are using a Unity editor older than 2019.X, please proceed with the patch below first.

Download patch : [Download patch](https://xyuditqzezxs1008973.cdn.ntruss.com/patch/unity_2020_X.zip)

[Replace folders and files]

../Assets/ExternalDependencyManager

../Assets/Firebase

- Change the folder name for the replaced Firebase library
Previous : ../Assets/Plugins/Android/Firebase
New : ../Assets/Plugins/Android/FirebaseApp.androidlib

- Edit mainTemplate.gradle (due to the change in the folder name)
Previous :
dependencies {
...
implementation project('Firebase')
New :
dependencies {
...
implementation project('FirebaseApp.androidlib')
...


- GAMEPOT's Unity plugin package contains some Firebase SDK, so using another Firebase SDK will cause an error due to the duplicate libraries.

Firebase Unity SDK(FirebaseAnalytics.unitypackage / FirebaseMessaging.unitypackage + Firebase SDK you wish to add) needs to be imported first to use the Unity Play Services Resolver.

On Unity, go to Assets > Play Services Resolver > Android Resolver > Settings and

select Use Jetifier.

Enable Resolution On Build / Enable Auto-Resolution / Patch gradle Template.properties need to be deselected to proceed with Resolver.

On Unity, go to Assets > Play Services Resolver > IOS Resolver > Settings and

deselect Add use_frameworks! to podfile / Always add the main target to Podfile to start the IOS build.


1. Must delete duplicate library files:
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


2. ../Assets/Plugins/Android/AndroidManifest.xml Confirm that your FCM-related codes are applied

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


3. Additional steps for IOS build with Firebase Unity 9.4.0

- In the result of the IOS build on the Unity editor, search for Podfile and edit it as follows. ( if another library exists, add :modular_headers => true )

Firebase / FirebaseCore / GoogleUtilities need to be added as shown on the examples below.


example )

```text

[Previous]

...
target 'UnityFramework' do
pod 'Firebase/Analytics', '9.4.0'
pod 'Firebase/Core', '9.4.0'
pod 'Firebase/Messaging', '9.4.0'
end

[New]

target 'UnityFramework' do
pod 'Firebase/Analytics', '9.4.0' , :modular_headers => true
pod 'Firebase/Core', '9.4.0' , :modular_headers => true
pod 'Firebase/Messaging', '9.4.0' , :modular_headers => true

pod 'Firebase', :modular_headers => true
pod 'FirebaseCore', :modular_headers => true
pod 'GoogleUtilities', :modular_headers => true
end

```

- On terminal, navigate to the location of the Podfile, run pod install, and proceed with this project's build after the file Unity-iPhone.xcworkspace is created