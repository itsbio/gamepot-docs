# 3rd-party SDK 적용 가이드

GAMEPOT SDK 이외에 적용하는 3rd-party SDK를 빌드애러 없이 게임 프로젝트에 적용하기 위한 가이드입니다.

> 각 SDK의 가이드를 기준으로 기술하며, API를 적용하는 방법은 각 SDK의 가이드를 참고하세요.

## Adjust

### Android ([Link](https://github.com/adjust/android_sdk/blob/master/doc/korean/README.md#qs-getting-started))

1. `build.gradle` 에 패키지 추가시 아래 두 패키지는 이미 포함되어있으니 무시하세요.

```java
implementation 'com.android.installreferrer:installreferrer:1.0'
implementation 'com.google.android.gms:play-services-analytics:16.0.4'
```

2. `AndroidManifest.xml` 에 이미 권한이 추가 되어있으니 무시하세요.

```java
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

### iOS([Link](https://github.com/adjust/ios_sdk/blob/master/README.md))

Gamepot과 충돌 사항이 없습니다.

### Unity

> 준비중입니다.

## Adbrix

### Android

> 준비중입니다.

### iOS

> 준비중입니다.

### Unity

## Singular ([Link](https://developers.singular.net/docs/android-sdk))

### Android (SDK 9.2.0)

1. `AndroidManifest.xml` 에 이미 권한이 추가 되어있으니 무시하세요.

```java
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

### iOS

### Unity ([Link](https://developers.singular.net/docs/unity-sdk))

1. 다음 경로의 라이브러리 파일을 삭제해 주세요.

`Assets/Plugins/Android/libs/installreferrer-1.0.aar`

## Appsflyer

### Android

> 준비중입니다.

### iOS

> 준비중입니다.

### Unity

> 준비중입니다.

