---
search:
  keyword:
    - gamepot
---

#### **네이버 클라우드 플랫폼의 상품 사용 방법을 보다 상세하게 제공하고, 다양한 API의 활용을 돕기 위해 <a href="https://guide.ncloud-docs.com/docs/ko/home" target="_blank">[설명서]</a>와 <a href="https://api.ncloud-docs.com/docs/ko/home" target="_blank">[API 참조서]</a>를 구분하여 제공하고 있습니다.**

<a href="https://api.ncloud-docs.com/docs/ko/game-gamepot" target="_blank">Gamepot API 참조서 바로가기 >></a><br />
<a href="https://guide.ncloud-docs.com/docs/game-gamepotconsole" target="_blank">Gamepot 설명서 바로가기 >></a>

# iOS SDK

## 1. 시작하기

#### Step 1. 개발환경 구성

iOS용 애플리케이션 개발을 위해서는 개발 툴\(Xcode\)을 설치해야 합니다. iOS에서 GAMEPOT을 사용하기 위한 시스템 환경은 다음과 같습니다.

- 운영체제: iOS 10.0 이상
- 개발 환경: Xcode

#### Step 2. Framework 추가


![gamepot_ios_01.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_ios_01%284%29.png)

다운로드한 iOS SDK 파일을 Xcode 프로젝트 폴더 타겟에 마우스로 끌어다 놓아 추가합니다.

#### Step 3. Dependencies 추가

이용하고자 하는 서비스에 따라 필수 Dependencies 목록이 다릅니다.

서비스에 따라 다음 표를 참고하여 Dependencies를 추가합니다.

서비스별 Dependencies

| Service         | Framework                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Dependencies                                                                                                                                                                                                                      | bundle                                   |
| :-------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------- |
| 기본\(Base\)    | AFNetworking.framework FirebaseAnalytics.framework FirebaseCore.framework FirebaseCoreDiagnostics.framework FirebaseInstanceID.framework FirebaseMessaging.framework FirebaseNanoPB.framework GamePot.framework GoogleToolboxForMac.framework nanopb.framework Protobuf.framework                                                                                                                                                                                                                                                                                                                    | libz.tbd WebKit.framework UserNotifications.framework                                                                                                                                                                             | GamePot.bundle                           |
| 로그인\(Login\) | \[ Base \]<br> GamePotChannel.framework <br><br> \[ Google Sign In \]<br> GamePotGoogleSignIn.framework GoogleSignIn.framework GoogleSignInDependencies.framework <br><br>\[ Facebook \] <br>FBSDKCoreKit.framework FBSDKLoginKit.framework GamePotFacebook.framework<br><br> \[ LINE \]<br> GamePotLine.framework LineSDK.framework LineSDKObjC.framework<br><br> \[ NAVER \]<br> GamePotNaver.framework NaverThirdPartyLogin.framework<br><br> \[ Twitter \]<br> GamePotTwitter.framework<br> TwitterKit.framework \(Dynamic Library로 추가\)<br> TwitterCore.framework \(Dynamic Library로 추가\) | \[ Google Sign In \] AuthenticationServices.framework LocalAuthentication.framework<br><br> \[ Facebook \] SafariServices.framework<br><br> \[ LINE \]<br>SafariServices.framework<br><br> \[ Twitter \] SafariServices.framework | \[ Google Sign In \] GoogleSignIn.bundle |
| GameCenter      | GamePotGameCenter.framework                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |                                                                                                                                                                                                                                   |                                          |
| AppleID         | GamePotApple.framework                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |                                                                                                                                                                                                                                   |                                          |

![gamepot_ios_02.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_ios_02%284%29.png)


#### Step 4. Bundle Resource 추가

이용하고자 하는 서비스에 따라 Bundle Resource 파일을 추가해야 합니다.

서비스별 Dependencies 표를 참고하여 Bundle Resource 파일을 추가합니다.

![gamepot_ios_03.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_ios_03%285%29.png)


#### Step 5. InfoPlist 추가

![gamepot_ios_04.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_ios_04%284%29.png)

GAMEPOT SDK는 Google Firebase를 사용합니다. 따라서 Google Firebase를 설정하여 생성된 GoogleService-Info.plist를 프로젝트에 추가합니다.

GAMEPOT SDK의 기본설정 값을 포함하고 있는 GamePotConfig-Info.plist 파일도 추가합니다. GamePotConfig-Info.plist 파일이 없다면 동일한 파일명으로 생성 후 키에 해당하는 값을 입력합니다.

**GamePotConfig-Info.plist 설정**

![gamepot_ios_05.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_ios_05%284%29.png)

```markup
gamepot_project_id : GAMEPOT 프로젝트 아이디
gamepot_elsa_projectid : GAMEPOT 로그 프로젝트 아이디(optional)
```

#### Step 6. 빌드 옵션 추가

**Build Settings &gt; Linking &gt; Other Linker Flags** 섹션에 -ObjC -lz -lstdc++ -lc++ 옵션을 추가합니다.

![gamepot_ios_06.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_ios_06%284%29.png)


#### Step 7. Info.plist 수정

Targets &gt;&gt; Info &gt;&gt; Custom iOS Target Properties 내에 아래 사용자 권한 획득 옵션을 추가 부탁드립니다.

해당 사용자 권한은 GamePot 고객센터 내의 파일 업로드 기능에서 사용 됩니다.

```text
NSCameraUsageDescription
NSPhotoLibraryUsageDescription
```

iOS 14 이상 버전

iOS 14 버전부터 IDFA 값 획득 시 사용자에게 권한을 획득해야만

IDFA 값 획득이 가능하도록 변경되었습니다.

따라서 IDFA 값 획득 시 사용자에게 권한 획득하는 팝업을 사용하신다면
Targets &gt;&gt; Info &gt;&gt; Custom iOS Target Properties 내에 아래 사용자 권한 획득 옵션을 추가 부탁드립니다.

> 2020.09.11<br/>
> Apple에서 IDFA 값 획득 시 사용자에게 권한 획득하는 팝업 필수 적용은 2021년 초까지 연기되었습니다.<br/>
> 아래 링크 참고 부탁드립니다.<br/> > https://developer.apple.com/news/?id=hx9s63c5

```text
NSUserTrackingUsageDescription
```

#### Step 8. Google Sign In 로그인 환경 설정

서비스별 Dependencies 표의 **Login &gt; Google Sign In**을 참고하여 Framework 및 Dependencies를 추가합니다.

GoogleService-Info.plist 파일의 `REVERSED_CLIENT_ID` 값을 복사하여 **Info &gt; URL Types**에 항목을 추가하여 URL Schemes에 값을 입력합니다.

![gamepot_ios_07.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_ios_07%284%29.png)

**GamePotConfig-Info.plist 설정**

![gamepot_ios_08.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_ios_08%284%29.png)

```markup
gamepot_google_app_id : GoogleService-Info.plist 파일의 CLIENT_ID 값
gamepot_google_url_schemes : GoogleService-Info.plist 파일의 REVERSED_CLIENT_ID 값
```

#### Step 9. Facebook 로그인 환경 설정

페이스북 콘솔에서 앱 생성시 앱 유형 : 없음 또는 소비자 또는 인스턴스 게임 선택후 앱 생성

> 라이브 전환이 가능해야하며 앱 검수 > 권한 및 기능 > public_profile / email 권한이 있어야 합니다. 

서비스별 Dependencies 표의 **Login &gt; Facebook**을 참고하여 Framework 및 Dependencies를 추가합니다.

Facebook App ID를 **Info &gt; URL Types**에 fb+Facebook App ID 형태로 추가합니다.

![gamepot_ios_09.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_ios_09%284%29.png)

**Info &gt; iOS Target Property**의 **LSApplicationQueriesSchemes**에 아래 항목을 추가합니다.

- fbapi
- fb-messenger-share-api
- fbauth2
- fbshareextension

![gamepot_ios_10.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_ios_10%284%29.png)

**GamePotConfig-Info.plist 설정**

![gamepot_ios_11.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_ios_11%284%29.png)

```markup
gamepot_facebook_app_id : Facebook App ID
gamepot_facebook_display_name : Facebook display name
```

#### Step 10. LINE 로그인 환경 설정

**GamePotConfig-Info.plist 설정**

```markup
gamepot_line_channelid : Line Channel ID
gamepot_line_url_schemes : Line URL Scheme (line3rdp.{프로젝트 번들 ID})
```

#### Step 11. Twitter 로그인 환경 설정

**GamePotConfig-Info.plist 설정**

```markup
gamepot_twitter_consumerkey : Twitter Consumer Key
gamepot_twitter_consumersecret :  Twitter Consumer Secret
```

#### Step12. Naver 로그인 환경 설정

**GamePotConfig-Info.plist 설정**

```text
gamepot_naver_clientid : Naver Client Id
gamepot_naver_secretid : Naver Secret Id
gamepot_naver_urlscheme : Naver Url Scheme
```

**Info &gt; iOS Target Property**의 **LSApplicationQueriesSchemes**에 아래 항목을 추가합니다.

- naversearchapp
- naversearchthirdlogin
- navercafe

**Info &gt; URL Types**에 gamepot_naver_urlscheme에 입력한 값을 추가 합니다.

#### Step13. AppleID 로그인 환경 설정

**Xcode &gt; TARGETS &gt; Signing & Capabilities &gt; + Capability &gt; Sign In with Apple을 추가 합니다.**

## 2. 초기화

AppDelegate 파일에 아래 부분을 추가합니다.

```text
#import <GamePot/GamePot.h>

#if __has_include(<AppTrackingTransparency/AppTrackingTransparency.h>)
#import <AppTrackingTransparency/AppTrackingTransparency.h>
#endif


- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    ...
    // GamePot SDK Initialize
    [[GamePot getInstance] setup];

    // Push Permission
    if(SYSTEM_VERSION_GRATERTHAN_OR_EQUALTO(@"10.0"))
    {
        UNUserNotificationCenter *center = [UNUserNotificationCenter currentNotificationCenter];
        center.delegate = self;
        [center requestAuthorizationWithOptions:(UNAuthorizationOptionSound | UNAuthorizationOptionAlert | UNAuthorizationOptionBadge) completionHandler:^(BOOL granted, NSError * _Nullable error){
            if(!error){
                dispatch_async(dispatch_get_main_queue(), ^{
                    [[UIApplication sharedApplication] registerForRemoteNotifications];
                });
            }
        }];
    }
    else
    {
        // Code for old versions
        UIUserNotificationType allNotificationTypes = (UIUserNotificationTypeSound | UIUserNotificationTypeAlert | UIUserNotificationTypeBadge);
        UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:allNotificationTypes categories:nil];
        [application registerUserNotificationSettings:settings];
        [application registerForRemoteNotifications];
    }

// iOS 14 버전에서 IDFA 값을 가져오기 위한 권한 요청 팝업 호출
// 프로젝트에 AppTrackingTransparency.framework 추가 되어 있지 않으면, 호출 되지 않음.
#if __has_include(<AppTrackingTransparency/AppTrackingTransparency.h>)
   if (@available(iOS 14, *)) {
       if(NSClassFromString(@"ATTrackingManager"))
       {
           // 리스너 등록 되어 있지 않을 시 요청 팝업 발생 되지 않음.
           [ATTrackingManager requestTrackingAuthorizationWithCompletionHandler:^(ATTrackingManagerAuthorizationStatus status) {

               switch (status)
               {
                   case ATTrackingManagerAuthorizationStatusNotDetermined:
                       break;
                   case ATTrackingManagerAuthorizationStatusRestricted:
                       break;
                   case ATTrackingManagerAuthorizationStatusDenied:
                       break;
                   case ATTrackingManagerAuthorizationStatusAuthorized:
                       break;
                   default:
                       break;
               }
           }];
       }
   }
#endif
    ...
}

 // Push
- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
{
    ...
    [[GamePot getInstance] handleRemoteNotificationsWithDeviceToken:deviceToken];
    ...
}

- (void)applicationWillEnterForeground:(UIApplication *)application {
    [[GamePotChat getInstance] start];
}

- (void)applicationDidEnterBackground:(UIApplication *)application {
    [[GamePotChat getInstance] stop];
}
```

## 3. 로그인, 로그아웃, 회원 탈퇴

구글, 페이스북, 네이버 등 다양한 로그인 SDK를 통합하여 사용할 수 있습니다.

#### Step 1. 설정

```text
// AppDelegate.m
#import <GamePotChannel/GamePotChannel.h>

// Google Login 사용 시
#import <GamePotGoogleSignIn/GamePotGoogleSignIn.h>

// Facebook Login 사용 시
#import <GamePotFacebook/GamePotFacebook.h>

// AppleID Login 사용 시
#import <GamePotApple/GamePotApple.h>

// Line Login 사용 시
#import <GamePotLine/GamePotLine.h>

// Twitter Login 사용 시
#import <GamePotTwitter/GamePotTwitter.h>

// Naver Login 사용 시
#import <GamePotNaver/GamePotNaver.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    ...
    // GamePotSDK 채널 초기화. 사용하려는 채널별로 addChannel을 사용해야만 하며,
    // Guest 방식은 기본으로 포함됩니다.
    // Google Login 초기화
    GamePotChannelInterface* google     = [[GamePotGoogleSignIn alloc] init];
    [[GamePotChannelManager getInstance] addChannelWithType:GOOGLE interface:google];

    // Facebook 로그인 초기화
    GamePotChannelInterface* facebook   = [[GamePotFacebook alloc] init];
    [[GamePotChannelManager getInstance] addChannelWithType:FACEBOOK interface:facebook];

    // AppleID 로그인 초기화
    GamePotChannelInterface* apple      = [[GamePotApple alloc] init];
    [[GamePotChannel getInstance] addChannelWithType:APPLE interface:apple];

    // Line 로그인 초기화
    GamePotChannelInterface* line = [[GamePotLine alloc] init];
    [[GamePotChannel getInstance] addChannelWithType:LINE interface:line];

    // Twitter 로그인 초기화
    GamePotChannelInterface* twitter = [[GamePotTwitter alloc] init];
    [[GamePotChannel getInstance] addChannelWithType:TWITTER interface:twitter];

      // Naver 로그인 초기화
      GamePotChannelInterface* naver = [[GamePotNaver alloc] init];
      [[GamePotChannel getInstance] addChannelWithType:NAVER interface:naver];

    // 로그인 처리를 위해 필요합니다.
    [[GamePotChannel getInstance] application:application didFinishLaunchingWithOptions:launchOptions];

    ...
}

- (BOOL)application:(UIApplication *)app openURL:(NSURL *)url options:(NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options
{
    // 로그인 처리를 위해 필요합니다.
    BOOL nChannelResult = [[GamePotChannel getInstance] application:app openURL:url options:options];
    return nChannelResult;
}
```

#### Step 2. 로그인

**[로그인]** 버튼 클릭 시에 연동합니다.

```text
#import <GamePotChannel/GamePotChannel.h>
// 로그인 타입 정의
// GamePotChannelType.GOOGLE
// GamePotChannelType.FACEBOOK
// GamePotChannelType.GUEST
// GamePotChannelType.LINE
// GamePotChannelType.TWITTER
// GamePotChannelType.NAVER
// GamePotChannelType.APPLE

// 구글 로그인 버튼 클릭 시에 호출
[[GamePotChannel getInstance] Login:GOOGLE viewController:self success:^(GamePotUserInfo* userInfo) {
    // 로그인 완료
} cancel:^{
    // 로그인 시도 중 유저가 취소 하였을 때
} fail:^(NSError *error) {
    // 로그인 중 오류 발생
    // TODO: 게임 팝업으로 실패 원인에 대한 문구를 노출시켜 주세요.
    // TODO: 문구는 [error localizedDescription]를 사용해 주세요.
}];
```

#### Step 3. 자동 로그인

GAMEPOT은 자동 로그인을 지원합니다.

```text
#import <GamePotChannel/GamePotChannel.h>

// 마지막 로그인된 정보를 가져와서 해당 정보로 자동 로그인이 될 수 있도록 호출합니다.
// lastLoginType: 마지막 로그인 값을 가져올 수 있습니다.
GamePotChannelType type = [[GamePotChannel getInstance] lastLoginType];

if(type != NONE)
{
    // 마지막에 로그인했던 로그인 타입으로 로그인하는 방식입니다.
    // 자동 로그인 처리 시 아래와 같이 호출하면 됩니다.
    [[GamePotChannel getInstance] Login:type viewController:self success:^(GamePotUserInfo* userInfo) {

    } cancel:^{

    } fail:^(NSError *error) {
        // TODO: 게임 팝업으로 실패 원인에 대한 문구를 노출시켜 주세요.
        // TODO: 문구는 [error localizedDescription]를 사용해 주세요.
    }];
}
else
{
    // 마지막 로그인된 정보가 없음. 로그인 버튼이 있는 로그인 화면으로 이동
}
```

#### Step 4. 로그아웃

현재 회원 계정을 로그아웃시킵니다.

```text
#import <GamePotChannel/GamePotChannel.h>

[[GamePotChannel getInstance] LogoutWithSuccess:^{
    // 로그아웃 완료 후에는 초기화면으로 이동합니다.
} fail:^(NSError *error) {
    // 로그아웃 실패 오류 메시지를 보여줍니다.
    // TODO: 게임 팝업으로 실패 원인에 대한 문구를 노출시켜 주세요.
    // TODO: 문구는 [error localizedDescription]를 사용해 주세요.
}];
```

#### Step 5. 회원 탈퇴

현재 회원 계정을 탈퇴시킵니다.

```text
#import <GamePotChannel/GamePotChannel.h>

[[GamePotChannel getInstance] DeleteMemberWithSuccess:^{
    // 회원 탈퇴 성공 로그인 화면으로 이동
} fail:^(NSError *error) {
    // 회원 탈퇴 실패
    // TODO: 게임 팝업으로 실패 원인에 대한 문구를 노출시켜 주세요.
    // TODO: 문구는 [error localizedDescription]를 사용해 주세요.
}];
```

#### Step 6. 검증

로그인 완료 후 로그인 정보를 개발사 서버에서 GAMEPOT 서버로 전달하면 로그인 검증이 진행됩니다.

자세한 설명은 `Server to server api` 매뉴에 `Authentication check` 항목을 참고해주세요.

## 4. 계정 연동

하나의 게임 계정에 복수 개의 소셜 계정\(구글/페이스북 등\)을 연결/해제할 수 있는 기능입니다.\(최소 연동 소셜 계정은 1가지입니다.\)

게임 내에서 연동 화면 UI를 구현하고, 연동 버튼을 누를 때 아래 코드를 호출합니다.

#### Step 1. 계정 연동

Google, Facebook 등의 아이디로 계정을 연동할 수 있습니다.

```text
#import <GamePotChannel/GamePotChannel.h>

// 타입 정의
// GamePotChannelType.GOOGLE
// GamePotChannelType.FACEBOOK
// GamePotChannelType.LINE
// GamePotChannelType.TWITTER
// GamePotChannelType.NAVER
// GamePotChannelType.APPLE

[[GamePotChannel getInstance] CreateLinking:GOOGLE viewController:self success:^(GamePotUserInfo *userInfo) {
    // TODO: 연동 완료. 게임 팝업으로 연동 결과에 대한 문구를 노출시켜 주세요.(예: 계정 연동에 성공했습니다.)
} cancel:^{
    // TODO: 사용자가 취소한 경우
} fail:^(NSError *error) {
    // TODO: 연동 실패. 게임 팝업으로 연동 실패 원인에 대한 문구를 노출시켜 주세요.
    // TODO: 문구는 [error localizedDescription]를 사용해 주세요.
}];
```

#### Step 2. 연동된 리스트

해당 API를 통해 계정에 대해 연동 여부를 확인할 수 있습니다.

```text
#import <GamePotChannel/GamePotChannel.h>

// 타입 정의
// GamePotChannelType.GOOGLE
// GamePotChannelType.FACEBOOK
// GamePotChannelType.LINE
// GamePotChannelType.TWITTER
// GamePotChannelType.NAVER
// GamePotChannelType.APPLE

// 타입에 따른 연동 결과를 리턴합니다.
BOOL isGoogleLinked = [[GamePotChannel getInstance] isLinked:GOOGLE];

// 연동되어 있는 타입에 대해 JsonString 형태로 리턴합니다.
NSString* linkedList = [[GamePotChannel getInstance] getLinkedListJsonString];
```

#### Step 3. 연동 해제

기존에 연동되어 있는 계정을 해제합니다.

```text
#import <GamePotChannel/GamePotChannel.h>

[[GamePotChannel getInstance] DeleteLinking:GOOGLE success:^{
     // TODO: 해제 완료. 게임 팝업으로 연동 결과에 대한 문구를 노출시켜 주세요. (예: 계정 연동을 해제했습니다.)
} fail:^(NSError *error) {
     // TODO: 해제 실패. 게임 팝업으로 해지 실패 원인에 대한 문구를 노출시켜 주세요.
     // TODO: 문구는 [error localizedDescription]를 사용해 주세요.
}];
```

## 5. 결제

#### Step 1. 설정

결제의 결과 값은 Delegate 형태로 구현되어 있습니다. 따라서 아래와 같이 Delegate를 추가해 주세요.

```text
#import <GamePot/GamePot.h>

@interface ViewController () <GamePotPurchaseDelegate>
@end
@implementation ViewController

- (void)viewDidLoad
{
    ...
    [[GamePot getInstance] setPurchaseDelegate:self];
    ...
}

- (void)GamePotPurchaseSuccess:(GamePotPurchaseInfo *)_info
{
    // 결제 성공
}

- (void)GamePotPurchaseFail:(NSError *)_error
{
    // 결제 오류
    // TODO: 게임 팝업으로 실패 원인에 대한 문구를 노출시켜 주세요.
    // TODO: 문구는 [error localizedDescription]를 사용해 주세요.
}

- (void)GamePotPurchaseCancel
{
    // 결제 시동 중 취소
    // '결제가 취소되었습니다.'라는 문구를 게임 팝업으로 노출합니다.
}
@end
```

#### Step 2. 결제 시도

```text
CASE 1 : 일반적인 결제시

#import <GamePot/GamePot.h>

// productid : 스토어에 등록된 상품 ID를 입력합니다.
[[GamePot getInstance] purchase:productid];
```

```text
CASE 2 : 결제시 진행되는 영수증 번호를 별도로 관리하고자 할 때 :

#import <GamePot/GamePot.h>

// productId : 스토어에 등록된 상품ID를 입력해 주시면 됩니다.
// uniqueId  : 별도로 관리하는 영수증 번호를 넣으시면 됩니다.
[[GamePot getInstance] purchase:productid uniqueId:uniqueid];
```

```text
CASE 3 : 결제시 진행되는 영수증 번호 / 서버아이디 / 캐릭터아이디 / 기타 정보를 webhook으로 전달 하고자 할때 :

#import <GamePot/GamePot.h>

// productId : 스토어에 등록된 상품ID를 입력해 주시면 됩니다.
// uniqueId  : 별도로 관리하는 영수증 번호를 넣으시면 됩니다.
// serverId  : 결제를 진행한 캐릭터의 서버아이디를 입력해 주시면 됩니다.
// playerId  : 결제를 진행한 캐릭터의 캐릭터 아이디를 입력해 주시면 됩니다.
// etc       : 결제를 진행한 캐릭터 기타 정보를 넣으시면 됩니다.
[[GamePot getInstance] purchase:productid uniqueId:uniqueid serverId:serverid playerId:playerid etc:etc]];
```

#### Step 3. **결제 아이템 리스트 획득**

스토어에서 전달하는 인앱 아이템 리스트를 획득할 수 있습니다.

```text
NSArray<SKProduct*>* itemList = [[GamePot getInstance] getDetails];

// Device설정에 따른 통화 가격 얻어올때
[[GamePot getInstance] getLocalizePrice:[product productIdentifier]];
```

#### Step 4. 결제 아이템 지급

GAMEPOT은 Server to server api를 통해 결제 스토어에 영수증 검증까지 모두 마친 후 개발사 서버에 지급 요청을 하기 때문에 불법 결제가 불가능합니다.

이를 위해선 `Server to server api` 메뉴에 `Purchase` 항목을 참고하여 처리하셔야 합니다.

## 6. 기타 API

### SDK 지원 로그인 UI

SDK 내에서, 자체적으로 (완성된 형태의) Login UI를 제공합니다.

```c++
#import <GamePot/GamePot.h>
#import <GamePotChannel/GamePotChannel.h>

NSArray* order = @[@(GOOGLE), @(FACEBOOK), @(APPLE),@(NAVER), @(LINE), @(TWITTER), @(GUEST)];
GamePotChannelLoginOption* option = [[GamePotChannelLoginOption alloc] init:order];
[option setShowLogo:YES];

[[GamePotChannel getInstance] showLoginWithUI:self option:options success:^(GamePotUserInfo *userInfo) {
    // 로그인 완료. 게임 로직에 맞게 처리해주세요.
            
} update:^(GamePotAppStatus *appStatus) {
        // TODO: 강제 업데이트가 필요한 경우. 아래 API를 호출하면 SDK 자체에서 팝업을 띄울 수 있습니다.
        // TODO: Customizing을 하고자 하는 경우 아래 API를 호출하지 말고 Customizing을 하면 됩니다.
        [[GamePot getInstance] showAppStatusPopup:self setAppStatus:appStatus
         setCloseHandler:^{
            // TODO: showAppStatusPopup API를 호출하신 경우 앱을 종료해야 하는 상황에 호출됩니다.
            // TODO: 종료 프로세스를 처리해주세요.
        } setNextHandler:^(NSObject* resultPayload) {
            // TODO : Dashboard 업데이트 설정에서 권장 설정 시 "다음에 하기" 버튼이 노출 됩니다.
            // 해당 버튼을 사용자가 선택 시 호출 됩니다.
            // TODO : resultPayload 정보를 이용하여 로그인 완료 시와 동일하게 처리해주세요.
            // GamePotUserInfo* userInfo = (GamePotUserInfo*)resultPayload;

        }];
    } maintenance:^(GamePotAppStatus *appStatus) {
          // TODO: 점검 중인 경우. 아래 API를 호출하면 SDK 자체에서 팝업을 띄울 수 있습니다.
        // TODO: Customizing을 하고자 하는 경우 아래 API를 호출하지 말고 Customizing을 하면 됩니다.
        [[GamePot getInstance] showAppStatusPopup:self setAppStatus:appStatus
         setCloseHandler:^{
            // TODO: showAppStatusPopup API를 호출하신 경우 앱을 종료해야 하는 상황에 호출됩니다.
            // TODO: 종료 프로세스를 처리해주세요.
        }];
    } exit:^{
    // X 버튼 클릭시 처리
}];
```

#### 로그인 UI 이미지 로고 설정

로그인 UI 상단에 노출되는 이미지 로고는 SDK 내부에서 기본 이미지로 노출하며, 직접 추가할 수도 있습니다.

**이미지 로고 직접 넣기**

> 이미지 로고는 GamePot.bundle 내에, ic_stat_gamepot_logo.png 파일로 존재합니다.

이미지 파일명을 `ic_stat_gamepot_login_logo.png`로 변경한 다음 교체합니다.

(권장 사이즈 : 310x220)

### 쿠폰

사용자에게 입력받은 쿠폰을 사용할 때 아래 코드를 호출해 주세요.

> 쿠폰 입력 화면 UI는 개발사에서 구현해주세요.

```text
#import <GamePot/GamePot.h>

[[GamePot getInstance] coupon:/*사용자에게 입력받은 쿠폰*/ handler:^(BOOL _success, NSError *_error) {
    if(_success)
    {
        // TODO: message에 쿠폰 사용에 대한 결과가 리턴됩니다. 게임 팝업에 이 메시지를 노출해 주세요.
    }
    else
    {
        // TODO: _error에 쿠폰 사용 실패 원인에 대한 정보가 리턴됩니다.
        // [_error localizedDescription]의 내용을 게임 팝업으로 노출해 주세요.
    }
}];
```

#### 아이템 지급

쿠폰 사용이 성공하면 개발사 서버에 Server to server api를 통해 아이템 지급을 요청합니다.

이를 위해선 `Server to server api` 메뉴에 `Item` 항목을 참고하여 처리하셔야 합니다.

### Push

```text
#import <GamePot/GamePot.h>

// 푸시 수신 On/Off
[[GamePot getInstance] setPushEnable:YES success:^{

} fail:^(NSError *error) {

}];

// 야간푸시 수신 On/Off
[[GamePot getInstance] setNightPushEnable:YES success:^{

} fail:^(NSError *error) {

}];

// 푸시/야간푸시를 한번에 설정
// 로그인 전에 푸시/야간푸시 허용 여부를 받는 게임이라면 로그인 후에 아래 코드를 반드시 호출합니다.
[[GamePot getInstance] setPushStatus:YES night:YES ad:YES success:^{
    <#code#>
} fail:^(NSError *error) {
    <#code#>
}];
```

### Image Push
iOS 앱에서 알림 이미지를 수신하고 처리하려면 알림 서비스 확장 프로그램을 추가해야 합니다.

- Notification Service Extension 프로젝트에 추가하기
    1. Xcode -> File -> New -> Target.. 메뉴 클릭
    2. Target을 클릭하여 출력되는 화면에서 Notification Service Extension을 선택 후 Next를 클릭
    3. 이후 추가될 Target(Notification Service Extension)의 Project Name을 지정 후 Finish를 클릭 -> Notification Service Extension 모듈이 추가된것을 확인

- 알림 서비스 확장 프로그램 추가하기
    1. 생성된 Notification Service Extension 모듈의 NotificationService.h 파일을 아래와 같이 수정

        ```text
        // GamePot/GamePotNotificationServiceExtension.h를 Import
        // #import <UserNotifications/UserNotifications.h>
        #import <GamePot/GamePotNotificationServiceExtension.h>

        // UNNotificationServiceExtension 대신 GamePotNotificationServiceExtension를 상속
        // @interface NotificationService : UNNotificationServiceExtension
        @interface NotificationService : GamePotNotificationServiceExtension
        @end
        ```

    2. 생성된 Notification Service Extension 모듈의 NotificationService.m 파일을 아래와 같이 수정
        ```text
        ...
        - (void)didReceiveNotificationRequest:(UNNotificationRequest *)request withContentHandler:(void (^)(UNNotificationContent * _Nonnull))contentHandler {
            // self.contentHandler = contentHandler;
            // self.bestAttemptContent = [request.content mutableCopy];

            // Modify the notification content here...
            // self.bestAttemptContent.title = [NSString stringWithFormat:@"%@ [modified]", self.bestAttemptContent.title];

            // self.contentHandler(self.bestAttemptContent);
            [super didReceiveNotificationRequest:request withContentHandler:contentHandler];
        }
        ...
        ```
    3. 생성된 Notification Service Extension 모듈의 Targets >> Build Phases >> Link Binary With Libraries에 GamePot.framework 추가


### 공지사항

대시보드 - 공지사항에서 업로드한 이미지가 노출되는 기능입니다.

#### 호출

```text
[[GamePot getInstance] showNotice:/*viewController*/ setSchemeHandler:^(NSString *scheme) {
    NSLog(@"scheme = %@", scheme);
}];
```

### 공지사항(분류 별 호출)

대시보드 - 공지사항에서 업로드한 이미지 중, 분류로 설정한 이미지만 노출하는 기능입니다.

#### 호출

```text
[[GamePot getInstance] showEvent:/*viewController*/ setType:/*Type*/ setSchemeHandler:^(NSString *scheme) {
    NSLog(@"scheme = %@", scheme);
}];
```

### 고객센터

대시보드 - 고객센터와 연동되는 유저와 운영자간에 소통 채널입니다.

고객문의 UI는 디바이스 언어에 맞게 변경됩니다. 한국어, 영어, 일어, 중국어(간체, 번체)를 지원하며 그 외 언어는 영어로 보여집니다.

#### 호출

```text
[[GamePot getInstance] showHelpWebView:(UIViewController *)];
```

외부링크를 지원하여 로그인하지 않은 고객도 문의를 등록할 수 있습니다.

#### 호출

```text
// showWebView Type
    // WEBVIEW_NORMAL // 뒤로가기 버튼 없음.
    // WEBVIEW_NORMALWITHBACK // 뒤로가기 버튼 존재

    [[GamePot getInstance] showWebView:/*현재 ViewController*/ setType:/*Type*/ setURL:/*외부문의 접속 URL*/];
```

### 로컬 푸시\(Local Push notification\)

푸시 서버를 통하지 않고 단말기에서 자체적으로 푸시를 노출하는 기능입니다.

#### 호출

#### 푸시 등록

정해진 시간에 로컬 푸시를 노출하는 방법은 아래와 같습니다.

> 리턴 값으로 전달되는 pushid는 개발사에서 관리합니다.

```text
 NSDateFormatter* formatter = [[NSDateFormatter alloc] init];
 [formatter setDateFormat:@"yyyy-MM-dd HH:mm:ss"];

 NSString* strDate = [formatter stringFromDate:[[NSDate date] dateByAddingTimeInterval:30]];

 int pushId  = [[GamePot getInstance] sendLocalPush:@"Title" setMessage:@"Message" setDateString:strDate];
```

#### 등록한 푸시 취소

푸시 등록 시 얻은 pushid를 기반으로 기존에 등록된 푸시를 취소할 수 있습니다.

```text
[[GamePot getInstance] cancelLocalPush:(int)pushId];
```

### 점검, 강제 업데이트

점검이나 강제 업데이트 기능이 필요한 경우 대시보드 - 운영에서 기능을 활성화할 경우 동작합니다.

#### 호출

기존에 적용된 아래 API에서 사용이 가능합니다.

#### 1. Login API

```text
[[GamePotChannel getInstance] Login:GAMECENTER viewController:self
    success:^(GamePotUserInfo* userInfo) {
            // 로그인 완료. 게임 로직에 맞게 처리해주세요.
    } cancel:^{
            // 사용자가 로그인을 취소한 상황.
    } fail:^(NSError *error) {
            // 로그인 실패. [error localizedDescription]를 이용해서 오류 메시지를 보여주세요.
    } update:^(GamePotAppStatus *appStatus) {
        // TODO: 강제 업데이트가 필요한 경우. 아래 API를 호출하면 SDK 자체에서 팝업을 띄울 수 있습니다.
        // TODO: Customizing을 하고자 하는 경우 아래 API를 호출하지 말고 Customizing을 하면 됩니다.
        [[GamePot getInstance] showAppStatusPopup:self setAppStatus:appStatus
         setCloseHandler:^{
            // TODO: showAppStatusPopup API를 호출하신 경우 앱을 종료해야 하는 상황에 호출됩니다.
            // TODO: 종료 프로세스를 처리해주세요.
        } setNextHandler:^(NSObject* resultPayload) {
            // TODO : Dashboard 업데이트 설정에서 권장 설정 시 "다음에 하기" 버튼이 노출 됩니다.
            // 해당 버튼을 사용자가 선택 시 호출 됩니다.
            // TODO : resultPayload 정보를 이용하여 로그인 완료 시와 동일하게 처리해주세요.
            // GamePotUserInfo* userInfo = (GamePotUserInfo*)resultPayload;

        }];
    } maintenance:^(GamePotAppStatus *appStatus) {
          // TODO: 점검 중인 경우. 아래 API를 호출하면 SDK 자체에서 팝업을 띄울 수 있습니다.
        // TODO: Customizing을 하고자 하는 경우 아래 API를 호출하지 말고 Customizing을 하면 됩니다.
        [[GamePot getInstance] showAppStatusPopup:self setAppStatus:appStatus
         setCloseHandler:^{
            // TODO: showAppStatusPopup API를 호출하신 경우 앱을 종료해야 하는 상황에 호출됩니다.
            // TODO: 종료 프로세스를 처리해주세요.
        }];
    }];
```

### 약관 동의 (GDPR 포함)

'GDPR' 및 '이용약관', '개인정보 수집 및 이용안내' 동의를 쉽게 받을 수 있도록 UI를 제공합니다.

`BLUE` 테마와 `GREEN` 테마 두 가지의 `기본테마` 이외에도, 새롭게 추가된 11 종류의 `개선테마`를 제공합니다.

#### 약관 동의 호출 (자동)
`GAMEPOT SDK V3.3.0` 부터, **로그인 시 자동으로 약관 동의 팝업이 노출** 됩니다.

로그인 전, 플래그 값을 통해 이를 변경할 수 있습니다.
```
// Default Value는 YES
// 자동 팝업 시, MATERIAL_BLUE 테마로 적용
// false로 셋팅 시, 로그인 할 때 약관 동의 팝업이 노출되지 않습니다.
[[GamePot getInstance] setAutoAgree:YES];

// MATERIAL_ORANGE 테마로 커스텀 적용 시
GamePotAgreeOption* options = [[GamePotAgreeOption alloc] init:MATERIAL_ORANGE];
[[GamePot getInstance] setAgreeBuilder:options];

...

[[GamePotChannel getInstance] Login:GamePotChannelType viewController:self success:^(GamePotUserInfo* userInfo) {

} cancel:^{

} fail:^(NSError *error) {

} update:^(GamePotAppStatus *appStatus) {

} maintenance:^(GamePotAppStatus *appStatus) {

}];

...
```

#### 약관 동의 호출 (수동)

```text
// 블루테마 [[GamePotAgreeOption alloc] init:BLUE];
// 그린테마 [[GamePotAgreeOption alloc] init:GREEN];

// 개선테마
//  [[GamePotAgreeOption alloc] init:MATERIAL_RED];
//  [[GamePotAgreeOption alloc] init:MATERIAL_BLUE];
//  [[GamePotAgreeOption alloc] init:MATERIAL_CYAN];
//  [[GamePotAgreeOption alloc] init:MATERIAL_ORANGE];
//  [[GamePotAgreeOption alloc] init:MATERIAL_PURPLE];
//  [[GamePotAgreeOption alloc] init:MATERIAL_DARKBLUE];
//  [[GamePotAgreeOption alloc] init:MATERIAL_YELLOW];
//  [[GamePotAgreeOption alloc] init:MATERIAL_GRAPE];
//  [[GamePotAgreeOption alloc] init:MATERIAL_GRAY];
//  [[GamePotAgreeOption alloc] init:MATERIAL_GREEN];
//  [[GamePotAgreeOption alloc] init:MATERIAL_PEACH];
```
> 약관 동의 팝업 노출 여부는 개발사에서 게임에 맞게 처리해주세요.
>
> '보기'버튼을 클릭 시 보여지는 내용은 대시보드에서 적용 및 수정이 가능합니다.

Request:

```
GamePotAgreeOption* option = [[GamePotAgreeOption alloc] init:MATERIAL_BLUE];
[[GamePot getInstance] showAgreeView:self option:option handler:^(GamePotAgreeInfo *result) {
   // [result agree] : 필수 약관을 모두 동의한 경우 true
   // [result agreeNight] : 야간 광고성 수신 동의를 체크한 경우 true, 그렇지 않으면 false
   // agreeNight 값은 로그인 완료 후 [[GamePot getInstance] setNightPushEnable]; api를
   // 통해 전달하세요.
}];
```

#### Customizing

테마를 사용하지 않고 게임에 맞게 색을 변경합니다.

약관 동의를 호출하기 전에 `GamePotAgreeOption`에서 각 영역별로 색을 지정할 수 있습니다.

##### 약관 자동 호출 Customizing 설정
약관 자동 호출 시 팝업을 아래와 같이 Customizing 설정이 가능합니다.
```
GamePotAgreeOption* options = [[GamePotAgreeOption alloc] init:MATERIAL_BLUE];

[[GamePot getInstance] setAgreeBuilder:options];
```
##### Customizing 세부 설정
```text
 GamePotAgreeOption* option = [[GamePotAgreeOption alloc] init:MATERIAL_BLUE];

[option setHeaderBackGradient:@[@0xFF00050B,@0xFF0F1B21]];
[option setHeaderTitleColor:0xFF042941];
[option setContentBackGradient:@[@0xFF112432,@0xFF112432]];
[option setContentIconColor:0xFF042941];
[option setContentCheckColor:0xFF91adb5];
[option setContentTitleColor:0xFF98b3c6];
[option setContentShowColor:0xFF98b3c6];
[option setFooterBackGradient:@[@0xFF112432,@0xFF112432]];
[option setFooterButtonGradient:@[@0xFF1E3A57,@0xFF57B2E2]];
[option setFooterButtonOutlineColor:0xFF0b171a];
[option setFooterTitleColor:0xFFFFFFD5];

// 문구 변경
[option setAllMessage:@"모두 동의"];
[option setTermMessage:@"필수) 이용약관"];
[option setPrivacyMessage:@"필수) 개인정보 취급 방침"];
[option setPushMessage:@"선택) 일반 푸쉬 수신 동의"];
[option setNightPushMessage:@"선택) 야간 푸쉬 수신 동의"];
[option setFooterTitle:@"게임 시작하기"];

// 광고성 수신동의(일반/야간) 체크 후, 게임 시작 시 Toast 메시지(동의 시간) 노출 여부
[option setShowToastPushStatus:YES];

// 광고성 수신동의(일반/야간) 메세지 수정
[option setPushToastMsg:@"Push on"];
[option setNightPushToastMsg:@"Night Push on"];

// 미사용시 @""로 설정
[option setHeaderTitle:@"약관 동의"];

// 일반 광고성 수신동의 버튼 노출 여부
[option setShowPush:YES];

// 야간 광고성 수신동의 버튼 노출 여부
[option setShowNightPush:YES];

// 일반 광고성 수신동의 링크 설정 (미사용 시, 설정 안함)
[option setPushDetailURL:@"https://..."];

// 야간 광고성 수신동의 링크 설정 (미사용 시, 설정 안함)
[option setNightPushDetailURL:@"https://..."];

```

각각의 변수는 아래 영역에 적용됩니다.

> contentIconDrawable의 이미지는 IOS에는 노출 되지 않습니다.

- AgeView

![gamepot_ios_14.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_ios_14%287%29.png)

- EmailView

![gamepot_ios_14_1.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_ios_14_1.png)

- AgreeView

![gamepot_ios_14_2.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_ios_14_2.png)

### 이용약관

이용약관 UI를 호출합니다.

> 대시보드 - 고객지원 - 이용약관 설정 항목에 내용을 먼저 입력하세요.

```java
#import <GamePot/GamePot.h>

[[GamePot getInstance] showTerms:/*ViewController*/];
```

### 개인정보 취급방침

개인정보 취급방침 UI를 호출합니다.

> 대시보드 - 고객지원 - 개인정보취급방침 설정 항목에 내용을 먼저 입력하세요.

```java
#import <GamePot/GamePot.h>

[[GamePot getInstance] showPrivacy:/*ViewController*/];
```

### 환불규정

환불규정 UI를 호출합니다.

> 대시보드 - 고객지원 - 환불규정 설정 항목에 내용을 먼저 입력하세요.

```java
#import <GamePot/GamePot.h>

[[GamePot getInstance] showRefund:/*ViewController*/];
```

### 원격 구성

대시보드로 등록한 매개변수 값을 클라이언트 상에서 가져옵니다.

> 대시보드 - 설정 - 원격구성 화면에서 매개변수를 먼저 추가해주세요.

추가한 매개변수는 로그인 시점에 로드되며, 이후 시점부터 호출이 가능합니다.

```java
#import <GamePot/GamePot.h>

//key : 매개변수 string
NSString *str_value = [[GamePot getInstance] getConfig:(NSString*)key];

//대시보드에 추가한 모든 매개변수를 json 형태로 가져옵니다.
NSArray *json_value = [[GamePot getInstance] getConfigs];
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
#import <GamePot/GamePotSendLog.h>
#import <GamePot/GamePotSendLogCharacter.h>

GamePotSendLogCharacter* info = [[GamePotSendLogCharacter alloc] init];

[info put:@"name" forKey:GAMEPOT_NAME];
[info put:@"playerid" forKey:GAMEPOT_PLAYER_ID];
[info put:@"serverid" forKey:GAMEPOT_SERVER_ID];
[info put:@"level" forKey:GAMEPOT_LEVEL];
[info put:@"userdata" forKey:GAMEPOT_USERDATA];

BOOL result = [GamePotSendLog characterInfo:info];

// Result is TRUE : validation success. Logs will send to GamePot Server
// Result is FALSE : validation was failed. Please check logcat

```

### GDPR 약관 체크리스트

대시보드에서 활성화 한, GDPR 약관 항목을 리스트형태로 가져옵니다.

```c++
(NSArray*) [[GamePot getInstance] getGDPRCheckedList];

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

```c++
#import <GamePot/GamePot.h>

[[GamePot getInstance] checkAppStatus:^{
    
    //Login Success

} setFailHandler:^(NSError *error) {

    //Failed

} setUpdateHandler:^(GamePotAppStatus *status) {

    //NeedUpdate

} setMaintenanceHandler:^(GamePotAppStatus *status) {

    //OnMaintenance

}];
```

## 7. 다운로드

GAMEPOT 대시보드의 **SDK 다운로드** 메뉴에서 SDK를 다운로드할 수 있습니다.

# 부록

### 3rd party SDK 연동 지원

TODO : 설명

## 로그인

TODO : 설명

> 자동 로그인을 지원하지 않음. 매번 호출 
필요.

> userid 값에 :(colon) 이 들어가면 안됩니다.

| 파라미터명     | 필수 | 타입             | 설명                      |
| :------------- | :--- | :--------------- | :------------------------ |
| viewController | 필수 | UIViewController | 현재 ViewContoller        |
| userid         | 필수 | NSString         | 유저 유니크 아이디        |
| success        | 필수 | String           | 성공시 콜백               |
| fail           | 필수 | String           | 실패시 콜백               |
| update         | 선택 | String           | 업데이트 기능 동작시 콜백 |
| maintenance    | 선택 | String           | 점검 기능 동작시 콜백     |

```text
NSString userid = @"memberid of 3rd party sdk";

[[GamePotChannel getInstance] loginByThirdPartySDK:self uId:userid success:^(GamePotUserInfo* userInfo) {
    // 로그인 완료. 게임 로직에 맞게 처리해주세요.
} cancel:^{
    // 사용자가 로그인을 취소한 상황.
} fail:^(NSError *error) {
    // 로그인 실패. [error localizedDescription]를 이용해서 오류 메시지를 보여주세요.
} update:^(GamePotAppStatus *appStatus) {
    // TODO: 강제 업데이트가 필요한 경우. 아래 API를 호출하면 SDK 자체에서 팝업을 띄울 수 있습니다.
    // TODO: Customizing을 하고자 하는 경우 아래 API를 호출하지 말고 Customizing을 하면 됩니다.
    [[GamePot getInstance] showAppStatusPopup:self setAppStatus:appStatus
        setCloseHandler:^{
        // TODO: showAppStatusPopup API를 호출하신 경우 앱을 종료해야 하는 상황에 호출됩니다.
        // TODO: 종료 프로세스를 처리해주세요.
    } setNextHandler:^(NSObject* resultPayload) {
        // TODO : Dashboard 업데이트 설정에서 권장 설정 시 "다음에 하기" 버튼이 노출 됩니다.
        // 해당 버튼을 사용자가 선택 시 호출 됩니다.
        // TODO : resultPayload 정보를 이용하여 로그인 완료 시와 동일하게 처리해주세요.
        // GamePotUserInfo* userInfo = (GamePotUserInfo*)resultPayload;

    }];
} maintenance:^(GamePotAppStatus *appStatus) {
    // TODO: 점검 중인 경우. 아래 API를 호출하면 SDK 자체에서 팝업을 띄울 수 있습니다.
    // TODO: Customizing을 하고자 하는 경우 아래 API를 호출하지 말고 Customizing을 하면 됩니다.
    [[GamePot getInstance] showAppStatusPopup:self setAppStatus:appStatus
        setCloseHandler:^{
        // TODO: showAppStatusPopup API를 호출하신 경우 앱을 종료해야 하는 상황에 호출됩니다.
        // TODO: 종료 프로세스를 처리해주세요.
    }];
}];
```

## 결제

TODO : 설명

> 결제 아이템이 게임팟 대시보드에 등록되어있어야 합니다.

| 파라미터명    | 필수 | 타입                 | 설명                                   |
| :------------ | :--- | :------------------- | :------------------------------------- |
| productid     | 필수 | NSString             | 게임팟 대시보드에 등록된 아이템 아이디 |
| transactionid | 필수 | NSString             | 결제 영수증 번호(xxxxxxxxxxx)          |
| currency      | 선택 | NSString             | 통화(KRW, USD)                         |
| price         | 선택 | NSDecimalNumber      | 결제 아이템 금액                       |
| paymentid     | 선택 | NSString             | 결제 스토어(apple)                     |
| success       | 선택 | GamePotCommonSuccess | 성공시 콜백                            |
| fail          | 선택 | GamePotCommonFail    | 실패시 콜백                            |

```text
NSString* productId = @"purchase_001";
NSString* transactionId = @"xxxxxxxxxxx";
NSString* currency = @"USD";
NSDecimalNumber* price = [[NSDecimalNumber alloc] initWithString:@"1.09"];
NSString* paymentId = "apple";
NSString* uniqueId = "developer unique id";

[[GamePot getInstance] sendPurchaseByThirdPartySDK:productId transactionId:transactionId currency:currency price:price paymentId:paymentId uniqueId:uniqueId success:^{
    // success
} fail:^(NSError *error) {
    // fail
}];
```
