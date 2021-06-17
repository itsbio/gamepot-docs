# Troubleshooting

## 64-bit 환경에서 빌드 할 때, 네아로(네이버 아이디 로그인)시도 시 크래시가 발생. (API 28 이상의 Android 빌드)

⒈ `AndroidManifest.xml` 파일에 다음 코드를 추가

> Unity의 경우, /Assets/Plugins/Android/AndroidManifest.xml를 수정

```java
// TODO : <application> 태그 안에 넣어주세요.

<application>

...

   <uses-library android:name="org.apache.http.legacy" android:required="false" />

...

</application>
```

ref.) 해당 부분이 패치된 라이브러리의 교체로 대신할 수 있습니다. \[[gamepot-channel-naver.aar](https://kr.object.ncloudstorage.com/itsb/patch/gamepot-channel-naver.aar)\]


## 플레이 스토어 APK 업로드 시, com.nhncorp.nelo2.android.util 암호화패턴 보안알림 발생

⒈ logging 기능 관련 라이브러리가 obsolete여서 발생하는 문제

⒉ (대시보드 로그 기능을 사용하지 않을 경우) Gamepot SDK의 라이브러리 중, 아래 목록의 라이브러리를 제거

 |||
 | :------  | :------  |
 | 1. gamepot-logger.aar |
 | 2. nelo2-android-sdk-common-0.10.2.jar |
 | 3. nelo2-android-sdk-https-0.10.2.jar |
 |||

## Line i386 x86_64 IOS Archive 업로드 이슈

⒈ 콘솔(터미널)에서 LineSDK.framework 파일 위치로 이동 후, 아래 명령어를 하나씩 입력 해주세요.

```text
(허용되지 않은 아키텍쳐를 제거하는 코드 입니다.) 

lipo -remove x86_64 ./LineSDK.framework/LineSDK -o ./LineSDK.framework/LineSDK
lipo -remove i386 ./LineSDK.framework/LineSDK -o ./LineSDK.framework/LineSDK
lipo -remove x86_64 ./LineSDKObjC.framework/LineSDKObjC -o ./LineSDKObjC.framework/LineSDKObjC
lipo -remove i386 ./LineSDKObjC.framework/LineSDKObjC -o ./LineSDKObjC.framework/LineSDKObjC
```

## Twitter i386 x86_64 IOS 빌드 이슈

⒈ 콘솔(터미널)에서 TwitterCore.framework 파일 위치로 이동 후, 아래 명령어를 하나씩 입력 해주세요.

```text
(허용되지 않은 아키텍쳐를 제거하는 코드 입니다.)  

lipo -remove x86_64 ./TwitterCore.framework/TwitterCore -o ./TwitterCore.framework/TwitterCore
lipo -remove i386 ./TwitterCore.framework/TwitterCore -o ./TwitterCore.framework/TwitterCore
lipo -remove x86_64 ./TwitterKit.framework/TwitterKit -o ./TwitterKit.framework/TwitterKit
lipo -remove i386 ./TwitterKit.framework/TwitterKit -o ./TwitterKit.framework/TwitterKit
```

## AdbrixRM i386 x86_64 IOS 빌드 이슈

⒈ 콘솔(터미널)에서 AdBrixRM.framework 파일 위치로 이동 후, 아래 명령어를 하나씩 입력 해주세요.

```text
(허용되지 않은 아키텍쳐를 제거하는 코드 입니다.) 

lipo -remove x86_64 ./AdBrixRM.framework/AdBrixRM -o ./AdBrixRM.framework/AdBrixRM
lipo -remove i386 ./AdBrixRM.framework/AdBrixRM -o ./AdBrixRM.framework/AdBrixRM
```


## 네아로 NaverThirdPartyLogin.framework i386 x86_64 이슈
```text
(허용되지 않은 아키텍쳐를 제거하는 코드 입니다.) 

lipo -remove x86_64 ./NaverThirdPartyLogin.framework/NaverThirdPartyLogin -o ./NaverThirdPartyLogin.framework/NaverThirdPartyLogin
lipo -remove i386 ./NaverThirdPartyLogin.framework/NaverThirdPartyLogin -o ./NaverThirdPartyLogin.framework/NaverThirdPartyLogin
```


## Unity 2018.4.4이상, Unity 2019.2.0이상에서 Android 빌드 이슈

⒈ `mainTemplate.gradle` 파일을 아래와 같이 수정

> TODO 항목을 참고하세요.

```java
// TODO : GradleVersion이 사용되는 곳을 모두 제거합니다.

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
                  // TODO : Android gradle plugin version을 3.4.0버전으로 변경합니다.
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

⒉ Firebase 관련 파일을 수정

- ⒈ [링크](https://kr.object.ncloudstorage.com/gamepot/Firebase_patch.zip)를 통해 패치파일을 다운로드

- ⒉ 아래와 같이 파일 복사

    ```java
    /Firebase_patch/Assets/Firebase/Editor
     위 경로의 파일을 아래 경로에 복사
    -> {unity project}/Assets/Firebase/Editor

    {unity project}/Assets/PlayServicesResolver/Editor
     위 경로의 파일을 모두 삭제 후 아래 경로에 파일을 복사
    -> /Firebase_patch/Assets/PlayServicesResolver/Editor
    ```

- ⒊ /Assets/Plugins/Android/Firebase/res 폴더가 생성되지 않았다면 Unity 재실행


## (Unity) 네이버 플러그 SDK (plug_sdk_4_4_7.unitypackage.unitypackage 이상) 를 적용 시, IOS 빌드 오류 발생.

- [링크](https://kr.object.ncloudstorage.com/itsb/patch/Patch_GamePotNaverLogin_20200508.zip)를 통해 패치파일을 다운로드 및 압축 해제  (GamePotNaver.framework)

- 다운받은 패치(GamePotNaver.framework)를 기존 경로의 framework와 교체해주세요.

## (IOS) 네이버 플러그 SDK를 적용 시, 웹뷰를 통해 네이버 아이디 로그인 불가. 

- XCode에서 info.plist를 열어주세요.

 - 다음과 같이, Naver Cafe의 URLScheme 값을 해당 Array의 가장 첫번째 인덱스로 올려 저장한 다음 로그인 정상동작을 확인해주세요.  
 
![gamepot_troubleshooting_01](./images/gamepot_troubleshooting_01.png)


## (Unity) IDFA 허용 여부 확인 팝업 제거 (IOS 13 이하) 

- (유니티 프로젝트, 혹은 XCode 프로젝트에서) GamePotAppDelegate.mm을 열어주세요.
    
    경로
        - (Unity Project) Assets/Plugins/IOS/Source/GamePotAppDelegate.mm
        - (XCode) Libraries/Plugins/IOS/Source/GamePotAppDelegate.mm

 - 다음과 같이, AppTrackingTransparency를 초기화하는 부분을 제거해주세요.
 
![gamepot_troubleshooting_02](./images/gamepot_troubleshooting_02.png)

![gamepot_troubleshooting_03](./images/gamepot_troubleshooting_03.png)
