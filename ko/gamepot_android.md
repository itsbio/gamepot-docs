---
search:
  keyword: ['gamepot']
---

#### **네이버 클라우드 플랫폼의 상품 사용 방법을 보다 상세하게 제공하고, 다양한 API의 활용을 돕기 위해 <a href="https://guide.ncloud-docs.com/docs/ko/home" target="_blank">[설명서]</a>와 <a href="https://api.ncloud-docs.com/docs/ko/home" target="_blank">[API 참조서]</a>를 구분하여 제공하고 있습니다.**

<a href="https://api.ncloud-docs.com/docs/ko/game-gamepot" target="_blank">Gamepot API 참조서 바로가기 >></a><br />
<a href="https://guide.ncloud-docs.com/docs/game-gamepotconsole" target="_blank">Gamepot 설명서 바로가기 >></a>

# Android SDK

## 1. 시작하기

### 개발 환경 구성

Android용 애플리케이션의 개발을 위해서는 개발 툴\(Android Studio 등\)을 설치해야 합니다. 사용하는 개발 툴에 따라서는 추가적으로 Java SDK와 Android SDK 등을 설치해야 할 수도 있습니다.

Android에서 GAMEPOT을 사용하기 위한 시스템 환경은 다음과 같습니다.

\[ 시스템 환경 \]

- 최소사항: API 17 \(Jelly Bean, 4.2\) 이상, gradle 3.3.3 또는 gradle 3.4.3 이상
- 개발 환경: Android Studio

#### 프로젝트 생성

![gamepot_android_01.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_android_01%284%29.png)


#### 라이브러리 추가

다운로드한 AOS SDK 파일을 app/libs 폴더에 추가합니다.

![gamepot_android_02.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_android_02%283%29.png)

#### build.gradle 설정

build.gradle 파일은 프로젝트 root 폴더와 app 폴더에 각각 존재합니다.

1. 프로젝트 root 폴더의 build.gradle 파일 수정

   ```java
   buildscript {

       repositories {
           ...
           google()
           jcenter()
           maven { url "https://jitpack.io" }
           maven { url "https://jcenter.bintray.com" }
       }
       dependencies {
          ...
           classpath 'com.google.gms:google-services:4.2.0'
       }
   }

   allprojects {
       repositories {
           ...
           google()
           jcenter()
           maven { url "https://jitpack.io" }
           maven { url "https://jcenter.bintray.com" }
       }
   }
   ```

2. app 폴더의 build.gradle 수정

   > \[xxxxx\]에는 실제 적용될 값을 넣습니다.

| 값                           | 설명                                                                                           |
| :--------------------------- | :--------------------------------------------------------------------------------------------- |
| gamepot_project_id           | GAMEPOT에서 발급받은 프로젝트 아이디를 입력해 주세요.                                          |
| gamepot_store                | 스토어값 \(`google` 또는 `one` 또는 `galaxy`\)                                                 |
| gamepot_payment              | 결제수단값 \(스토어가 google인 경우에만 해당되며 현재는 `mycard`지원\)                         |
| gamepot_app_title            | 앱 제목 \(FCM\)                                                                                |
| gamepot_push_default_channel | 등록된 기본 채널 이름 \(Default\) - 변경하지 마세요.                                           |
| facebook_app_id              | 페이스북 발급 받은 앱ID                                                                        |
| fb_login_protocol_scheme     | 페이스북에서 발급 받은 protocol scheme fb\[app_id\]                                            |
| gamepot_elsa_projectid       | NCLOUD ELSA 사용시 프로젝트ID \([자세히 보기](https://www.ncloud.com/product/analytics/elsa)\) |

```java
android {
    defaultConfig {
        ...
        // GamePot [START]
        resValue "string", "gamepot_project_id", "[projectId]" // required
        resValue "string", "gamepot_store", "[storeId]" // required
        resValue "string", "gamepot_payment", "[storeId]" // optional
        resValue "string", "gamepot_app_title","@string/app_name" // required (fcm)
        resValue "string", "gamepot_push_default_channel","Default" // required (fcm)
        resValue "string", "facebook_app_id", "[Facebook ID]" // facebook
        resValue "string", "fb_login_protocol_scheme", "fb[Facebook ID]" // (facebook)
        // resValue "string", "gamepot_elsa_projectid", "" // (ncp elsa)
        // GamePot [END]
    }

    packagingOptions {
        exclude 'META-INF/proguard/androidx-annotations.pro'
    }
}

repositories {
    flatDir {
        dirs 'libs'
    }
}

dependencies {
    implementation 'androidx.appcompat:appcompat:1.2.0'
    implementation 'androidx.multidex:multidex:2.0.1'

    // GamePot common [START]
    implementation(name: 'gamepot-common', ext: 'aar')
    implementation('io.socket:socket.io-client:1.0.0') {
        exclude group: 'org.json', module: 'json'
    }
    implementation('com.github.ihsanbal:LoggingInterceptor:3.0.0') {
        exclude group: 'org.json', module: 'json'
    }
    implementation "com.github.nisrulz:easydeviceinfo:2.4.1"
    implementation 'pub.devrel:easypermissions:1.3.0'
    implementation 'com.android.installreferrer:installreferrer:1.0'
    implementation 'com.google.code.gson:gson:2.8.2'
    implementation 'com.jakewharton.timber:timber:4.7.0'
    implementation 'com.squareup.okhttp3:okhttp:4.9.1'
    implementation 'com.apollographql.apollo:apollo-runtime:1.0.0-alpha2'
    implementation 'com.apollographql.apollo:apollo-android-support:1.0.0-alpha2'
    implementation 'com.android.billingclient:billing:3.0.3'
    implementation 'com.github.bumptech.glide:glide:3.7.0'
    implementation 'com.romandanylyk:pageindicatorview:1.0.3'
    implementation 'androidx.sqlite:sqlite-framework:2.0.1'
    implementation 'com.cookpad.puree:puree:4.1.6'
    implementation 'com.google.firebase:firebase-core:18.0.1'
    implementation 'com.google.firebase:firebase-messaging:21.0.1'
    // GamePot common [END]

    implementation(name: 'gamepot-channel-base', ext: 'aar')
    // GamePot facebook [START]
    implementation(name: 'gamepot-channel-facebook', ext: 'aar')
    implementation 'com.facebook.android:facebook-android-sdk:8.1.0'
    // GamePot facebook [END]

    // GamePot google sigin [START]
    implementation(name: 'gamepot-channel-google-signin', ext: 'aar')
    implementation "com.google.android.gms:play-services-auth:19.0.0"
    // GamePot google sigin [END]
}

// ADD THIS AT THE BOTTOM
apply plugin: 'com.google.gms.google-services'
```

3. 구글에서 발급받은 google-service.json 파일을 /app/ 폴더 하위에 복사합니다.
4. Gradle Sync Now

   Android Studio에서 **[아래]** 버튼을 클릭하여 새로고침합니다.

![gamepot_android_03.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_android_03%285%29.png)

- 새로고침을 누른 후 발생할 수 있는 실패

  - Configuration 'compile' is obsolete and has been replaced with 'implementation' and 'api'. It will be removed at the end of 2018. For more information see: [http://d.android.com/r/tools/update-dependency-configurations.html](http://d.android.com/r/tools/update-dependency-configurations.html)

    > Gradle 버전을 3 이상 쓰시는 경우 compile을 implementation

  - No matching client found for package name 'packagename'

    > app의 패키지명과 google-service.json에 선언된 패키지명을 일치하도록 변경해주세요.

#### AndroidManifest.xml 설정

일반적으로 게임에 사용되는 설정 값을 추가합니다. 각 설정별로 자세한 설명은 코드를 참고해주세요.

> 권장 사항으로 개발사 판단하에 적용 여부를 검토해주세요.

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <!--전화 기능이 없는 기기(태블릿)에서도 스토어에서 다운로드할 수 있도록 설정-->
    <uses-feature android:name="android.hardware.telephony" android:required="false" />
    <!--음성 채팅이 지원되는 게임을 마이크가 없는 기기에서도 스토어에서 다운로드할 수 있도록 설정-->
    <uses-feature android:name="android.hardware.microphone" android:required="false" />

    <!--allowBackup을 필히 false로 해주세요. (게임이 재설치되면 자동으로 shared preference값을 복구하는 것을 막는 용도입니다.)-->
    <application
        android:name="androidx.multidex.MultiDexApplication"
        android:allowBackup="false"
        tools:replace="android:allowBackup">

        <!--resizeableActivity : 앱 분할 화면 보기 기능 비활성화-->
        <activity
            android:resizeableActivity="false">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>

        <!--갤럭시 S8과 같은 스크린 대응-->
        <meta-data android:name="android.max_aspect" android:value="2.1" />

    </application>
</manifest>
```

#### Push Notification 아이콘 설정


![gamepot_android_04.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_android_04%284%29.png){height="" width=""}

푸시 수신 시 Notification bar에 보여줄 icon은 기본적으로 SDK 내부의 기본 이미지로 처리되며, 게임에 맞게 직접 넣을 수도 있습니다.

**icon 직접 넣기**

> [Android Asset Studio](http://romannurik.github.io/AndroidAssetStudio/icons-notification.html#source.type=clipart&source.clipart=ac_unit&source.space.trim=1&source.space.pad=0&name=ic_stat_gamepot_small)를 사용하여 아이콘을 제작하면 자동으로 폴더별로 제작되므로 각 폴더에 넣기만 하면 됩니다.

1. res/drawable 관련 폴더를 아래와 같이 생성
   - res/drawable-mdpi/
   - res/drawable-hdpi/
   - res/drawable-xhdpi/
   - res/drawable-xxhdpi/
   - res/drawable-xxxhdpi/
2. 아래 사이즈별로 이미지 제작
   - 24x24
   - 36x36
   - 48x48
   - 72x72
   - 96x96
3. 아래와 같이 각 폴더별로 사이즈에 맞는 이미지를 추가

| 폴더명                | 사이즈 |
| :-------------------- | :----- |
| res/drawable-mdpi/    | 24x24  |
| res/drawable-hdpi/    | 36x36  |
| res/drawable-xhdpi/   | 48x48  |
| res/drawable-xxhdpi/  | 72x72  |
| res/drawable-xxxhdpi/ | 96x96  |

1. 이미지 파일명을 `ic_stat_gamepot_small`로 변경

## 2. 초기화

MainActivity.java 파일에 아래 부분을 추가합니다.

```java
import io.gamepot.common.GamePot;
import io.gamepot.common.GamePotLocale;

@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    // GAMEPOT 초기화. context는 꼭 application context를 넣어 주세요.
    // setup API는 다른 API보다 가장 처음에 호출해야 합니다.
    GamePot.getInstance().setup(getApplicationContext());
}

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    GamePot.getInstance().onActivityResult(requestCode, resultCode, data);
}

@Override
protected void onStart() {
    super.onStart();
    GamePotChat.getInstance().start();
    GamePot.getInstance().onStart(this);
}

@Override
protected void onStop() {
    super.onStop();
    GamePotChat.getInstance().stop();
}

@Override
protected void onDestroy() {
    super.onDestroy();
    GamePot.getInstance().onDestroy();
}
```

## 3. 로그인, 로그아웃, 회원 탈퇴

구글, 페이스북, 네이버 등 다양한 로그인 SDK를 통합하여 사용할 수 있습니다.

### 구글\(Firebase\) 콘솔 설정

APK 빌드 시 사용한 Keystore의 SHA-1 값을 Firebase console에 추가합니다.

> SHA-1 값은 개발사에 요청합니다.


![gamepot_android_05.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_android_05%284%29.png)

### 페이스북 콘솔 설정

APK 빌드 시 사용한 Keystore의 키 해시 값을 페이스북 콘솔에 추가합니다.

> 키 해시 값은 개발사에 요청합니다.


![gamepot_android_06.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_android_06%284%29.png)

### 설정

#### MainActivity.java 파일 수정

로그인 관련 코드를 아래와 같이 선언합니다.

```java
import io.gamepot.channel.GamePotChannel;
import io.gamepot.channel.GamePotChannelType;
import io.gamepot.channel.facebook.GamePotFacebook;
import io.gamepot.channel.google.signin.GamePotGoogleSignin;

public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        // setup API는 맨 처음에 호출돼야 합니다.
        GamePot.getInstance().setup(getApplicationContext());

        ...
        // 로그인을 사용하려는 채널별로 addChannel을 호출해주세요.(Guest 방식은 기본으로 포함)
        // Google Login 초기화
        GamePotChannel.getInstance().addChannel(this, GamePotChannelType.GOOGLE, new GamePotGoogleSignin());
        // Facebook Login 초기화
        GamePotChannel.getInstance().addChannel(this, GamePotChannelType.FACEBOOK, new GamePotFacebook());
        ...
    }

    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        GamePotChannel.getInstance().onActivityResult(this, requestCode, resultCode, data);
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        GamePotChannel.getInstance().onDestroy();
    }
}
```

### 로그인

로그인 UI는 개발사에서 구현하고, 로그인 버튼 클릭 시에 연동합니다.

```java
import io.gamepot.channel.GamePotChannel;
import io.gamepot.channel.GamePotChannelListener;
import io.gamepot.channel.GamePotChannelType;
import io.gamepot.channel.GamePotUserInfo;
import io.gamepot.common.GamePotError;

// 로그인 타입 정의
// GamePotChannelType.GOOGLE: 구글
// GamePotChannelType.FACEBOOK: 페이스북
// GamePotChannelType.NAVER: 네이버
// GamePotChannelType.LINE: 라인
// GamePotChannelType.TWITTER: 트위터
// GamePotChannelType.APPLE: 애플
// GamePotChannelType.GUEST: 게스트

// 구글 로그인 버튼을 눌렀을 때 호출
GamePotChannel.getInstance().login(this, GamePotChannelType.GOOGLE, new GamePotChannelListener<GamePotUserInfo>() {
    @Override
    public void onCancel() {
        // 사용자가 로그인을 취소한 상황.
    }

    @Override
    public void onSuccess(GamePotUserInfo userinfo) {
        // 로그인 완료. 게임 로직에 맞게 처리해주세요.
        // userinfo.getMemberid() : 회원 고유 아이디
    }

    @Override
    public void onFailure(GamePotError error) {
        // 로그인 실패. error.getMessage()를 이용해서 오류 메시지를 보여주세요.
    }
});
```

#### 회원 고유 아이디

```java
GamePot.getInstance().getMemberId();
```

### 자동 로그인

사용자가 마지막에 로그인 했던 정보를 전달하는 API를 이용하여 자동 로그인을 구현할 수 있습니다.

```java
import io.gamepot.channel.GamePotChannel;
import io.gamepot.channel.GamePotChannelListener;
import io.gamepot.channel.GamePotChannelType;
import io.gamepot.channel.GamePotUserInfo;
import io.gamepot.common.GamePotError;

// 사용자가 마지막에 로그인했던 정보를 전달하는 API
final GamePotChannelType lastLoginType = GamePotChannel.getInstance().getLastLoginType();

if(lastLoginType != GamePotChannelType.NONE) {
    // 마지막에 로그인했던 로그인 타입으로 로그인하는 방식입니다.
    GamePotChannel.getInstance().login(this, lastLoginType, new GamePotChannelListener<GamePotUserInfo>() {
        @Override
        public void onCancel() {
            // 사용자가 로그인을 취소한 상황.
        }

        @Override
        public void onSuccess(GamePotUserInfo info) {
            // 자동 로그인 완료. 게임 로직에 맞게 처리해주세요.
        }

        @Override
        public void onFailure(GamePotError error) {
            // 자동 로그인 실패. error.getMessage()를 이용해서 오류 메시지를 보여주세요.
        }
    });
}
else
{
    // 처음 게임을 실행했거나 로그아웃한 상태. 로그인을 할 수 있는 로그인 화면으로 이동해주세요.
}
```

### 로그아웃

현재 회원 계정을 로그아웃합니다.

```java
import io.gamepot.channel.GamePotChannel;
import io.gamepot.common.GamePotCommonListener;
import io.gamepot.common.GamePotError;

GamePotChannel.getInstance().logout(this, new GamePotCommonListener() {
    @Override
    public void onSuccess() {
        // 로그아웃 완료. 초기 화면으로 이동해주세요.
    }

    @Override
    public void onFailure(GamePotError error) {
        // 로그아웃 실패. error.getMessage()를 이용해서 오류 메시지를 보여주세요.
    }
});
```

### 회원 탈퇴

현재 회원 계정을 탈퇴시킵니다.

```java
import io.gamepot.channel.GamePotChannel;
import io.gamepot.common.GamePotCommonListener;
import io.gamepot.common.GamePotError;

GamePotChannel.getInstance().deleteMember(this, new GamePotCommonListener() {
    @Override
    public void onSuccess() {
        // 회원탈 퇴 성공. 초기화면으로 이동해주세요.
    }

    @Override
    public void onFailure(GamePotError error) {
        // 회원 탈퇴 실패. error.getMessage()를 이용해서 오류 메시지를 보여주세요.
    }
});
```

### 검증

로그인 완료 후 로그인 정보를 개발사 서버에서 GAMEPOT 서버로 전달하면 로그인 검증이 진행됩니다.

자세한 설명은 `Server to server api` 매뉴에 `Authentication check` 항목을 참고해주세요.

## 4. 계정 연동

하나의 게임 계정에 복수 개의 소셜 계정\(구글, 페이스북 등\)을 연결/해제할 수 있는 기능입니다.\(최소 연동 소셜 계정은 1가지입니다.\)

> 연동화면 UI는 개발사에서 구현해주세요.

### 계정 연동

Google, Facebook 등의 아이디로 계정을 연동할 수 있습니다.

```java
import io.gamepot.channel.GamePotChannel;
import io.gamepot.channel.GamePotChannelListener;
import io.gamepot.channel.GamePotChannelType;
import io.gamepot.channel.GamePotUserInfo;
import io.gamepot.common.GamePotError;

// 구글 계정에 연동
// GamePotChannelType.GOOGLE
// 페이스북 계정에 연동
// GamePotChannelType.FACEBOOK
// 네이버 계정에 연동
// GamePotChannelType.NAVER
// 라인 계정에 연동
// GamePotChannelType.LINE
// 트위터 계정에 연동
// GamePotChannelType.TWITTER
// 애플 계정에 연동
// GamePotChannelType.APPLE

GamePotChannel.getInstance().createLinking(this, GamePotChannelType.GOOGLE, new GamePotChannelListener<GamePotUserInfo>() {
    @Override
    public void onSuccess(GamePotUserInfo userInfo) {
        // 연동 완료. 연동 결과에 대한 문구를 노출시켜 주세요.(예: 계정 연동에 성공했습니다.)
    }

    @Override
    public void onCancel() {
        // 사용자가 취소한 경우
    }

    @Override
    public void onFailure(GamePotError error) {
        // 연동 실패. error.getMessage()를 이용해서 오류 메시지를 보여주세요.
    }
});
```

### 연동된 리스트

해당 API를 통해 계정에 대해 연동 여부를 확인하실 수 있습니다.

```java
import io.gamepot.channel.GamePotChannel;
import java.util.ArrayList;

// 타입 정의
// GamePotChannelType.GOOGLE
// GamePotChannelType.FACEBOOK
// GamePotChannelType.NAVER
// GamePotChannelType.LINE
// GamePotChannelType.TWITTER
// GamePotChannelType.APPLE
// 타입에 따른 연동 결과를 반환합니다.
boolean isLinked = GamePotChannel.getInstance().isLinked(GamePotChannelType.GOOGLE);

// 연동되어 있는 모든 타입에 대해 JSON 형태로 반환합니다.
// 만약 GOOGLE과 FACEBOOK에 연동된 경우 아래와 같이 반환됩니다.
// [{“provider”:”google”},{“provider”:”facebook”}]
JSONArray linking = GamePotChannel.getInstance().getLinkedList();
```

### 연동 해제

기존에 연동되어 있는 계정을 해제합니다.

```java
import io.gamepot.channel.GamePotChannel;
import io.gamepot.channel.GamePotChannelType;
import io.gamepot.common.GamePotCommonListener;
import io.gamepot.common.GamePotError;

GamePotChannel.getInstance().deleteLinking(this, GamePotChannelType.GOOGLE, new GamePotCommonListener() {
    @Override
    public void onSuccess() {
        // 연동 해제 완료. 연동 결과에 대한 문구를 노출시켜 주세요. (예: 계정 연동을 해지했습니다.)
    }

    @Override
    public void onFailure(GamePotError error) {
        // 연동 해제 실패. error.getMessage()를 이용해서 오류 메시지를 보여주세요.
    }
});
```

## 5. 결제
> 게임팟 결제는 소모성 인앱 상품 타입만을 지원하고 있으며 원스토어 인앱 SDK는 V17버전만 지원합니다.

> 원스토어 인앱 SDK 포함 : gamepot-billing-onestore.aar

> 갤럭시 스토어 인앱 SDK 포함: gamepot-billing-galaxystore.aar

결제의 결과 값은 Listener 형태로 구현되어 있습니다.

MainActivity.java에서 앱 실행 시 한 번 호출하도록 선언합니다.

```java
import io.gamepot.common.GamePot;
import io.gamepot.common.GamePotPurchaseInfo;
import io.gamepot.common.GamePotPurchaseListener;
import io.gamepot.common.GamePotError;

public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        // setup API는 맨 처음에 호출돼야 합니다.
        GamePot.getInstance().setup(getApplicationContext());

        ...
        GamePot.getInstance().setPurchaseListener(new GamePotPurchaseListener<GamePotPurchaseInfo>() {
            @Override
            public void onSuccess(GamePotPurchaseInfo info) {
                // 결제 성공. 아이템 지급 요청은 webhook에 설정된 주소로 server to server로 요청합니다.
                // 이 곳에서는 결과에 대한 처리만 해주시고 실제 아이템 지급은 하지 마세요.
            }

            @Override
            public void onFailure(GamePotError error) {
                // 결제 실패. error.getMessage()를 이용해서 오류 메시지를 보여주세요.
            }

            @Override
            public void onCancel() {
                // 결제 진행 중 사용자가 취소한 경우
            }
        });
        ...
    }
}
```

### 결제 시도

하나의 결제 API로 GooglePlay, OneStore 모두 결제가 가능합니다.

> 결제 시도 ~ 결제 완료/실패 과정중에 인게임에서 사용하는 로딩 화면을 띄워 중복 호출을 하지 않도록 처리해주세요.

```java
CASE 1 : 일반적인 결제시

import io.gamepot.common.GamePot;

// productId : 스토어에 등록된 상품ID를 입력해 주시면 됩니다.
GamePot.getInstance().purchase("product id");
```

```java
CASE 2 : 결제시 진행되는 영수증 번호를 별도로 관리하고자 할 때 :

import io.gamepot.common.GamePot;

// productId : 스토어에 등록된 상품ID를 입력해 주시면 됩니다.
// uniqueId  : 별도로 관리하는 영수증 번호를 넣으시면 됩니다.
GamePot.getInstance().purchase("product id", "uniqueId");
```

```java
CASE 3 : 결제시 진행되는 영수증 번호 / 서버아이디 / 캐릭터아이디 / 기타 정보를 webhook으로 전달 하고자 할때 :

import io.gamepot.common.GamePot;

// productId : 스토어에 등록된 상품ID를 입력해 주시면 됩니다.
// uniqueId  : 별도로 관리하는 영수증 번호를 넣으시면 됩니다.
// serverId  : 결제를 진행한 캐릭터의 서버아이디를 입력해 주시면 됩니다.
// playerId  : 결제를 진행한 캐릭터의 캐릭터 아이디를 입력해 주시면 됩니다.
// etc       : 결제를 진행한 캐릭터 기타 정보를 넣으시면 됩니다.
GamePot.getInstance().purchase("product id","uniqueId","serverId","playerId","etc");
```

### 결제 아이템 리스트 획득

스토어에서 전달하는 인앱 아이템 리스트를 획득할 수 있습니다.

```java
import io.gamepot.common.GamePot;

GamePotPurchaseDetailList details = GamePot.getInstance().getPurchaseDetailList();
```

### 결제 아이템 지급

GAMEPOT은 Server to server api를 통해 결제 스토어에 영수증 검증까지 모두 마친 후 개발사 서버에 지급 요청을 하기 때문에 불법 결제가 불가능합니다.

이를 위해선 `Server to server api` 메뉴에 `Purchase` 항목을 참고하여 처리하셔야 합니다.

## 6. 외부결제

원스토어의 경우 기본 스토어 결제 모듈이 아닌 제 3의 결제모듈을 허용하고 있습니다.

### 설정

대시보드에 외부결제 항목을 참고하여 대시보드 설정을 먼저 진행하세요.

`5. 결제` 항목을 먼저 구현했다면 추가로 설정할 부분은 없습니다.

### 결제 시도

```java
import io.gamepot.common.GamePot;

// activity : 현재 액티비티
// product id : 대시보드에 등록한 결제 아이디
GamePot.getInstance().purchaseThirdPayments(activity, product id);
```

### 결제 아이템 리스트 획득

```java
import io.gamepot.common.GamePot;

GamePotPurchaseDetailList thirdPaymentsDetailList = GamePot.getInstance().getPurchaseThirdPaymentsDetailList();
```

## 7. 기타 API

### SDK 지원 로그인 UI

SDK 내에서, 자체적으로 (완성된 형태의) Login UI를 제공합니다.

```java
import io.gamepot.channel.GamePotChannel;
import io.gamepot.channel.GamePotChannelListener;
import io.gamepot.channel.GamePotAppStatusChannelListener;
import io.gamepot.channel.GamePotChannelType;
import io.gamepot.channel.GamePotChannelLoginBuilder;
import io.gamepot.channel.GamePotUserInfo;
import io.gamepot.common.GamePotError;


//예시)
ArrayList<GamePotChannelType> channelList = new ArrayList<>( Arrays.asList(GamePotChannelType.GOOGLE, GamePotChannelType.FACEBOOK,GamePotChannelType.NAVER, GamePotChannelType.TWITTER, GamePotChannelType.LINE, GamePotChannelType.APPLE, GamePotChannelType.GUEST) );

GamePotChannelLoginBuilder builder = new GamePotChannelLoginBuilder(channelList);

// 구글 로그인 버튼을 눌렀을 때 호출
GamePotChannel.getInstance().showLoginWithUI(MainActivity.this, builder, new GamePotAppStatusChannelLoginDialogListener<GamePotUserInfo>() {
    @Override
    public void onExit() {
        // X 버튼 클릭시 처리 
    }

    @Override
    public void onNeedUpdate(GamePotAppStatus status) {
        // TODO: 강제 업데이트가 필요한 경우. 아래 API를 호출하면 SDK 자체에서 팝업을 띄울 수 있습니다.
        // TODO: Customizing을 하고자 하는 경우 아래 API를 호출하지 말고 Customizing을 하면 됩니다.
        GamePot.getInstance().showAppStatusPopup(MainActivity.this, status, new GamePotAppCloseListener() {
            @Override
            public void onClose() {
                // TODO: showAppStatusPopup API를 호출하신 경우 앱을 종료해야 하는 상황에 호출됩니다.
                // TODO: 종료 프로세스를 처리해주세요.
                MainActivity.this.finish();
            }

            @Override
            public void onNext(Object obj) {
                // TODO : Dashboard 업데이트 설정에서 권장 설정 시 "다음에 하기" 버튼이 노출 됩니다.
                // 해당 버튼을 사용자가 선택 시 호출 됩니다.
                // TODO : obj 정보를 이용하여 로그인 완료 시와 동일하게 처리해주세요.
                // GamePotUserInfo userInfo = (GamePotUserInfo)obj;
            }
        });
    }

    @Override
    public void onMainternance(GamePotAppStatus status) {
        // TODO: 점검 중인 경우. 아래 API를 호출하면 SDK 자체에서 팝업을 띄울 수 있습니다.
        // TODO: Customizing을 하고자 하는 경우 아래 API를 호출하지 말고 Customizing을 하면 됩니다.
        GamePot.getInstance().showAppStatusPopup(MainActivity.this, status, new GamePotAppCloseListener() {
            @Override
            public void onClose() {
                // TODO: showAppStatusPopup API를 호출하신 경우 앱을 종료해야 하는 상황에 호출됩니다.
                // TODO: 종료 프로세스를 처리해주세요.
                MainActivity.this.finish();
            }
        });
    }

    @Override
    public void onCancel() {
        // 사용자가 로그인을 취소한 상황.
    }

    @Override
    public void onSuccess(GamePotUserInfo userinfo) {
        // 로그인 완료. 게임 로직에 맞게 처리해주세요.
    }

    @Override
    public void onFailure(GamePotError error) {
        // 로그인 실패. error.getMessage()를 이용해서 오류 메시지를 보여주세요.
    }
});
```

#### 로그인 UI 이미지 로고 설정

로그인 UI 상단에 노출되는 이미지 로고는 SDK 내부에서 기본 이미지로 노출하며, 직접 추가할 수도 있습니다.

**이미지 로고 직접 넣기**

> [Android Asset Studio](http://romannurik.github.io/AndroidAssetStudio/icons-notification.html#source.type=clipart&source.clipart=ac_unit&source.space.trim=1&source.space.pad=0&name=ic_stat_gamepot_login_logo)를 사용하여 아이콘을 제작하면 자동으로 폴더별로 제작되므로 각 폴더에 넣기만 하면 됩니다.

1. res/drawable 관련 폴더를 아래와 같이 생성

   - res/drawable-mdpi/
   - res/drawable-hdpi/
   - res/drawable-xhdpi/
   - res/drawable-xxhdpi/
   - res/drawable-xxxhdpi/

2. 아래 사이즈별로 이미지 제작

   - 78x55
   - 116x82
   - 155x110
   - 232x165
   - 310x220

3. 아래와 같이 각 폴더별로 사이즈에 맞는 이미지를 추가

| 폴더명                | 사이즈  |
| :-------------------- | :------ |
| res/drawable-mdpi/    | 78x55   |
| res/drawable-hdpi/    | 116x82  |
| res/drawable-xhdpi/   | 155x110 |
| res/drawable-xxhdpi/  | 232x165 |
| res/drawable-xxxhdpi/ | 310x220 |

- 이미지 파일명을 `ic_stat_gamepot_login_logo.png`로 변경

### 네이버 로그인

#### build.gradle 설정

```java
android {
    defaultConfig {
        ...
        resValue "string", "gamepot_naver_clientid", "xxxxxxxx" // Naver 개발자 콘솔에서 획득
        resValue "string", "gamepot_naver_secretid", "xxx" // Naver 개발자 콘솔에서 획득
    }
}

dependencies {
  ...
  compile(name: 'gamepot-channel-naver', ext: 'aar')
  ...
}
```

#### MainActivity.java 설정

```java
import io.gamepot.channel.GamePotChannel;
import io.gamepot.channel.GamePotChannelType;
import io.gamepot.channel.naver.GamePotNaver;

@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
        ...
        GamePotChannel.getInstance().addChannel(this, GamePotChannelType.NAVER, new GamePotNaver());
}
```

#### 로그인

```java
GamePotChannel.getInstance().login(this, GamePotChannelType.NAVER, new GamePotAppStatusChannelListener<GamePotUserInfo>() {
  ...
});
```

### 라인 로그인

#### build.gradle 설정

```java
android {
    defaultConfig {
        ...
        resValue "string", "gamepot_line_channelid","00000000" // Line 개발자 콘솔에서 획득
    }
}

dependencies {
  ...
  compile(name: 'gamepot-channel-line', ext: 'aar')
  compile(name: 'line-sdk-4.0.10', ext: 'aar')
  ...
}
```

#### MainActivity.java 설정

```java
import io.gamepot.channel.GamePotChannel;
import io.gamepot.channel.GamePotChannelType;
import io.gamepot.channel.line.GamePotLine;

@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
        ...
        GamePotChannel.getInstance().addChannel(this, GamePotChannelType.LINE, new GamePotLine());
}
```

#### 로그인

```java
GamePotChannel.getInstance().login(this, GamePotChannelType.LINE, new GamePotAppStatusChannelListener<GamePotUserInfo>() {
  ...
});
```

### 트위터 로그인

#### build.gradle 설정

```java
android {
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }

    defaultConfig {
        ...
        resValue "string", "gamepot_twitter_consumerkey","xxxxx" // Twitter 개발자 콘솔에서 획득
        resValue "string", "gamepot_twitter_consumersecret","xxx" // Twitter 개발자 콘솔에서 획득
    }
}

dependencies {
  ...
  compile(name: 'gamepot-channel-twitter', ext: 'aar')
  compile('com.twitter.sdk.android:twitter-core:3.3.0@aar') {
      transitive = true
  }
  ...
}
```

#### MainActivity.java 설정

```java
import io.gamepot.channel.GamePotChannel;
import io.gamepot.channel.GamePotChannelType;
import io.gamepot.channel.twitter.GamePotTwitter;

@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
        ...
        GamePotChannel.getInstance().addChannel(this, GamePotChannelType.TWITTER, new GamePotTwitter());
}
```

#### 로그인

```java
GamePotChannel.getInstance().login(this, GamePotChannelType.TWITTER, new GamePotAppStatusChannelListener<GamePotUserInfo>() {
  ...
});
```

### 애플 로그인(Web Login)

#### build.gradle 설정

```java
dependencies {
  ...
  compile(name: 'gamepot-channel-apple-signin', ext: 'aar')
  ...
}
```

#### MainActivity.java 설정

```java
import io.gamepot.channel.GamePotChannel;
import io.gamepot.channel.GamePotChannelType;
import io.gamepot.channel.apple.signin.GamePotAppleSignin;

@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
        ...
        GamePotChannel.getInstance().addChannel(this, GamePotChannelType.APPLE, new GamePotAppleSignin());
}
```

#### 로그인

```java
GamePotChannel.getInstance().login(this, GamePotChannelType.APPLE, new GamePotAppStatusChannelListener<GamePotUserInfo>() {
  ...
});
```

### 쿠폰

사용자에게 입력받은 쿠폰을 사용할 때 아래 코드를 호출해 주세요.

> 쿠폰 입력 화면 UI는 개발사에서 구현해주세요.

```java
import io.gamepot.common.GamePot;
import io.gamepot.common.GamePotError;
import io.gamepot.common.GamePotListener;

GamePot.getInstance().coupon(/*사용자에게 입력받은 쿠폰*/, new GamePotListener<String>() {
    @Override
    public void onSuccess(String message) {
        // 쿠폰 사용 성공. message값을 팝업으로 노출해주세요.
    }

    @Override
    public void onFailure(GamePotError error) {
        // 쿠폰 사용 실패. error.getMessage()를 이용해서 오류 메시지를 보여주세요.
    }
});
```

#### 아이템 지급

쿠폰 사용이 성공하면 개발사 서버에 Server to server api를 통해 아이템 지급을 요청합니다.

이를 위해선 `Server to server api` 메뉴에 `Item` 항목을 참고하여 처리하셔야 합니다.

### Push on/off

전체푸시, 야간푸시, 광고성푸시 3가지 종류의 푸시를 각각 on/off를 처리 할 수 있습니다.

> on/off 설정하는 UI는 개발사에서 구현해주세요.

```java
import io.gamepot.common.GamePot;
import io.gamepot.common.GamePotError;
import io.gamepot.common.GamePotCommonListener;

// 푸시 수신 On/Off
GamePot.getInstance().setPushEnable(/*true or false*/, new GamePotCommonListener() {
    @Override
    public void onSuccess() {
    }

    @Override
    public void onFailure(GamePotError error) {
    }
});

// 야간 푸시 수신 On/Off
GamePot.getInstance().setNightPushEnable(/*true or false*/, new GamePotCommonListener() {
    @Override
    public void onSuccess() {
    }

    @Override
    public void onFailure(GamePotError error) {
    }
});

// 푸시, 야간푸시를 한번에 설정
// 로그인 전에 푸시, 야간푸시 허용 여부를 받는 게임이라면 로그인 후에 아래 코드로 필히 호출합니다.
GamePot.getInstance().setPushEnable(/*true or false*/, /*true or false*/, true, new GamePotCommonListener() {
    @Override
    public void onSuccess() {
    }

    @Override
    public void onFailure(GamePotError error) {
    }
});
```

현재 푸시 상태를 가져오려면 아래 코드를 참고하세요.

```java
import io.gamepot.common.GamePot;
import org.json.JSONObject;

// enable: 전체푸시
// night: 야간푸시
// {"enable":true, "night":true}
JSONObject status = GamePot.getInstance().getPushStatus();
```

### 공지사항

대시보드 - 공지사항에서 업로드한 이미지가 노출되는 기능입니다.

#### 호출

```java
/* showTodayButton : '오늘 하루 보지 않기' 버튼 노출 여부. false인 경우 무조건 노출 */
boolean showTodayButton = true;

GamePot.getInstance().showNotice(/*현재 액티비티*/, showTodayButton, new GamePotNoticeDialog.onSchemeListener() {
    @Override
    public void onReceive(String scheme) {
        // TODO : scheme 처리
    }
});
```

### 공지사항(분류 별 호출)

대시보드 - 공지사항에서 업로드한 이미지 중, 분류로 설정한 이미지만 노출하는 기능입니다.

#### 호출

```java
/* 대시보드 공지사항 >> 분류에서 설정한 분류명 */
string type = "";

GamePot.getInstance().showEvent(/*현재 액티비티*/, type, new GamePotNoticeDialog.onSchemeListener() {
    @Override
    public void onReceive(String scheme) {
        // TODO : scheme 처리
    }
});
```

### 고객지원

대시보드 - 고객지원 - 고객문의와 연동되는 유저와 운영자간에 소통 채널입니다.

고객문의 UI는 디바이스 언어에 맞게 변경됩니다. 한국어, 영어, 일어, 중국어(간체, 번체)를 지원하며 그 외 언어는 영어로 보여집니다.

#### 호출

```java
GamePot.getInstance().showCSWebView(/*현재 액티비티*/);
```

외부링크를 지원하여 로그인하지 않은 고객도 문의를 등록할 수 있습니다.

#### 호출

```java
String url = "게임팟에서 발급받은 외부고객지원 URL";

GamePot.getInstance().showWebView(/*현재 액티비티*/, url, true);
```

### FAQ

대시보드 - 고객지원 - FAQ와 연동되는 FAQ 목록입니다.

#### 호출

```java
GamePot.getInstance().showFaq(/*현재 액티비티*/);
```

### 로컬 푸시\(Local Push notification\)

푸시 서버를 통하지 않고 단말기에서 자체적으로 푸시를 노출하는 기능입니다.

#### 호출

**푸시 등록**

정해진 시간에 로컬 푸시를 노출하는 방법은 아래와 같습니다.

> 리턴 값으로 전달되는 pushid는 개발사에서 관리합니다.

```java
String date = "2018-09-27 20:00:00";
GamePotLocalPushBuilder builder = new GamePotLocalPushBuilder(getActivity())
                        .setTitle("로컬푸시 테스트")
                        .setMessage("로컬푸시 메시지입니다. " + date)
                        .setDateString(date).build();
int pushid = GamePot.getInstance().sendLocalPush(builder);
```

**등록한 푸시 취소**

푸시 등록 시 얻은 pushid를 기반으로 기존에 등록된 푸시를 취소할 수 있습니다.

```java
GamePot.getInstance().cancelLocalPush(/*현재 액티비티*/, /*푸시 등록시 얻은 pushid*/);
```

### 점검, 강제 업데이트

점검이나 강제 업데이트 기능이 필요한 경우 대시보드 - 운영에서 기능을 활성화할 경우 동작합니다.

#### 호출

기존에 적용된 아래 API에서 사용이 가능합니다.

**1. login API**

기존 login API에서 listener를 `GamePotAppStatusChannelListener`로 변경합니다.

```java
GamePotChannel.getInstance().login(this, GamePotChannelType.GOOGLE, new GamePotAppStatusChannelListener<GamePotUserInfo>() {
    @Override
    public void onNeedUpdate(GamePotAppStatus status) {
        // TODO: 강제 업데이트가 필요한 경우. 아래 API를 호출하면 SDK 자체에서 팝업을 띄울 수 있습니다.
        // TODO: Customizing을 하고자 하는 경우 아래 API를 호출하지 말고 Customizing을 하면 됩니다.
        GamePot.getInstance().showAppStatusPopup(MainActivity.this, status, new GamePotAppCloseListener() {
            @Override
            public void onClose() {
                // TODO: showAppStatusPopup API를 호출하신 경우 앱을 종료해야 하는 상황에 호출됩니다.
                // TODO: 종료 프로세스를 처리해주세요.
                MainActivity.this.finish();
            }

            @Override
            public void onNext(Object obj) {
                // TODO : Dashboard 업데이트 설정에서 권장 설정 시 "다음에 하기" 버튼이 노출 됩니다.
                // 해당 버튼을 사용자가 선택 시 호출 됩니다.
                // TODO : obj 정보를 이용하여 로그인 완료 시와 동일하게 처리해주세요.
                // GamePotUserInfo userInfo = (GamePotUserInfo)obj;
            }
        });
    }

    @Override
    public void onMainternance(GamePotAppStatus status) {
        // TODO: 점검 중인 경우. 아래 API를 호출하면 SDK 자체에서 팝업을 띄울 수 있습니다.
        // TODO: Customizing을 하고자 하는 경우 아래 API를 호출하지 말고 Customizing을 하면 됩니다.
        GamePot.getInstance().showAppStatusPopup(MainActivity.this, status, new GamePotAppCloseListener() {
            @Override
            public void onClose() {
                // TODO: showAppStatusPopup API를 호출하신 경우 앱을 종료해야 하는 상황에 호출됩니다.
                // TODO: 종료 프로세스를 처리해주세요.
                MainActivity.this.finish();
            }
        });
    }

    @Override
    public void onCancel() {
        // 사용자가 로그인을 취소한 상황.
    }

    @Override
    public void onSuccess(GamePotUserInfo userinfo) {
        // 로그인 완료. 게임 로직에 맞게 처리해주세요.
    }

    @Override
    public void onFailure(GamePotError error) {
        // 로그인 실패. error.getMessage()를 이용해서 오류 메시지를 보여주세요.
    }
});
```

### 약관 동의 (GDPR 포함)

'GDPR' 및 '이용약관', '개인정보 수집 및 이용안내' 동의를 쉽게 받을 수 있도록 UI를 제공합니다.

`BLUE` 테마와 `GREEN` 테마 두 가지의 `기본테마` 이외에도, 새롭게 추가된 11 종류의 `개선테마`를 제공합니다.

#### 약관 동의 호출 (자동)

`GAMEPOT SDK V3.3.0` 부터, **로그인 시 자동으로 약관 동의 팝업이 노출** 됩니다.

로그인 전, 플래그 값을 통해 이를 변경할 수 있습니다.

```java
// Default Value는 true
// 자동 팝업 시, MATERIAL_BLUE 테마로 적용 
// false로 셋팅 시, 로그인 할 때 약관 동의 팝업이 노출되지 않습니다.
GamePot.getInstance().setAutoAgree(true);

// MATERIAL_ORANGE 테마로 커스텀 적용 시
GamePotAgreeBuilder bulider = new GamePotAgreeBuilder(GamePotAgreeBuilder.THEME.MATERIAL_ORANGE);
GamePot.getInstance().setAutoAgreeBuilder(bulider);

...

GamePotChannel.getInstance().login(GamePotChannelType);

...
```

#### 약관 동의 호출 (수동)

```java
// 기본 테마
GamePotAgreeBuilder.THEME.BLUE
GamePotAgreeBuilder.THEME.GREEN

//개선 테마
GamePotAgreeBuilder.THEME.MATERIAL_RED,
GamePotAgreeBuilder.THEME.MATERIAL_BLUE,
GamePotAgreeBuilder.THEME.MATERIAL_CYAN,
GamePotAgreeBuilder.THEME.MATERIAL_ORANGE,
GamePotAgreeBuilder.THEME.MATERIAL_PURPLE,
GamePotAgreeBuilder.THEME.MATERIAL_DARKBLUE,
GamePotAgreeBuilder.THEME.MATERIAL_YELLOW,
GamePotAgreeBuilder.THEME.MATERIAL_GRAPE,
GamePotAgreeBuilder.THEME.MATERIAL_GRAY,
GamePotAgreeBuilder.THEME.MATERIAL_GREEN,
GamePotAgreeBuilder.THEME.MATERIAL_PEACH,
```

> 약관 동의 팝업 노출 여부는 개발사에서 게임에 맞게 처리해주세요.
>
> '보기' 버튼을 클릭 시 보여지는 내용은 대시보드에서 적용 및 수정이 가능합니다.

Request:

```java
// 기본 호출(MATERIAL_BLUE 테마로 적용)
GamePot.getInstance().showAgreeDialog(/*activity*/, new GamePotAgreeBuilder(), new GamePotListener<GamePotAgreeInfo>() {
    @Override
    public void onSuccess(GamePotAgreeInfo data) {
        // data.agree : 필수 약관을 모두 동의한 경우 true
        // data.agreeNight : 야간 광고성 수신 동의를 체크한 경우 true, 그렇지 않으면 false
        // agreeNight 값은 로그인 완료 후 setPushNightStatus api를 통해 전달하세요.
    }

    @Override
    public void onFailure(GamePotError error) {
        // error.message를 팝업 등으로 유저에게 알려주세요.
    }
});

// MATERIAL_ORANGE 테마로 적용시
GamePotAgreeBuilder bulider = new GamePotAgreeBuilder(GamePotAgreeBuilder.THEME.MATERIAL_ORANGE);
GamePot.getInstance().showAgreeDialog(/*activity*/, bulider, new GamePotListener<GamePotAgreeInfo>() {
  ....
}
```

#### Customizing

테마를 사용하지 않고 게임에 맞게 색을 변경합니다.

약관 동의를 호출하기 전에 `GamePotAgreeBuilder`에서 각 영역별로 색을 지정할 수 있습니다.

```java
GamePotAgreeBuilder agreeBuilder= new GamePotAgreeBuilder();

agreeBuilder.setHeaderBackGradient(new int[] {0xFF00050B,0xFF0F1B21});
agreeBuilder.setHeaderTitleColor(0xFFFF0000);
agreeBuilder.setHeaderBottomColor(0xFF00FF00);
// 미사용시 ""로 설정
agreeBuilder.setHeaderTitle("약관 동의");
// res/drawable 객체 아이디
agreeBuilder.setHeaderIconDrawable(R.drawable.ic_stat_gamepot_agree);

agreeBuilder.setContentBackGradient(new int[] { 0xFFFF2432, 0xFF11FF32 });
agreeBuilder.setContentTitleColor(0xFF0429FF);
agreeBuilder.setContentCheckColor(0xFFFFADB5);
agreeBuilder.setContentIconColor(0xFF98FFC6);
agreeBuilder.setContentShowColor(0xFF98B3FF);
// res/drawable 객체 아이디
agreeBuilder.setContentIconDrawable(R.drawable.ic_stat_gamepot_small);

agreeBuilder.setFooterBackGradient(new int[] { 0xFFFFFFFF, 0xFF112432 });
agreeBuilder.setFooterButtonGradient(new int[] { 0xFF1E3A57, 0xFFFFFFFF });
agreeBuilder.setFooterButtonOutlineColor(0xFFFF171A);
agreeBuilder.setFooterTitleColor(0xFFFF00D5);
agreeBuilder.setFooterTitle("게임 시작하기");

//광고성 수신동의(일반/야간) 체크 후, 게임 시작 시 Toast 메시지(동의 시간) 노출 여부
agreeBuilder.setShowToastPushStatus(true);

// 광고성 수신동의(일반/야간) 메세지 수정
agreeBuilder.setPushToastMsg("Push on");
agreeBuilder.setNightPushToastMsg("Night Push on");

// 일반 광고성 수신동의 버튼 노출 여부
agreeBuilder.setShowPush(true);

// 야간 광고성 수신동의 버튼 노출 여부
agreeBuilder.setShowNightPush(true);

// 일반 광고성 수신동의 링크 버튼 설정(미사용 시, 입력 안함)
agreeBuilder.setPushDetailURL("https://...");

// 야간 광고성 수신동의 링크 버튼 설정 (미사용 시, 입력 안함)
agreeBuilder.setNightPushDetailURL("https://...");

// 문구 변경
agreeBuilder.setAllMessage("모두 동의");
agreeBuilder.setTermMessage("필수) 이용약관");
agreeBuilder.setPrivacyMessage("필수) 개인정보 취급 방침");
agreeBuilder.setPushMessage("선택) 일반 푸시 수신 동의");
agreeBuilder.setNightPushMessage("선택) 야간 푸시 수신 동의");

GamePot.getInstance().showAgreeDialog(/*activity*/, agreeBuilder, new GamePotListener<GamePotAgreeInfo>() {
  ....
}
```

각각의 변수는 아래 영역에 적용됩니다.

> contentIconDrawable의 기본 이미지는 푸시 아이콘으로 설정됩니다.

- AgeView

![gamepot_android_09.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_android_09%289%29.png)

- EmailView

![gamepot_android_09_1.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_android_09_1%281%29.png)

- AgreeView

![gamepot_android_09_2.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_android_09_2.png)

### 이용약관

이용약관 UI를 호출합니다.

> 대시보드 - 고객지원 - 이용약관 설정 항목에 내용을 먼저 입력하세요.

```java
import io.gamepot.common.GamePot;

// activity : 현재 액티비티
GamePot.getInstance().showTerms(activity);
```

### 개인정보 취급방침

개인정보 취급방침 UI를 호출합니다.

> 대시보드 - 고객지원 - 개인정보취급방침 설정 항목에 내용을 먼저 입력하세요.

```java
import io.gamepot.common.GamePot;

// activity : 현재 액티비티
GamePot.getInstance().showPrivacy(activity);
```

### 환불규정

환불규정 UI를 호출합니다.

> 대시보드 - 고객지원 - 환불규정 설정 항목에 내용을 먼저 입력하세요.

```java
import io.gamepot.common.GamePot;

// activity : 현재 액티비티
GamePot.getInstance().showRefund(activity);
```

### 원격 구성

대시보드로 등록한 매개변수 값을 클라이언트 상에서 가져옵니다.

> 대시보드 - 설정 - 원격구성 화면에서 매개변수를 먼저 추가해주세요.

추가한 매개변수는 로그인 시점에 로드되며, 이후 시점부터 호출이 가능합니다.

```java
import io.gamepot.common.GamePot;

//key : 매개변수 string
String str_value = GamePot.getInstance().getConfig(key);

//대시보드에 추가한 모든 매개변수를 json string 형태로 가져옵니다.
String json_value = GamePot.getInstance().getConfigs();
```

### 게임 로그 전송

게임에서 사용되는 정보를 담아 호출하면 `대시보드` - `게임`에서 조회가 가능합니다.

아래는 사용할 수 있는 예약어 정의 표 입니다.

| 예약어                            | 필수 | 타입   | 설명         | 최대 길이 |
| :-------------------------------- | :--- | :----- | :----------- | --------- |
| GamePotSendLogCharacter.NAME      | 필수 | String | 케릭터명     | 128       |
| GamePotSendLogCharacter.LEVEL     | 선택 | String | 레벨         | 128       |
| GamePotSendLogCharacter.SERVER_ID | 선택 | String | 서버아이디   | 128       |
| GamePotSendLogCharacter.PLAYER_ID | 선택 | String | 케릭터아이디 | 128       |
| GamePotSendLogCharacter.USERDATA  | 선택 | String | ETC          | 128       |

```java
import android.text.TextUtils;

import io.gamepot.common.GamePotSendLogCharacter;
import io.gamepot.common.GamePotSendLog;

String name = "케릭터명";
String level = "10";
String serverid = "svn_001";
String playerid = "283282191001";
String userdata = "";

GamePotSendLogCharacter obj = new GamePotSendLogCharacter();
if(!TextUtils.isEmpty(name))
    obj.put(GamePotSendLogCharacter.NAME, name);
if(!TextUtils.isEmpty(level))
    obj.put(GamePotSendLogCharacter.LEVEL, level);
if(!TextUtils.isEmpty(serverid))
    obj.put(GamePotSendLogCharacter.SERVER_ID, serverid);
if(!TextUtils.isEmpty(playerid))
    obj.put(GamePotSendLogCharacter.PLAYER_ID, playerid);
if(!TextUtils.isEmpty(playerid))
    obj.put(GamePotSendLogCharacter.USERDATA, userdata);

// result : 로그 전송 성공 true, 그렇지 않으면 false
boolean result = GamePotSendLog.characterInfo(obj);
```

### GDPR 약관 체크리스트

대시보드에서 활성화 한, GDPR 약관 항목을 리스트형태로 가져옵니다.

```java
import io.gamepot.common.GamePot;

(List<String>) GamePot.getInstance().getGDPRCheckedList();

//리턴되는 각 파라메터는, 대시보드의 다음 설정에 해당합니다.
gdpr_privacy : 개인정보취급방침
gdpr_term : 이용약관
gdpr_gdpr : GDPR 이용약관
gdpr_push_normal : 이벤트 Push 수신동의
gdpr_push_night : 야간 이벤트 Push 수신동의 (한국만 해당)
gdpr_adapp_custom : 개인 맞춤광고 보기에 대한 동의 (GDPR 적용국가)
gdpr_adapp_nocustom : 개인 맞춤이 아닌 광보 보기에 대한 동의 (GDPR 적용국가)
```

### AppStatus 확인

현재 클라이언트의 AppStatus를 확인할 수 있습니다.

```java
import io.gamepot.common.GamePot;

GamePot.getInstance().checkAppStatus(new GamePotAppStatusResultListener() {
    @Override
    public void onSuccess(){
   
    }
    @Override
    public void onFailure(GamePotError error){

    }
    @Override
    public void onNeedUpdate(GamePotAppStatus status){

    }
    @Override
    public void onMainternance(GamePotAppStatus status){

    }
});
```

# 부록

### 3rd party SDK 연동 지원

TODO : 설명

## 로그인

TODO : 설명

> 자동 로그인을 지원하지 않음. 매번 호출 필요.

| 파라미터명 | 필수 | 타입                                                     | 설명               |
| :--------- | :--- | :------------------------------------------------------- | :----------------- |
| activity   | 필수 | String                                                   | 현재 Activity      |
| userid     | 필수 | String                                                   | 유저 유니크 아이디 |
| listener   | 필수 | GamePotChannelListener / GamePotAppStatusChannelListener | 요청 결과          |

```java
String memberId = "memberid of 3rd party sdk";

GamePotChannel.getInstance().loginByThirdPartySDK(getActivity(), memberId, new GamePotAppStatusChannelListener<GamePotUserInfo>() {
    @Override
    public void onNeedUpdate(GamePotAppStatus status) {
        // TODO: 강제 업데이트가 필요한 경우. 아래 API를 호출하면 SDK 자체에서 팝업을 띄울 수 있습니다.
        // TODO: Customizing을 하고자 하는 경우 아래 API를 호출하지 말고 Customizing을 하면 됩니다.
        GamePot.getInstance().showAppStatusPopup(MainActivity.this, status, new GamePotAppCloseListener() {
            @Override
            public void onClose() {
                // TODO: showAppStatusPopup API를 호출하신 경우 앱을 종료해야 하는 상황에 호출됩니다.
                // TODO: 종료 프로세스를 처리해주세요.
                MainActivity.this.finish();
            }

            @Override
            public void onNext(Object obj) {
                // TODO : Dashboard 업데이트 설정에서 권장 설정 시 "다음에 하기" 버튼이 노출 됩니다.
                // 해당 버튼을 사용자가 선택 시 호출 됩니다.
                // TODO : obj 정보를 이용하여 로그인 완료 시와 동일하게 처리해주세요.
                // GamePotUserInfo userInfo = (GamePotUserInfo)obj;
            }
        });
    }

    @Override
    public void onMainternance(GamePotAppStatus status) {
        // TODO: 점검 중인 경우. 아래 API를 호출하면 SDK 자체에서 팝업을 띄울 수 있습니다.
        // TODO: Customizing을 하고자 하는 경우 아래 API를 호출하지 말고 Customizing을 하면 됩니다.
        GamePot.getInstance().showAppStatusPopup(MainActivity.this, status, new GamePotAppCloseListener() {
            @Override
            public void onClose() {
                // TODO: showAppStatusPopup API를 호출하신 경우 앱을 종료해야 하는 상황에 호출됩니다.
                // TODO: 종료 프로세스를 처리해주세요.
                MainActivity.this.finish();
            }
        });
    }

    @Override
    public void onCancel() {
        // 사용자가 로그인을 취소한 상황.
    }

    @Override
    public void onSuccess(GamePotUserInfo userinfo) {
        // 로그인 완료. 게임 로직에 맞게 처리해주세요.
    }

    @Override
    public void onFailure(GamePotError error) {
        // 로그인 실패. error.getMessage()를 이용해서 오류 메시지를 보여주세요.
    }
});
```

## 결제

TODO : 설명

> 결제 아이템이 게임팟 대시보드에 등록되어있어야 합니다.

| 파라미터명    | 필수 | 타입            | 설명                                    |
| :------------ | :--- | :-------------- | :-------------------------------------- |
| productid     | 필수 | String          | 게임팟 대시보드에 등록된 아이템 아이디  |
| transactionid | 필수 | String          | 결제 영수증 번호(GPA-xxx-xxxx-xxxx)     |
| currency      | 선택 | String          | 통화(KRW, USD)                          |
| price         | 선택 | double          | 결제 아이템 금액                        |
| paymentid     | 선택 | String          | 결제 스토어(google, apple, one, galaxy) |
| uniqueid      | 선택 | String          | 개발사에서 사용하는 고유 아이디         |
| listener      | 선택 | GamePotListener | 요청 결과                               |

```java
String productId = "purchase_001";
String transactionId = "GPA-xxx-xxxx-xxxx";
String currency = "KRW";
double price = 1200;
String paymentId = "google";
String uniqueId = "developer unique id";

GamePot.getInstance().sendPurchaseByThirdPartySDK(productId, transactionId, currency, price, paymentId, uniqueId, null);
```