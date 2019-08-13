# 3rd-party SDK 적용 가이드

GAMEPOT SDK 이외에 적용하는 3rd-party SDK를 빌드애러 없이 게임 프로젝트에 적용하기 위한 가이드입니다.

> 각 SDK의 가이드를 기준으로 기술하며, API를 적용하는 방법은 각 SDK의 가이드를 참고하세요.

## Adjust

### Android ([Link](https://github.com/adjust/android_sdk/blob/master/doc/korean/README.md#qs-getting-started))

1. 将包添加到`build.gradle`时，已包含以下两个包。

```java
implementation 'com.android.installreferrer:installreferrer:1.0'
implementation 'com.google.android.gms:play-services-analytics:16.0.4'
```

2. 请忽略“AndroidManifest.xml”中已添加的权限。

```java
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

### iOS([Link](https://github.com/adjust/ios_sdk/blob/master/README.md))

```java
与Gamepot没有冲突。
```

### Unity

## Adbrix

### Android

### iOS

### Unity

## Singular

### Android

### iOS

### Unity

## Appsflyer

### Android

### iOS

### Unity
