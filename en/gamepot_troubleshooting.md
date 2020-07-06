# Troubleshooting

## When building in 64-bit environment, a crash occurs when attempting Nearo (Naver ID login). (Android build of API 28 or higher)

⒈ Add the following code to the `AndroidManifest.xml` file

> For Unity, edit /Assets/Plugins/Android/AndroidManifest.xml

```java
// TODO: Please put it inside the <application> tag.

<application>

...

   <uses-library android:name="org.apache.http.legacy" android:required="false" />

...

</application>
```

ref.) that part can be replaced by replacement of the patched library. \[[gamepot-channel-naver.aar](https://kr.object.ncloudstorage.com/itsb/patch/gamepot-channel-naver.aar)\]

## When uploading Play Store APK, com.nhncorp.nelo2.android.util encryption pattern security notification occurs

Problem caused by obsolete library related to logging function

⒉ (If you do not use the dashboard log function) Among the library of Gamepot SDK, remove the library listed below

|                                        |     |
| :------------------------------------- | :-- |
| 1. gamepot-logger.aar                  |
| 2. nelo2-android-sdk-common-0.10.2.jar |
| 3. nelo2-android-sdk-https-0.10.2.jar  |
|                                        |     |

## Line i386 x86_64 IOS Archive upload issue

이동 After moving to the location of the LineSDK.framework file in the console (terminal), enter the following commands one by one.

```text
(This code removes the disallowed architecture.)

lipo -remove x86_64 ./LineSDK.framework/LineSDK -o ./LineSDK.framework/LineSDK
lipo -remove i386 ./LineSDK.framework/LineSDK -o ./LineSDK.framework/LineSDK
lipo -remove x86_64 ./LineSDKObjC.framework/LineSDKObjC -o ./LineSDKObjC.framework/LineSDKObjC
lipo -remove i386 ./LineSDKObjC.framework/LineSDKObjC -o ./LineSDKObjC.framework/LineSDKObjC
```

## Twitter i386 x86_64 IOS build issue

After moving to the location of TwitterCore.framework in the console (terminal), enter the following commands one by one.

```text
(This code removes the disallowed architecture.)

lipo -remove x86_64 ./TwitterCore.framework/TwitterCore -o ./TwitterCore.framework/TwitterCore
lipo -remove i386 ./TwitterCore.framework/TwitterCore -o ./TwitterCore.framework/TwitterCore
lipo -remove x86_64 ./TwitterKit.framework/TwitterKit -o ./TwitterKit.framework/TwitterKit
lipo -remove i386 ./TwitterKit.framework/TwitterKit -o ./TwitterKit.framework/TwitterKit
```

## AdbrixRM i386 x86_64 IOS build issue

After moving to the location of AdBrixRM.framework in the console (terminal), enter the following commands one by one.

```text
(This code removes the disallowed architecture.)

lipo -remove x86_64 ./AdBrixRM.framework/AdBrixRM -o ./AdBrixRM.framework/AdBrixRM
lipo -remove i386 ./AdBrixRM.framework/AdBrixRM -o ./AdBrixRM.framework/AdBrixRM
```

## Nearo NaverThirdPartyLogin.framework i386 x86_64 issue

```text
(This code removes the disallowed architecture.)

lipo -remove x86_64 ./NaverThirdPartyLogin.framework/NaverThirdPartyLogin -o ./NaverThirdPartyLogin.framework/NaverThirdPartyLogin
lipo -remove i386 ./NaverThirdPartyLogin.NaverThirdPartyLogin -o ./NaverThirdPartyLogin.framework/NaverThirdPartyLogin
```

## Android build issue in Unity 2018.4.4 or higher, Unity 2019.2.0 or higher

⒈ Modify `mainTemplate.gradle` file as below

> See TODO.

```java
// TODO: Remove all where GradleVersion is used.

buildscript {
    repositories {
        // if (GradleVersion.current() >= GradleVersion.version("4.2")) {
            google()
            jcenter()
        //} else {
        // jcenter()
        //}
    }
    dependencies {
        // if (GradleVersion.current() <GradleVersion.version("4.0")) {
        // classpath'com.android.tools.build:gradle:2.1.0'
        //} else if (GradleVersion.current() <GradleVersion.version("4.2")) {
        // classpath'com.android.tools.build:gradle:2.3.0'
        //} else {
                  // TODO: Change Android gradle plugin version to 3.4.0 version.
            classpath'com.android.tools.build:gradle:3.4.0'
        //}
        classpath'com.google.gms:google-services:3.2.0'
    }
}

allprojects {
   repositories {
        flatDir {
            dirs'libs'
        }

        // if (GradleVersion.current() >= GradleVersion.version("4.2")) {
            google()
            jcenter()
        //} else {
        // jcenter()
        //}
   }
}


dependencies {
    // if (GradleVersion.current() >= GradleVersion.version("4.2")) {
        implementation fileTree(include: ['*.jar'], dir:'libs')
        implementation project(":GamePotResources")
        implementation project(':Firebase')
    //} else {
    // compile fileTree(include: ['*.jar'], dir:'libs')
    // compile project(":GamePotResources")
    // compile project(':Firebase')
    //}
}

fileTree(dir:'libs', include: ['*.aar'])
        .each {File file ->
    // println file.name
    // if (GradleVersion.current() >= GradleVersion.version("4.2")) {
        dependencies.add("implementation", [name: file.name.lastIndexOf('.').with {it != -1? file.name[0..<it]: file.name }, ext:'aar '])
    //} else {
    // dependencies.add("compile", [name: file.name.lastIndexOf('.').with {it != -1? file.name[0..<it]: file.name }, ext: 'aar'])
    //}
}
```

⒉ Edit Firebase related files

-Download the patch file through [Link](https://kr.object.ncloudstorage.com/gamepot/Firebase_patch.zip)

-Copy file as below

```java
/Firebase_patch/Assets/Firebase/Editor
 Copy files from the above path to the below path
-> {unity project}/Assets/Firebase/Editor

{unity project}/Assets/PlayServicesResolver/Editor
 After deleting all files in the above path, copy the files to the below path
-> /Firebase_patch/Assets/PlayServicesResolver/Editor
```

-⒊ If /Assets/Plugins/Android/Firebase/res folder is not created, restart Unity

## (Unity) When applying Naver Plug SDK (plug_sdk_4_4_7.unitypackage.unitypackage or higher), IOS build error occurs.

-Download and extract patch files through [Link](https://kr.object.ncloudstorage.com/itsb/patch/Patch_GamePotNaverLogin_20200508.zip) (GamePotNaver.framework)

-Replace the downloaded patch (GamePotNaver.framework) with the framework of the existing path.

## (IOS) When NAVER Plug SDK is applied, NAVER ID login is not possible through web view.

-Open info.plist in XCode.

-As shown below, upload and save the URLScheme value of the Naver Cafe to the first index of the corresponding Array, then check the normal operation of the login.

![gamepot_troubleshooting_01](./images/gamepot_troubleshooting_01.png)
