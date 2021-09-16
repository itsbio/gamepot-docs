## Set preferences<a name="Setpreferences"></a>


### Android<a name="Android1"></a>


```d
minSdkVersion : API 17 (Jelly Bean, 4.2)
```

**How to configure project settings**

Open the file /Plugin/GamePotSDKPlugin/Source/GamePot/GamePot_Android_UPL.xml in your editor.

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
         resValue "string", "gamepot_naver_clientid", ""                               // optional (get from the NAVER developer console)
         resValue "string", "gamepot_naver_secretid", ""                              // optional (get from the NAVER developer console)
         resValue "string", "gamepot_line_channelid",""                               // optional (get from the LINE developer console)
         resValue "string", "gamepot_twitter_consumerkey", ""                   // optional (get from the Twitter developer console)
         resValue "string", "gamepot_twitter_consumersecret", ""               // optional (get from the Twitter developer console)
         resValue "string", "gamepot_elsa_projectid", ""                              // optional (ncp elsa)
    }
    ...
}
  </insert>
</buildGradleAdditions>
```

Edit the following required values. These values must be edited for the project to work.

```java
resValue "string", "[key]", "[value]"
```

| Value                          | Description                                                  |
| :----------------------------- | :----------------------------------------------------------- |
| gamepot_project_id             | Enter a project ID issued from GAMEPOT.                      |
| gamepot_store                  | Store value \(`google`, `one`, or `galaxy`\)                 |
| gamepot_app_title              | App title \(FCM\)                                            |
| gamepot_push_default_channel   | Default channel name registered \(Default\) - Do not change. |
| facebook_app_id                | App ID issued from Facebook                                  |
| fb_login_protocol_scheme       | Protocol scheme fb[app_id] issued from Facebook              |
| gamepot_naver_clientid         | Get from the NAVER developer console                         |
| gamepot_naver_secretid         | Get from the NAVER developer console                         |
| gamepot_line_channelid         | Get from the LINE developer console                          |
| gamepot_twitter_consumerkey    | Get from the Twitter developer console                       |
| gamepot_twitter_consumersecret | Get from the Twitter developer console                       |
| gamepot_elsa_projectid         | Project ID when using NCLOUD ELSA \([View more](https://www.ncloud.com/product/analytics/elsa)\) |

|

**How to change the push icon in the notification bar**

![gamepot_unreal_003.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_unreal_003%281%29.png)


When you receive a push notification, a small icon shown as the default image inside the SDK is displayed on the Android notification bar. You can also choose a custom image for the game.

If you would like to specify your own image, add them to each `drawable` folder. You can easily and automatically create images for each folder using \([Android Asset Studio](http://romannurik.github.io/AndroidAssetStudio/icons-notification.html#source.type=clipart&source.clipart=ac_unit&source.space.trim=1&source.space.pad=0&name=ic_stat_gamepot_small).\)

The image file name should be specified as ic_stat_gamepot_small.

| Folder name                                                  | Size  |
| :----------------------------------------------------------- | :---- |
| $S(PluginDir)/ThirdParty/Android/GamePotResources/res/drawable-mdpi/ | 24x24 |
| $S(PluginDir)/ThirdParty/Android/GamePotResources/res/drawable-hdpi/ | 36x36 |
| $S(PluginDir)/ThirdParty/Android/GamePotResources/res/drawable-xhdpi/ | 48x48 |
| $S(PluginDir)/ThirdParty/Android/GamePotResources/res/drawable-xxhdpi/ | 72x72 |
| $S(PluginDir)/ThirdParty/Android/GamePotResources/res/drawable-xxxhdpi/ | 96x96 |


### iOS<a name="iOS1"></a>

**How to configure project settings**

Copy the `GoogleService-Info.plist` file downloaded from Google Firebase to `/Plugin/GamePotSDKPlugin/Source/GamePot/ThirdParty/iOS/`.

Add the required environment variables in `$S(PluginDir)/ThirdParty/iOS/GamePotResources.embeddedframework/Resources/GamePotConfig-Info.plist`.

![gamepot_unreal_001.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_unreal_001%281%29.png)


| Environment variable           | Description                                             |
| :----------------------------- | :------------------------------------------------------ |
| gamepot_project_id             | Enter a project ID issued from GAMEPOT.                 |
| gamepot_facebook_app_id        | App ID issued from Facebook                             |
| gamepot_facebook_display_name  | Name displayed in Facebook                              |
| gamepot_google_app_id          | CLIENT_ID value of the GoogleService-Info file          |
| gamepot_google_url_schemes     | REVERSED_CLIENT_ID value of the GoogleService-Info file |
| gamepot_facebook_app_id        | Facebook App ID                                         |
| gamepot_facebook_display_name  | Facebook display name                                   |
| gamepot_naver_clientid         | Naver Client Id                                         |
| gamepot_naver_secretid         | Naver Secret Id                                         |
| gamepot_naver_urlscheme        | Naver Url Scheme                                        |
| gamepot_line_channelid         | Line Channel ID                                         |
| gamepot_line_url_schemes       | LINE URL scheme (line3rdp.{project bundle ID})          |
| gamepot_twitter_consumerkey    | Twitter Consumer Key                                    |
| gamepot_twitter_consumersecret | Twitter Consumer Secret                                 |
| gamepot_elsa_projectid         | Project ID when using NCLOUD ELSA                       |

|

Compress `GamePotResources.embeddedframework` as **.zip**
and proceed with the build while it is placed
in the `$S(PluginDir)/ThirdParty/iOS/GamePotResources.embeddedframework.zip` path.

Before an iOS build,

Please `add the option to obtain user permission` below in Project settings >> iOS >> Extra PList Data >> Additional Plist Data.

The user permissions are used for uploading files in the GAMEPOT customer center.

```text
<key>NSCameraUsageDescription</key>
<string>$(PRODUCT_NAME) camera use.</string>
<key>NSPhotoLibraryUsageDescription</key>
<string>$(PRODUCT_NAME) photo library use.</string>
```

iOS 14 or higher version

From iOS 14, when acquiring IDFA values, a permission needs to be acquired from the user

in order to acquire an IDFA value.

Therefore, if you're using a pop-up to acquire permissions from the user when acquiring IDFA values,
Please `add the option to obtain user permission` below in Project settings >> iOS >> Extra PList Data >> Additional Plist Data.


09/11/2020
Mandatory application for the pop-ups acquiring permissions from the user when acquiring IDFA values from Apple has been postponed to early 2021.
Please refer to the link below.
https://developer.apple.com/news/?id=hx9s63c5



```text
<key>NSUserTrackingUsageDescription</key>
<string>$(PRODUCT_NAME) This identifier will collect IDFA for advertising purposes.</string>
```

IDFA permissions request pop-up call (explicit)

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

> `For iOS platforms,` an explicit pop-up request asking permissions for the IDFA value acquisition is initially displayed when the login API is called.

> Please modify the `FIOSGamePotSdk::Login(ENLoginType::Type)` function if you do not wish to call the pop-up request at the time of login. `$S(PluginDir)/Private/iOS/IOSGamePotSdk.cpp`

```c++
void FIOSGamePotSdk::Login(ENLoginType::Type _loginType)
{
    //Explicitly display the IDFA pop-up before login <-- Annotate when necessary
    FIOSGamePotSdk::requestTrackingAuthorization();
    ...
```

For iOS, permissions for receiving push notifications must be acquired by the user in advance.
At an appropriate time (e.g., login success), call the following function for requesting permissions.

```c++
if(LOGIN_SUCCESS)
{
    //Explicitly request push notification permissions to be acquired
    FPlatformMisc::RegisterForRemoteNotifications();
}
```

## 1. Reset<a name="1Reset"></a>


Add the following code to the object used in the first scene (level) loaded when the game starts.

 - E.g., "ASampleGameModeBase.h"

```c++
//Callback Event Listener declaration for the GAMEPOT API (used in the level)UCLASS()class GAMEPOTSDKSAMPLE_API ASampleGameModeBase : public AGameModeBase{    ...      void OnLoginSuccess(FNUserInfo NUserInfo);   void OnLoginCancel();   void OnLoginFailure(FNError NError);   void OnLoginMaintenance(FNAppStatus NAppStatus);   void OnLoginNeedUpdate(FNAppStatus NAppStatus);   void OnLoginExit();   ...};
```

 - E.g., "ASampleGameModeBase.cpp"

```c++
#include "GamePotSDKPluginModule.h"

void ASampleGameModeBase::InitGame(const FString& MapName, const FString& Options, FString& ErrorMessage)
{
    AGameModeBase::InitGame(MapName, Options, ErrorMessage);

     //Bind (the Event Listener declared in the header) to GamePotPluginModule's Callback Event Listener
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

List of (binding) Event Listeners

```c++
    // Login succeeded
    FOnSdkLoginSuccess OnSdkLoginSuccess(FNUserInfo NUserInfo);     
    // Login canceled            
    FOnSdkLoginCancel OnSdkLoginCancel(); 
    // Login failed                                     
    FOnSdkLoginFailure OnSdkLoginFailure(FNError NError);   
    // Login (maintenance)                   
    FOnSdkLoginMaintenance OnSdkLoginMaintenance(FNAppStatus NAppStatus);
    // Login (update)      
    FOnSdkLoginNeedUpdate OnSdkLoginNeedUpdate(FNAppStatus NAppStatus);   
    // Login UI close (when using showLoginWithUI)     
    FOnSdkLoginExit OnSdkLoginExit();         
    // Close app (if during maintenance or update)                                      
    FOnSdkAppClose OnSdkAppClose();   

    // Logout success                                                                          
    FOnSdkLogoutSuccess OnSdkLogoutSuccess();   
    // Logout failed                               
    FOnSdkLogoutFailure OnSdkLogoutFailure(FNError NError);      

    // Close showWebview          
    FOnWebviewClose OnSdkWebviewClose(FString msg);

    // Purchase success
    FOnSdkPurchaseSuccess OnSdkPurchaseSuccess(FNPurchaseInfo NPurchaseInfo);
    // Purchase canceled
    FOnSdkPurchaseCancel OnSdkPurchaseCancel();
    // Purchase failed
    FOnSdkPurchaseFailure OnSdkPurchaseFailure(FNError NError);  

    // getPurchaseDetailListAsync succeeded
    FOnSdkPurchaseDetailListSuccess OnSdkPurchaseDetailListSuccess(TArray<FNPurchaseItem> Items);
    // getPurchaseDetailListAsync failed
    FOnSdkPurchaseDetailListFailure OnSdkPurchaseDetailListFailure(FNError NError);

    // createLinking succeeded
    FOnSdkCreateLinkingSuccess OnSdkCreateLinkingSuccess(FNUserInfo NUserInfo);
    // createLinking canceled
    FOnSdkCreateLinkingCancel OnSdkCreateLinkingCancel();
    // createLinking failed
    FOnSdkCreateLinkingFailure OnSdkCreateLinkingFailure(FNError NError);

    // deleteLinking succeeded
    FOnSdkDeleteLinkingSuccess OnSdkDeleteLinkingSuccess();
    // deleteLinking failed
    FOnSdkDeleteLinkingFailure OnSdkDeleteLinkingFailure(FNError NError);

    // Call back the click action scheme on notice images (showNotice, showEvent)
    FOnSdkReceiveScheme OnSdkReceiveScheme(FString scheme);

    // deleteMember succeeded
    FOnSdkDeleteMemberSuccess OnSdkDeleteMemberSuccess();
    // deleteMember failed
    FOnSdkDeleteMemberFailure OnSdkDeleteMemberFailure(FNError NError);

    // Coupon (use) succeeded
    FOnSdkCouponSuccess OnSdkCouponSuccess(FString msg);
    // Coupon (use) failed
    FOnSdkCouponFailure OnSdkCouponFailure(FNError NError);

    // showAgreeDialog (Terms and Conditions agreement status) renewal succeeded
    FOnAgreeDialogSuccess OnSdkAgreeDialogSuccess(FNAgreeResultInfo NAgreeResultInfo);
    // showAgreeDialog (Terms and Conditions agreement status) renewal failed
    FOnAgreeDialogFailure OnSdkAgreeDialogFailure(FNError NError);

    // setPush succeeded
    FOnPushSuccess OnSdkPushSuccess();
    // setPushAdStatus succeeded
    FOnPushAdSuccess OnSdkPushAdSuccess();
    // setPushNightStatus succeeded
    FOnPushNightSuccess OnSdkPushNightSuccess();
    // setPushStatus succeeded
    FOnPushStatusSuccess OnSdkPushStatusSuccess();

    // setPush failed
    FOnPushFailure OnSdkPushFailure(FNError NError);
    // setPushAdStatus failed
    FOnPushAdFailure OnSdkPushAdFailure(FNError NError);
    // setPushNightStatus failed
    FOnPushNightFailure OnSdkPushNightFailure(FNError NError);
    // setPushStatus failed
    FOnPushStatusFailure OnSdkPushStatusFailure(FNError NError);
```

NUserInfo definition

```c++
USTRUCT()
struct FNUserInfo
{
    UPROPERTY()
    FString memberid;           // Member ID (user’s unique ID)                   
    UPROPERTY()
    FString name;               // Name
    UPROPERTY()
    FString profileUrl;         // Profile URL (if it exists)                     
    UPROPERTY()
    FString email;              // Email (if it exists)
    UPROPERTY()
    FString token;              // Token for checking user validity (used in Token AuthenticationAPI)
    UPROPERTY()
    FString userid;             // Social media ID (Google, Facebook, etc.)
}
```

## 2. Error codes<a name="2Errorcodes"></a>


NError definition

```c++
USTRUCT()
struct FNError
{
    //Detail Error code
    static const int CODE_UNKNOWN_ERROR = 0;                    // Unknown error
    static const int CODE_NOT_INITALIZE = 1;                    // Initialization failed
    static const int CODE_INVAILD_PARAM = 2;                    // Invalid parameter
    static const int CODE_MEMBERID_IS_EMPTY = 3;                    // No member ID data
    static const int CODE_NOT_SIGNIN = 4;                    // Not logged in
    static const int CODE_NETWORK_MODULE_NOT_INIT = 3000;                 // Network module is not initialized
    static const int CODE_NETWORK_ERROR = 3001;                 // Network connection error or timeout occurred
    static const int CODE_SERVER_ERROR = 4000;                 // Error occurred in server-side
    static const int CODE_SERVER_HTTP_ERROR = 4001;                 // When http response code is not successful
    static const int CODE_SERVER_NETWORK_ERROR = 4002;                 // Network connection error or timeout occurred
    static const int CODE_SERVER_PARSING_ERROR = 4003;                 // Error occurred when parsing data received from the server
    static const int CODE_CHARGE_UNKNOWN_ERROR = 5000;                 // When an unknown error occurred during payment or an error is received from the store
    static const int CODE_CHARGE_PRODUCTID_EMPTY = 5001;                 // No product ID specified
    static const int CODE_CHARGE_PRODUCTID_WRONG = 5002;                 // Incorrect product ID
    static const int CODE_CHARGE_CONSUME_ERROR = 5003;                 // Error occurred upon consuming

    UPROPERTY()
    int code;               // error Code

    UPROPERTY()
    FString message;        // error Message
}
```

## 3. Set up login environment<a name="3Setuploginenvironment"></a>


### Google login<a name="Googlelogin"></a>


#### Google Firebase Console<a name="GoogleFirebaseConsole"></a>

1. Copy google-service.json file for Android downloaded from Google Firebase Console to `/Plugins/GamePotSDKPlugin/Source/GamePot/ThirdParty/Android/`.
2. Add the SHA-1 value of the keystore used when your APK is built to Google Firebase Console.

**If you see a notification from onCancel when logging in to Google and you are unable to log in**, please check the following:

1. Check if the requested google-service.json file is applied correctly.
2. Verify that the keystore used during build is the one from which the SHA-1, registered in Google Firebase Console, is extracted.
3. Verify that the build was made with the package name registered in Google Firebase Console.


#### Android

Modify GamePot_Android_UPL.xml

```xml
...<resourceCopies>    <copyFile src="$S(PluginDir)/ThirdParty/Android/libs/gamepot-channel-google-signin.aar" dst="$S(BuildDir)/libs/gamepot-channel-google-signin.aar" /></resourceCopies>...<buildGradleAdditions>    <insert>        ...        dependencies {            ...            implementation(name: 'gamepot-channel-google-signin', ext: 'aar')            ...        }        ...    </insert></buildGradleAdditions>...
```

#### IOS

1. Decompress `$S(PluginDir)/ThirdParty/iOS/GamePotResouces.embeddedframework.zip`.

2. Download the GoogleService-Info.plist file for iOS, copy to the `$S(PluginDir)/ThirdParty/iOS/GamePotResouces.embeddedframework/Resources/` path, and **recompress**.

![gamepot_unreal_004.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_unreal_004.png)


### Facebook login<a name="Facebooklogin"></a>


#### Facebook Developer Console<a name="FacebookDeveloperConsole"></a>


Add the key hash value of the keystore, used when your APK is built, to the Facebook console.

#### Android<a name="Android2"></a>


Edit GamePot_Android_UPL.xml

```xml
...<resourceCopies>        <copyFile src="$S(PluginDir)/ThirdParty/Android/libs/gamepot-channel-facebook.aar" dst="$S(BuildDir)/libs/gamepot-channel-facebook.aar" /></resourceCopies>......<buildGradleAdditions>    <insert>        ...        dependencies {            ...            implementation(name: 'gamepot-channel-facebook', ext: 'aar')            ...        }        ...        defaultConfig {            resValue "string", "facebook_app_id", "1234567890"            resValue "string", "fb_login_protocol_scheme", "fb1234567890"        }        ...    </insert></buildGradleAdditions>...<gameActivityImportAdditions>  <insert>    import io.gamepot.channel.facebook.GamePotFacebook;  </insert></gameActivityImportAdditions>
```

#### iOS<a name="iOS2"></a>


Add the following items to GamePotConfig-Info.plist file to enter the value.

```text
gamepot_facebook_app_id // App ID issued from Facebook developer console
```

If viewing GamePotConfig-Info.plist with SourceCode, add the following.

```markup
...<key>gamepot_facebook_app_id</key><string>xxxxxx</string>...
```


### Apple login<a name="Applelogin"></a>



>This features is for iOS only. (For Android, it is supported as web login)



**Add the flag value as follows in the ` [/Script/IOSRuntimeSettings.IOSRuntimeSettings] ` field in Config/DefaultEngine.ini.**


>bEnableSignInWithAppleSupport=True



## 4. Login/Logout/Withdrawal/Validation<a name="4LoginLogoutWithdrawalValidation"></a>


### Login<a name="Login1"></a>


Create a user account without any additional subscription process. It creates a MemberId to identify users and returns the created information in FNUserInfo.

LoginType definition

```c++
UENUM()namespace ENLoginType{    enum Type    {        NONE,        GOOGLE,        GOOGLEPLAY,        FACEBOOK,        NAVER,        GAMECENTER,        TWITTER,        LINE,        APPLE,        GUEST,        THIRDPARTYSDK,        STANDALONE    };}
```

- Case 1

Request:

```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())FGamePotSDKPluginModule::GetSharedGamePotSdk()->Login(ENLoginType::Type loginType);
```

Response:

```c++
void ASampleGameModeBase::OnLoginSuccess(FNUserInfo NUserInfo){    // Login succeeded}void ASampleGameModeBase::OnLoginCancel(){    // Login canceled}void ASampleGameModeBase::OnLoginFailure(FNError NError){   // Login failed    // Provide NError.message to the user in a pop-up or other means.}// Check (call this when Check is enabled in the dashboard.)void ASampleGameModeBase::OnLoginMaintenance(FNAppStatus NAppStatus){   // To do: Notify the user with a pop-up based on the status information passed in a parameter.    // To do: Choose between the following two methods.    // Case 1: Implement your own UI through an in-game pop-up window.    // Case 2: Use an SDK pop-up. (In this case, call the following code snippet.)    IGamePotSdk* ptr = FGamePotSDKPluginModule::GetSharedGamePotSdk();    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())        ptr->showAppStatusPopup(NAppStatus.ToJsonString());}// Force update (use this method when the store version does not match the client version)void ASampleGameModeBase::OnLoginNeedUpdate(FNAppStatus NAppStatus){     // To do: Notify the user with a pop-up based on the status information passed in a parameter.    // To do: Choose between the following two methods.    // Case 1: Implement your own UI through an in-game pop-up window.    // Case 2: Use an SDK's own pop-up UI. (In this case, call the following code snippet.)    IGamePotSdk* ptr = FGamePotSDKPluginModule::GetSharedGamePotSdk();    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())        ptr->showAppStatusPopup(NAppStatus.ToJsonString());}void ASampleGameModeBase::OnLoginExit(){   // To do: When implementing force updates or checks using the Case 2 method    // To do: Implement your own code here to force exit the app.}void ASampleGameModeBase::OnAppClose(){    // Exit app    // To do: When implementing force updates or checks using the Case 2 method    // To do: Implement your own code here to force exit the app.}
```

NAppStatus definition

```c++
USTRUCT()struct FNAppStatus{    UPROPERTY()    FString type;       // AppStatus type: "maintenance" (check), and "needupdate" (update)       UPROPERTY()    FString message;    // Check settings: Message entered in Dashboard    UPROPERTY()    FString url;        // Check settings: URL entered in Dashboard        UPROPERTY()    FString currentAppVersion;  // Update: Current app version        UPROPERTY()    FString updateAppVersion;   // Update: App version entered in Dashboard        UPROPERTY()    int currentAppVersionCode;  // Update: Current app code        UPROPERTY()    FString updateAppVersionCode;   // Update: App version code entered in Dashboard        UPROPERTY()    bool isForce;       // Update: True if force update is enabled in Dashboard        UPROPERTY()    FString resultPayload;  // This is a JSON value passed from the client SDK; you can ignore it.        UPROPERTY()    double startedAt;    // Check: Start time (timestamp)        UPROPERTY()    double endedAt;     // Check: End time (timestamp)}
```

### Auto login<a name="Autologin"></a>

```c++
ENLoginType::Type loginType =  FGamePotSDKPluginModule::GetSharedGamePotSdk()->getLastLoginType();if(loginType != ENLoginType::NONE) {{    // Log in with the user's last login type.    FGamePotSDKPluginModule::GetSharedGamePotSdk()->Login(loginType);}else{    // The user logs in the game for the first time, or is currently logged out. Move to the login screen where the user can log in.}
```

### Logout<a name="Logout"></a>


It logs a user out. This does not delete the user’s account; the user can log in again later.

- Case 1

Request:

```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())    FGamePotSDKPluginModule::GetSharedGamePotSdk()->Logout();
```

Response:

```csharp
void ASampleGameModeBase::OnLogoutSuccess(){}void ASampleGameModeBase::OnLogoutFailure(FNError NError){    // When logout fails,    // Provide NError.message to the user in a pop-up or other means.}
```

### Withdrawal<a name="Withdrawal"></a>


This deletes a user’s account; this can't be undone.

- Case 1

Request:

```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())    FGamePotSDKPluginModule::GetSharedGamePotSdk()->deleteMember();
```

Response:

```c++
/// Account successfully deleted.
void ASampleGameModeBase::OnDeleteMemberSuccess()
{

}

void ASampleGameModeBase::OnDeleteMemberFailure(FNError NError)
{
   // When deleting an account fails,
    // Provide NError.message to the user in a pop-up or other means.
}
```

### Validation<a name="Validation"></a>


After the login is complete, the login information is passed from the developer server to the GAMEPOT server to perform login validation.

Please refer to the `Token Authentication` section in the Server to server api menu.

## 5. Connect accounts<a name="5Connectaccounts"></a>


Connect or disconnect a game account to or from multiple social media accounts \(including Google or Facebook\). \(At least one social media account must be connected.\)


>The developer must implement the connection screen UI.



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

### Connect<a name="Connect"></a>


This connects user accounts to their social media accounts such as Google or Facebook.

- Case 1

Request:

```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->createLinking(ENLinkingType::Type linkingType);
```

Response:

```c++
void ASampleGameModeBase::OnCreateLinkingSuccess(FNUserInfo NUserInfo) {
        // Account connection succeeded.
}

void ASampleGameModeBase::OnCreateLinkingCancel() {
        // When a user cancels account connection

}
void ASampleGameModeBase::OnCreateLinkingFailure(FNError NError) {
        // When account connection fails,
        // Provide NError.message to the user in a pop-up or other means.
}

```

You can get information for all accounts currently connected.

```c++  
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())     TArray<FNLinkingInfo> linkedList = FGamePotSDKPluginModule::GetSharedGamePotSdk()->getLinkedList();
```

Connect information definition

```c++
USTRUCT()struct FNLinkingInfo{    UPROPERTY()    ENLinkingType::Type provider;      // Information of connected accounts (e.g., Google, Facebook, NAVER, Apple)}
```

### Disconnect accounts<a name="Disconnectaccounts"></a>


This disconnects user accounts from their social media accounts.

- Case 1

Request :

```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())    FGamePotSDKPluginModule::GetSharedGamePotSdk()->deleteLinking(ENLinkingType::Type linkType);
```

Response:

```c++
void ASampleGameModeBase::OnDeleteLinkingSuccess() {/// Account disconnection succeeded}void ASampleGameModeBase::OnDeleteLinkingFailure(FNError NError) {    /// Account disconnection failed     // When account disconnection fails,    // Provide NError.message to the user in a pop-up or other means.}
```

## 6. Payment<a name="6Payment"></a>


### View in-app products<a name="Viewinappproducts"></a>


This gets in-app product information registered in the store.

This feature displays a price, currency, and product name, depending on each user.

```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())    TArray<FNPurchaseItem> itemList = FGamePotSDKPluginModule::GetSharedGamePotSdk()->getPurchaseItems();
```

### NPurchaseItem definition<a name="NPurchaseItemdefinition"></a>


NPurchaseItem definition

```c++
USTRUCT()struct FNPurchaseItem{    UPROPERTY()    FString productId;              // Product ID        UPROPERTY()    FString type;                   // Fix product type as "inapp"    UPROPERTY()    FString price;                  // Google Store price: $0.99, other stores: 0.99       UPROPERTY()    FString price_amount;           // Currency code, e.g., KRW, USD    UPROPERTY()    FString price_amount_micros;    // (Recommended for UI display) The combined value of the currency and price. The currency unit will not be sent for ONE Store, e.g., $0.99    UPROPERTY()    FString price_currency_code;    UPROPERTY()    FString price_with_currency;    UPROPERTY()    FString title;                   // Product name           UPROPERTY()    FString description;            // Product description}
```

### In-app product payment<a name="Inappproductpayment"></a>


Payments can be made in both Google, Apple, and app stores using the following function.

- Case 1

Request:

```c++
// productId: Enter the product ID registered in the store.// uniqueId: Enter the receipt number managed separately.// serverId: Enter the server ID of the character for whom the payment is made.// playerId: Enter the character ID for whom the payment is made.// etc.: Enter other character information for whom the payment is made.if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())    FGamePotSDKPluginModule::GetSharedGamePotSdk()->purchase(FString productId, FString uniqueId, FString serverId, FString playerId, FString etc);
```

### FNPurchaseInfo definition<a name="FNPurchaseInfodefinition"></a>


This is the information of the item for which payment was successfully made. It is for your reference.

```c++
USTRUCT()struct FNPurchaseInfo{    UPROPERTY()    FString price;                         // Price of the purchased item        UPROPERTY()    FString productId;                  // ID of purchased item       UPROPERTY()    FString currency;                    // Currency of the payment (KRW/USD)     UPROPERTY()    FString orderId;                      // Store order ID        UPROPERTY()    FString productName;            // Name of purchased item     UPROPERTY()    FString gamepotOrderId;         // Order ID (created in GAMEPOT)        UPROPERTY()    FString uniqueId;                    // Receipt ID (separately managed by developer company)      UPROPERTY()    FString serverId;                    // Server ID (of the character for whom the purchase was made)        UPROPERTY()    FString playerId;                    // Character ID (of the character for whom the purchase was made)      UPROPERTY()    FString etc;                         // Other information (of the character for whom the purchase was made)      UPROPERTY()    FString signature;                  // Store signature         UPROPERTY()    FString originalJSONData;   // Receipt data}
```

Response:

```c++
/// In-app payment succeeded void ASampleGameModeBase::OnPurchaseSuccess(FNPurchaseInfo NPurchaseInfo) { }/// In-app payment canceled void ASampleGameModeBase::OnPurchaseCancel() { }/// In-app payment failed void ASampleGameModeBase::OnPurchaseFailure(FNError NError) {       // When an in-app payment fails,    // Provide NError.message to the user in a pop-up or other means. }
```

### Provide purchased items<a name="Providepurchaseditems"></a>

GAMEPOT requests items from the developer server after checking receipts from the store by using the Server to server api, thereby preventing illegal payments.

Refer to `Purchase Webhook` in `Server to server api` menu to implement this.

### External payment<a name="Externalpayment"></a>


This enables payment in stores, allowing for external payments and unofficial stores.


>Only the call API is different. The others, such as response and Purchase Webhook, are the same as for regular payment.

>This requires a setting to use features. Please refer to the External payment item in the dashboard manual.



- Case 1

Request:

```csharp
​```c++// productId: Product ID registered in the storeif (FGamePotSDKPluginModule::IsGamePotSdkAvailable())    FGamePotSDKPluginModule::GetSharedGamePotSdk()->purchaseThirdPayments(FString productId);
```

Use the following API for the product information list when using external payment.

Request:

```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())    TArray<FNPurchaseItem> itemList = FGamePotSDKPluginModule::GetSharedGamePotSdk()->getPurchaseThirdPaymentsItems();
```

## 7. Other APIs<a name="7OtherAPIs"></a>


### Login UI supported by SDK<a name="LoginUIsupportedbySDK"></a>


SDK provides an independent, complete login UI.

### FNLoginUIInfo definition<a name="FNLoginUIInfodefinition"></a>


```c++
USTRUCT()struct FNLoginUIInfo{    //Whether to show the image logo    UPROPERTY()    bool showLogo;    //Login type to show as UI    UPROPERTY()    TArray<ENLoginType::Type> loginTypes;  //Google, Facebook, etc.}
```

#### Call SDK login UI<a name="CallSDKloginUI"></a>


- Case 1

Request:

```c++
//Type of login UI to callif (FGamePotSDKPluginModule::IsGamePotSdkAvailable())    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showLoginWithUI(FNLoginUIInfo NLoginUIInfo);
```

Response:

```c++
void ASampleGameModeBase::OnLoginSuccess(FNUserInfo NUserInfo){    // Login succeeded}void ASampleGameModeBase::OnLoginCancel(){    // Login canceled}void ASampleGameModeBase::OnLoginFailure(FNError NError){   // Login failed    // provide error.message to the user in a pop-up or other means.}
```

Response:

 **It's the same as the regular login API response logic. (However, in case of onLoginCancel/onLoginFailure, it will be processed as a toast message at the native level.)**

```c++
void ASampleGameModeBase::OnLoginSuccess(FNUserInfo NUserInfo){    // Login succeeded}void ASampleGameModeBase::OnLoginCancel(){    // Login canceled}// Check (call this when Check is enabled in the dashboard.)void ASampleGameModeBase::OnLoginMaintenance(FNAppStatus NAppStatus){   // To do: Notify the user with a pop-up based on the status information passed in a parameter.    // To do: Choose between the following two methods.    // Case 1: Implement your own UI through an in-game pop-up window.    // Case 2: Use an SDK pop-up. (In this case, call the following code snippet.)    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())        FGamePotSDKPluginModule::GetSharedGamePotSdk()->showAppStatusPopup(NAppStatus.ToJsonString());}// Force update (use this method when the store version does not match the client version)void ASampleGameModeBase::OnLoginNeedUpdate(FNAppStatus NAppStatus){     // To do: Notify the user with a pop-up based on the status information passed in a parameter.    // To do: Choose between the following two methods.    // Case 1: Implement your own UI through an in-game pop-up window.    // Case 2: Use an SDK pop-up. (In this case, call the following code snippet.)    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())        FGamePotSDKPluginModule::GetSharedGamePotSdk()->showAppStatusPopup(NAppStatus.ToJsonString());}void ASampleGameModeBase::OnLoginExit(){    // To do: When closing the LoginUI}void ASampleGameModeBase::OnAppClose(){    // Exit app    // To do: When implementing force updates or checks using the Case 2 method    // To do: Implement your own code here to force exit the app.}
```


#### Customizing<a name="Customizing"></a>

**How to change login UI image logo**

The image logo at the top of the login UI shows the default image within the SDK, and this can be replaced by users.

**[Android]**


If you would like to specify your own image, add them to each `drawable` folder. You can easily and automatically create images for each folder using \([Android Asset Studio](http://romannurik.github.io/AndroidAssetStudio/icons-notification.html#source.type=clipart&source.clipart=ac_unit&source.space.trim=1&source.space.pad=0&name=ic_stat_gamepot_login_logo\).



The image file name should be specified as ic_stat_gamepot_login_logo.png.

| Folder name                                                  | Size  |
| :----------------------------------------------------------- | :---- |
| $S(PluginDir)/ThirdParty/GamePotResources/res/drawable-mdpi/ | 24x24 |
| $S(PluginDir)/ThirdParty/GamePotResources/res/drawable-hdpi/ | 36x36 |
| $S(PluginDir)/ThirdParty/GamePotResources/res/drawable-xhdpi/ | 48x48 |
| $S(PluginDir)/ThirdParty/GamePotResources/res/drawable-xxhdpi/ | 72x72 |
| $S(PluginDir)/ThirdParty/GamePotResources/res/drawable-xxxhdpi/ | 96x96 |


### Apple login (for Android - Web login)<a name="AppleloginforAndroidWeblogin"></a>


#### GAMEPOT Dashboard<a name="GAMEPOTDashboard"></a>


Dashboard Project Settings >> General >> Apple ID Login Settings


>To use this feature, it needs to be enabled in Apple Developer Console.

>Refer to **View Help** of relevant item in the dashboard.


Modify GamePot_Android_UPL.xml

```xml
...<resourceCopies>        <copyFile src="$S(PluginDir)/ThirdParty/Android/libs/gamepot-channel-apple-signin.aar" dst="$S(BuildDir)/libs/gamepot-channel-apple-signin.aar" /></resourceCopies>...<buildGradleAdditions>    <insert>        ...        dependencies {            ...            implementation(name: 'gamepot-channel-apple-signin', ext: 'aar')            ...        }        ...    </insert></buildGradleAdditions>...<gameActivityImportAdditions>  <insert>    import io.gamepot.channel.naver.GamePotAppleSignin;  </insert></gameActivityImportAdditions>...
```

Add the following AAR file to the $S(PluginDir)/ThirdParty/Android/libs path.

- gamepot-channel-apple-signin.aar


### NAVER login<a name="NAVERlogin"></a>


#### Naver Developers<a name="NaverDevelopers"></a>


Register an application after selecting the API used as `Login with NAVER ID`.

#### Android<a name="Android3"></a>


Edit GamePot_Android_UPL.xml

```xml
...<resourceCopies>        <copyFile src="$S(PluginDir)/ThirdParty/Android/libs/gamepot-channel-naver.aar" dst="$S(BuildDir)/libs/gamepot-channel-naver.aar" /></resourceCopies>...<buildGradleAdditions>    <insert>        ...        dependencies {            ...            implementation(name: 'gamepot-channel-naver', ext: 'aar')            ...        }        ...        defaultConfig {            resValue "string", "gamepot_naver_clientid", "abcdefg1234567890"            resValue "string", "gamepot_naver_secretid", "hijklmn"        }        ...    </insert></buildGradleAdditions>...<gameActivityImportAdditions>  <insert>    import io.gamepot.channel.naver.GamePotNaver;  </insert></gameActivityImportAdditions>...
```

Enter the client ID issued on the console in the `gamepot_naver_clientid` value, and the client secret in the `gamepot_naver_secretid` value.

Add the following AAR file to the $S(PluginDir)ThirdParty/Android/libs path.

- gamepot-channel-naver.aar


#### iOS<a name="iOS3"></a>


Modify GamePotSDKPlugin.Build.cs

```csharp
...public GamePotSDKPlugin(ReadOnlyTargetRules Target) : base(Target){    ...           else if (Target.Platform == UnrealTargetPlatform.IOS)        {                PublicAdditionalFrameworks.Add(                new Framework(                    "GamePotNaver",                    ModuleDirectory+"/ThirdParty/iOS/GamePotNaver.framework"                )            );                PublicAdditionalFrameworks.Add(                new Framework(                    "NaverThirdPartyLogin",                    ModuleDirectory+"/ThirdParty/iOS/NaverThirdPartyLogin.framework"                )        }    ...}...
```

Add the following items to the GamePotConfig-Info.plist file and enter the corresponding values.

```text
gamepot_naver_clientid // Client ID to be used in NAVERgamepot_naver_secretid // Secret ID to be used in NAVERgamepot_naver_urlscheme // urlscheme to be used in NAVER
```

Add the following when viewing the GamePotConfig-Info.plist file with SourceCode

```markup
...<key>gamepot_naver_clientid</key><string>xxxxxx</string><key>gamepot_naver_secretid</key><string>xxxxxx</string><key>gamepot_naver_urlscheme</key><string>xxxxxx</string>...
```

### LINE login<a name="LINElogin"></a>

#### LINE Developers<a name="LINEDevelopers"></a>


Add the package name, keystore's SHA value, and url scheme value used when your APK is built for the LINE console.

#### Android<a name="Android4"></a>


Edit GamePot_Android_UPL.xml

```xml
...<resourceCopies>    <copyFile src="$S(PluginDir)/ThirdParty/Android/libs/gamepot-channel-line.aar" dst="$S(BuildDir)/libs/gamepot-channel-line.aar" />    <copyFile src="$S(PluginDir)/ThirdParty/Android/libs/line-sdk-4.0.10.aar" dst="$S(BuildDir)/libs/line-sdk-4.0.10.aar" /></resourceCopies>...<buildGradleAdditions>    <insert>        ...        dependencies {            ...            implementation(name: 'gamepot-channel-line', ext: 'aar')            implementation(name: 'line-sdk-4.0.10', ext: 'aar')            ...        }        ...        defaultConfig {            resValue "string", "gamepot_line_channelid","xxxxxxx"        }        ...    </insert></buildGradleAdditions>...<gameActivityImportAdditions>  <insert>    import io.gamepot.channel.line.GamePotLine;  </insert></gameActivityImportAdditions>...
```

Add the following AAR file to the $S(PluginDir)/ThirdParty/Android/libs path.

- gamepot-channel-line.aar
- line-sdk-4.0.10.aar



#### iOS<a name="iOS4"></a>


Modify GamePotSDKPlugin.Build.cs

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

Add the following items to GamePotConfig-Info.plist file to enter the value.

```text
gamepot_line_channelid // Client ID to be used in NAVER
gamepot_line_url_schemes // Line URL Scheme (line3rdp.{Project bundle identifier})
```

If viewing GamePotConfig-Info.plist with SourceCode, add the following.

```markup
...<key>gamepot_line_channelid</key><string>xxxxxx</string><key>gamepot_line_url_schemes</key><string>xxxxxx</string>...
```

### Twitter login<a name="Twitterlogin"></a>

#### Twitter Developers<a name="TwitterDevelopers"></a>


#### Android<a name="Android5"></a>


Edit GamePot_Android_UPL.xml

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

Add the following AAR files to the /Plugin/GamePotSDKPlugin/Source/GamePot/ThirdParty/Android/libs path.

- gamepot-channel-twitter.aar
- twitter-core-3.3.0.aar



#### iOS<a name="iOS5"></a>


Modify GamePotSDKPlugin.Build.cs

```csharp
...public GamePotSDKPlugin(ReadOnlyTargetRules Target) : base(Target){    ...           else if (Target.Platform == UnrealTargetPlatform.IOS)        {                PublicAdditionalFrameworks.Add(                new Framework(                    "GamePotTwitter",                    ModuleDirectory+"/ThirdParty/iOS/GamePotTwitter.framework"                )            );            PublicAdditionalFrameworks.Add(                new Framework(                    "TwitterCore",                    ModuleDirectory+"/ThirdParty/iOS/TwitterCore.framework"                )            );            PublicAdditionalFrameworks.Add(                new Framework(                    "TwitterKit",                    ModuleDirectory+"/ThirdParty/iOS/TwitterKit.framework"                )            );        }    ...}...
```

Add the following items to GamePotConfig-Info.plist file to enter the value.

```text
gamepot_twitter_consumerkey : Twitter Consumer Keygamepot_twitter_consumersecret :  Twitter Consumer Secret
```

If viewing GamePotConfig-Info.plist with SourceCode, add the following

```markup
...<key>gamepot_twitter_consumerkey</key><string>xxxxxx</string>...
```

### Coupon<a name="Coupon"></a>


#### Use coupon<a name="Usecoupon"></a>



>The developer must implement the UI to enter coupons.



- Case 1

Request:

```c++
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())    {        FGamePotSDKPluginModule::GetSharedGamePotSdk()->coupon(FString couponNumber); // Coupon number        FGamePotSDKPluginModule::GetSharedGamePotSdk()->coupon(FString couponNumber, FString userData); // Coupon number, user information    }
```

Response:

```c++
void ASampleGameModeBase::OnCouponSuccess(FString msg){    /// Succeeded in using coupon}void ASampleGameModeBase::OnCouponFailure(FNError NError){      // When an attempt to use a coupon fails,    // provide error.message to the user in a pop-up or other means.}
```

#### Provide items<a name="Provideitems"></a>


When a coupon is used successfully, request an item from the developer server by using the Server to server api.

Refer to `Item Webhook` in Server to server api menu to implement this.

### Push on/off<a name="Pushonoff"></a>


General push and night push can separately turn on or off.

 
>The developer should implement the UI to turn push notifications on or off.



#### Set push<a name="Setpush"></a>


- Case 1

Request:

```c++
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())        FGamePotSDKPluginModule::GetSharedGamePotSdk()->setPushStatus(bool pushEnable); 
```

Response:

```c++
void ASampleGameModeBase::OnPushSuccess(){    /// Push status change succeeded}void ASampleGameModeBase::OnPushFailure(FNError NError){        // When changing push status fails,    // provide error.message to the user in a pop-up or other means.}
```


#### Set night push<a name="Setnightpush"></a>


- Case 1

Request:

```c++
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())        FGamePotSDKPluginModule::GetSharedGamePotSdk()->setPushNightStatus(bool nightPushEnable); 
```

Response:

```c++
void ASampleGameModeBase::OnPushNightSuccess(){    /// Push status change succeeded}void ASampleGameModeBase::OnPushNightFailure(FNError NError){        // When changing push status fails,    // provide error.message to the user in a pop-up or other means.}
```

#### Set ad push<a name="Setadpush"></a>


- Case 1

Request:

```c++
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())        FGamePotSDKPluginModule::GetSharedGamePotSdk()->setPushADStatus(bool adPushEnable); 
```

Response:

```c++
void ASampleGameModeBase::OnPushAdSuccess(){    /// Push status change succeeded}void ASampleGameModeBase::OnPushFailure(FNError NError){        // When changing push status fails,    // provide error.message to the user in a pop-up or other means.}
```

#### Set push, night push, and ad push at the same time<a name="Setpush,nightpush,andadpushatthesametime"></a>


For games that prompt users to turn push or night push on or off before login, call the following code snippet after login.

- Case 1

Request:

```c++
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())        FGamePotSDKPluginModule::GetSharedGamePotSdk()->setPushStatus(bool pushEnable, bool nightPushEnable, bool adPushEnable); 
```

Response:

```c++
void ASampleGameModeBase::OnPushStatusSuccess(){    /// Push status change succeeded}void ASampleGameModeBase::OnPushStatusFailure(FNError NError){        // When changing push status fails,    // provide error.message to the user in a pop-up or other means.}
```

#### Get push status<a name="Getpushstatus"></a>


-  FNPushInfo definition

```c++
USTRUCT()struct FNPushInfo{    UPROPERTY()    bool enable;       // Whether (general) push is enabled                   UPROPERTY()    bool night;         // Whether night push is enabled    UPROPERTY()    bool ad;            // Whether ad push is enabled}
```

Request:

```c++
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())        FNPushInfo NPushInfo = FGamePotSDKPluginModule::GetSharedGamePotSdk()->getPushStatus(); 
```

### Notice<a name="Notice"></a>


This shows images added to the Notice in the GAMEPOT dashboard in order.

Recommended specs for images are shown below.

- Dimensions: 720 _1200\(Portrait\) / 1280_ 640\(Landscape\)

 
>If images are outside of the specs, process them with center crop.


- Size: 250 KB or smaller

Request:

```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showNotice(bool showToday = true); // true: Apply Do not show for 24 hours// false: Force exposure regardless of Do not show for 24 hours
```

```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showEvent(FString Type); // Type: Only show the relevant image set in Dashboard Notice >> Classification
```

Response:

If `Click action` is set as `SCHEME` in the GAMEPOT dashboard, then the `SCHEME` value is sent when the image is clicked.

```c++
 void ASampleGameModeBase::OnReceiveScheme(FString scheme) {      // Send the scheme value set in the GAMEPOT dashboard }
```

### Support<a name="Support"></a>


Customers can register inquiries and admins can answer them.

Inquiry UI changes according to the device language setting. It supports Korean, English, Japanese, Chinese (Simplified, Traditional). English is applied for other languages.

#### Call<a name="Call1"></a>


```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showCSWebView(); 
```

It supports external links so that customers who haven't logged in can register inquiries.

#### Call<a name="Call2"></a>


```c++
// url: External customer support URL issued by GAMEPOT
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showWebView(FString url); 
```

### \(Local push notification\)<a name="Localpushnotification"></a>


This feature enables devices to display push notifications by themselves, not via the push server.

#### Add push<a name="Addpush"></a>


Refer to the following code to display local push notifications at a specified time.

 
>The pushId passed as a return value should be managed by the developer.



```c++
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
         int pushId = FGamePotSDKPluginModule::GetSharedGamePotSdk()->sendLocalPush(FString date, FString title, FString message); 

// date : (Format - timestamp "yyyy-MM-dd HH:mm:ss") 
// ex >  DateTime.Parse("2018-01-01 00:00:00")
//  title :  "title"
// message :  "content"
```

#### Cancel push<a name="Cancelpush"></a>

You can cancel previously added push notifications using the pushId you get when adding push.

```c++
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
         bool success = FGamePotSDKPluginModule::GetSharedGamePotSdk()->cancelLocalPush(int /*pushId you got when adding push*/); 
```

### Agree to Terms and Conditions<a name="AgreetoTermsandConditions"></a>


Provide UI to easily obtain agreement to Terms and Conditions and Collection and use of personal information.

11 types of new `improved themes` are provided in addition to two `basic themes`, `BLUE` and `GREEN`.

Each area can be customized as well.

#### Call Agree to Terms and Conditions<a name="CallAgreetoTermsandConditions"></a>


#### FNAgreeInfo definition<a name="FNAgreeInfodefinition"></a>


```c++
USTRUCT()
struct FNAgreeInfo
{    
    // Basic theme
    UPROPERTY()
    FString theme;
    
    // Title
    // Background color (gradient)
    UPROPERTY()
    TArray<FString> headerBackGradient;
    
    // Title area bottom line color
    UPROPERTY()
    FString headerBottomColor;
    
    // Icon image file name (aos - drawable/ios - bundle)
    UPROPERTY()
    FString headerIconDrawable;
    
    // Subject
    UPROPERTY()
    FString headerTitle;
    
    // Subject color
    UPROPERTY()
    FString headerTitleColor;
    
    // Content
    // Background color (gradient)
    UPROPERTY()
    TArray<FString> contentBackGradient;
  
    // Icon image file name (aos - drawable/ios - bundle)
    UPROPERTY()
    FString contentIconDrawable;
    
    // Icon color
    UPROPERTY()
    FString contentIconColor;
   
    // Check button color
    UPROPERTY()
    FString contentCheckColor;
    
    // Check content color
    UPROPERTY()
    FString contentTitleColor;
    
    // Instruction text color to show all
    UPROPERTY()
    FString contentShowColor;
    
    // Bottom (Game start)
    // Background color (gradient)
    UPROPERTY()
    TArray<FString> footerBackGradient;
  
    // Game start button background color (gradient)
    UPROPERTY()
    TArray<FString> footerButtonGradient;
    
    // Game start button outline color
    UPROPERTY()
    TArray<FString> footerButtonOutlineColor;

    // Game start text
    UPROPERTY()
    TArray<FString> footerTitle;

    // Game start text color
    UPROPERTY()
    TArray<FString> footerTitleColor;
    
    //Whether to show general push notification
    UPROPERTY()
    bool showPush;
    
    // Whether to show night push notification
    UPROPERTY()
    bool showNightPush;
    
    // When "Agree to all" text changes
    UPROPERTY()
    FString allMessage;
    
    // When "Terms and Conditions" text changes
    UPROPERTY()
    FString termMessage;
    
    // When "Privacy Policy" text changes
    UPROPERTY()
    FString privacyMessage;
    
    // When general push text changes
    UPROPERTY()
    FString pushMessage;
    
    // When night push text changes
    UPROPERTY()
    FString nightPushMessage;
    
    UPROPERTY()
    FString pushDetailURL;
    
    UPROPERTY()
    FString nightPushDetailURL;
}

```


Handle whether or not the Agree to Terms and Conditions pop-up is shown according to the game.
The content shown when the user clicks the View button can be edited and applied in the dashboard.



- Case 1

Request:

```c++
// Case 1) Basic call (with BLUE theme)
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showAgreeDialog(); 

// Case 2) When applying other themes
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
{
    // - Basic theme
    // BLUE
    // GREEN
    
    //  - Improved theme
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
// If agreed to Terms and Conditions
void ASampleGameModeBase::OnAgreeDialogSuccess(FNAgreeResultInfo NAgreeResultInfo)
{
       // NAgreeResultInfo.agree: true if agreed to all required Terms and Conditions
        // NAgreeResultInfo.agreePush: true if checked to agree to receive general push notifications; otherwise, it is false.
        // NAgreeResultInfo.agreeNight: true if checked to agree to receive night ad push notifications; otherwise, it is false.
        // Send agreeNight value through setPushNightStatus API after login is complete.
}

void ASampleGameModeBase::OnAgreeDialogFailure(FNError NError)
{
    // Error triggered
}
```

-  Customizing

Each variable applies to the following area:

 
>contentIconDrawable appears to AOS only, and its default value is set to the push icon.



![gamepot_unreal_002.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_unreal_002%281%29.png)

### Terms and Conditions<a name="TermsandConditions"></a>


Call Terms and Conditions UI.

 
>Enter content first in Dashboard - Support - Set Terms and Conditions.



```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showTerms(); 
```

### Privacy Policy<a name="PrivacyPolicy"></a>


Call Privacy Policy UI.

 
>Enter content first in Dashboard - Support - Set Privacy Policy.



```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showPrivacy(); 
```

### Refund policy<a name="Refundpolicy"></a>


Call refund policy UI.

 
>Enter content first in Dashboard - Support - Set refund policy.



```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showRefund(); 
```

### Remote configuration<a name="Remoteconfiguration"></a>


Import parameter values registered with the dashboard from the client.


>Add parameters in Dashboard - Settings - Remote configuration screen.

>The parameters added are loaded at login. You can call them after they have been loaded.



```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
{
    //"test_01": Parameter FString
    FString value = FGamePotSDKPluginModule::GetSharedGamePotSdk()->getConfig("test_01"); 

    //Import all parameters added in the dashboard in JSON string format.
    FString json_value = FGamePotSDKPluginModule::GetSharedGamePotSdk()->getConfigs();
}
```

### Automatic cancellation feature for payment cancellation abusers<a name="Automaticcancellationfeatureforpaymentcancellationabusers"></a>


It provides UI for the Automatic cancellation feature for payment cancellation abusers. Customizable in each area.

 
If a user cancels a payment by requesting Google directly (limited to Google payment), then the user can be suspended with the Cancel Google payment feature.
When the user logs in, a pop-up appears in the SDK to encourage the user to pay for the item again.
When the user pays again, they can successfully regain access.
If the user repays all canceled payments, then the suspension is automatically lifted.



### NVoidInfo definition<a name="NVoidInfodefinition"></a>


```c++
USTRUCT()
struct FNVoidInfo
{
    // Basic theme
    UPROPERTY()
    FString theme;
    
    // Background color (gradient)
    UPROPERTY()
    TArray<FString> headerBackGradient;
    
    // Subject
    UPROPERTY()
    FString headerTitle;
    
    // Subject color
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
   
   // Background color (gradient)
    UPROPERTY()
    TArray<FString> footerBackGradient;
    
    // Button background color (gradient)
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
        //Types of themes
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

### Transfer game logs<a name="Transfergamelogs"></a>


You can call the logs that contain in-game information and view them in `Dashboard` - ` Game`.

Check reserved words from the table below:

| Reserved words               | Required | Type    | Description    |
| :--------------------------- | :------- | :------ | :------------- |
| FNSendLogCharacter.NAME      | Required | FString | Character name |
| FNSendLogCharacter.LEVEL     | Optional | FString | Level          |
| FNSendLogCharacter.SERVER_ID | Optional | FString | Server ID      |
| FNSendLogCharacter.PLAYER_ID | Optional | FString | Character ID   |
| FNSendLogCharacter.USERDATA  | Optional | FString | ETC            |

### FNSendLogCharacter definition<a name="FNSendLogCharacterdefinition"></a>


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

    // Result is TRUE : validation success. Logs will send to GamePot Server
    // Result is FALSE : validation was failed. Please check logcat
}

```

### GDPR Terms and Conditions checklist<a name="GDPRTermsandConditionschecklist"></a>


Shows the list of GDPR Terms and Conditions items activated from Dashboard.

```c++
//The returning data format is the FString type, and will show as string[]. E.g., "[ gdpr_privacy, gdpr_term ]" 
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FString gdpr_list = FGamePotSDKPluginModule::GetSharedGamePotSdk()->getGDPRCheckedList();

// gdpr_privacy: Privacy Policy
// gdpr_term: Terms and Conditions
// gdpr_gdpr: GDPR Terms and Conditions
// gdpr_push_normal: Consent to receive event push notifications
// gdpr_push_night: Consent to receive nighttime event push notifications (only applicable in Korea)
// gdpr_adapp_custom: Consent to view personalized advertisement (for countries where GDPR is applicable)
// gdpr_adapp_custom: Consent to view non-personalized advertisement (for countries where GDPR is applicable)
```

## Appendix<a name="Appendix"></a>


### Third-party SDK connection is supported.<a name="ThirdpartySDKconnectionissupported"></a>


## Login<a name="Login2"></a>


>Auto login is not supported. Call is required every time.



| Parameter name | Required | Type    | Description      |
| :------------- | :------- | :------ | :--------------- |
| userid         | Required | FString | User's unique ID |

```c++
FString userid = TEXT("memberid of 3rd party sdk");

if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->loginByThirdPartySDK(userid);
```

## Payment<a name="Payment"></a>



>Purchased items must be registered in the GAMEPOT dashboard.



| Parameter name | Required | Type    | Description                                      |
| :------------- | :------- | :------ | :----------------------------------------------- |
| productid      | Required | FString | Item ID registered in the GAMEPOT dashboard      |
| transactionid  | Required | FString | Payment receipt number (GPA-xxx-xxxx-xxxx)       |
| store          | Required | FString | (Store for payment - Google, Apple, ONE, Galaxy) |
| currency       | Optional | FString | Currency (KRW, USD)                              |
| price          | Optional | double  | Amount of purchased items                        |
| paymentid      | Optional | FString | Payment ID (Usually the same as store_id)        |
| uniqueid       | Optional | FString | Developer's unique ID                            |

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