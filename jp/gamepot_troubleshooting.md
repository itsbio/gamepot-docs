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
