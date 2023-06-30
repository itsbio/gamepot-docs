---
search:
  keyword: ['gamepot']
---

#### **为提供 NAVER CLOUD PLATFORM 产品的详细使用方法和 API 的多种使用方式，分别提供<a href="https://guide.ncloud-docs.com/docs/zh/home" target="_blank">[说明书]</a>和<a href="https://api.ncloud-docs.com/docs/zh/home" target="_blank">[API 参考指南]</a>以供参考。**

<a href="https://api.ncloud-docs.com/docs/zh/game-gamepot" target="_blank">进入 Gamepot API 参考指南 >></a><br />
<a href="https://guide.ncloud-docs.com/docs/zh/game-gamepot-overview" target="_blank">进入 Gamepot 说明书 >></a><br />
<a href="https://guide.ncloud-docs.com/docs/zh/game-gamepotunreal" target="_blank">进入 Gamepot Unreal SDK 说明书 >></a>

下面将介绍在Unreal开发游戏时所需的GAMEPOT Unreal SDK使用方法。通过安装SDK并配置环境，可关联游戏和仪表盘。

为使用Unreal的GAMEPOT SDK，所需的配置要求如下。

- 最低配置：Unreal 4.26以上

## SDK安装及环境配置<a name="SDK설치및환경구성"></a>

安装GAMEPOT Unreal SDK后配置环境并关联GAMEPOT仪表盘和游戏，即可使用游戏开发所需的功能。

### 安装SDK<a name="SDK설치"></a>

安装GAMEPOT Unreal SDK后，在Unreal中配置项目的方法如下。

1. 请使用管理员账户登录仪表盘。
2. 依次点击**下载SDK > Unreal**菜单后点击**下载**。

### Android环境配置<a name="안드로이드환경설정"></a>

如要使用GAMEPOT Unreal SDK开发基于Android的游戏，需设置所需环境。

#### 设置最低配置<a name="최소사양설정"></a>

如要设置可安装及运行应用的最低配置，请使用下列代码。

```D
minSdkVersion：API 17以上（Jelly Bean 4.2）
```

#### 修改GamePot_Android_UPL.xml<a name="GamePotAndroidUPLxml수정"></a>

如果为设置Android环境修改GamePot_Android_UPL.xml文件，在Unreal打开下载的$S(PluginDir)/GamePot_Android_UPL.xml文件后参考表的内容修改代码的输入值。

- 不使用`(optional)`值时，请删除相应行。
  
  | 值   | 概述  |
  | --- | --- |
  | gamepot_project_id | 由GAMEPOT发放的项目ID |
  | gamepot_store | 商店值（`google`、`one`或`galaxy`） |
  | gamepot_app_title | 应用标题（FCM） |
  | gamepot_push_default_channel | 已添加的默认渠道名称，请勿修改。 |
  | facebook_app_id | 从Facebook控制台获取的应用ID |
  | fb_login_protocol_scheme | 从Facebook控制台获取的protocol scheme fb[app_id] |
  | gamepot_naver_clientid | 从NAVER开发人员控制台获取 |
  | gamepot_naver_secretid | 从NAVER开发人员控制台获取 |
  | gamepot_line_channelid | 从LINE开发人员控制台获取 |
  | gamepot_twitter_consumerkey | 从Twitter开发人员控制台获取 |
  | gamepot_twitter_consumersecret | 从Twitter开发人员控制台获取 |
  | gamepot_elsa_projectid | 使用NAVER Cloud ELSA时项目ID |
  | gamepot_region	| 주의! 게임팟 대시보드 생성 리전이 싱가포르인 경우에만 sg 입력 |
  | gamepot_license_url |주의! 게임팟 대시보드 생성 리전이 일본인경우 경우만 https://gamepot.apigw.ntruss.com/fw/jp-v1 입력  |
  
  ```C#
  <buildGradleAdditions>
      <insert>
  ...
  android {
      ...
      defaultConfig {
          ...
           resValue "string", "gamepot_project_id", ""                                      // required
           resValue "string", "gamepot_store", "google"                                   // required
           resValue "string", "gamepot_app_title","@string/app_name"           // required (fcm)
           resValue "string", "gamepot_push_default_channel","Default"        // required (fcm)
           resValue "string", "facebook_app_id", ""                                          // optional（Facebook）
           resValue "string", "fb_login_protocol_scheme", ""                          // optional（Facebook）
           resValue "string", "gamepot_naver_clientid", ""                              // optional（从NAVER开发人员控制台获取）
           resValue "string", "gamepot_naver_secretid", ""                             // optional（从NAVER开发人员控制台获取）
           resValue "string", "gamepot_line_channelid",""                              // optional（从LINE开发人员控制台获取）
           resValue "string", "gamepot_twitter_consumerkey", ""                  // optional（从Twitter开发人员控制台获取）
           resValue "string", "gamepot_twitter_consumersecret", ""              // optional（从Twitter开发人员控制台获取）
           resValue "string", "gamepot_elsa_projectid", ""                             // optional（NAVER Cloud ELSA项目ID）
      }
      ...
  }
    </insert>
  </buildGradleAdditions>
  ```
  

#### 设置推送通知图标<a name="푸시알림아이콘설정"></a>

可设置接收推送消息时要显示于通知栏的图标。如果不另行设置，则使用包含在SDK的默认图片，也可自行设置适合游戏的图标。

设置推送通知图标的方法如下。

1. 如下在项目路径下分别创建res/drawable文件夹后，根据各大小添加图片文件。
  
  | 文件夹名 | 长度  |
  | --- | --- |
  | $S(PluginDir)/ThirdParty/Android/GamePotResources/res/drawable-mdpi/ | 24x24 |
  | $S(PluginDir)/ThirdParty/Android/GamePotResources/res/drawable-hdpi/ | 36x36 |
  | $S(PluginDir)/ThirdParty/Android/GamePotResources/res/drawable-xhdpi/ | 48x48 |
  | $S(PluginDir)/ThirdParty/Android/GamePotResources/res/drawable-xxhdpi/ | 72x72 |
  | $S(PluginDir)/ThirdParty/Android/GamePotResources/res/drawable-xxxhdpi/ | 96x96 |
  
2. 将图片文件名变更为ic_stat_gamepot_small。
  

### iOS环境设置<a name="iOS환경설정"></a>

如要使用GAMEPOT Unreal SDK开发基于的iOS游戏，需设置所需环境。

빌드시 **버전 코드**는 정수형태로 유니크하게 증가하는 방식으로 진행 부탁드립니다.

#### 配置项目<a name="프로젝트구성"></a>

为设置iOS环境，按以下方法配置项目。

1. 将从Google Firebase控制台获取的GoogleService-Info.plist文件添加到Unreal项目中。
  
2. 请参考表的内容在项目的GamePotConfig-Info.plist文件变更以下设置。
  
  | 环境变量 | 概述  |
  | --- | --- |
  | gamepot_project_id | 由GAMEPOT发放的项目ID |
  | gamepot_facebook_app_id | 由Facebook获取的应用ID |
  | gamepot_facebook_display_name | 在Facebook上显示的名称 |
  | gamepot_google_app_id | GoogleService-Info文件的`CLIENT_ID`值 |
  | gamepot_google_url_schemes | GoogleService-Info文件的`REVERSED_CLIENT_ID`值 |
  | gamepot_naver_clientid | NAVER Client ID |
  | gamepot_naver_secretid | NAVER Secret ID |
  | gamepot_naver_urlscheme | NAVER URL Scheme |
  | gamepot_line_channelid | LINE Channel ID |
  | gamepot_line_url_schemes | LINE URL Scheme（line3rdp.{项目绑定ID}） |
  | gamepot_twitter_consumerkey | Twitter Consumer Key |
  | gamepot_twitter_consumersecret | Twitter Consumer Secret |
  | gamepot_elsa_projectid | 使用NAVER Cloud ELSA时项目ID |
  | gamepot_region	| 주의! 게임팟 대시보드 생성 리전이 싱가포르인 경우에만 sg 입력 |
  | gamepot_license_url |주의! 게임팟 대시보드 생성 리전이 일본인경우 경우만 https://gamepot.apigw.ntruss.com/fw/jp-v1 입력  |
  
3. 请在项目设置**iOS > Extra Plist Data > Additional Plist Data**中，按照如下内容添加用户权限获取选项。
  
  - 使用GAMEPOT客户咨询UI时所需的权限
  
  ```text
  <key>NSCameraUsageDescription</key>
  <string>$(PRODUCT_NAME) camera use.</string>
  <key>NSPhotoLibraryUsageDescription</key>
  <string>$(PRODUCT_NAME) photo library use.</string>
  <key>NSMicrophoneUsageDescription</key>
  <string>$(PRODUCT_NAME) Microphone use.</string>
  ```
  
  - 且为从用户获得IDFA值使用权限请求弹窗的情况
  
  ```text
  <key>NSUserTrackingUsageDescription</key>
  <string>$(PRODUCT_NAME) This identifier will collect IDFA for advertising purposes.</string>
  ```
  
4. 将GamePotResources.embeddedframework压缩为.zip后
  添加到$S(PluginDir)/ThirdParty/iOS/GamePotResources.embeddedframework.zip的路径并进行构建。
  

### 重置<a name="초기화"></a>

如要执行重置，在开始游戏时加载的第一个场景中使用的对象中添加以下代码。本指南以各示例文件为标准进行说明。

- 重置示例1 - ASampleGameModeBase.h
  
  ```C#
      #include "GamePotSDKPluginModule.h"
  
  //（相应级别使用的）对GAMEPOT API的Callback Event Listener声明
  UCLASS()
  class GAMEPOTSDKSAMPLE_API ASampleGameModeBase : public AGameModeBase
  {
      ...   
     void OnLoginSuccess(FNUserInfo NUserInfo);
     void OnLoginCancel();
     void OnLoginFailure(FNError NError);
     void OnLoginMaintenance(FNAppStatus NAppStatus);
     void OnLoginNeedUpdate(FNAppStatus NAppStatus);
     void OnLoginExit();
     ...
  };
  ```
  
  <br>
  
- 重置示例2 - ASampleGameModeBase.cpp
  
  ```C#
  #include "ASampleGameModeBase.h"
  
  void ASampleGameModeBase::InitGame(const FString& MapName, const FString& Options, FString& ErrorMessage)
  {
      AGameModeBase::InitGame(MapName, Options, ErrorMessage);
  
       //（在报头声明的Event Listener）绑定至GamePotPluginModule的Callback Event Listener
       if (FGamePotSDKPluginModule::IsAvailable())
       {
           FGamePotSDKPluginModule::OnSdkLoginSuccess.AddUObject(this, &ASampleGameModeBase::OnLoginSuccess);
           FGamePotSDKPluginModule::OnSdkLoginCancel.AddUObject(this, &ASampleGameModeBase::OnLoginCancel);
           FGamePotSDKPluginModule::OnSdkLoginFailure.AddUObject(this, &ASampleGameModeBase::OnLoginFailure);
           FGamePotSDKPluginModule::OnSdkLoginMaintenance.AddUObject(this, &ASampleGameModeBase::OnLoginMaintenance);
           FGamePotSDKPluginModule::OnSdkLoginNeedUpdate.AddUObject(this, &ASampleGameModeBase::OnLoginNeedUpdate);
           FGamePotSDKPluginModule::OnSdkLoginExit.AddUObject(this, &ASampleGameModeBase::OnLoginExit);
  
           FGamePotSDKPluginModule::OnSdkLogoutSuccess.AddUObject(this, &ASampleGameModeBase::OnLogoutSuccess);
           FGamePotSDKPluginModule::OnSdkLogoutFailure.AddUObject(this, &ASampleGameModeBase::OnLogoutFailure);   
          ...
       }
  }
  
  void ASampleGameModeBase::OnLoginSuccess(FNUserInfo NUserInfo)
  {
      // Handling NUserInfo..
  }
  
  void ASampleGameModeBase::OnLoginCancel()
  {
  }
  
  void ASampleGameModeBase::OnLoginFailure(FNError NError)
  {
      // Handling NError Info..
  }
  ```
  
  <br>
  
- （绑定）Event Listener列表
  
  ```C#
    // 登录成功
      FOnSdkLoginSuccess OnSdkLoginSuccess(FNUserInfo NUserInfo);     
      // 取消登录
      FOnSdkLoginCancel OnSdkLoginCancel(); 
      // 登录失败
      FOnSdkLoginFailure OnSdkLoginFailure(FNError NError);   
      // 登录（维护）
      FOnSdkLoginMaintenance OnSdkLoginMaintenance(FNAppStatus NAppStatus);
      // 登录（更新）
      FOnSdkLoginNeedUpdate OnSdkLoginNeedUpdate(FNAppStatus NAppStatus);   
      // 关闭登录UI（使用showLoginWithUI时）
      FOnSdkLoginExit OnSdkLoginExit();         
      // （维护、更新时）应用结束
      FOnSdkAppClose OnSdkAppClose();   
  
      // 退出登录成功
      FOnSdkLogoutSuccess OnSdkLogoutSuccess();   
      // 退出登录失败
      FOnSdkLogoutFailure OnSdkLogoutFailure(FNError NError);      
  
      // showWebview关闭
      FOnWebviewClose OnSdkWebviewClose(FString msg);
  
      // 购买成功
      FOnSdkPurchaseSuccess OnSdkPurchaseSuccess(FNPurchaseInfo NPurchaseInfo);
      // 取消购买
      FOnSdkPurchaseCancel OnSdkPurchaseCancel();
      // 购买失败
      FOnSdkPurchaseFailure OnSdkPurchaseFailure(FNError NError);  
  
      // getPurchaseDetailListAsync成功
      FOnSdkPurchaseDetailListSuccess OnSdkPurchaseDetailListSuccess(TArray<FNPurchaseItem> Items);
      // getPurchaseDetailListAsync失败
      FOnSdkPurchaseDetailListFailure OnSdkPurchaseDetailListFailure(FNError NError);
  
      // createLinking成功
      FOnSdkCreateLinkingSuccess OnSdkCreateLinkingSuccess(FNUserInfo NUserInfo);
      // 取消createLinking
      FOnSdkCreateLinkingCancel OnSdkCreateLinkingCancel();
      // createLinking失败
      FOnSdkCreateLinkingFailure OnSdkCreateLinkingFailure(FNError NError);
  
      // deleteLinking成功
      FOnSdkDeleteLinkingSuccess OnSdkDeleteLinkingSuccess();
      // deleteLinking失败
      FOnSdkDeleteLinkingFailure OnSdkDeleteLinkingFailure(FNError NError);
  
      // 公告事项图片（showNotice、showEvent）点击操作后回调scheme
      FOnSdkReceiveScheme OnSdkReceiveScheme(FString scheme);
  
      // deleteMember成功
      FOnSdkDeleteMemberSuccess OnSdkDeleteMemberSuccess();
      // deleteMember失败
      FOnSdkDeleteMemberFailure OnSdkDeleteMemberFailure(FNError NError);
  
      // 优惠券（使用）成功
      FOnSdkCouponSuccess OnSdkCouponSuccess(FString msg);
      // 优惠券（使用）失败
      FOnSdkCouponFailure OnSdkCouponFailure(FNError NError);
  
      // showAgreeDialog（是否同意条款）更新成功
      FOnAgreeDialogSuccess OnSdkAgreeDialogSuccess(FNAgreeResultInfo NAgreeResultInfo);
      // showAgreeDialog（是否同意条款）更新失败
      FOnAgreeDialogFailure OnSdkAgreeDialogFailure(FNError NError);
  
      // setPush成功
      FOnPushSuccess OnSdkPushSuccess();
      // setPushAdStatus成功
      FOnPushAdSuccess OnSdkPushAdSuccess();
      // setPushNightStatus成功
      FOnPushNightSuccess OnSdkPushNightSuccess();
      // setPushStatus成功
      FOnPushStatusSuccess OnSdkPushStatusSuccess();
  
      // setPush失败
      FOnPushFailure OnSdkPushFailure(FNError NError);
      // setPushAdStatus失败
      FOnPushAdFailure OnSdkPushAdFailure(FNError NError);
      // setPushNightStatus失败
      FOnPushNightFailure OnSdkPushNightFailure(FNError NError);
      // setPushStatus失败
      FOnPushStatusFailure OnSdkPushStatusFailure(FNError NError);
  ```
  

### 设置错误代码<a name="오류코드설정"></a>

如要设置错误代码，请使用下列代码。

```C#
USTRUCT()
struct FNError
{
    //Detail Error code
    static const int CODE_UNKNOWN_ERROR = 0;                   // 未知错误
    static const int CODE_NOT_INITALIZE = 1;                   // 初始化失败
    static const int CODE_INVAILD_PARAM = 2;                   // 参数不正确时
    static const int CODE_MEMBERID_IS_EMPTY = 3;                   // 没有组成人员ID数据的情况
    static const int CODE_NOT_SIGNIN = 4;                   // 未登录的状态
    static const int CODE_NETWORK_MODULE_NOT_INIT = 3000;                // 网络模块未重置的情况
    static const int CODE_NETWORK_ERROR = 3001;                // 发生网络连接错误及超时时
    static const int CODE_SERVER_ERROR = 4000;                // 在server-side发生的错误
    static const int CODE_SERVER_HTTP_ERROR = 4001;                // http response code不成功时
    static const int CODE_SERVER_NETWORK_ERROR = 4002;                // 发生网络连接错误及超时时
    static const int CODE_SERVER_PARSING_ERROR = 4003;                // 解析从服务器接收的数据时发生错误
    static const int CODE_CHARGE_UNKNOWN_ERROR = 5000;                // 支付时发生未知错误并由商店传递错误的情况
    static const int CODE_CHARGE_PRODUCTID_EMPTY = 5001;                // 未输入product id的情况
    static const int CODE_CHARGE_PRODUCTID_WRONG = 5002;                // product id输入错误时
    static const int CODE_CHARGE_CONSUME_ERROR = 5003;                // consume出错

    UPROPERTY()
    int code;               // error Code

    UPROPERTY()
    FString message;        // error Message
}
```

## 登录相关功能<a name="로그인관련기능"></a>

集成Google、Facebook、NAVER等各种登录SDK功能，可在GAMEPOT Unreal SDK中使用。

### 使用前设置<a name="사용전설정"></a>

如要使用登录相关SDK功能，需完成控制台设置并声明登录相关代码。

#### 设置Google登录环境<a name="구글로그인환경설정"></a>

为使用登录功能，按以下方法设置Google Firebase控制台。

1. 将从Google Firebase控制台获取的Android专用google-service.json文件复制到$S(PluginDir)/ThirdParty/Android/路径下。
2. 将配置APK时使用的Keystore文件的SHA-1值添加到Firebase控制台。

<br>

- 尝试Google登录时，如果onCancel响应并无法登录，请按以下方法解决。
  
  - 确认是否正常应用google-service.json文件
  - 确认配置APK时使用的Keystore和为注册到Firebase控制台导出SHA-1值的Keystore是否相同
  - 确认构建时是否使用了注册到Firebase控制台的包名称

3. AdditionalPlistData中添加Google相关CFBundleURLSchemes值

```java
<key>CFBundleURLTypes</key>
<array>
<dict>
<key>CFBundleTypeRole</key>
<string>Editor</string>
<key>CFBundleURLSchemes</key>
<array>
<string>GoogleService-Info.plist文件中REVERSED_CLIENT_ID值，例如）com.googleusercontent.apps.XXXXXXXXX</string>
</array>
...
</dict>
```

#### 设置Facebook登录环境<a name="페이스북로그인환경설정"></a>

为使用登录功能，按以下方法设置Facebook控制台。

1. 在Facebook for Developers控制台将应用类型选择为**None**、**Consumer**或**Gaming**后创建应用。
  
2. 将配置APK时使用的Keystore的密钥哈希值添加到Facebook for Developers控制台。
  
3. 将从Facebook for Developers控制台获取的应用ID输入到下列代码后，添加到Android专用GamePot_Android_UPL.xml文件。
  
  ```java
  ...
  <resourceCopies>
          <copyFile src="$S(PluginDir)/ThirdParty/Android/libs/gamepot-channel-facebook.aar" dst="$S(BuildDir)/libs/gamepot-channel-facebook.aar" />
  </resourceCopies>
  ...
  
  ...
  <buildGradleAdditions>
      <insert>
  
          ...
          dependencies {
              ...
              implementation(name: 'gamepot-channel-facebook', ext: 'aar')
              ...
          }
  
          ...
  
          defaultConfig {
              resValue "string", "facebook_app_id", "1234567890"
              resValue "string", "fb_login_protocol_scheme", "fb1234567890"
          }
          ...
  
      </insert>
  </buildGradleAdditions>
  
  ...
  
  <gameActivityImportAdditions>
    <insert>
      import io.gamepot.channel.facebook.GamePotFacebook;
    </insert>
  </gameActivityImportAdditions>
  ```
  
4. 将在GamepotConfig-info.plist 文件添加下列代码。
  
  ```text
  gamepot_facebook_app_id// 从Facebook开发者控制台获取的应用ID
  ```
  
  用SourceCode查看时，如下进行添加
  
  ```markup
  ...
   <key>gamepot_facebook_app_id</key>
   <string>xxxxxx</string>
   ...
  ```
  
5. AdditionalPlistData中添加Facebook相关CFBundleURLSchemes及LSApplicationQueriesSchemes值
  

```java
<key>CFBundleURLTypes</key>
<array>
<dict>
<key>CFBundleTypeRole</key>
<string>Editor</string>
<key>CFBundleURLSchemes</key>
<array>
<string>fb[Facebook应用ID]，例如）fb100001</string>
</array>
...
</dict>
…..
<key>LSApplicationQueriesSchemes</key>
<array>
<string>fbapi</string>
<string>fb-messenger-api</string>
<string>fb-messenger-share-api</string>
<string>fbauth2</string>
<string>fbshareextension</string>
……
</array>
```

#### 设置Apple登录环境<a name="애플로그인환경설정"></a>

如要设置iOS专用Apple登录环境，请在项目的Config路径DefaultEngine.ini文件内的`/Script/IOSRuntimeSettings.IOSRuntimeSettings`项目中添加`bEnableSignInWithAppleSupport=True` flag值。

### 登录功能<a name="로그인기능"></a>

如要使用根据开发商实现的登录UI点击登录按钮时操作的SDK登录功能，请使用下列代码。将创建用于确认用户信息的`MemberId`，创建的信息保存到`FNUserInfo`后返回。

```C
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
FGamePotSDKPluginModule::GetSharedGamePotSdk()->Login(ENLoginType::Type loginType);

void ASampleGameModeBase::OnLoginSuccess(FNUserInfo NUserInfo)
{
    // 登录成功
}

void ASampleGameModeBase::OnLoginCancel()
{
    // 取消登录
}

void ASampleGameModeBase::OnLoginFailure(FNError NError)
{
   // 登录失败
    // 请使用NError.message显示错误消息。
}

// 维护（仪表盘的维护功能处于激活状态时调用）
void ASampleGameModeBase::OnLoginMaintenance(FNAppStatus NAppStatus)
{
   // 须基于参数传递的status信息创建并显示弹窗。请从下列两种方式中选择一种配置弹窗。
    // 方式1：使用开发商自行实现UI的游戏内弹窗
    // 方式2：调用下列代码后使用SDK自主弹窗
    IGamePotSdk* ptr = FGamePotSDKPluginModule::GetSharedGamePotSdk();
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
        ptr->showAppStatusPopup(NAppStatus.ToJsonString());
}

// 强制更新（商店版本和客户端版本不一致时调用）
void ASampleGameModeBase::OnLoginNeedUpdate(FNAppStatus NAppStatus)
{
     // 须基于参数传递的status信息创建并显示弹窗。请从下列两种方式中选择一种配置弹窗。
    // 方式1：使用开发商自行实现UI的游戏内弹窗
    // 方式2：调用下列代码后使用SDK自主弹窗
    IGamePotSdk* ptr = FGamePotSDKPluginModule::GetSharedGamePotSdk();
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
        ptr->showAppStatusPopup(NAppStatus.ToJsonString());
}

void ASampleGameModeBase::OnLoginExit()
{
   // 如果使用方式2实现强制更新或维护功能时，因有可能强制结束应用，请在此处可执行结束应用。
}

void ASampleGameModeBase::OnAppClose()
{
    // 结束应用
    // 如果使用方式2实现强制更新或维护功能时，因有可能强制结束应用，请在此处可执行结束应用。
}
```

#### 定义LoginType、NUserInfo、NAppStatus<a name="LoginTypeNUserInfoNAppStatus정의"></a>

如要设置登录功能的各个参数，请使用下列代码。

- **`LoginType`**
  
  ```C
  UENUM()
  namespace ENLoginType
  {
      enum Type
      {
          NONE,
          GOOGLE,
          GOOGLEPLAY,
          FACEBOOK,
          NAVER,
          GAMECENTER,
          TWITTER,
          LINE,
          APPLE,
          GUEST,
          THIRDPARTYSDK,
          STANDALONE
      };
  }
  ```
  
- **`NUserInfo`**
  
  ```C
  USTRUCT()
  struct FNUserInfo
  {
      UPROPERTY()
      FString memberid;          // 组成人员ID（用户唯一ID）
      UPROPERTY()
      FString name;              // 姓名
      UPROPERTY()
      FString profileUrl;        // 头像URL（存在时）
      UPROPERTY()
      FString email;             // 邮件（如果有）
      UPROPERTY()
      FString token;             // 玩家有效性检查用Token（在Token Authentication API中使用）
      UPROPERTY()
      FString userid;            // 社交媒体ID
  }
  ```
  
- **`NAppStatus`**
  
  ```C
  USTRUCT()
  struct FNAppStatus
  {
      UPROPERTY()
      FString type;      // 是AppStatus类型，"maintenance"为维护，"needupdate"为更新
  
      UPROPERTY()
      FString message;   // 维护设置：在仪表盘输入的消息
  
      UPROPERTY()
      FString url;       // 维护设置：在仪表盘输入的URL
  
      UPROPERTY()
      FString currentAppVersion; // 更新：当前的应用版本
  
      UPROPERTY()
      FString updateAppVersion;  // 更新：在仪表盘输入的应用版本
  
      UPROPERTY()
      int currentAppVersionCode; // 更新：当前的应用代码
  
      UPROPERTY()
      FString updateAppVersionCode;  // 更新：在仪表盘输入的应用版本代码
  
      UPROPERTY()
      bool isForce;      // 更新：在仪表盘设置强制更新时为true
  
      UPROPERTY()
      FString resultPayload; // 由客户端SDK传递的JSON值，可忽略。
  
      UPROPERTY()
      double startedAt;   // 维护：开始时间（时间戳）
  
      UPROPERTY()
      double endedAt;    // 维护：结束时间（时间戳）
  }
  ```
  

#### 设置为获取IDFA值的权限请求弹窗<a name="IDFA값획득을위한권한요청팝업설정"></a>

如要在iOS平台使用为获取用户IDFA值的权限请求弹窗时，请使用下列代码。

```C
   if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
        FGamePotSDKPluginModule::GetSharedGamePotSdk()->requestTrackingAuthorization();

    void ASampleGameModeBase::OnSdkResultTrackingAuthorization(FNResultTrackingAuthorization info) {
        // info.authorization (FString)
        //        ATTrackingManagerAuthorizationStatusNotDetermined,
        //        ATTrackingManagerAuthorizationStatusRestricted,
        //        ATTrackingManagerAuthorizationStatusDenied,
        //        ATTrackingManagerAuthorizationStatusAuthorized,
        //        ATTrackingManagerAuthorizationStatusUnknown
    }

    // 可随机显示IDFA值获取权限请求弹窗。获取权限后，即使调用方法也不会弹出弹窗。
```

<br>

- **变更弹窗请求时间**

iOS平台获取IDFA值的权限请求弹窗，将在调用登录API时请求。如果不希望在登录时调用此弹窗，在$S(PluginDir)/Private/iOS/IOSGamePotSdk.cpp文件如下修改函数。

```C
void FIOSGamePotSdk::Login(ENLoginType::Type _loginType)
{
    //在登录前阶段明确显示IDFA权限请求弹窗<-- 必要时，做注释处理
    FIOSGamePotSdk::requestTrackingAuthorization();
    ...
```

### 使用第三方账户登录功能<a name="계정별로그인기능사용"></a>

如要使用第三方账户登录功能，请使用下列代码应用设置。

#### NAVER登录<a name="네이버로그인"></a>

如要使用NAVER登录功能，需在NAVER Developers控制台将使用API选择为`NAVER ID登录`后注册应用并使用下列代码。

- **Android**
  
  - 修改GamePot_Android_UPL.xml
  
  ```xml
  ...
  <resourceCopies>
          <copyFile src="$S(PluginDir)/ThirdParty/Android/libs/gamepot-channel-naver.aar" dst="$S(BuildDir)/libs/gamepot-channel-naver.aar" />
  </resourceCopies>
  
  ...
  
  <buildGradleAdditions>
      <insert>
  
          ...
          dependencies {
              ...
              implementation(name: 'gamepot-channel-naver', ext: 'aar')
              ...
          }
  
          ...
  
          defaultConfig {
              resValue "string", "gamepot_naver_clientid", "abcdefg1234567890"
              resValue "string", "gamepot_naver_secretid", "hijklmn"
          }
          ...
  
      </insert>
  </buildGradleAdditions>
  
  ...
  
  <gameActivityImportAdditions>
    <insert>
      import io.gamepot.channel.naver.GamePotNaver;
    </insert>
  </gameActivityImportAdditions>
  
  ...
  ```
  
  - 将从NAVER开发者控制台获取的Client ID输入到`gamepot_naver_clientid`值中，将Client Secret输入到`gamepot_naver_secretid`值中
  - 在$S(PluginDir)ThirdParty/Android/libs项目路径下添加gamepot-channel-naver.aar文件

<br>

- **iOS**
  
  - 修改GamePotSDKPlugin.Build.cs文件
  
  ```C#
  ...
  
  public GamePotSDKPlugin(ReadOnlyTargetRules Target) : base(Target)
  {
      ...
             else if (Target.Platform == UnrealTargetPlatform.IOS)
          {
                  PublicAdditionalFrameworks.Add(
                  new Framework(
                      "GamePotNaver",
                      ModuleDirectory+"/ThirdParty/iOS/GamePotNaver.framework"
                  )
              );
  
                  PublicAdditionalFrameworks.Add(
                  new Framework(
                      "NaverThirdPartyLogin",
                      ModuleDirectory+"/ThirdParty/iOS/NaverThirdPartyLogin.framework"
                  )
          }
      ...
  }
  ...
  ```
  
  - 修改GamePotConfig-info.plist文件
  
  ```text
   gamepot_naver_clientid// 拟在NAVER使用的Client ID
   gamepot_naver_secretid// 拟在NAVER使用的Secret ID
   gamepot_naver_urlscheme// 拟在NAVER使用的URL Scheme
  ```
  
  用SourceCode查看时，如下进行添加
  
  ```markup
  ...
  <key>gamepot_naver_clientid</key>
  <string>xxxxxx</string>
  <key>gamepot_naver_secretid</key>
  <string>xxxxxx</string>
  <key>gamepot_naver_urlscheme</key>
  <string>xxxxxx</string>
  ...
  ```
  

AdditionalPlistData中添加NAVER相关CFBundleURLSchemes及LSApplicationQueriesSchemes值

```java
<key>CFBundleURLTypes</key>
<array>
<dict>
<key>CFBundleTypeRole</key>
<string>Editor</string>
<key>CFBundleURLSchemes</key>
<array>
<string>NAVER控制台中设置的IOS Schemes值</string>
</array>
...
</dict>
…..
<key>LSApplicationQueriesSchemes</key>
<array>
<string>naversearchapp</string>
<string>naversearchthirdlogin</string>
<string>navercafe</string>
……
</array>
```

#### LINE登录<a name="라인로그인"></a>

如要使用LINE登录功能，需将配置APK时使用的包名称、Keystore的SHA-1值、URL Scheme值添加到LINE Developers控制台后使用下列代码。

- **Android**
  
  - 修改GamePot_Android_UPL.xml
  
  ```xml
  ...
  <resourceCopies>
      <copyFile src="$S(PluginDir)/ThirdParty/Android/libs/gamepot-channel-line.aar" dst="$S(BuildDir)/libs/gamepot-channel-line.aar" />
      <copyFile src="$S(PluginDir)/ThirdParty/Android/libs/line-sdk-4.0.10.aar" dst="$S(BuildDir)/libs/line-sdk-4.0.10.aar" />
  </resourceCopies>
  
  ...
  
  <buildGradleAdditions>
      <insert>
  
          ...
          dependencies {
              ...
              implementation(name: 'gamepot-channel-line', ext: 'aar')
              implementation(name: 'line-sdk-4.0.10', ext: 'aar')
              ...
          }
  
          ...
  
          defaultConfig {
              resValue "string", "gamepot_line_channelid","xxxxxxx"
          }
          ...
  
      </insert>
  </buildGradleAdditions>
  
  ...
  
  <gameActivityImportAdditions>
    <insert>
      import io.gamepot.channel.line.GamePotLine;
    </insert>
  </gameActivityImportAdditions>
  
  ...
  ```
  
  - 在$S(PluginDir)/ThirdParty/Android/libs项目路径下添加gamepot-channel-line.aar文件和line-sdk-4.0.10.aar文件
    
    <br>
    
- **iOS**
  
  - 修改GamePotSDKPlugin.Build.cs文件
  
  ```C#
  ...
  
  public GamePotSDKPlugin(ReadOnlyTargetRules Target) : base(Target)
  {
      ...
             else if (Target.Platform == UnrealTargetPlatform.IOS)
          {
                  PublicAdditionalFrameworks.Add(
                  new Framework(
                      "GamePotLine",
                      ModuleDirectory+"/ThirdParty/iOS/GamePotLine.framework"
                  )
              );
  
              PublicAdditionalFrameworks.Add(
                  new Framework(
                      "LineSDK",
                      ModuleDirectory+"/ThirdParty/iOS/LineSDK.framework"
                  )
              );
  
              PublicAdditionalFrameworks.Add(
                  new Framework(
                      "LineSDKObjC",
                      ModuleDirectory+"/ThirdParty/iOS/LineSDKObjC.framework"
                  )
              );
          }
      ...
  }
  ...
  ```
  
  - 修改GamePotConfig-info.plist文件
  
  ```text
   gamepot_line_channelid// 拟在NAVER使用的Client ID
   gamepot_line_url_schemes// LINE URL Scheme（line3rdp.{项目包identifier}）
  ```
  
  用SourceCode查看时，如下进行添加
  
  ```markup
  ...
  <key>gamepot_line_channelid</key>
  <string>xxxxxx</string>
  <key>gamepot_line_url_schemes</key>
  <string>xxxxxx</string>
  ...
  ```
  

AdditionalPlistData中添加LINE相关CFBundleURLSchemes及LSApplicationQueriesSchemes值

```java
<key>CFBundleURLTypes</key>
<array>
<dict>
<key>CFBundleTypeRole</key>
<string>Editor</string>
<key>CFBundleURLSchemes</key>
<array>
<string>line3rdp.{项目捆绑标识符}<</string>
</array>
...
</dict>
…..
<key>LSApplicationQueriesSchemes</key>
<array>
<string>lineauth2</string>
……
</array>
```

<!--
#### Twitter登录<a name="트위터로그인"></a>

如要使用Twitter登录功能，请使用下列代码。

- **Android**
  
  - 修改GamePot_Android_UPL.xml
  
  ```xml
  ...
  <resourceCopies>
          <copyFile src="$S(PluginDir)/ThirdParty/Android/libs/gamepot-channel-twitter.aar" dst="$S(BuildDir)/libs/gamepot-channel-twitter.aar" />
          <copyFile src="$S(PluginDir)/ThirdParty/Android/libs/twitter-core-3.3.0.aar" dst="$S(BuildDir)/libs/twitter-core-3.3.0.aar" />
  </resourceCopies>
  
  ...
  
  <buildGradleAdditions>
      <insert>
          ...
          dependencies {
              ...
              implementation(name: 'gamepot-channel-twitter', ext: 'aar')
              implementation(name: 'twitter-core-3.3.0', ext: 'aar') {
                  transitive = true
              }
              ...
          }
  
          ...
  
          defaultConfig {
              resValue "string", "gamepot_twitter_consumerkey", ""
              resValue "string", "gamepot_twitter_consumersecret", ""
          }
          ...
  
      </insert>
  </buildGradleAdditions>
  
  ...
  
  <gameActivityImportAdditions>
    <insert>
      import io.gamepot.channel.twitter.GamePotTwitter;
    </insert>
  </gameActivityImportAdditions>
  
  ...
  ```
  
  - 在$S(PluginDir)/ThirdParty/Android/libs项目路径下添加gamepot-channel-twitter.aar文件和twitter-core-3.3.0.aar文件
    
    <br>
    
- **iOS**
  
  - 修改GamePotSDKPlugin.Build.cs文件
  
  ```C#
  ...
  
  public GamePotSDKPlugin(ReadOnlyTargetRules Target) : base(Target)
  {
      ...
             else if (Target.Platform == UnrealTargetPlatform.IOS)
          {
                  PublicAdditionalFrameworks.Add(
                  new Framework(
                      "GamePotTwitter",
                      ModuleDirectory+"/ThirdParty/iOS/GamePotTwitter.framework"
                  )
              );
  
              PublicAdditionalFrameworks.Add(
                  new Framework(
                      "TwitterCore",
                      ModuleDirectory+"/ThirdParty/iOS/TwitterCore.framework"
                  )
              );
  
              PublicAdditionalFrameworks.Add(
                  new Framework(
                      "TwitterKit",
                      ModuleDirectory+"/ThirdParty/iOS/TwitterKit.framework"
                  )
              );
          }
      ...
  }
  ...
  ```
  
  - 修改GamePotConfig-info.plist文件
  
  ```text
   gamepot_twitter_consumerkey : Twitter Consumer Key
   gamepot_twitter_consumersecret :  Twitter Consumer Secret
  ```
  
  用SourceCode查看时，如下进行添加
  
  ```markup
  ...
  <key>gamepot_twitter_consumerkey</key>
  <string>xxxxxx</string>
  ...
  ```
  

AdditionalPlistData中添加Twitter相关CFBundleURLSchemes及LSApplicationQueriesSchemes值

```java
<key>CFBundleURLTypes</key>
<array>
<dict>
<key>CFBundleTypeRole</key>
<string>Editor</string>
<key>CFBundleURLSchemes</key>
<array>
<string>twitterkit-{使用的gamepot_twitter_consumerkey}<</string>
</array>
...
</dict>
…..
<key>LSApplicationQueriesSchemes</key>
<array>
<string>twitter</string>
<string>twitterauth</string>
……
</array>
```
-->

#### Apple Web登录<a name="애플웹로그인"></a>

如要使用Apple Web登录，在仪表盘的**项目设置 > 一般**菜单设置Apple ID登录后使用下列代码。

- 修改GamePot_Android_UPL.xml

```xml
...
<resourceCopies>
        <copyFile src="$S(PluginDir)/ThirdParty/Android/libs/gamepot-channel-apple-signin.aar" dst="$S(BuildDir)/libs/gamepot-channel-apple-signin.aar" />
</resourceCopies>

...

<buildGradleAdditions>
    <insert>

        ...
        dependencies {
            ...
            implementation(name: 'gamepot-channel-apple-signin', ext: 'aar')
            ...
        }

        ...

    </insert>
</buildGradleAdditions>

...

<gameActivityImportAdditions>
  <insert>
    import io.gamepot.channel.naver.GamePotAppleSignin;
  </insert>
</gameActivityImportAdditions>

...
```

- 向项目$S(PluginDir)/ThirdParty/Android/libs路径添加gamepot-channel-apple-signin.aar文件

### 自动登录功能<a name="자동로그인기능"></a>

如要使用通过传输会员最后一次登录信息的API自动登录功能时，请使用下列代码。

```C
ENLoginType::Type loginType =  FGamePotSDKPluginModule::GetSharedGamePotSdk()->getLastLoginType();

if(loginType != ENLoginType::NONE) {
{
    // 以最后一次登录的类型登录的方式。
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->Login(loginType);
}
else
{
    // 第一次运行游戏或已退出登录的状态。请跳转到可以进行登录的登录界面。
}
```

### 退出功能<a name="로그아웃기능"></a>

如要使用退出功能，请使用下列代码。

```C
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->Logout();

void ASampleGameModeBase::OnLogoutSuccess()
{
}

void ASampleGameModeBase::OnLogoutFailure(FNError NError)
{
    // 退出登录失败。请使用NError.message显示错误消息。
}
```

### 会员注销功能<a name="회원탈퇴기능"></a>

如要使用会员注销功能，请使用下列代码。

```C
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->deleteMember();

/// 会员注销成功
void ASampleGameModeBase::OnDeleteMemberSuccess()
{

}

void ASampleGameModeBase::OnDeleteMemberFailure(FNError NError)
{
   // 会员注销失败。请使用NError.message显示错误消息。
}
```

### 登录验证功能<a name="로그인검증기능"></a>

登录成功并由开发商服务器向GAMEPOT服务器传递登录信息后，即可进行登录验证。

详细说明请参考[登录验证请求](/docs/zh/zh/game-gamepotserver#로그인검증요청)。

## 第三方账户关联<a name="외부계정연동"></a>

可以在一个游戏账户中关联或解除关联多个第三方账户。

### 账户关联功能<a name="계정연동기능"></a>

如要使用Google、Facebook、NAVER等第三方账户的关联功能，请使用下列代码。

```C
UENUM()
namespace ENLinkingType
{
    enum Type
    {
        NONE,
        GOOGLEPLAY,
        GAMECENTER,
        GOOGLE,
        FACEBOOK,
        NAVER,
        TWITTER,
        LINE,
        APPLE,
        THIRDPARTYSDK
    };
}

if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->createLinking(ENLinkingType::Type linkingType);

void ASampleGameModeBase::OnCreateLinkingSuccess(FNUserInfo NUserInfo) {
        // 账户关联成功
}

void ASampleGameModeBase::OnCreateLinkingCancel() {
        // 玩家取消账户关联时

}
void ASampleGameModeBase::OnCreateLinkingFailure(FNError NError) {
        // 账户关联失败。请使用NError.message显示错误消息。
}
```

### 关联列表确认功能<a name="연동리스트확인기능"></a>

如要确认与账户关联的第三方账户列表，请使用下列代码。

```C
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
     TArray<FNLinkingInfo> linkedList = FGamePotSDKPluginModule::GetSharedGamePotSdk()->getLinkedList();


//定义链接信息
USTRUCT()
struct FNLinkingInfo
{
    UPROPERTY()
    ENLinkingType::Type provider;     // 账户关联信息（Google、FaceBook、NAVER、Apple…）
}
}
```

### 解除关联功能<a name="연동해제기능"></a>

如要使用解除与第三方账户的关联功能，请使用下列代码。

```C
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->deleteLinking(ENLinkingType::Type linkType);

void ASampleGameModeBase::OnDeleteLinkingSuccess() {
/// 账户关联解除成功
}

void ASampleGameModeBase::OnDeleteLinkingFailure(FNError NError) {
    /// 账户关联解除失败。请使用NError.message显示错误消息。
}
```

## 支付功能<a name="결제기능"></a>

可使用应用内购买所需的支付功能。

### 应用内商品查询功能<a name="인앱상품조회기능"></a>

如要使用查询商店内商品信息的功能，请使用下列代码。

```C
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    TArray<FNPurchaseItem> itemList = FGamePotSDKPluginModule::GetSharedGamePotSdk()->getPurchaseItems();


USTRUCT()
struct FNPurchaseItem
{
    UPROPERTY()
    FString productId;             // 商品ID

    UPROPERTY()
    FString type;                  // 商品类型。固定为"inapp"

    UPROPERTY()
    FString price;                 // 价格Google商店：$0.99，其他商店：0.99

    UPROPERTY()
    FString price_amount;        

    UPROPERTY()
    FString price_amount_micros;   // （显示于UI时推荐）货币与价格合并的值。ONE Store不会传输货币单位。例如）$0.99

    UPROPERTY()
    FString price_currency_code;   // 货币代码 例如KRW、USD

    UPROPERTY()
    FString price_with_currency;

    UPROPERTY()
    FString title;                  // 商品名称

    UPROPERTY()
    FString description;           // 商品描述
}
```

### 支付尝试功能<a name="결제시도기능"></a>

可以通过一个支付API，在Google Play商店、Apple App Store均可使用支付尝试功能。

如要使用支付尝试功能，请使用下列代码。

```C#
// productId：商店中添加的商品ID
// uniqueId：单独管理的发票号
// serverId：付费角色的服务器ID
// playerId：付费角色的角色ID
// etc     ：付费角色的其他信息

if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->purchase(FString productId, FString uniqueId, FString serverId, FString playerId, FString etc);

    /// 应用内支付成功
 void ASampleGameModeBase::OnPurchaseSuccess(FNPurchaseInfo NPurchaseInfo)
 {
 }

/// 取消应用内支付
 void ASampleGameModeBase::OnPurchaseCancel()
 {
 }

/// 应用内支付失败
 void ASampleGameModeBase::OnPurchaseFailure(FNError NError)
 {
       // 请使用NError.message显示错误消息。
 }
```

### 获取付费道具信息的功能<a name="결제아이템정보획득기능"></a>

如要使用获取由商店传递的应用内付费道具信息功能，请使用下列代码。

```C#
USTRUCT()
struct FNPurchaseInfo
{
    UPROPERTY()
    FString price;                        // 付费道具的价格
    UPROPERTY()
    FString productId;                 // 付费道具的ID
    UPROPERTY()
    FString currency;                   // 支付价格货币（KRW/USD）
    UPROPERTY()
    FString orderId;                     // 商店的Order ID
    UPROPERTY()
    FString productName;           // 付费道具的名称
    UPROPERTY()
    FString gamepotOrderId;        // GAMEPOT生成的Order ID
    UPROPERTY()
    FString uniqueId;                   // 由开发商单独管理的发票ID
    UPROPERTY()
    FString serverId;                   // 付费角色的服务器ID
    UPROPERTY()
    FString playerId;                   // 付费角色的角色ID
    UPROPERTY()
    FString etc;                        // 进行支付的角色的其他信息
    UPROPERTY()
    FString signature;                 // 商店签名
    UPROPERTY()
    FString originalJSONData;  // 发票数据
}
```

### 发放付费道具的功能<a name="결제아이템지급기능"></a>

可设置为与支付商店的发票明细进行对照并完成所有验证后向开发商服务器传递发放请求。

详细说明请参考[道具发放请求](/docs/zh/zh/game-gamepotserver#아이템지급요청)。

### My Card支付<a name="Mycard결제"></a>

:::(info) (参考)
关联My Card所需的FacServiceID/KEY值请联系My Card进行确认，然后在仪表盘中设置。
:::

1. 在仪表盘 >> 支付 >> IAP的商店类型：Google项目 > 添加价格 > 货币（例如TWD）/输入价格信息后进行保存。
  
2. 在仪表盘 >> 项目设置 >> 第三方支付项目中添加My Card后，请确认相应的FacService ID / Sign Key是否正常输入。
  
3. 支付时调用以下SDK代码。
  

```c++
// productId：输入已添加至商店的商品ID。
// uniqueId：输入单独管理的发票号。
// serverId：输入进行付费的角色的服务器ID。
// playerId：输入进行付费的角色的角色ID。
// etc      ： 输入付费角色的其他信息。

if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->purchase(FString productId, FString uniqueId, FString serverId, FString playerId, FString etc);
```

- 使用My Card时付费道具的调用形式请使下方API。
  
  ```c++
  if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
  TArray<FNPurchaseItem> itemList = FGamePotSDKPluginModule::GetSharedGamePotSdk()->getPurchaseThirdPaymentsItems();
  ```
  

4. $S(PluginDir)/GamePot_Android_UPL.xml文件须使用编辑器打开。
  
  ```java
  ...
   <resourceCopies>
   ...
   <copyFile src="$S(PluginDir)/ThirdParty/Android/libs/gamepot-billing-mycard.aar" dst="$S(BuildDir)/libs/gamepot-billing-mycard.aar" />
   ....
  
  <buildGradleAdditions>
  ...
      dependencies {
     ...
     implementation(name: 'gamepot-billing-mycard', ext: 'aar')
     ...
  
     defaultConfig {
     ...
     resValue "string", "gamepot_store", "google"
     resValue "string", "gamepot_payment", "mycard"// 只有当商店为Google时才能运行。
  ```
  

5 .请确认./ThirdParty/Android/libs/gamepot-billing-mycard.aar文件夹内是否包含gamepot-billing-mycard.aar。

### 第三方支付<a name="외부결제"></a>

如要关联第三方支付模块，首先参考[第三方支付服务关联](/docs/zh/zh/game-gamepot-projectmgmt#외부결제서비스연동)完成设置后使用下列代码。

```C#
// productId：已添加至商城的商品ID
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->purchaseThirdPayments(FString productId);


// 用于调用产品信息列表的API
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    TArray<FNPurchaseItem> itemList = FGamePotSDKPluginModule::GetSharedGamePotSdk()->getPurchaseThirdPaymentsItems();
```

## SDK自主提供的登录UI<a name="SDK자체제공로그인UI"></a>

可以使用GAMEPOT Unreal SDK提供的完整的登录UI。

### 调用SDK自主提供的登录UI<a name="SDK자체제공로그인UI호출"></a>

如要调用GAMEPOT Unreal SDK提供的登录UI，请使用下列代码。

```C
USTRUCT()
struct FNLoginUIInfo
{
    //是否插入图片
    UPROPERTY()
    bool showLogo;

    //拟显示在UI上的登录类型
    UPROPERTY()
    TArray<ENLoginType::Type> loginTypes;  //google, facebook...
}

//拟调用的登录UI类型
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showLoginWithUI(FNLoginUIInfo NLoginUIInfo);

void ASampleGameModeBase::OnLoginSuccess(FNUserInfo NUserInfo)
{
    // 登录成功
}

void ASampleGameModeBase::OnLoginCancel()
{
    // 取消登录
}

void ASampleGameModeBase::OnLoginFailure(FNError NError)
{
   // 登录失败。请使用error.message显示错误消息。
}

// 维护（仪表盘的维护选项处于激活状态时调用）
void ASampleGameModeBase::OnLoginMaintenance(FNAppStatus NAppStatus)
{
   // 须基于参数传递的status信息创建并显示弹窗。请从下列两种方式中选择一种配置弹窗。
    // 方式1：使用开发商自行实现UI的游戏内弹窗
    // 方式2：调用下列代码后使用SDK自主弹窗

    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
        FGamePotSDKPluginModule::GetSharedGamePotSdk()->showAppStatusPopup(NAppStatus.ToJsonString());
}

// 强制更新（商店版本和客户端版本不一致时调用）
void ASampleGameModeBase::OnLoginNeedUpdate(FNAppStatus NAppStatus)
{
     // 须基于参数传递的status信息创建并显示弹窗。请从下列两种方式中选择一种配置弹窗。
    // 方式1：使用开发商自行实现UI的游戏内弹窗
    // 方式2：调用下列代码后使用SDK自主弹窗

    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
        FGamePotSDKPluginModule::GetSharedGamePotSdk()->showAppStatusPopup(NAppStatus.ToJsonString());
}

void ASampleGameModeBase::OnLoginExit()
{
    // TODO：终止登录UI时，
}

void ASampleGameModeBase::OnAppClose()
{
    // 结束应用
    // 如果使用方式2实现强制更新或维护功能时，因有可能强制结束应用，请在此处可执行结束应用。

}
```

### 设置自主提供的登录UI图片标志（Android）<a name="자체제공로그인UI이미지로고설정안드로이드"></a>

可设置Android专用自主提供的登录UI上方显示的图片。如果不另行设置，则使用包含在SDK的默认图片，也可自行设置适合游戏的图片。

Android专用自主提供的登录UI图片的设置方法如下。

1. 如下所示，在以下路径下分别创建res/drawable文件夹后，根据各大小添加图片文件。
  
  | 文件夹名 | 长度  |
  | --- | --- |
  | $S(PluginDir)/ThirdParty/GamePotResources/res/drawable-mdpi// | 24x24 |
  | $S(PluginDir)/ThirdParty/GamePotResources/res/drawable-hdpi/ | 36x36 |
  | $S(PluginDir)/ThirdParty/GamePotResources/res/drawable-xhdpi/ | 48x48 |
  | $S(PluginDir)/ThirdParty/GamePotResources/res/drawable-xxhdpi/ | 72x72 |
  | $S(PluginDir)/ThirdParty/GamePotResources/res/drawable-xxxhdpi/ | 96x96 |
  
2. 请将图片文件名变更为 ic_stat_gamepot_login_logo.png。
  

## 优惠券功能<a name="쿠폰기능"></a>

如要使用用户输入优惠券即处理为已使用的功能，请使用下列代码。

```C
   if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    {
        FGamePotSDKPluginModule::GetSharedGamePotSdk()->coupon(FString couponNumber);// 优惠券号码

        FGamePotSDKPluginModule::GetSharedGamePotSdk()->coupon(FString couponNumber, FString userData);// 优惠券号码、用户信息
    }

void ASampleGameModeBase::OnCouponSuccess(FString msg)
{
    /// 优惠券使用成功
}

void ASampleGameModeBase::OnCouponFailure(FNError NError)
{
      // 优惠券使用失败。请使用error.message显示错误消息。
}
```

### 发放道具<a name="아이템지급"></a>

优惠券使用成功时，向开发商服务器请求发放道具。

详细说明请参考[道具发放请求](/docs/zh/zh/game-gamepotserver#아이템지급요청)。

## 推送功能<a name="푸시기능"></a>

可开启或关闭全部推送、夜间推送、广告推送功能，并可使用本地推送功能。
使用推送功能时，需将广告推送设置为true（广告推送值为false时，无论一般/夜间推送如何设置，都不会收到推送。）

### 一般推送设置<a name="일반푸시설정"></a>

如要设置一般推送，请使用下列代码。

```C
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
        FGamePotSDKPluginModule::GetSharedGamePotSdk()->setPushStatus(bool pushEnable); 

void ASampleGameModeBase::OnPushSuccess()
{
    /// 对推送状态变更的服务器通信成功
}

void ASampleGameModeBase::OnPushFailure(FNError NError)
{
        // 推送状态变更失败。请使用error.message显示错误消息。
}
```

### 夜间推送设置<a name="야간푸시설정"></a>

如要设置夜间推送，请使用下列代码。

```C
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
        FGamePotSDKPluginModule::GetSharedGamePotSdk()->setPushNightStatus(bool nightPushEnable); 

void ASampleGameModeBase::OnPushNightSuccess()
{
    /// 对夜间推送状态变更的服务器通信成功
}

void ASampleGameModeBase::OnPushNightFailure(FNError NError)
{
        // 夜间推送状态变更失败。请使用error.message显示错误消息。
}
```

### 广告推送设置<a name="광고푸시설정"></a>

如要设置广告推送，请使用下列代码。

```C
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
        FGamePotSDKPluginModule::GetSharedGamePotSdk()->setPushADStatus(bool adPushEnable); 

void ASampleGameModeBase::OnPushAdSuccess()
{
    /// 对广告推送状态变更的服务器通信成功
}

void ASampleGameModeBase::OnPushFailure(FNError NError)
{
        // 广告推送状态变更失败。请使用error.message显示错误消息。
```

#### 同时设置一般/夜间/广告推送<a name="일반야간광고푸시한번에설정"></a>

如果是登录前需要确认是否允许推送的游戏，登录后必须调用以下代码。

```C
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
        FGamePotSDKPluginModule::GetSharedGamePotSdk()->setPushStatus(bool pushEnable, bool nightPushEnable, bool adPushEnable); 

void ASampleGameModeBase::OnPushStatusSuccess()
{
    /// 对推送状态变更的服务器通信成功
}

void ASampleGameModeBase::OnPushStatusFailure(FNError NError)
{
        // 推送状态变更失败。请使用error.message显示错误消息。
}
```

### 确认推送状态<a name="푸시상태확인"></a>

如要确认当前推送状态，请使用下列代码。

```C#
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
        FNPushInfo NPushInfo = FGamePotSDKPluginModule::GetSharedGamePotSdk()->getPushStatus(); 

USTRUCT()
struct FNPushInfo
{
    UPROPERTY()
    bool enable;      // 是否允许一般推送

    UPROPERTY()
    bool night;        // 是否允许夜间推送

    UPROPERTY()
    bool ad;           // 是否允许广告推送
}
```

### 本地推送功能<a name="로컬푸시기능"></a>

可以不通过推送消息服务器，直接在设备自主显示推送。

如要通过注册推送在规定时间显示本地推送时，请使用下列代码。

```C
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
         int pushId = FGamePotSDKPluginModule::GetSharedGamePotSdk()->sendLocalPush(FString date, FString title, FString message); 

// date : (Format - timestamp "yyyy-MM-dd HH:mm:ss") 
// ex >  DateTime.Parse("2018-01-01 00:00:00")
//  title :  "title"
// message :  "content"

// pushid的返回值由开发商管理
```

#### 取消已注册的本地推送<a name="등록한로컬푸시취소"></a>

如要使用注册本地推送时获得的`pushid`值取消已注册的推送，请使用下列代码。

```C
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
         bool success = FGamePotSDKPluginModule::GetSharedGamePotSdk()->cancelLocalPush(int /*添加推送时获取的pushId*/);
```

## 显示公告事项图片的功能<a name="공지사항이미지표시기능"></a>

可设置为在仪表盘**公告事项**菜单显示上传的图片。推荐图片大小如下。

- 大小：720x1200（Portrait）、1280x640（Landscape）
- 容量：250KB以下

如要在仪表盘**公告事项**菜单显示上传的图片，请使用下列代码。

```C
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showNotice(bool showToday = true); 

// true：应用“今日不再显示”
// false：与“今日不再显示”无关，强制显示

if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showEvent(FString Type); 

// Type：仅显示与仪表盘公告事项 > 分类菜单中设置的分类名称相对应的图片

 void ASampleGameModeBase::OnReceiveScheme(FString scheme)
 {
      // 传递在GAMEPOT仪表盘设置的scheme值
 }
```

## 客户支持功能<a name="고객지원"></a>

通过与仪表盘关联，可使用客户咨询、调用政策及条款UI、同意收集等功能。

### 客户咨询功能<a name="고객문의기능"></a>

可使用会员发送咨询，由负责人回复的客户咨询功能。与仪表盘的**客户支持 > 客户咨询**菜单关联。

客户咨询UI根据设备语言将变更为韩语、英语、日语、中文（简体、繁体）中的一个语言，除此之外的设备语言，则变更为英语。

如要与仪表盘关联使用客户咨询功能，请使用下列代码。

```C
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showCSWebView(); 
```

#### 外部链接客户咨询<a name="외부링크고객문의"></a>

如要允许通过外部链接访问的未登录客户也能提交咨询，请使用下列代码。

```C
// url：GAMEPOT发放的外部客户支持URL
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showWebView(FString url); 
```

### 条款及政策UI调用功能<a name="약관및정책UI호출기능"></a>

可在仪表盘的**客户支持**菜单以UI形式调用已撰写的各种条款、政策。

如要调用条款及政策UI，请使用下列代码。

- **使用条款**
  
  ```C
  if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
      FGamePotSDKPluginModule::GetSharedGamePotSdk()->showTerms(); 
  ```
  
- **隐私政策**
  
  ```C
  if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
      FGamePotSDKPluginModule::GetSharedGamePotSdk()->showPrivacy(); 
  ```
  
- **退款政策**
  
  ```C
  if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
      FGamePotSDKPluginModule::GetSharedGamePotSdk()->showRefund(); 
  ```
  

### 条款同意功能（含GDPR）<a name="약관동의기능GDPR포함"></a>

可使用提供的弹窗UI功能收集在仪表盘已撰写的各种政策及条款的同意。也可以收集GDPR政策的同意。

#### 调用条款同意UI<a name="약관동의UI호출"></a>

如要变更并调用提供的条款同意UI主题，请使用下列代码。

```C
// 方式一.一般调用（应用BLUE主题）
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showAgreeDialog(); 

// 方式二.应用其他主题时
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
{
    // - 默认主题
    // BLUE
    // GREEN

    // - 改善主题
    // MATERIAL_RED,
    // MATERIAL_BLUE,
    // MATERIAL_CYAN,
    // MATERIAL_ORANGE,
    // MATERIAL_PURPLE,
    // MATERIAL_DARKBLUE,
    // MATERIAL_YELLOW,
    // MATERIAL_GRAPE,
    // MATERIAL_GRAY,
    // MATERIAL_GREEN,
    // MATERIAL_PEACH,

    FNAgreeInfo info;
    info.theme = "MATERIAL_RED";
    info.headerTitle = TEXT("title");
    info.headerBackGradient = "{ 0xFF00050B, 0xFF0F1B21 }";
    info.headerBottomColor = "0xFFFF0000";
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showAgreeDialog(info.ToJsonString()); 
}

// 同意条款时
void ASampleGameModeBase::OnAgreeDialogSuccess(FNAgreeResultInfo NAgreeResultInfo)
{
       // NAgreeResultInfo.agree：同意全部必要条款时为true
        // NAgreeResultInfo.agreePush：勾选同意接收（一般）推送时为true，否则为false
        // NAgreeResultInfo.agreeNight ：勾选同意夜间接收广告类消息时为true，否则为false
        // agreePush/agreeNight值请在登录成功后通过setPushStatus API一次性设置。
}

void ASampleGameModeBase::OnAgreeDialogFailure(FNError NError)
{
    // 发生错误
}
```

- 定义NAgreeInfo
  
  ```
  USTRUCT()
  struct FNAgreeInfo
  {    
      // 默认主题
      UPROPERTY()
      FString theme;
  
      // 标题
      // 背景颜色（Gradient）
      UPROPERTY()
      TArray<FString> headerBackGradient;
  
      // 标题区下方的线条颜色
      UPROPERTY()
      FString headerBottomColor;
  
      // 图标图片的文件名（aos - drawable / ios - bundle）
      UPROPERTY()
      FString headerIconDrawable;
  
      // 标题
      UPROPERTY()
      FString headerTitle;
  
      // 标题颜色
      UPROPERTY()
      FString headerTitleColor;
  
      // 内容
      // 背景颜色（Gradient）
      UPROPERTY()
      TArray<FString> contentBackGradient;
  
      // 图标图片的文件名（aos - drawable / ios - bundle）
      UPROPERTY()
      FString contentIconDrawable;
  
      // 图标颜色
      UPROPERTY()
      FString contentIconColor;
  
      // 确定按钮的颜色
      UPROPERTY()
      FString contentCheckColor;
  
      // 确认内容的颜色
      UPROPERTY()
      FString contentTitleColor;
  
      // 查看语句的颜色
      UPROPERTY()
      FString contentShowColor;
  
      // 页脚（开始游戏）
      // 背景颜色（Gradient）
      UPROPERTY()
      TArray<FString> footerBackGradient;
  
      // 游戏开始按钮的背景颜色（Gradient）
      UPROPERTY()
      TArray<FString> footerButtonGradient;
  
      // 游戏开始按钮的边框颜色
      UPROPERTY()
      TArray<FString> footerButtonOutlineColor;
  
      // 游戏开始语句
      UPROPERTY()
      TArray<FString> footerTitle;
  
      // 游戏开始语句的颜色
      UPROPERTY()
      TArray<FString> footerTitleColor;
  
      //是否显示一般推送
      UPROPERTY()
      bool showPush;
  
      // 是否显示夜间推送
      UPROPERTY()
      bool showNightPush;
  
      // 更改“同意全部”语句时
      UPROPERTY()
      FString allMessage;
  
      // 更改“使用条款”语句时
      UPROPERTY()
      FString termMessage;
  
      // 更改“个人信息处理方针”语句时
      UPROPERTY()
      FString privacyMessage;
  
      // 更改“一般推送”语句时
      UPROPERTY()
      FString pushMessage;
  
      // 更改“夜间推送”语句时
      UPROPERTY()
      FString nightPushMessage;
  
      UPROPERTY()
      FString pushDetailURL;
  
      UPROPERTY()
      FString nightPushDetailURL;
  }
  ```
  
  <br>
  
- 各个变量将应用到如下图片所显示的区域中。
  ![gamepotunreal002ko](./images/gamepot_unreal_002_zh.png)
  

#### GDPR条款确认列表功能<a name="GDPR약관체크리스트기능"></a>

如要以列表形式导入在仪表盘激活的GDPR条款项目，请使用下列代码。

```C
//返回的数据格式为FString类型，且为string[]格式。例如> "[ gdpr_privacy, gdpr_term ]"
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FString gdpr_list = FGamePotSDKPluginModule::GetSharedGamePotSdk()->getGDPRCheckedList();

// gdpr_privacy：隐私政策
// gdpr_term：使用条款
// gdpr_gdpr：GDPR使用条款
// gdpr_push_normal：同意接收活动推送
// gdpr_push_night：同意接收夜间活动推送（仅限韩国）
// gdpr_adapp_custom：同意接收个人精准广告投放（GDPR实施国家）
// gdpr_adapp_nocustom：同意接收除个人精准广告投放以外的一般广告（GDPR实施国家）
```

## 恶意使用支付取消的用户重新支付弹窗功能<a name="결제취소악용자재결제팝업기능"></a>

对通过仪表盘的**支付取消**菜单恶意使用Google取消支付的用户进行自动停用处理时，可向该恶意用户显示由SDK提供的重新支付弹窗UI。通过UI重新支付取消支付的道具时，将自动解除停用。

如要针对恶意使用支付取消的用户使用重新支付弹窗功能，请使用下列代码。

```C
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    {
        //主题种类
        // MATERIAL_RED,
        // MATERIAL_BLUE,
        // MATERIAL_CYAN,
        // MATERIAL_ORANGE,
        // MATERIAL_PURPLE,
        // MATERIAL_DARKBLUE,
        // MATERIAL_YELLOW,
        // MATERIAL_GRAPE,
        // MATERIAL_GRAY,
        // MATERIAL_GREEN,
        // MATERIAL_PEACH

        NVoidInfo info;
        info.theme = "MATERIAL_RED";
        FGamePotSDKPluginModule::GetSharedGamePotSdk()->setVoidBuilder(info.ToJsonString());
    }
```

- 定义NVoidInfo

```C
USTRUCT()
struct FNVoidInfo
{
    // 默认主题
    UPROPERTY()
    FString theme;

    // 背景颜色（Gradient）
    UPROPERTY()
    TArray<FString> headerBackGradient;

    // 标题
    UPROPERTY()
    FString headerTitle;

    // 标题颜色
    UPROPERTY()
    FString headerTitleColor;

    UPROPERTY()
    TArray<FString> contentBackGradient;

    UPROPERTY()
    TArray<FString> listHeaderBackGradient;  

    UPROPERTY()
    FString listHeaderTitleColor;

    UPROPERTY()
    TArray<FString> listContentBackGradient;

    UPROPERTY()
    FString listContentTitleColor;

   // 背景颜色（Gradient）
    UPROPERTY()
    TArray<FString> footerBackGradient;

    // 按钮的背景颜色（Gradient）
    UPROPERTY()
    TArray<FString> footerButtonGradient;

    UPROPERTY()
    FString footerTitleColor;

    UPROPERTY()
    FString descHTML;

    UPROPERTY()
    FString descColor;

    UPROPERTY()
    FString listHeaderTitle;

    UPROPERTY()
    FString footerTitle;
}
```

## 远程配置功能<a name="원격구성기능"></a>

可导入注册在仪表盘**游戏 > 远程配置**菜单的服务器参数值。如果在SDK使用导入的参数值，无需更新游戏可对各个要素进行修改及控制。

导入的参数值会在登录时加载，之后可以被调用。

如要使用远程配置功能，请使用下列代码。

```C
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
{
    //"test_01"：参数FString
    FString value = FGamePotSDKPluginModule::GetSharedGamePotSdk()->getConfig("test_01"); 

    //以JSON string格式获取添加至仪表盘的所有参数。
    FString json_value = FGamePotSDKPluginModule::GetSharedGamePotSdk()->getConfigs();
}
```

## 游戏日志传输功能<a name="게임로그전송기능"></a>

调用游戏日志后，可在仪表盘的**游戏 > 日志**菜单进行确认。

如要使用游戏日志传输功能，请参考表的内容在下列代码输入保留字后调用代码。

- **保留字及代码**
  
  | 保留字 | 是否必需 | 类型  | 概述  | 最大长度 |
  | --- | --- | --- | --- | --- |
  | `FNSendLogCharacter.NAME` | 必填  | `FString` | 角色名称 | 128 |
  | `FNSendLogCharacter.LEVEL` | 选择  | `FString` | 级别  | 128 |
  | `FNSendLogCharacter.SERVER_ID` | 选择  | `FString` | 服务器ID | 128 |
  | `FNSendLogCharacter.PLAYER_ID` | 选择  | `FString` | 角色ID | 128 |
  | `FNSendLogCharacter.USERDATA` | 选择  | `FString` | 其他信息 | 128 |
  
  ```C
  USTRUCT()
  struct FNSendLogCharacter
  {
      UPROPERTY()
      FString NAME;
  
      UPROPERTY()
      FString PLAYER_ID;
  
      UPROPERTY()
      FString SERVER_ID;
  
      UPROPERTY()
      FString LEVEL;
  
      UPROPERTY()
      FString USERDATA;
  }
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    {
        FNSendLogCharacter info;
        info.NAME = TEXT("tester");
        info.PLAYER_ID = TEXT("player_id");
  
        bool result = FGamePotSDKPluginModule::GetSharedGamePotSdk()->characterInfo(info.ToJsonString());
  
        // 结果值true：验证成功。日志将发送到GAMEPOT服务器。
        // 结果值false：验证失败。请确认logcat。
    }
  ```
  

### setUserData设置<a name="setUserData설정"></a>

登录后想给相应会员添加附加信息时使用。
密钥数量上限为50个
值长度上限为1024字节
相应信息只能在会员详细项目中确认。

```C#
ex)
TSharedPtr<FJsonObject> JsonObject = MakeShareable(new FJsonObject);
JsonObject->SetStringField("appversion", "1.0.23");
JsonObject->SetStringField("server", "s1");

if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->setUserData(JsonObject);


void AGamePotSampleGameModeBase_Main::OnSetUserDataSuccess()
{
// 成功
}
void AGamePotSampleGameModeBase_Main::OnSetUserDataFailure(FNError NError)
{
// 失败
}
```

## 第三方SDK关联<a name="3rdPartySDK연동"></a>

GAMEPOT Unreal SDK支持与第三方SDK关联。

### 第三方SDK登录关联<a name="3rdPartySDK로그인연동"></a>

如要通过第三方SDK关联使用登录功能，请参考表的内容在下列参数输入值后使用代码。

- **参数及代码**
  
  - 由于不支持自动登录，因此需要每次调用。
  
  | 参数名 | 是否必需 | 类型  | 概述  |
  | --- | --- | --- | --- |
  | `userid` | 必填  | `FString` | 用户唯一ID<br>值无法使用“:”（冒号） |
  
  ```C
  FString userid = TEXT("memberid of 3rd party sdk");
  
  if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
      FGamePotSDKPluginModule::GetSharedGamePotSdk()->loginByThirdPartySDK(userid);
  ```
  

### 第三方SDK支付关联<a name="3rdPartySDK결제연동"></a>

如要通过第三方SDK关联使用支付功能，请参考表的内容在下列代码输入参数值后使用代码。

- **参数及代码**
  
  | 参数名 | 是否必需 | 类型  | 概述  |
  | --- | --- | --- | --- |
  | `productid` | 必填  | `FString` | 在仪表盘添加的道具ID |
  | `transactionid` | 必填  | `FString` | 付费发票号（GPA-xxx-xxxx-xxxx） |
  | `store` | 必填  | 付费商店（`google`、`apple`、`one`、`galaxy`） |     |
  | `currency` | 选择  | `FString` | 货币（KRW、USD） |
  | `price` | 选择  | `double` | 付费道具的金额 |
  | `paymentid` | 选择  | `FString` | 支付ID<br>一般与store_id相同 |
  | `uniqueid` | 选择  | `FString` | 开发商使用的唯一ID |
  
  ```C
  FString productId = "purchase_001";
  FString transactionId = "GPA-xxx-xxxx-xxxx";
  FString currency = "KRW";
  double price = 1200;
  FString paymentId = "google";
  FString uniqueId = "developer unique id";
  
  if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
  {
      FGamePotSDKPluginModule::GetSharedGamePotSdk()->sendPurchaseByThirdPartySDK(FString productId, FString transactionId, FString currency, double price, FString store, FString paymentId, FString uniqueId);
  }
  ```