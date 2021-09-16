## 基本环境设置<a name="基本环境设置"></a>

### Android<a name="Android1"></a>


```d
minSdkVersion : API 17 (Jelly Bean, 4.2)
```

**项目环境设置方法**

使用编辑器打开$S(PluginDir)/GamePot_Android_UPL.xml文件。

```java

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
         resValue "string", "facebook_app_id", ""                                           // optional (facebook)
         resValue "string", "fb_login_protocol_scheme", ""                           // optional (facebook)
         resValue "string", "gamepot_naver_clientid", ""                               // optional (Naver 从开发者控制台获得)
         resValue "string", "gamepot_naver_secretid", ""                              // optional (Naver 从开发者控制台获得)
         resValue "string", "gamepot_line_channelid",""                               // optional (Line 从开发者控制台获得)
         resValue "string", "gamepot_twitter_consumerkey", ""                   // optional (Twitter 从开发者控制台获得)
         resValue "string", "gamepot_twitter_consumersecret", ""               // optional (Twitter 从开发者控制台获得)
         resValue "string", "gamepot_elsa_projectid", ""                              // optional (ncp elsa)
    }
    ...
}
  </insert>
</buildGradleAdditions>
```

找到下面的必要值进行修改。修改以后，方可正常使用。

```java
resValue "string", "[key]", "[value]"
```

|值|描述|
| :--------------------------- | :--------------------------------------------------------------------------------------------- |
|gamepot_project_id           |输入GAMEPOT发放的项目ID。|
|gamepot_store                |商店值（`Google`、`ONE`或`Galaxy`）|
|gamepot_app_title            |应用标题（FCM）|
|gamepot_push_default_channel |已添加的默认频道名称（Default） - 请勿更改。|
|facebook_app_id              |Facebook发放的应用ID|
|fb_login_protocol_scheme     |Facebook发放的protocol scheme fb\[app_id\]|
| gamepot_naver_clientid     | Naver 从开发者控制台获得               |
| gamepot_naver_secretid     | Naver 从开发者控制台获得                 |
| gamepot_line_channelid     | Line 从开发者控制台获得               |
| gamepot_twitter_consumerkey     | Twitter 从开发者控制台获得          |
| gamepot_twitter_consumersecret     | Twitter 从开发者控制台获得      |
|gamepot_elsa_projectid       |使用NCLOUD ELSA时的项目ID（[查看详情](https://www.ncloud.com/product/analytics/elsa)）|
|

**通知栏的推送图标变更方法**

![gamepot_unreal_003_zh.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_unreal_003_zh.png)


收到推送时，在Android通知栏上显示的小图标是SDK自带的默认图片。用户可自行添加其他图片。

直接添加时，须按照`drawable`文件夹分别放入图片。（[Android Asset Studio](http://romannurik.github.io/AndroidAssetStudio/icons-notification.html#source.type=clipart&source.clipart=ac_unit&source.space.trim=1&source.space.pad=0&name=ic_stat_gamepot_small)可自动按照各文件夹制作图片，非常方便。）

图片文件名须为ic_stat_gamepot_small。

|文件夹名|大小|
| :------------------------------------------------------------- | :---- |
| $S(PluginDir)/ThirdParty/Android/GamePotResources/res/drawable-mdpi/    | 24x24 |
| $S(PluginDir)/ThirdParty/Android/GamePotResources/res/drawable-hdpi/    | 36x36 |
| $S(PluginDir)/ThirdParty/Android/GamePotResources/res/drawable-xhdpi/   | 48x48 |
| $S(PluginDir)/ThirdParty/Android/GamePotResources/res/drawable-xxhdpi/  | 72x72 |
| $S(PluginDir)/ThirdParty/Android/GamePotResources/res/drawable-xxxhdpi/ | 96x96 |



### iOS<a name="iOS1"></a>


将从Google Firebase下载的`GoogleService-Info.plist`文件复制到`$S(PluginDir)/ThirdParty/iOS/GamePotResources.embeddedframework/Resources/`下。

在`$S(PluginDir)/ThirdParty/iOS/GamePotResources.embeddedframework/Resources/GamePotConfig-Info.plist`内添加必要的环境变量。

![gamepot_unreal_001_zh.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_unreal_001_zh.png)


|环境变量|描述|
| :---------------------------- | :---------------------------------------------------- |
|gamepot_project_id            |输入GAMEPOT发放的项目ID。|
|gamepot_facebook_app_id       |Facebook发放的应用ID|
|gamepot_facebook_display_name |在Facebook上显示的名称|
|gamepot_google_app_id         |GoogleService-Info文件的CLIENT_ID值|
|gamepot_google_url_schemes    |GoogleService-Info文件的REVERSED_CLIENT_ID值|
| gamepot_facebook_app_id  |   Facebook App ID  |
| gamepot_facebook_display_name |  Facebook display name   |
| gamepot_naver_clientid   |  Naver Client Id   |
| gamepot_naver_secretid  |   Naver Secret Id  |
| gamepot_naver_urlscheme  |   Naver Url Scheme  |
| gamepot_line_channelid  |  Line Channel ID   |
| gamepot_line_url_schemes  |   Line URL Scheme (line3rdp.{项目标号 ID})  |
| gamepot_twitter_consumerkey  |   Twitter Consumer Key  |
| gamepot_twitter_consumersecret  |  Twitter Consumer Secret  |
|gamepot_elsa_projectid        |使用NCLOUD ELSA时的项目ID|

`GamePotResources.embeddedframework` 乙方 **压缩到 zip** 之后，
在`$S(Plugin Dir)/ThirdParty/iOS/GamePot Resources.embedded framework.zip`路径中配置的状态下 请进行Build。

在iOS上构建之前

请在项目设置 >> iOS >> Extra PList Data >> Additional Plist Data中，按照如下内容`添加用户权限获取选项`。

相应用户权限将在GAMEPOT客服中心的文件上传功能中用到。

```text
<key>NSCameraUsageDescription</key>
<string>$(PRODUCT_NAME) camera use.</string>
<key>NSPhotoLibraryUsageDescription</key>
<string>$(PRODUCT_NAME) photo library use.</string>
```

iOS 14以上版本

从iOS 14版本开始，必须向用户获取权限

方可获取IDFA值。

因此，为了在获取IDFA值时使用向用户请求权限的弹窗，
请在项目设置 >> iOS >> Extra PList Data >> Additional Plist Data中，按照如下内容`添加用户权限获取选项`。


>2020.09.11.
>Apple在获取IDFA值时必须显示向用户请求权限的弹窗这一规定延期至2021年初施行。
>请参考下方链接。
>[https://developer.apple.com/news/?id=hx9s63c5](https://developer.apple.com/news/?id=hx9s63c5)



```text
<key>NSUserTrackingUsageDescription</key>
<string>$(PRODUCT_NAME) This identifier will collect IDFA for advertising purposes.</string>
```

IDFA 权限请求弹出( 明示)

Request :

```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->requestTrackingAuthorization();
```

Response:

```c++
void ASampleGameModeBase::OnSdkResultTrackingAuthorization(FNResultTrackingAuthorization info) {
    // info.authorization (FString)
    //        ATTrackingManagerAuthorizationStatusNotDetermined,
    //        ATTrackingManagerAuthorizationStatusRestricted,
    //        ATTrackingManagerAuthorizationStatusDenied,
    //        ATTrackingManagerAuthorizationStatusAuthorized,
    //        ATTrackingManagerAuthorizationStatusUnknown
}

```

> `iOS平台为例`,登录时,调用API获得的价格IDFA的权限,首先要明确地弹出要求。

> 如果您不想在登录时呼叫相应弹窗请求，请修改`FIOSGamePotSdk::Login(ENLoginType:::Type)`函数。`$S(PluginDir)/Private/iOS/IOSGamePotSdk.cpp`

```c++
void FIOSGamePotSdk::Login(ENLoginType::Type _loginType)
{
    //登录前， 显示 IDFA弹出 < - 需要时， 注释处理
    FIOSGamePotSdk::requestTrackingAuthorization();
    ...
```

IOS为了接收Push，需要事先从使用者那里获得相应权限。
在适当的时间点( ex- Login Success) 请求相应权限后呼叫函数。

```c++
if(LOGIN_SUCCESS)
{
    //明确、权限获得邀请,Push
    FPlatformMisc::RegisterForRemoteNotifications();
}
```

## 1. 初始化<a name="1初始化"></a>


在游戏开始时加载的第一个场景（级别）使用的对象中添加以下代码。
 
 - ex> "ASampleGameModeBase.h"

```c++
//（相应级别使用的）GAMEPOT API的Callback Event Listener声明
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

 - ex> "ASampleGameModeBase.cpp"

```c++
#include "GamePotSDKPluginModule.h"

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

（Binding）Event Listener列表

```c++
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

定义NUserInfo

```c++
USTRUCT()
struct FNUserInfo
{
    UPROPERTY()
    FString memberid;           // 会员ID（玩家的唯一ID）
    UPROPERTY()
    FString name;               // 姓名
    UPROPERTY()
    FString profileUrl;         // 头像URL（存在时）
    UPROPERTY()
    FString email;              // 电子邮件（存在时）
    UPROPERTY()
    FString token;              // 玩家有效性检查用Token（在Token Authentication API中使用）
    UPROPERTY()
    FString userid;             // 社交账户ID（Google、Facebook…）
}
```

## 2. 错误代码<a name="2错误代码"></a>


定义NError

```c++
USTRUCT()
struct FNError
{
    //Detail Error code
    static const int CODE_UNKNOWN_ERROR = 0;                    // 未知错误
    static const int CODE_NOT_INITALIZE = 1;                    // 初始化失败
    static const int CODE_INVAILD_PARAM = 2;                    // 参数不正确时
    static const int CODE_MEMBERID_IS_EMPTY = 3;                    // 没有会员ID数据时
    static const int CODE_NOT_SIGNIN = 4;                    // 未登录的状态
    static const int CODE_NETWORK_MODULE_NOT_INIT = 3000;                 // 网络模块未初始化时
    static const int CODE_NETWORK_ERROR = 3001;                 // 发生网络连接错误及超时时
    static const int CODE_SERVER_ERROR = 4000;                 // server-side发生错误
    static const int CODE_SERVER_HTTP_ERROR = 4001;                 // http response code非成功时
    static const int CODE_SERVER_NETWORK_ERROR = 4002;                 // 发生网络连接错误及超时时
    static const int CODE_SERVER_PARSING_ERROR = 4003;                 // 解析从服务器接收的数据时发生错误
    static const int CODE_CHARGE_UNKNOWN_ERROR = 5000;                 // 支付时发生未知错误并由商店传递错误时
    static const int CODE_CHARGE_PRODUCTID_EMPTY = 5001;                 // 未放入product id时
    static const int CODE_CHARGE_PRODUCTID_WRONG = 5002;                 // 放入错误的product id时
    static const int CODE_CHARGE_CONSUME_ERROR = 5003;                 // consume出错

    UPROPERTY()
    int code;               // error Code

    UPROPERTY()
    FString message;        // error Message
}
```

## 3. 设置登录环境<a name="3设置登录环境"></a>


### Google登录<a name="Google登录"></a>


#### Google Firebase Console<a name="GoogleFirebaseConsole"></a>

1. 登录Google Firebase Console并下载Android用google-service.json文件后，复制到`/Plugins/GamePotSDKPlugin/Source/GamePot/ThirdParty/Android/`下。
2. 在Google Firebase Console添加构建APK时使用的Keystore中的SHA-1值。

**Google登录时响应onCancel且无法登录时**，请检查以下内容。

1. 检查是否已正常应用上面请求应用的google-service.json文件
2. 检查构建时使用的Keystore是否为导出已添加至Firebase Console的SHA-1的Keystore
3. 检查构建时是否使用了添加至Firebase Console的包名

#### Android

GamePot_Android_UPL.xml 수정

```xml
...
<resourceCopies>
    <copyFile src="$S(PluginDir)/ThirdParty/Android/libs/gamepot-channel-google-signin.aar" dst="$S(BuildDir)/libs/gamepot-channel-google-signin.aar" />
</resourceCopies>
...

<buildGradleAdditions>
    <insert>
        ...
        dependencies {
            ...
            implementation(name: 'gamepot-channel-google-signin', ext: 'aar')
            ...
        }
        ...
    </insert>
</buildGradleAdditions>
...
```

#### IOS

1. `$S(PluginDir)/ThirdParty/iOS/GamePotResouces.embeddedframework.zip`解压 。

2. 下载 IOS 专用 GoogleService-Info.plist 文件后，复制到 `$S(Plugin Dir)/ThirdParty/iOS/GamePot Resouces.embeddedframework/Resources/`的路径上，再进行压缩。

![gamepot_unreal_004_zh.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_unreal_004_zh.png)

### Facebook登录<a name="Facebook登录"></a>


#### Facebook Developer Console<a name="FacebookDeveloperConsole"></a>


在Facebook Console添加构建APK时使用的Keystore的Key哈希值。

#### Android<a name="Android2"></a>


修改GamePot_Android_UPL.xml

```xml
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

#### iOS<a name="iOS2"></a>


在GamePotConfig-Info.plist文件中添加以下项目并输入相应值。

```text
gamepot_facebook_app_id // Facebook开发人员控制台发放的应用ID
```

用SourceCode查看GamePotConfig-Info.plist文件时按如下形式添加

```markup
...
<key>gamepot_facebook_app_id</key>
<string>xxxxxx</string>
...
```


### Apple登录<a name="Apple登录"></a>



>此功能仅适用于iOS。（在Android上，以Web登录形式支持）



在**Config/DefaultEngine.ini的` [/Script/IOSRuntimeSettings.IOSRuntimeSettings] `一项中添加以下Flag值。**


>bEnableSignInWithAppleSupport=True


## 4. 登录/退出登录/注销/验证<a name="4登录退出登录注销验证"></a>


### 登录<a name="登录1"></a>


直接创建用户账户，无需注册过程。生成用于确认所有会员身份的MemberId，所生成的信息会被保存在FNUserInfo中返回。

定义LoginType

```c++
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

- Case 1

Request:

```c++

if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
FGamePotSDKPluginModule::GetSharedGamePotSdk()->Login(ENLoginType::Type loginType);

```

Response:

```c++
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
    // 请以弹窗等形式告知玩家NError.message。
}


// 维护（仪表盘的维护选项处于激活状态时调用）
void ASampleGameModeBase::OnLoginMaintenance(FNAppStatus NAppStatus)
{
   // 待进行事项：须基于参数传递的status信息创建弹窗并告知给用户。
    // 待进行事项：请从下列两种方式中选择一种。
    // 方式一：由开发商利用游戏内弹窗直接提供UI
    // 方式二：使用SDK的弹窗（这种情况下请调用下方代码。）

    IGamePotSdk* ptr = FGamePotSDKPluginModule::GetSharedGamePotSdk();
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
        ptr->showAppStatusPopup(NAppStatus.ToJsonString());
}

// 强制更新（商店版本和客户端版本不一致时调用）
void ASampleGameModeBase::OnLoginNeedUpdate(FNAppStatus NAppStatus)
{
     // 待进行事项：须基于参数传递的status信息创建弹窗并告知给用户。
    // 待进行事项：请从下列两种方式中选择一种。
    // 方式一：由开发商利用游戏内弹窗直接提供UI
    // 方式二：使用SDK自带的弹窗UI（这种情况下请调用下方代码。）

    IGamePotSdk* ptr = FGamePotSDKPluginModule::GetSharedGamePotSdk();
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
        ptr->showAppStatusPopup(NAppStatus.ToJsonString());
}

void ASampleGameModeBase::OnLoginExit()
{
   // 待进行事项：通过方式二实现强制更新或维护功能时
    // 待进行事项：考虑到可能需要强制终止应用的情况，请添加可以终止应用的代码。
}

void ASampleGameModeBase::OnAppClose()
{
    // 终止应用
    // 待进行事项：通过方式二实现强制更新或维护功能时
    // 待进行事项：考虑到可能需要强制终止应用的情况，请添加可以终止应用的代码。
}

```

定义NAppStatus

```c++
USTRUCT()
struct FNAppStatus
{
    UPROPERTY()
    FString type;       // AppStatus类型包括“maintenance”：维护，“needupdate”：更新
   
    UPROPERTY()
    FString message;    // 维护设置：在仪表盘输入的消息

    UPROPERTY()
    FString url;        // 维护设置：在仪表盘输入的URL
    
    UPROPERTY()
    FString currentAppVersion;  // 更新：当前的应用版本
    
    UPROPERTY()
    FString updateAppVersion;   // 更新：在仪表盘输入的应用版本
    
    UPROPERTY()
    int currentAppVersionCode;  // 更新：当前的应用代码
    
    UPROPERTY()
    FString updateAppVersionCode;   // 更新：在仪表盘输入的应用版本代码
    
    UPROPERTY()
    bool isForce;       // 更新：在仪表盘设置强制更新时，为true
    
    UPROPERTY()
    FString resultPayload;  // 客户端SDK传递的JSON值，可忽略。
    
    UPROPERTY()
    double startedAt;    // 维护：开始时间（timestamp）
    
    UPROPERTY()
    double endedAt;     // 维护：结束时间（timestamp）
}
```

### 自动登录<a name="自动登录"></a>


```c++
ENLoginType::Type loginType =  FGamePotSDKPluginModule::GetSharedGamePotSdk()->getLastLoginType();

if(loginType != ENLoginType::NONE) {
{
    // 以最后一次登录的类型登录的方式。
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->Login(loginType);
}
else
{
    // 第一次运行游戏或已退出登录的状态。请跳转到可以登录的登录页面。
}
```

### 退出登录<a name="退出登录"></a>


让用户退出登录。此功能不会删除账户，支持使用同一账户登录。

- Case 1

Request:

```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->Logout();
```

Response:

```csharp
void ASampleGameModeBase::OnLogoutSuccess()
{
}

void ASampleGameModeBase::OnLogoutFailure(FNError NError)
{
    // 退出登录失败时
    // 请以弹窗等形式告知玩家NError.message。
}
```

### 注销<a name="注销"></a>


注销会员，且不可恢复。

- Case 1

Request:

```c++

if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->deleteMember();
```

Response:

```c++
/// 会员注销成功
void ASampleGameModeBase::OnDeleteMemberSuccess()
{

}

void ASampleGameModeBase::OnDeleteMemberFailure(FNError NError)
{
   // 会员注销失败时
    // 请以弹窗等形式告知玩家NError.message。
}
```

### 验证<a name="验证"></a>


登录成功并由开发商服务器向GAMEPOT服务器传递登录信息后，即开始进行登录验证。

详细说明请参考Server to server api菜单中的`Token Authentication`一项。

## 5. 关联账户<a name="5关联账户"></a>


可以将一个游戏账户与多个社交账户（Google、Facebook等）关联或解除关联的功能。（须至少关联一个社交账户。）


>关联页面UI由开发商提供。


```c++
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
```

### 关联<a name="关联"></a>


可以使用Google/Facebook等社交网站的ID关联账户。

- Case 1

Request:

```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->createLinking(ENLinkingType::Type linkingType);
```

Response:

```c++
void ASampleGameModeBase::OnCreateLinkingSuccess(FNUserInfo NUserInfo) {
        // 账户关联成功
}

void ASampleGameModeBase::OnCreateLinkingCancel() {
        // 玩家取消账户关联时

}
void ASampleGameModeBase::OnCreateLinkingFailure(FNError NError) {
        // 账户关联失败时
        // 请以弹窗等形式告知玩家NError.message。
}

```

可以导入当前关联的所有账户信息。

```c++  
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
     TArray<FNLinkingInfo> linkedList = FGamePotSDKPluginModule::GetSharedGamePotSdk()->getLinkedList();
```

定义链接信息

```c++
USTRUCT()
struct FNLinkingInfo
{
    UPROPERTY()
    ENLinkingType::Type provider;      // 账户关联信息（Google、FaceBook、NAVER、Apple…）
}
```

### 解除关联<a name="解除关联"></a>


解除已有的账户关联。

- Case 1

Request :

```c++

if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->deleteLinking(ENLinkingType::Type linkType);

```

Response:

```c++

void ASampleGameModeBase::OnDeleteLinkingSuccess() {
/// 账户关联解除成功
}

void ASampleGameModeBase::OnDeleteLinkingFailure(FNError NError) {
    /// 账户关联解除失败
     // 解除关联失败时
    // 请以弹窗等形式告知玩家NError.message。
}
```

## 6. 支付<a name="6支付"></a>


### 查询应用内商品<a name="查询应用内商品"></a>


传递已添加至商店的商品信息。

启用此功能，可根据用户显示不同的价格、货币和商品名称。

```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    TArray<FNPurchaseItem> itemList = FGamePotSDKPluginModule::GetSharedGamePotSdk()->getPurchaseItems();
```

### 定义NPurchaseItem<a name="定义NPurchaseItem"></a>


定义NPurchaseItem

```c++
USTRUCT()
struct FNPurchaseItem
{
    UPROPERTY()
    FString productId;              // 商品ID

    UPROPERTY()
    FString type;                   // 商品类型，固定为“inapp”

    UPROPERTY()
    FString price;                  // 价格 Google商店：$0.99，其他商店：0.99

    UPROPERTY()
    FString price_amount;           // 货币代码 例如KRW、USD

    UPROPERTY()
    FString price_amount_micros;    // （在UI上显示时建议使用）货币与价格结合的值。如果是ONE Store，则不发送货币单位。例如$0.99

    UPROPERTY()
    FString price_currency_code;

    UPROPERTY()
    FString price_with_currency;

    UPROPERTY()
    FString title;                   // 商品名称

    UPROPERTY()
    FString description;            // 商品描述
}
```

### 支付应用内商品<a name="支付应用内商品"></a>


使用以下函数之一即可在Google、Apple和App Store中进行付费。

- Case 1

Request:

```c++
// productId：输入已添加至商店的商品ID。
// uniqueId：输入单独管理的发票号。
// serverId：输入进行付费的角色的服务器ID。
// playerId：输入进行付费的角色的角色ID。
// etc：输入进行付费的角色的其他信息。

if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->purchase(FString productId, FString uniqueId, FString serverId, FString playerId, FString etc);

```

### 定义FNPurchaseInfo<a name="定义FNPurchaseInfo"></a>

表示付费成功的道具信息。请用作参考。

```c++

USTRUCT()
struct FNPurchaseInfo
{
    UPROPERTY()
    FString price;                         // 付费道具的价格
    UPROPERTY()
    FString productId;                  // 付费道具的ID
    UPROPERTY()
    FString currency;                    // 支付价格货币（KRW/USD）
    UPROPERTY()
    FString orderId;                      // 商店的Order ID
    UPROPERTY()
    FString productName;            // 付费道具的名称
    UPROPERTY()
    FString gamepotOrderId;         // （GAMEPOT生成的）order id
    UPROPERTY()
    FString uniqueId;                    // （由开发商单独管理的）发票ID
    UPROPERTY()
    FString serverId;                    // （进行付费的角色的）服务器ID
    UPROPERTY()
    FString playerId;                    // （进行付费的角色的）角色ID
    UPROPERTY()
    FString etc;                         // （进行付费的角色的）其他信息
    UPROPERTY()
    FString signature;                  // 商店签名
    UPROPERTY()
    FString originalJSONData;   // 发票数据
}
```

Response:

```c++
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
       // 支付失败时
    // 请以弹窗等形式告知玩家NError.message。
 }
```

### 发放付费道具<a name="发放付费道具"></a>


GAMEPOT通过Server to server api在付费的商店完成发票验证后，才向开发商的服务器发送发放请求，因此不存在非法支付的问题。

为此必须参考`Server to server api`菜单的`Purchase Webhook`项目进行处理。

### 外部支付<a name="外部支付"></a>


此功能允许用户在支持外部支付的商店以及非官方商店进行支付。


>除了调用API以外，响应和Purchase Webhook等其他部分与常规支付相同。
>使用该功能之前，必须先进行设置。请参考仪表盘手册中的“外部支付”项目。


- Case 1

Request:

```csharp

```c++
// productId：已添加至商城的商品ID
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->purchaseThirdPayments(FString productId);
```

使用外部支付功能时，商品信息列表请使用以下API。

Request:

```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    TArray<FNPurchaseItem> itemList = FGamePotSDKPluginModule::GetSharedGamePotSdk()->getPurchaseThirdPaymentsItems();
```

## 7. 其他API<a name="7其他API"></a>


### SDK提供的登录UI<a name="SDK提供的登录UI"></a>


SDK自带（完成状态的）登录UI。

### 定义FNLoginUIInfo<a name="定义FNLoginUIInfo"></a>


```c++
USTRUCT()
struct FNLoginUIInfo
{
    //是否插入图片
    UPROPERTY()
    bool showLogo;

    //拟显示在UI上的登录类型
    UPROPERTY()
    TArray<ENLoginType::Type> loginTypes;  //Google、Facebook...
}
```

#### 调用SDK登录UI<a name="调用SDK登录UI"></a>


- Case 1

Request:

```c++
//拟调用的登录UI类型
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showLoginWithUI(FNLoginUIInfo NLoginUIInfo);
```

Response:

```c++
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
    // 请以弹窗等形式告知玩家error.message。
}
```

Response:

 **与一般登录API的响应逻辑相同。（但响应结果为onLoginCancel/onLoginFailure时，将在Native级别上以提醒消息形式进行处理。）**

```c++

void ASampleGameModeBase::OnLoginSuccess(FNUserInfo NUserInfo)
{
    // 登录成功
}

void ASampleGameModeBase::OnLoginCancel()
{
    // 取消登录
}

// 维护（仪表盘的维护选项处于激活状态时调用）
void ASampleGameModeBase::OnLoginMaintenance(FNAppStatus NAppStatus)
{
   // 待进行事项：须基于参数传递的status信息创建弹窗并告知给用户。
    // 待进行事项：请从下列两种方式中选择一种。
    // 方式一：由开发商利用游戏内弹窗直接提供UI
    // 方式二：使用SDK的弹窗（这种情况下请调用下方代码。）

    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
        FGamePotSDKPluginModule::GetSharedGamePotSdk()->showAppStatusPopup(NAppStatus.ToJsonString());
}

// 强制更新（商店版本和客户端版本不一致时调用）
void ASampleGameModeBase::OnLoginNeedUpdate(FNAppStatus NAppStatus)
{
     // 待进行事项：须基于参数传递的status信息创建弹窗并告知给用户。
    // 待进行事项：请从下列两种方式中选择一种。
    // 方式一：由开发商利用游戏内弹窗直接提供UI
    // 方式二：使用SDK的弹窗（这种情况下请调用下方代码。）

    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
        FGamePotSDKPluginModule::GetSharedGamePotSdk()->showAppStatusPopup(NAppStatus.ToJsonString());
}

void ASampleGameModeBase::OnLoginExit()
{
    // 待进行事项：结束LoginUI时
}

void ASampleGameModeBase::OnAppClose()
{
    // 终止应用
    // 待进行事项：通过方式二实现强制更新或维护功能时
    // 待进行事项：考虑到可能需要强制终止应用的情况，请添加可以终止应用的代码。
}

```


#### Customizing<a name="Customizing"></a>


**登录UI图片标志变更方法**

登录UI上方显示的图片标志是SDK自带的默认图片。用户可自行添加其他图片。

**[Android]**


>直接添加时，须按照`drawable`文件夹分别放入图片。（Android Asset Studio]([http://romannurik.github.io/AndroidAssetStudio/icons-notification.html#source.type=clipart&source.clipart=ac_unit&source.space.trim=1&source.space.pad=0&name=ic_stat_gamepot_login_logo可自动按照各文件夹制作图片，非常方便。](http://romannurik.github.io/AndroidAssetStudio/icons-notification.html#source.type=clipart&source.clipart=ac_unit&source.space.trim=1&source.space.pad=0&name=ic_stat_gamepot_login_logo可自动按照各文件夹制作图片，非常方便。)）



图片文件名应为ic_stat_gamepot_login_logo.png。

|文件夹名|大小|
| :------------------------------------------------------------- | :---- |
| $S(PluginDir)/ThirdParty/GamePotResources/res/drawable-mdpi/    | 24x24 |
| $S(PluginDir)/ThirdParty/GamePotResources/res/drawable-hdpi/    | 36x36 |
| $S(PluginDir)/ThirdParty/GamePotResources/res/drawable-xhdpi/   | 48x48 |
| $S(PluginDir)/ThirdParty/GamePotResources/res/drawable-xxhdpi/  | 72x72 |
| $S(PluginDir)/ThirdParty/GamePotResources/res/drawable-xxxhdpi/ | 96x96 |



### Apple登录（Android - Web登录）<a name="Apple登录AndroidWeb登录"></a>


#### GAMEPOT Dashboard<a name="GAMEPOTDashboard"></a>


在仪表盘上的项目设置 >> 常规 >> Apple ID Login下进行设置。


>为了使用此功能，必须先设置Apple Developer Console。

>请参考仪表盘上相应项目的**查看帮助**。



GamePot_Android_UPL.xml 修整

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

在$S(PluginDir)/ThirdParty/Android/libs 路径下添加以下aar文件。

- gamepot-channel-apple-signin.aar


### NAVER登录<a name="NAVER登录"></a>


#### Naver Developers<a name="NaverDevelopers"></a>

使用API选择`NAVER ID登录`后添加应用程序

#### Android<a name="Android3"></a>


修改GamePot_Android_UPL.xml

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


将从控制台发放的Client ID输入`gamepot_naver_clientid`中、Client Secret输入`gamepot_naver_secretid`中。

在$S(PluginDir)ThirdParty/Android/libs路径下添加以下aar文件。

- gamepot-channel-naver.aar



#### iOS<a name="iOS3"></a>


GamePotSDKPlugin.Build.cs 修整

```csharp
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

在GamePotConfig-Info.plist文件中添加以下项目并输入相应值。

```text
gamepot_naver_clientid // 拟在NAVER使用的Client ID
gamepot_naver_secretid // 拟在NAVER使用的Secret ID
gamepot_naver_urlscheme // 拟在NAVER使用的URL Scheme
```

用SourceCode查看GamePotConfig-Info.plist文件时按如下形式添加

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

### LINE登录<a name="LINE登录"></a>


#### LINE Developers<a name="LINEDevelopers"></a>


在LINE控制台添加构建APK时使用的包名和Keystore中的SHA值、URL Scheme值。

#### Android<a name="Android4"></a>


修改GamePot_Android_UPL.xml

GamePot_Android_UPL.xml  修整

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

在$S(PluginDir)/ThirdParty/Android/libs 路径下添加以下aar文件。

- gamepot-channel-line.aar
- line-sdk-4.0.10.aar


#### iOS<a name="iOS4"></a>

GamePotSDKPlugin.Build.cs 修整

```csharp
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

在GamePotConfig-Info.plist文件中添加以下项目并输入相应值。

```text
gamepot_line_channelid // 拟在NAVER使用的Client ID
gamepot_line_url_schemes // LINE URL Scheme(line3rdp.{项目包Identifier})
```

用SourceCode查看GamePotConfig-Info.plist文件时按如下形式添加即可。

```markup
...
<key>gamepot_line_channelid</key>
<string>xxxxxx</string>
<key>gamepot_line_url_schemes</key>
<string>xxxxxx</string>
...
```

### Twitter登录<a name="Twitter登录"></a>


#### Twitter Developers<a name="TwitterDevelopers"></a>


#### Android<a name="Android5"></a>

修改GamePot_Android_UPL.xml

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


在$S(PluginDir)/ThirdParty/Android/libs路径下添加以下aar文件。

- gamepot-channel-twitter.aar
- twitter-core-3.3.0.aar



#### iOS<a name="iOS5"></a>


GamePotSDKPlugin.Build.cs 수정

```csharp
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

在GamePotConfig-Info.plist文件中添加以下项目并输入相应值。

```text
gamepot_twitter_consumerkey : Twitter Consumer Key
gamepot_twitter_consumersecret :  Twitter Consumer Secret
```

用SourceCode查看GamePotConfig-Info.plist文件时按如下形式添加

```markup
...
<key>gamepot_twitter_consumerkey</key>
<string>xxxxxx</string>
...
```

### 优惠券<a name="优惠券"></a>


#### 使用优惠券<a name="使用优惠券"></a>



>输入优惠券的UI由开发商提供。



- Case 1

Request:

```c++
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    {
        FGamePotSDKPluginModule::GetSharedGamePotSdk()->coupon(FString couponNumber); // 优惠券号码

        FGamePotSDKPluginModule::GetSharedGamePotSdk()->coupon(FString couponNumber, FString userData); // 优惠券号码、用户信息
    }
```

Response:

```c++
void ASampleGameModeBase::OnCouponSuccess(FString msg)
{
    /// 优惠券使用成功
}

void ASampleGameModeBase::OnCouponFailure(FNError NError)
{
      // 优惠券使用失败时
    // 请以弹窗等形式告知玩家error.message。
}
```

#### 发放道具<a name="发放道具"></a>


优惠券使用成功时，程序将通过Server to server api向开发商的服务器发送道具发放请求。

为此，须参考Server to server api菜单的`Item Webhook`项目进行处理。

### Push on/off<a name="Pushonoff"></a>


推送和夜间推送可以分别进行开启/关闭处理。


>设置开启/关闭的UI由开发商提供。



#### 推送设置<a name="推送设置"></a>


- Case 1

Request:

```c++
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
        FGamePotSDKPluginModule::GetSharedGamePotSdk()->setPushStatus(bool pushEnable);
```

Response:

```c++
void ASampleGameModeBase::OnPushSuccess()
{
    /// 对推送状态变更的服务器通信成功
}

void ASampleGameModeBase::OnPushFailure(FNError NError)
{
        // 推送状态变更失败时
    // 请以弹窗等形式告知玩家error.message。
}
```


#### 夜间推送设置<a name="夜间推送设置"></a>


- Case 1

Request:

```c++
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
        FGamePotSDKPluginModule::GetSharedGamePotSdk()->setPushNightStatus(bool nightPushEnable);
```

Response:

```c++
void ASampleGameModeBase::OnPushNightSuccess()
{
    /// 对推送状态变更的服务器通信成功
}

void ASampleGameModeBase::OnPushNightFailure(FNError NError)
{
        // 推送状态变更失败时
    // 请以弹窗等形式告知玩家error.message。
}
```

#### 广告推送设置<a name="广告推送设置"></a>


- Case 1

Request:

```c++
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
        FGamePotSDKPluginModule::GetSharedGamePotSdk()->setPushADStatus(bool adPushEnable);
```

Response:

```c++
void ASampleGameModeBase::OnPushAdSuccess()
{
    /// 对推送状态变更的服务器通信成功
}

void ASampleGameModeBase::OnPushFailure(FNError NError)
{
        // 推送状态变更失败时
    // 请以弹窗等形式告知玩家error.message。
}
```

#### 推送/夜间推送/广告推送同时设置<a name="推送/夜间推送/广告推送同时设置"></a>


如果是登录前需要获得推送/夜间推送权限的游戏，登录后必须调用以下代码。

- Case 1

Request:

```c++
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
        FGamePotSDKPluginModule::GetSharedGamePotSdk()->setPushStatus(bool pushEnable, bool nightPushEnable, bool adPushEnable);
```

Response:

```c++
void ASampleGameModeBase::OnPushStatusSuccess()
{
    /// 对推送状态变更的服务器通信成功
}

void ASampleGameModeBase::OnPushStatusFailure(FNError NError)
{
        // 推送状态变更失败时
    // 请以弹窗等形式告知玩家error.message。
}
```

#### 查询推送状态<a name="查询推送状态"></a>

- 定义FNPushInfo

```c++
USTRUCT()
struct FNPushInfo
{
    UPROPERTY()
    bool enable;       // 是否允许（一般）推送

    UPROPERTY()
    bool night;         // 是否允许夜间推送

    UPROPERTY()
    bool ad;            // 是否允许广告推送
}
```

Request:

```c++
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
        FNPushInfo NPushInfo = FGamePotSDKPluginModule::GetSharedGamePotSdk()->getPushStatus();
```

### 公告事项<a name="公告事项"></a>


利用此功能，可在GAMEPOT仪表盘上依次显示添加至“公告事项”的图片。

图片规格建议如下。

- 尺寸：720 _1200（竖屏）/1280_ 640（横屏）


>如果不符合上述尺寸，将采用Center Crop方式处理图片。



- 大小：250KB以下

Request:

```c++

if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showNotice(bool showToday = true);

// true：应用“今日不再显示”
// false：与“今日不再显示”无关，强制显示
```

```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showEvent(FString Type);

// Type：仅显示与“仪表盘公告事项 >> 分类”中的分类名称相对应的图片
```

Response:

GAMEPOT仪表盘上如果将`点击操作`设为`SCHEME`，点击相应图片时将传递`SCHEME`值。

```c++
 void ASampleGameModeBase::OnReceiveScheme(FString scheme)
 {
      // 传递在GAMEPOT仪表盘设置的scheme值
 }
```

### 客户支持<a name="客户支持"></a>


此功能可以帮助客户向运营商提交问题并接收答复。

客户咨询UI按照设备语言变更显示。支持韩语、英语、日语、中文（简体、繁体），其他语言以英文显示。

#### 调用<a name="调用1"></a>


```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showCSWebView();
```

支持外部链接，未登录的客户也可以提交咨询问题。

#### 调用<a name="调用2"></a>


```c++
// url：GAMEPOT发放的外部客户支持URL
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showWebView(FString url);
```

### 本地推送（本地推送通知）<a name="本地推送本地推送通知"></a>


此功能可绕过推送服务器，直接在终端显示推送。

#### 添加推送<a name="添加推送"></a>


在指定时间显示本地推送的方法如下。


>返回的pushId值由开发商进行管理。



```c++
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
         int pushId = FGamePotSDKPluginModule::GetSharedGamePotSdk()->sendLocalPush(FString date, FString title, FString message);

// date : (Format - timestamp "yyyy-MM-dd HH:mm:ss")
// ex >  DateTime.Parse("2018-01-01 00:00:00")
//  title :  "title"
// message :  "content"
```

#### 取消已添加的推送<a name="取消已添加的推送"></a>


利用添加推送时获取的pushId可取消已添加的推送。

```c++
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
         bool success = FGamePotSDKPluginModule::GetSharedGamePotSdk()->cancelLocalPush(int /*添加推送时获取的pushId*）;
```


### Image Push (iOS)<a name="ImagePush"></a>

Unreal没有为项目添加 Notification Service Extension
无法使用 iOS Image Push 功能 。

### 条款同意<a name="条款同意"></a>


为了便于征得“使用条款”和“个人信息收集与使用指南”同意，提供相应UI。

除了`BLUE`与`GREEN`两种`默认主题`以外，还新增了11种`更新主题`。

各模块还支持自定义。

#### 调用条款同意<a name="调用条款同意"></a>

#### 定义FNAgreeInfo<a name="定义FNAgreeInfo"></a>


```c++
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
    
    // 图标图片的文件名（aos - drawable/ios - bundle）
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
  
    // 图标图片的文件名（aos - drawable/ios - bundle）
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


>请开发商根据游戏情况决定是否弹出条款同意窗口。

>点击“查看”按钮时显示的内容可以在仪表盘上应用和修改。



- Case 1

Request:

```c++

// 方式一. 一般调用（应用BLUE主题）
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showAgreeDialog();

// 方式二. 应用其他主题时
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
```

Response:

```c++
// 同意条款时
void ASampleGameModeBase::OnAgreeDialogSuccess(FNAgreeResultInfo NAgreeResultInfo)
{
       // NAgreeResultInfo.agree：同意全部强制条款时为true
        // NAgreeResultInfo.agreePush：勾选同意接收（一般）推送时为true，否则为false
        // NAgreeResultInfo.agreeNight：勾选同意接收夜间广告类推送时为true，否则为false
        // agreeNight值请在登录成功后通过setPushNightStatus API传递。
}

void ASampleGameModeBase::OnAgreeDialogFailure(FNError NError)
{
    // 发生错误
}
```

-  Customizing

各个变量将应用到以下区域。


> contentIconDrawable只在AOS中显示，默认值为推送图标。



![gamepot_unreal_002_zh.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_unreal_002_zh.png)


### 使用条款<a name="使用条款"></a>


调用使用条款UI。


>请先在“仪表盘 - 客户支持 - 使用条款设置”中输入内容。



```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showTerms();
```

### 隐私政策<a name="隐私政策"></a>


调用隐私政策UI。


>请先在“仪表盘 - 客户支持 -隐私政策设置”中输入内容。



```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showPrivacy();
```

### 退款规定<a name="退款规定"></a>


调用退款规定UI。


>请先在“仪表盘 - 客户支持 - 退款规定设置”中输入内容。



```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showRefund();
```

### 远程配置<a name="远程配置"></a>


从客户端获取添加至仪表盘的参数值。


>在“仪表盘 - 设置 - 远程配置”界面添加参数。

>添加的参数会在登录时加载，之后可以被调用。



```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
{
    //"test_01"：参数FString
    FString value = FGamePotSDKPluginModule::GetSharedGamePotSdk()->getConfig("test_01");

    //以json string格式获取添加至仪表盘的所有参数。
    FString json_value = FGamePotSDKPluginModule::GetSharedGamePotSdk()->getConfigs();
}
```

### 恶意使用支付取消的用户自动终止功能<a name="恶意使用支付取消的用户自动终止功能"></a>


提供恶意使用支付取消的用户自动终止功能UI。可以按各区域进行定制。


>仅限Google支付，玩家随意向Google发送支付取消请求时，可通过“取消Google支付”功能冻结该玩家账户。

>此时该玩家登录时，通过SDK显示的弹窗引导玩家重新支付相应道具，

>完成支付时，则允许其继续正常登录。

>玩家重新支付所有已取消支付的项目时，将自动解除冻结。



### 定义NVoidInfo<a name="定义NVoidInfo"></a>


```c++
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

```c++
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

### 发送游戏日志<a name="发送游戏日志"></a>


添加游戏中使用的信息后调用时，可在`仪表盘` - `游戏`中进行查询。

下面是可使用的保留字定义表。

|保留字|选项|类型|描述|
| :-------------------------------- | :--- | :----- | :----------- |
|FNSendLogCharacter.NAME      |必选|FString |角色名|
|FNSendLogCharacter.LEVEL     |可选|FString |级别|
|FNSendLogCharacter.SERVER_ID |可选|FString |服务器ID|
|FNSendLogCharacter.PLAYER_ID |可选|FString |角色ID|
|FNSendLogCharacter.USERDATA  |可选|FString |ETC          |

### 定义FNSendLogCharacter<a name="定义FNSendLogCharacter"></a>


```c++
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
```

```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
{
    FNSendLogCharacter info;
    info.NAME = TEXT("tester");
    info.PLAYER_ID = TEXT("player_id");

    bool result = FGamePotSDKPluginModule::GetSharedGamePotSdk()->characterInfo(info.ToJsonString());

    // Result is TRUE : validation success.Logs will send to GamePot Server
    // Result is FALSE : validation was failed.Please check logcat
}

```

### GDPR条款确认列表<a name="GDPR条款确认列表"></a>


以列表形式导入在仪表盘上激活的GDPR条款项目。

```c++
//返回的数据类型和形式分别为FString和string[]。例如："[ gdpr_privacy, gdpr_term ]"
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FString gdpr_list = FGamePotSDKPluginModule::GetSharedGamePotSdk()->getGDPRCheckedList();

// gdpr_privacy：隐私政策
// gdpr_term：使用条款
// gdpr_gdpr：GDPR使用条款
// gdpr_push_normal：同意接收事件推送
// gdpr_push_night：同意接收夜间事件推送（仅限韩国）
// gdpr_adapp_custom：同意接收个人精准广告投放（GDPR实施国家）
// gdpr_adapp_nocustom：同意接收个人精准投放以外的一般广告（GDPR实施国家）
```

## 附录<a name="附录"></a>


### 支持第三方SDK关联<a name="支持第三方SDK关联"></a>


## 登录<a name="登录2"></a>



>不支持自动登录。需要每次调用。



|参数名|选项|类型|描述|
| :--------- | :--- | :----- | :----------------- |
|userid     |必选|FString |玩家的唯一ID|

```c++
FString userid = TEXT("memberid of 3rd party sdk");

if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->loginByThirdPartySDK(userid);
```

## 支付<a name="支付"></a>



>付费道具必须已添加至GAMEPOT仪表盘。



|参数名|选项|类型|描述|
| :------------ | :--- | :----- | :----------------------------------------- |
|productid     |必选|FString |已添加至GAMEPOT仪表盘的道具ID|
|transactionid |必选|FString |付费发票号（GPA-xxx-xxxx-xxxx）|
|store         |必选|FString |（付费商店 - Google、Apple、ONE、Galaxy）|
|currency      |可选|FString |货币（KRW、USD）|
|price         |可选|double |付费道具的金额|
|paymentid     |可选|FString |支付ID（一般与store_id相同）|
|uniqueid      |可选|FString |开发商使用的唯一ID|

```c++
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
