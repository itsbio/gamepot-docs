## 基本環境設定<a name="基本環境設定"></a>


### Android<a name="Android1"></a>


```d
minSdkVersion : API 17 (Jelly Bean, 4.2)
```

**プロジェクト環境の設定方法**

/Plugin/GamePotSDKPlugin/Source/GamePot/GamePot_Android_UPL.xmlファイルをエディタで開きます。

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
         resValue "string", "gamepot_naver_clientid", ""                               // optional (Naver 開発者コンソールで獲得)
         resValue "string", "gamepot_naver_secretid", ""                              // optional (Naver 開発者コンソールで獲得)
         resValue "string", "gamepot_line_channelid",""                               // optional (Line 開発者コンソールで獲得)
         resValue "string", "gamepot_twitter_consumerkey", ""                   // optional (Twitter 開発者コンソールで獲得)
         resValue "string", "gamepot_twitter_consumersecret", ""               // optional (Twitter 開発者コンソールで獲得)
         resValue "string", "gamepot_elsa_projectid", ""                              // optional (ncp elsa)
    }
    ...
}
  </insert>
</buildGradleAdditions>
```

以下の必須値を探して修正します。以下の値を修正しないと正常に動作しません。

```java
resValue "string", "[key]", "[value]"
```

|値|説明|
| :--------------------------- | :--------------------------------------------------------------------------------------------- |
| gamepot_project_id           | GAMEPOTで発行されたプロジェクトIDを入力してください。                  |
| gamepot_store                | ストア値\(`google`または`one`または`galaxy`\)                                  |
| gamepot_app_title            | アプリのタイトル \(FCM\)                                                                   |
| gamepot_push_default_channel | 登録されたデフォルトチャンネル名\（Default\） - 変更しないでください。                 |
| facebook_app_id              | フェイスブック発行されたアプリID                     |
| fb_login_protocol_scheme  | フェイスブックで発行された protocol scheme fb[app_id]          |
| gamepot_naver_clientid     | Naver 開発者コンソールで獲得               |
| gamepot_naver_secretid     | Naver 開発者コンソールで獲得                 |
| gamepot_line_channelid     | Line 開発者コンソールで獲得               |
| gamepot_twitter_consumerkey     | Twitter 開発者コンソールで獲得          |
| gamepot_twitter_consumersecret     | Twitter 開発者コンソールで獲得      |
| gamepot_elsa_projectid       | NCLOUD ELSA 使用時プロジェクトID \([詳細を見る](https://www.ncloud.com/product/analytics/elsa)\) |
|


**Notification barにあるプッシュアイコンの変更方法**

![gamepot_unreal_003_ja.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_unreal_003_ja.png)




プッシュ通知を受信する際にAndroid Notification barに表示するSmall iconは、SDK内部の基本画像が用いられ、直接追加することもできます。

直接追加するには`drawable`フォルダ別に画像を追加する必要があります。（[Android Asset Studio](http://romannurik.github.io/AndroidAssetStudio/icons-notification.html#source.type=clipart&source.clipart=ac_unit&source.space.trim=1&source.space.pad=0&name=ic_stat_gamepot_small)を利用して作成すると、自動的にフォルダ別に画像が作成されるため便利です。）

画像ファイル名は必ずic_stat_gamepot_smallにしてください。

|フォルダ名|サイズ|
| :------------------------------------------------------------- | :---- |
| $S(PluginDir)/ThirdParty/Android/GamePotResources/res/drawable-mdpi/    | 24x24 |
| $S(PluginDir)/ThirdParty/Android/GamePotResources/res/drawable-hdpi/    | 36x36 |
| $S(PluginDir)/ThirdParty/Android/GamePotResources/res/drawable-xhdpi/   | 48x48 |
| $S(PluginDir)/ThirdParty/Android/GamePotResources/res/drawable-xxhdpi/  | 72x72 |
| $S(PluginDir)/ThirdParty/Android/GamePotResources/res/drawable-xxxhdpi/ | 96x96 |



### iOS<a name="iOS1"></a>


Google Firebaseからダウンロードした`GoogleService-Info.plist`ファイルを`/Plugin/GamePotSDKPlugin/Source/GamePot/ThirdParty/iOS/`にコピーします。

`/Plugin/GamePotSDKPlugin/Source/GamePot/ThirdParty/iOS/GamePotConfig-Info.plist`内に必要な環境変数を追加してください。

![gamepot_unreal_001_ja.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_unreal_001_ja.png)

|環境変数|説明|
| :---------------------------- | :---------------------------------------------------- |
| gamepot_project_id            | GAMEPOTで発行されたプロジェクトIDを入力してください。 |
| gamepot_facebook_app_id       | Facebookの発行を受けたアプリID                       |
| gamepot_facebook_display_name |フェイスブックにみられる名前                              |
| gamepot_google_app_id         | GoogleService-Info ファイルの CLIENT_ID 値                |
| gamepot_google_url_schemes    | GoogleService-Info ファイルの REVERSED_CLIENT_ID 値       |
| gamepot_facebook_app_id  |   Facebook App ID  |
| gamepot_facebook_display_name |  Facebook display name   |
| gamepot_naver_clientid   |  Naver Client Id   |
| gamepot_naver_secretid  |   Naver Secret Id  |
| gamepot_naver_urlscheme  |   Naver Url Scheme  |
| gamepot_line_channelid  |  Line Channel ID   |
| gamepot_line_url_schemes  |   Line URL Scheme (line3rdp.{プロジェクトバンドル ID})  |
| gamepot_twitter_consumerkey  |   Twitter Consumer Key  |
| gamepot_twitter_consumersecret  |  Twitter Consumer Secret  |
| gamepot_elsa_projectid  | NCLOUD ELSA使用時プロジェクトID   |
|

`GamePotResources.embeddedframework` を**.zip**で圧縮した後、
`$S(PluginDir)/ThirdParty/iOS/GamePotResources.embeddedframework.zip` の経路に配置した状態で、
ビルドを実行してください。

iOSのビルドの前に、

プロジェクトセッティング >> iOS >> Extra PList Data >> Additional Plist Data内に以下の`ユーザー権限取得オプションを追加`してください。

このユーザー権限はGAMEPOTサポートセンター内のファイルアップロード機能で使用されます。

```text
<key>NSCameraUsageDescription</key>
<string>$(PRODUCT_NAME) camera use.</string>
<key>NSPhotoLibraryUsageDescription</key>
<string>$(PRODUCT_NAME) photo library use.</string>
```

iOS 14以上のバージョン

iOS 14バージョンからIDFA値を取得する際に、ユーザーから権限を取得しないと

IDFA値を取得できないように変更されました。

従って、IDFA値を取得する際にユーザーから権限を取得するポップアップを使用する場合は、
プロジェクトセッティング >> iOS >> Extra PList Data >> Additional Plist Data内に以下の`ユーザー権限取得オプションを追加`してください。


2020.09.11
AppleでIDFA値を取得する際にユーザーから権限を取得するポップアップの必須適用は、2021年の初めまで延期されました。
以下のリンクを参考にしてください。
[https://developer.apple.com/news/?id=hx9s63c5](https://developer.apple.com/news/?id=hx9s63c5)


```text
<key>NSUserTrackingUsageDescription</key>
<string>$(PRODUCT_NAME) This identifier will collect IDFA for advertising purposes.</string>
```

IDFA権限要請ポップアップ呼び出し(明示的)

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

> `iOSプラットフォームの場合、`ログインAPI呼び出し時にIDFA値獲得に対する権限を要請するポップアップを先に明示的に要請しています。

> このポップアップの要請をログイン時点で呼び出したくない場合は、「FIOS Game PotSdk::Login (EN Login Type::Type)」関数を修正してください。
>  `$S(PluginDir)/Private/iOS/IOSGamePotSdk.cpp`

```c++
void FIOSGamePotSdk::Login(ENLoginType::Type _loginType)
{
    //ログイン前、明示的にIDFAポップアップに露出 ←必要な場合は注釈処理
    FIOSGamePotSdk::requestTrackingAuthorization();
    ...
```

IOS の場合、Push を受信するため、事前にその権限をユーザーから獲得する必要があります。
適当な時点(ex - Login Success)に該当権限を要請する次の関数を呼び出してください。

```c++
if(LOGIN_SUCCESS)
{
    //明示的にPush権限獲得を要請
    FPlatformMisc::RegisterForRemoteNotifications();
}
```

## 1. 初期化<a name="1.初期化"></a>


ゲームを始める際にロードされる最初の画面（レベル）に使用されるインスタンスに、次のコードを追加します。
 
 - ex> "ASampleGameModeBase.h"

```c++
//（当該レベルで使用される）GAMEPOT APIに対する、Callback Event Listener宣言
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

     //（headerで宣言したEvent Listenerを）GamePotPluginModuleのCallback Event Listenerにバインド
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

（Binding）Event Listenerリスト

```c++
    // Loginに成功
    FOnSdkLoginSuccess OnSdkLoginSuccess(FNUserInfo NUserInfo);     
    // Loginをキャンセル
    FOnSdkLoginCancel OnSdkLoginCancel(); 
    // Loginに失敗
    FOnSdkLoginFailure OnSdkLoginFailure(FNError NError);   
    // Login（メンテナンス）
    FOnSdkLoginMaintenance OnSdkLoginMaintenance(FNAppStatus NAppStatus);
    // Login（アップデート）
    FOnSdkLoginNeedUpdate OnSdkLoginNeedUpdate(FNAppStatus NAppStatus);   
    // Login UI Close（showLoginWithUIを使用時）
    FOnSdkLoginExit OnSdkLoginExit();         
    // （メンテナンス、アップデート時）アプリを終了
    FOnSdkAppClose OnSdkAppClose();   

    // Logoutに成功
    FOnSdkLogoutSuccess OnSdkLogoutSuccess();   
    // Logoutに失敗
    FOnSdkLogoutFailure OnSdkLogoutFailure(FNError NError);      

    // showWebviewを閉じる
    FOnWebviewClose OnSdkWebviewClose(FString msg);

    // purchaseに成功
    FOnSdkPurchaseSuccess OnSdkPurchaseSuccess(FNPurchaseInfo NPurchaseInfo);
    // purchaseをキャンセル
    FOnSdkPurchaseCancel OnSdkPurchaseCancel();
    // purchaseに失敗
    FOnSdkPurchaseFailure OnSdkPurchaseFailure(FNError NError);  

    // getPurchaseDetailListAsyncに成功
    FOnSdkPurchaseDetailListSuccess OnSdkPurchaseDetailListSuccess(TArray<FNPurchaseItem> Items);
    // getPurchaseDetailListAsyncに失敗
    FOnSdkPurchaseDetailListFailure OnSdkPurchaseDetailListFailure(FNError NError);

    // createLinkingに成功
    FOnSdkCreateLinkingSuccess OnSdkCreateLinkingSuccess(FNUserInfo NUserInfo);
    // createLinkingをキャンセル
    FOnSdkCreateLinkingCancel OnSdkCreateLinkingCancel();
    // createLinkingに失敗
    FOnSdkCreateLinkingFailure OnSdkCreateLinkingFailure(FNError NError);

    // deleteLinkingに成功
    FOnSdkDeleteLinkingSuccess OnSdkDeleteLinkingSuccess();
    // deleteLinkingに失敗
    FOnSdkDeleteLinkingFailure OnSdkDeleteLinkingFailure(FNError NError);

    // 案内事項の画像（showNotice、showEvent）クリックアクションschemeコールバック
    FOnSdkReceiveScheme OnSdkReceiveScheme(FString scheme);

    // deleteMemberに成功
    FOnSdkDeleteMemberSuccess OnSdkDeleteMemberSuccess();
    // deleteMemberに失敗
    FOnSdkDeleteMemberFailure OnSdkDeleteMemberFailure(FNError NError);

    // coupon（使用）に成功
    FOnSdkCouponSuccess OnSdkCouponSuccess(FString msg);
    // coupon（使用）に失敗
    FOnSdkCouponFailure OnSdkCouponFailure(FNError NError);

    // showAgreeDialog（規約に同意したかどうか）更新に成功
    FOnAgreeDialogSuccess OnSdkAgreeDialogSuccess(FNAgreeResultInfo NAgreeResultInfo);
    // showAgreeDialog（規約に同意したかどうか）更新に失敗
    FOnAgreeDialogFailure OnSdkAgreeDialogFailure(FNError NError);

    // setPushに成功
    FOnPushSuccess OnSdkPushSuccess();
    // setPushAdStatusに成功
    FOnPushAdSuccess OnSdkPushAdSuccess();
    // setPushNightStatusに成功
    FOnPushNightSuccess OnSdkPushNightSuccess();
    // setPushStatusに成功
    FOnPushStatusSuccess OnSdkPushStatusSuccess();

    // setPushに失敗
    FOnPushFailure OnSdkPushFailure(FNError NError);
    // setPushAdStatusに失敗
    FOnPushAdFailure OnSdkPushAdFailure(FNError NError);
    // setPushNightStatusに失敗
    FOnPushNightFailure OnSdkPushNightFailure(FNError NError);
    // setPushStatusに失敗
    FOnPushStatusFailure OnSdkPushStatusFailure(FNError NError);
```

NUserInfoの定義

```c++
USTRUCT()
struct FNUserInfo
{
    UPROPERTY()
    FString memberid;           // メンバーID（ユーザーの固有ID）
    UPROPERTY()
    FString name;               // 名前
    UPROPERTY()
    FString profileUrl;         // プロフィールURL（ある場合）
    UPROPERTY()
    FString email;              // メール（ある場合）
    UPROPERTY()
    FString token;              // ユーザーの有効性チェック用Token（Token AuthenticationAPIで使用）
    UPROPERTY()
    FString userid;             // Social ID（Google、Facebook...）
}
```

## 2. エラーコード<a name="2.エラーコード"></a>


NErrorの定義

```c++
USTRUCT()
struct FNError
{
    //Detail Error code
    static const int CODE_UNKNOWN_ERROR = 0;                    // 不明なエラー
    static const int CODE_NOT_INITALIZE = 1;                    // 初期化に失敗
    static const int CODE_INVAILD_PARAM = 2;                    // パラメータが正しくない場合
    static const int CODE_MEMBERID_IS_EMPTY = 3;                    // メンバーIDデータがない場合
    static const int CODE_NOT_SIGNIN = 4;                    // ログインされていない状態
    static const int CODE_NETWORK_MODULE_NOT_INIT = 3000;                 // ネットワークモジュールが初期化されなかった場合
    static const int CODE_NETWORK_ERROR = 3001;                 // ネットワークコネクションエラー及びタイムアウト発生時
    static const int CODE_SERVER_ERROR = 4000;                 // server-sideで発生するエラー
    static const int CODE_SERVER_HTTP_ERROR = 4001;                 // http response codeが成功でない場合
    static const int CODE_SERVER_NETWORK_ERROR = 4002;                 // ネットワークコネクションエラー及びタイムアウト発生時
    static const int CODE_SERVER_PARSING_ERROR = 4003;                 // サーバから取得したデータをパースする際のエラー
    static const int CODE_CHARGE_UNKNOWN_ERROR = 5000;                 // 決済で不明なエラー発生及びストア側からエラー伝達時
    static const int CODE_CHARGE_PRODUCTID_EMPTY = 5001;                 // product idを入力しなかった場合
    static const int CODE_CHARGE_PRODUCTID_WRONG = 5002;                 // product idを正しく入力しなかった場合
    static const int CODE_CHARGE_CONSUME_ERROR = 5003;                 // consume時のエラー

    UPROPERTY()
    int code;               // error Code

    UPROPERTY()
    FString message;        // error Message
}
```

## 3. ログイン環境設定<a name="3.ログイン環境設定"></a>


### Googleログイン<a name="Googleログイン"></a>

#### Google Firebase Console<a name="GoogleFirebaseConsole"></a>


1. Google Firebase ConsoleからAndroid用google-service.jsonファイルをダウンロードし、`/Plugins/GamePotSDKPlugin/Source/GamePot/ThirdParty/Android/`にコピーします。
2. APKをビルドする際に使用したKeystoreのSHA-1値をGoogle Firebase Consoleに追加します。

**Googleログイン時にonCancelがレスポンスしてログインできない場合、** 以下の内容をチェックしてください。

1. 上記で適用リクエストしたgoogle-service.jsonファイルを正常に適用したか確認
2. ビルドする際に使用したキーストアが、Google Firebase Consoleに登録したSHA-1を抽出したキーストアなのか確認
3. Google Firebase Consoleに登録したパッケージ名でビルドしたか確認

#### Android

GamePot_Android_UPL.xml 修整

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

1. `$S(PluginDir)/ThirdParty/iOS/GamePotResouces.embeddedframework.zip`の圧縮を解除します。

2. IOS用GoogleService-Info.plistファイルをダウンロードした後、「$S(PluginDir)ThirdPartyiOSGamePotResouces.embeddedframeworkResources`」のパスにコピーした後、再び**再圧縮**します。

![gamepot_unreal_004_ja.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_unreal_004_ja.png)

### Facebookログイン<a name="Facebookログイン"></a>


#### Facebook Developer Console<a name="FacebookDeveloperConsole"></a>


APKをビルドする際に使用したKeystoreのキーハッシュ値をFacebookコンソールに追加します。

#### Android<a name="Android2"></a>


GamePot_Android_UPL.xmlの修正

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


GamePotConfig-Info.plistファイルに以下の項目を追加し、当該値を入力します。

```text
gamepot_facebook_app_id // Facebook開発者コンソールで発行されたapp id
```

GamePotConfig-Info.plistファイルをSourceCodeと見る場合、以下のように追加

```markup
...
<key>gamepot_facebook_app_id</key>
<string>xxxxxx</string>
...
```


### Appleログイン<a name="Appleログイン"></a>



>iOSにのみ該当する機能です。（Androidの場合、Web Loginの形でサポート）


**Config/DefaultEngine.ini内の` [/Script/IOSRuntimeSettings.IOSRuntimeSettings] `項目に次のFlag値を追加します。**


>bEnableSignInWithAppleSupport=True


## 4. ログイン/ログアウト/退会/検証<a name="4.ログイン/ログアウト/退会/検証"></a>


### ログイン<a name="ログイン1"></a>


別途の登録なしにユーザーアカウントが作成されます。すべての身元確認のためのMemberIdが作成され、作成された情報はFNUserInfoに保存されてリターンされます。

LoginTypeの定義

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
    // ログインに成功
}

void ASampleGameModeBase::OnLoginCancel()
{
    // ログインをキャンセル
}

void ASampleGameModeBase::OnLoginFailure(FNError NError)
{
   // ログインに失敗
    // NError.messageをポップアップなどでユーザーに知らせてください。
}


// メンテナンス（ダッシュボードでメンテナンスが有効化している場合に呼び出す）
void ASampleGameModeBase::OnLoginMaintenance(FNAppStatus NAppStatus)
{
   // やる事：パラメータに渡されたステータス情報をもとにポップアップを作り、ユーザーに知らせてください。
    // やる事：以下の二つの方式のうち一つを選択してください。
    // ケース1：ゲーム内ポップアップを通じて開発会社で直接UIを実装
    // ケース2：SDKのポップアップを使用（この場合は以下のコードを呼び出してください。）

    IGamePotSdk* ptr = FGamePotSDKPluginModule::GetSharedGamePotSdk();
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
        ptr->showAppStatusPopup(NAppStatus.ToJsonString());
}

// 強制アップデート（ストアバージョンとゲームクライアントバージョンが異なる場合に呼び出す）
void ASampleGameModeBase::OnLoginNeedUpdate(FNAppStatus NAppStatus)
{
     // やる事：パラメータに渡されたステータス情報をもとにポップアップを作り、ユーザーに知らせてください。
    // やる事：以下の二つの方式のうち一つを選択してください。
    // ケース1：ゲーム内ポップアップを通じて開発会社で直接UIを実装
    // ケース2：SDK独自のポップアップUIを利用（この場合は以下のコードを呼び出してください。）

    IGamePotSdk* ptr = FGamePotSDKPluginModule::GetSharedGamePotSdk();
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
        ptr->showAppStatusPopup(NAppStatus.ToJsonString());
}

void ASampleGameModeBase::OnLoginExit()
{
   // やる事：強制アップデートやメンテナンス機能をケース2の方式で実装する場合
    // やる事：アプリを強制終了できるため、ここでアプリを終了できるように実装してください。
}

void ASampleGameModeBase::OnAppClose()
{
    // アプリ終了
    // やる事：強制アップデートやメンテナンス機能をケース2の方式で実装する場合
    // やる事：アプリを強制終了できるため、ここでアプリを終了できるように実装してください。
}

```

NAppStatusの定義

```c++
USTRUCT()
struct FNAppStatus
{
    UPROPERTY()
    FString type;       // AppStatusタイプで「maintenance」：メンテナンス、「needupdate」：アップデート
   
    UPROPERTY()
    FString message;    // メンテナンスの設定：Dashboardで入力したメッセージ

    UPROPERTY()
    FString url;        // メンテナンスの設定：Dashboardで入力したURL
    
    UPROPERTY()
    FString currentAppVersion;  // アップデート：現在のApp Version
    
    UPROPERTY()
    FString updateAppVersion;   // アップデート：Dashboardで入力したApp Version
    
    UPROPERTY()
    int currentAppVersionCode;  // アップデート：現在のApp Code
    
    UPROPERTY()
    FString updateAppVersionCode;   // アップデート：Dashboardで入力したApp Version code
    
    UPROPERTY()
    bool isForce;       // アップデート：Dashboardで強制アップデート設定時、true
    
    UPROPERTY()
    FString resultPayload;  // クライアントSDKから伝達されたJson値で、無視しても構いません。
    
    UPROPERTY()
    double startedAt;    // メンテナンス：開始時間（timestamp）
    
    UPROPERTY()
    double endedAt;     // メンテナンス：終了時間（timestamp）
}
```

### 自動ログイン<a name="自動ログイン"></a>


```c++
ENLoginType::Type loginType =  FGamePotSDKPluginModule::GetSharedGamePotSdk()->getLastLoginType();

if(loginType != ENLoginType::NONE) {
{
    // 最後にログインしたログインタイプでログインする方式です。
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->Login(loginType);
}
else
{
    // 初めてゲームを実行したか、ログアウトした状態。ログインできるログイン画面に移動してください。
}
```

### ログアウト<a name="ログアウト"></a>


ユーザーをログアウトさせます。アカウントは削除されず、同じアカウントでログインできます。

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
    // ログアウトに失敗した場合
    // NError.messageをポップアップなどでユーザーに知らせてください。
}
```

### 退会<a name="退会"></a>


会員退会します。復旧はできません。

- Case 1

Request:

```c++

if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->deleteMember();
```

Response:

```c++
/// 会員退会に成功
void ASampleGameModeBase::OnDeleteMemberSuccess()
{

}

void ASampleGameModeBase::OnDeleteMemberFailure(FNError NError)
{
   // 会員退会に失敗した場合
    // NError.messageをポップアップなどでユーザーに知らせてください。
}
```

### 検証<a name="検証"></a>


ログイン完了後、ログイン情報を開発会社のサーバからGAMEPOTサーバに伝達するとログイン検証が行われます。

詳しい説明はServer to server apiメニューの`Token Authentication`項目を参考にしてください。

## 5.アカウント連携<a name="5.アカウント連携"></a>


一つのゲームアカウントに複数のソーシャルアカウント（Google/Facebookなど）を連携/解除できる機能です。（最小連携ソーシャルアカウント数は一つです。）


>連携画面のUIは開発会社で実装してください。



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

### 連携<a name="連携"></a>


Google / FacebookなどのIDでアカウントを連携できます。

- Case 1

Request:

```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->createLinking(ENLinkingType::Type linkingType);
```

Response:

```c++
void ASampleGameModeBase::OnCreateLinkingSuccess(FNUserInfo NUserInfo) {
        // アカウント連携に成功
}

void ASampleGameModeBase::OnCreateLinkingCancel() {
        // ユーザーがアカウント連携をキャンセルした場合

}
void ASampleGameModeBase::OnCreateLinkingFailure(FNError NError) {
        // アカウント連携に失敗した場合
        // NError.messageをポップアップなどでユーザーに知らせてください。
}

```

現在連携されているすべてのアカウント情報を取得できます。

```c++  
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
     TArray<FNLinkingInfo> linkedList = FGamePotSDKPluginModule::GetSharedGamePotSdk()->getLinkedList();
```

リンキング情報の定義

```c++
USTRUCT()
struct FNLinkingInfo
{
    UPROPERTY()
    ENLinkingType::Type provider;      // アカウント連携情報（Google、Facebook、NAVER、Apple..）
}
```

### 連携解除<a name="連携解除"></a>


現在連携されているアカウントを解除します。

- Case 1

Request :

```c++

if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->deleteLinking(ENLinkingType::Type linkType);

```

Response:

```c++

void ASampleGameModeBase::OnDeleteLinkingSuccess() {
/// アカウント連携の解除に成功
}

void ASampleGameModeBase::OnDeleteLinkingFailure(FNError NError) {
    /// アカウント連携の解除に失敗
     // 連携解除に失敗した場合
    // NError.messageをポップアップなどでユーザーに知らせてください。
}
```

## 6. 決済<a name="6.決済"></a>


### In-App商品照会<a name="InApp商品照会"></a>


ストアに登録された商品情報を伝達します。

この機能を活用すると、各ユーザに応じた料金、通貨、商品名が表示されます。

```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    TArray<FNPurchaseItem> itemList = FGamePotSDKPluginModule::GetSharedGamePotSdk()->getPurchaseItems();
```

### NPurchaseItemの定義<a name="NPurchaseItemの定義"></a>


NPurchaseItemの定義

```c++
USTRUCT()
struct FNPurchaseItem
{
    UPROPERTY()
    FString productId;              // 商品ID

    UPROPERTY()
    FString type;                   // 商品のタイプを「inapp」に固定

    UPROPERTY()
    FString price;                  // 価格 Googleストア：$0.99 その他のストア：0.99

    UPROPERTY()
    FString price_amount;           // 通貨コード ex）KRW、USD

    UPROPERTY()
    FString price_amount_micros;    // （UIに表示する場合に推奨）通貨と価格が合算された値は、ONEストアの場合、通貨単位が伝達されません。 ex）$0.99

    UPROPERTY()
    FString price_currency_code;

    UPROPERTY()
    FString price_with_currency;

    UPROPERTY()
    FString title;                   // 商品名

    UPROPERTY()
    FString description;            // 商品説明
}
```

### In-App商品決済<a name="InApp商品決済"></a>


以下の関数一つでGoogle、Apple、APPSTORE決済が可能になります。

- Case 1

Request:

```c++
// productId：ストアに登録されている商品IDを入力します。
// uniqueId：別途管理する領収証番号を入力します。
// serverId：決済を行ったキャラクターのサーバIDを入力します。
// playerId：決済を行ったキャラクターのキャラクターIDを入力します。
// etc：決済を行ったキャラクターのその他の情報を入力します。

if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->purchase(FString productId, FString uniqueId, FString serverId, FString playerId, FString etc);

```

### FNPurchaseInfoの定義<a name="FNPurchaseInfoの定義"></a>


決済成功後に決済したアイテム情報です。参考用にしてください。

```c++

USTRUCT()
struct FNPurchaseInfo
{
    UPROPERTY()
    FString price;                         // 決済アイテムの価格
    UPROPERTY()
    FString productId;                  // 決済アイテムID
    UPROPERTY()
    FString currency;                    // 決済価格の通貨（KRW/USD）
    UPROPERTY()
    FString orderId;                      // ストアOrder ID
    UPROPERTY()
    FString productName;            // 決済アイテム名
    UPROPERTY()
    FString gamepotOrderId;         // （GAMEPOTで作成した）Order ID
    UPROPERTY()
    FString uniqueId;                    // （開発会社で別途管理する）領収証ID
    UPROPERTY()
    FString serverId;                    // （決済を行ったキャラクターの）サーバID
    UPROPERTY()
    FString playerId;                    // （決済を行ったキャラクターの）キャラクターID
    UPROPERTY()
    FString etc;                         // （決済を行ったキャラクターの）その他の情報
    UPROPERTY()
    FString signature;                  // ストアのSignature
    UPROPERTY()
    FString originalJSONData;   // 領収証Data
}
```

Response:

```c++
/// In-App決済に成功
 void ASampleGameModeBase::OnPurchaseSuccess(FNPurchaseInfo NPurchaseInfo)
 {
 }

/// In-App決済をキャンセル
 void ASampleGameModeBase::OnPurchaseCancel()
 {
 }

/// In-App決済に失敗
 void ASampleGameModeBase::OnPurchaseFailure(FNError NError)
 {
       // 決済に失敗した場合
    // NError.messageをポップアップなどでユーザーに知らせてください。
 }
```

### 決済アイテム支給<a name="決済アイテム支給"></a>

GAMEPOTは、Server to server apiを通じて決済ストアの領収証検証まですべて完了してから開発会社のサーバに支給リクエストをするため、不正決済はできません。

そのためには`Server to server api`メニューの`Purchase Webhook`項目を参考にして処理してください。

### 外部決済<a name="外部決済"></a>


外部決済を許可しているストアと、公式ストアではないところで決済を使用できる機能です。


呼び出しAPIだけが異なり、レスポンスやPurchase Webhookなどその他は一般決済と同じです。
機能を使用するには設定が必要です。ダッシュボードマニュアルの「外部決済」項目を参考にしてください。


- Case 1

Request:

```csharp

```c++
// productId：マーケットに登録された商品ID
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->purchaseThirdPayments(FString productId);
```

外部決済を利用する場合、商品情報リストは以下のAPIを使用してください。

Request:

```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    TArray<FNPurchaseItem> itemList = FGamePotSDKPluginModule::GetSharedGamePotSdk()->getPurchaseThirdPaymentsItems();
```

## 7. その他のAPI<a name="7.その他のAPI"></a>

### SDKサポートログインUI<a name="SDKサポートログインUI"></a>


SDK内で、独自に（完成した形の）Login UIを提供します。

### FNLoginUIInfoの定義<a name="FNLoginUIInfoの定義"></a>


```c++
USTRUCT()
struct FNLoginUIInfo
{
    //画像ロゴ挿入の有無
    UPROPERTY()
    bool showLogo;

    //UIで表示するLogin Type
    UPROPERTY()
    TArray<ENLoginType::Type> loginTypes;  //Google、Facebook...
}
```

#### SDKログインUIの呼び出し<a name="SDKログインUIの呼び出し"></a>


- Case 1

Request:

```c++
//呼び出すログインUIタイプ
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showLoginWithUI(FNLoginUIInfo NLoginUIInfo);
```

Response:

```c++
void ASampleGameModeBase::OnLoginSuccess(FNUserInfo NUserInfo)
{
    // ログインに成功
}

void ASampleGameModeBase::OnLoginCancel()
{
    // ログインをキャンセル
}

void ASampleGameModeBase::OnLoginFailure(FNError NError)
{
   // ログインに失敗
    // error.messageをポップアップなどでユーザーに知らせてください。
}
```

Response:

 **一般ログインAPIレスポンスロジックと同じです。（ただし、onLoginCancel / onLoginFailureの場合、Nativeレベルでトーストメッセージで処理されます。）**

```c++

void ASampleGameModeBase::OnLoginSuccess(FNUserInfo NUserInfo)
{
    // ログインに成功
}

void ASampleGameModeBase::OnLoginCancel()
{
    // ログインをキャンセル
}

// メンテナンス（ダッシュボードでメンテナンスが有効化している場合に呼び出す）
void ASampleGameModeBase::OnLoginMaintenance(FNAppStatus NAppStatus)
{
   // やる事：パラメータに渡されたステータス情報をもとにポップアップを作り、ユーザーに知らせてください。
    // やる事：以下の二つの方式のうち一つを選択してください。
    // ケース1：ゲーム内ポップアップを通じて開発会社で直接UIを実装
    // ケース2：SDKのポップアップを使用（この場合は以下のコードを呼び出してください。）

    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
        FGamePotSDKPluginModule::GetSharedGamePotSdk()->showAppStatusPopup(NAppStatus.ToJsonString());
}

// 強制アップデート（ストアバージョンとゲームクライアントバージョンが異なる場合に呼び出す）
void ASampleGameModeBase::OnLoginNeedUpdate(FNAppStatus NAppStatus)
{
     // やる事：パラメータに渡されたステータス情報をもとにポップアップを作り、ユーザーに知らせてください。
    // やる事：以下の二つの方式のうち一つを選択してください。
    // ケース1：ゲーム内ポップアップを通じて開発会社で直接UIを実装
    // ケース2：SDKのポップアップを使用（この場合は以下のコードを呼び出してください。）

    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
        FGamePotSDKPluginModule::GetSharedGamePotSdk()->showAppStatusPopup(NAppStatus.ToJsonString());
}

void ASampleGameModeBase::OnLoginExit()
{
    // やる事：LoginUIを終了する際に
}

void ASampleGameModeBase::OnAppClose()
{
    // アプリ終了
    // やる事：強制アップデートやメンテナンス機能をケース2の方式で実装する場合
    // やる事：アプリを強制終了できるため、ここでアプリを終了できるように実装してください。
}

```


#### Customizing<a name="Customizing"></a>


**ログインUI画像ロゴの変更方法**

ログインUI上段に表示される画像ロゴは、SDKの内部で基本画像が表示され、直接追加することもできます。

**[Android]**


>直接追加するには`drawable`フォルダ別に画像を追加する必要があります。（[Android Asset Studio](http://romannurik.github.io/AndroidAssetStudio/icons-notification.html#source.type=clipart&source.clipart=ac_unit&source.space.trim=1&source.space.pad=0&name=ic_stat_gamepot_login_logo)を利用して作成すると、自動的にフォルダ別に画像が作成されるため便利です。）


画像ファイル名は ic_stat_gamepot_login_logo.pngにしてください。

|フォルダ名|サイズ|
| :------------------------------------------------------------- | :---- |
| $S(PluginDir)/ThirdParty/GamePotResources/res/drawable-mdpi/    | 24x24 |
| $S(PluginDir)/ThirdParty/GamePotResources/res/drawable-hdpi/    | 36x36 |
| $S(PluginDir)/ThirdParty/GamePotResources/res/drawable-xhdpi/   | 48x48 |
| $S(PluginDir)/ThirdParty/GamePotResources/res/drawable-xxhdpi/  | 72x72 |
| $S(PluginDir)/ThirdParty/GamePotResources/res/drawable-xxxhdpi/ | 96x96 |



### Appleログイン（forAndroid - Web Login）<a name="AppleログインforAndroidWeb Login"></a>


#### GAMEPOT Dashboard<a name="GAMEPOTDashboard Login"></a>

ダッシュボードのプロジェクトの設定 >> 一般 >> Apple ID Loginの設定


>機能を使用するにはApple Developer Console設定が必要です。
>ダッシュボードで当該項目の**ヘルプを見る**を参考にしてください。



GamePot_Android_UPL.xml 수정

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

$S(PluginDir)/ThirdParty/Android/libs 経路に以下のaarファイルを追加します。

- gamepot-channel-apple-signin.aar


### NAVERログイン<a name="NAVERログイン"></a>


#### Naver Developers<a name="NaverDevelopers"></a>


使用APIを`ネアロ（NAVER IDでログイン）`にし、アプリケーションを登録

#### Android<a name="Android3"></a>


GamePot_Android_UPL.xmlの修正

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

Consoleで発行されたClient IDを`gamepot_naver_clientid`値に入力し、Client Secretは`gamepot_naver_secretid`値に入力します。

$S(PluginDir)ThirdParty/Android/libs 経路に以下のaarファイルを追加します。

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

GamePotConfig-Info.plistファイルに以下の項目を追加し、当該値を入力します。

```text
gamepot_naver_clientid // NAVERで使用するClient ID
gamepot_naver_secretid // NAVERで使用するSecret ID
gamepot_naver_urlscheme // NAVERで使用するURL Scheme
```

GamePotConfig-Info.plistファイルをSourceCodeと見る場合、以下のように追加

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

### LINEログイン<a name="LINEログイン"></a>


#### LINE Developers<a name="LINEDevelopers"></a>


APKをビルドする際に使用したパッケージ名とkeystoreのSHA値、URL Scheme値をLINEのコンソールに追加します。

#### Android<a name="Android4"></a>


GamePot_Android_UPL.xmlの修正

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

$S(PluginDir)/ThirdParty/Android/libs 経路に以下のaarファイルを追加します。

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

GamePotConfig-Info.plistファイルに以下の項目を追加し、当該値を入力します。

```text
gamepot_line_channelid // NAVERで使用するClient ID
gamepot_line_url_schemes // Line URL Scheme (line3rdp.{プロジェクトバンドルidentifier})
```

GamePotConfig-Info.plistファイルをSourceCodeと見る場合、以下のように追加します。

```markup
...
<key>gamepot_line_channelid</key>
<string>xxxxxx</string>
<key>gamepot_line_url_schemes</key>
<string>xxxxxx</string>
...
```

### Twitterログイン<a name="Twitterログイン"></a>


#### Twitter Developers<a name="TwitterDevelopers"></a>


#### Android<a name="Android5"></a>


GamePot_Android_UPL.xmlの修正

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

/Plugin/GamePotSDKPlugin/Source/GamePot/ThirdParty/Android/libs 経路に以下のaarファイルを追加します。

- gamepot-channel-twitter.aar
- twitter-core-3.3.0.aar



#### iOS<a name="iOS5"></a>


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

GamePotConfig-Info.plistファイルに以下の項目を追加し、当該値を入力します。

```text
gamepot_twitter_consumerkey : Twitter Consumer Key
gamepot_twitter_consumersecret :  Twitter Consumer Secret
```

GamePotConfig-Info.plistファイルをSourceCodeと見る場合、以下のように追加

```markup
...
<key>gamepot_twitter_consumerkey</key>
<string>xxxxxx</string>
...
```

### クーポン<a name="クーポン"></a>


#### クーポン使用<a name="クーポン使用"></a>



>クーポンを入力するUIは開発会社で実装してください。



- Case 1

Request:

```c++
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    {
        FGamePotSDKPluginModule::GetSharedGamePotSdk()->coupon(FString couponNumber); // クーポン番号

        FGamePotSDKPluginModule::GetSharedGamePotSdk()->coupon(FString couponNumber, FString userData); // クーポン番号、ユーザー情報
    }
```

Response:

```c++
void ASampleGameModeBase::OnCouponSuccess(FString msg)
{
    /// クーポン使用に成功
}

void ASampleGameModeBase::OnCouponFailure(FNError NError)
{
      // クーポン使用に失敗した場合
    // error.messageをポップアップなどでユーザーに知らせてください。
}
```

#### アイテム支給<a name="アイテム支給"></a>


クーポンの使用に成功すると、開発会社のサーバにServer to server apiを通じてアイテム支給をリクエストします。

そのためにはServer to server apiメニューの`Item Webhook`項目を参考にして処理してください。

### Push on/off<a name="Pushonoff"></a>


プッシュ、夜間プッシュ通知をそれぞれON/OFFにできます。


>ON/OFFを設定するUIは開発会社で実装してください。



#### プッシュ通知設定<a name="プッシュ通知設定"></a>


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
    /// プッシュ通知の状態変更に関するサーバ通信に成功
}

void ASampleGameModeBase::OnPushFailure(FNError NError)
{
        // プッシュ通知の状態変更に失敗した場合
    // error.messageをポップアップなどでユーザーに知らせてください。
}
```


#### 夜間プッシュ通知設定<a name="夜間プッシュ通知設定"></a>

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
    /// プッシュ通知の状態変更に関するサーバ通信に成功
}

void ASampleGameModeBase::OnPushNightFailure(FNError NError)
{
        // プッシュ通知の状態変更に失敗した場合
    // error.messageをポップアップなどでユーザーに知らせてください。
}
```

#### プッシュ型広告設定<a name="プッシュ型広告設定"></a>


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
    /// プッシュ通知の状態変更に関するサーバ通信に成功
}

void ASampleGameModeBase::OnPushFailure(FNError NError)
{
        // プッシュ通知の状態変更に失敗した場合
    // error.messageをポップアップなどでユーザーに知らせてください。
}
```

#### プッシュ通知 / 夜間プッシュ通知 / プッシュ型広告を一度に設定<a name="プッシュ通知夜間プッシュ通知プッシュ型広告を一度に設定"></a>


ログイン前にプッシュ / 夜間プッシュ通知のOn/Offを設定するゲームの場合、ログインの後に以下のコードを必ず呼び出します。

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
    /// プッシュ通知の状態変更に関するサーバ通信に成功
}

void ASampleGameModeBase::OnPushStatusFailure(FNError NError)
{
        // プッシュ通知の状態変更に失敗した場合
    // error.messageをポップアップなどでユーザーに知らせてください。
}
```

#### プッシュ通知の状態照会<a name="プッシュ通知の状態照会"></a>


- FNPushInfoの定義

```c++
USTRUCT()
struct FNPushInfo
{
    UPROPERTY()
    bool enable;       // （一般）プッシュ通知を許可するかどうか

    UPROPERTY()
    bool night;         // 夜間プッシュ通知を許可するかどうか

    UPROPERTY()
    bool ad;            // 広告型プッシュ通知を許可するかどうか
}
```

Request:

```c++
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
        FNPushInfo NPushInfo = FGamePotSDKPluginModule::GetSharedGamePotSdk()->getPushStatus();
```

### 案内事項<a name="案内事項"></a>


GAMEPOTダッシュボードで「案内事項」に追加した画像を順に表示する機能です。

推奨する画像スペックは以下のとおりです。

- サイズ：720 _1200（Portrait） / 1280_ 640（Landscape）


>記のサイズを守らない場合、center cropで画像を処理します。



- 容量：250KB以下

Request:

```c++

if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showNotice(bool showToday = true);

// true：「今日は表示しない」を適用
// false：「今日は表示しない」とは関係なしに強制表示
```

```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showEvent(FString Type);

// タイプ：ダッシュボードの案内事項 >> 分類で設定した分類名に該当する画像のみ表示
```

Response:

GAMEPOTダッシュボードで`クリックアクション`を`SCHEME`に設定した場合、当該画像をクリックすると`SCHEME`値を伝達します。

```c++
 void ASampleGameModeBase::OnReceiveScheme(FString scheme)
 {
      // GAMEPOTダッシュボードで設定したscheme値を伝達
 }
```

### サポートセンター<a name="サポートセンター"></a>


顧客が運営者に対して問い合わせを登録して返答を受け取れる機能です。

問い合わせのUIはデバイスの言語に応じて変更されます。韓国語、英語、日本語、中国語（簡体字、繁体字）に対応し、その他の言語は英語で表示されます。

#### 呼び出し<a name="呼び出し1"></a>


```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showCSWebView();
```

外部リンクをサポートし、ログインしていない顧客も問い合わせを登録できます。

#### 呼び出し<a name="呼び出し2"></a>

```c++
// URL：GAMEPOTから発行された外部サポートセンターURL
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showWebView(FString url);
```

### ローカルプッシュ（Local Push notification）<a name="ローカルプッシュLocalPushnotification"></a>


プッシュサーバを介さずに端末にプッシュを表示する機能です。

#### プッシュ登録<a name="プッシュ登録"></a>


決められた時間にローカルプッシュを表示する方法は以下のとおりです。


>戻り値として返ってくるpushIdは開発会社で管理します。



```c++
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
         int pushId = FGamePotSDKPluginModule::GetSharedGamePotSdk()->sendLocalPush(FString date, FString title, FString message);

// date : (Format - timestamp "yyyy-MM-dd HH:mm:ss")
// ex >  DateTime.Parse("2018-01-01 00:00:00")
//  title :  "title"
// message :  "content"
```

#### 登録したプッシュのキャンセル<a name="登録したプッシュのキャンセル"></a>


プッシュ登録の際に取得したpushIdをもとに、これまでに登録したプッシュをキャンセルできます。

```c++
    if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
         bool success = FGamePotSDKPluginModule::GetSharedGamePotSdk()->cancelLocalPush(int /*プッシュ登録の際に取得したpushId*/);
```

### Image Push (iOS)<a name="ImagePush"></a>

Unrealは、プロジェクトにNotification Service Extensionを追加できる方法を提供していない。
iOS Image Push機能を使用できません。


### 規約に同意<a name="規約に同意"></a>


「利用規約」と「個人情報の収集及び利用に関する案内」の同意をスムーズに行えるようにUIを提供します。

`BLUE`テーマと`GREEN`テーマの2種類の`基本テーマ`の他にも、新たに追加された11種類の`改善テーマ`を提供します。

各領域別にCustomizingも可能です。

#### 規約同意を呼び出す<a name="規約同意を呼び出す"></a>


#### FNAgreeInfoの定義<a name="FNAgreeInfoの定義"></a>


```c++
USTRUCT()
struct FNAgreeInfo
{
    // 基本テーマ
    UPROPERTY()
    FString theme;
    
    // タイトル
    // 背景カラー（gradient）
    UPROPERTY()
    TArray<FString> headerBackGradient;
    
    // タイトル領域の下段ラインのカラー
    UPROPERTY()
    FString headerBottomColor;
    
    // アイコン画像のファイル名（aos - drawable / ios - bundle）
    UPROPERTY()
    FString headerIconDrawable;
    
    // タイトル
    UPROPERTY()
    FString headerTitle;
    
    // タイトルカラー
    UPROPERTY()
    FString headerTitleColor;
    
    // コンテンツ
    // 背景カラー（gradient）
    UPROPERTY()
    TArray<FString> contentBackGradient;
  
    // アイコン画像のファイル名（aos - drawable / ios - bundle）
    UPROPERTY()
    FString contentIconDrawable;
    
    // アイコンのカラー
    UPROPERTY()
    FString contentIconColor;
   
    // チェックボタンのカラー
    UPROPERTY()
    FString contentCheckColor;
    
    // チェック内容のカラー
    UPROPERTY()
    FString contentTitleColor;
    
    // 見るフレーズのカラー
    UPROPERTY()
    FString contentShowColor;
    
    // 下段（ゲーム開始）
    // 背景カラー（gradient）
    UPROPERTY()
    TArray<FString> footerBackGradient;
  
    // ゲーム開始ボタンの背景カラー（gradient）
    UPROPERTY()
    TArray<FString> footerButtonGradient;
    
    // ゲーム開始ボタンのフレームカラー
    UPROPERTY()
    TArray<FString> footerButtonOutlineColor;

    // ゲーム開始フレーズ
    UPROPERTY()
    TArray<FString> footerTitle;

    // ゲーム開始フレーズのカラー
    UPROPERTY()
    TArray<FString> footerTitleColor;
    
    //一般プッシュの表示有無
    UPROPERTY()
    bool showPush;
    
    // 夜間プッシュの表示有無
    UPROPERTY()
    bool showNightPush;
    
    // 「すべて同意」フレーズ変更時
    UPROPERTY()
    FString allMessage;
    
    // 「利用規約」フレーズ変更時
    UPROPERTY()
    FString termMessage;
    
    // 「個人情報の取扱方針」フレーズ変更時
    UPROPERTY()
    FString privacyMessage;
    
    // 「一般プッシュ」フレーズ変更時
    UPROPERTY()
    FString pushMessage;
    
    // 「夜間プッシュ」フレーズ変更時
    UPROPERTY()
    FString nightPushMessage;
    
    UPROPERTY()
    FString pushDetailURL;
    
    UPROPERTY()
    FString nightPushDetailURL;
}

```


>規約同意のポップアップの表示有無は、開発会社でゲームに合わせて処理してください。
**[見る]** ボタンをクリックすると表示される内容は、ダッシュボードで適用及び修正できます。


- Case 1

Request:

```c++

// ケース1）基本呼び出し（BLUEテーマを適用）
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showAgreeDialog();

// ケース2）その他のテーマを適用時
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
{
    // - 基本テーマ
    // BLUE
    // GREEN
    
    // - 改善テーマ
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
// 規約に同意した場合
void ASampleGameModeBase::OnAgreeDialogSuccess(FNAgreeResultInfo NAgreeResultInfo)
{
       // NAgreeResultInfo.agree : 規約の必須事項にすべて同意した場合、true
        // NAgreeResultInfo.agreePush : （一般）プッシュ通知を許可した場合はtrue、そうでない場合はfalse
        // NAgreeResultInfo.agreeNight : 夜間プッシュ型広告の通知を許可した場合はtrue、そうでない場合はfalse
        // agreeNight値はログインを完了してからsetPushNightStatus APIを通じて伝達してください。
}

void ASampleGameModeBase::OnAgreeDialogFailure(FNError NError)
{
    // エラー発生
}
```

-  Customizing

それぞれの変数は以下の領域に適用されます。



>contentIconDrawableはAOSでのみ表示され、基本値はプッシュアイコンとして設定されます。


![gamepot_unreal_002_ja.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_unreal_002_ja.png)


### 利用規約<a name="利用規約"></a>


利用規約UIを呼び出します。


> ダッシュボード - サポートセンター - 利用規約の設定項目にまず内容を入力してください。



```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showTerms();
```

### 個人情報の取扱方針<a name="個人情報の取扱方針"></a>


個人情報の取扱方針UIを呼び出します。


>ダッシュボード - サポートセンター - 個人情報の取扱方針の設定項目にまず内容を入力してください。


```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showPrivacy();
```

### 払い戻し規約<a name="払い戻し規約"></a>


払い戻し規約UIを呼び出します。


>ダッシュボード - サポートセンター - 払い戻し規約の設定項目にまず内容を入力してください。



```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->showRefund();
```

### Remote Config<a name="RemoteConfig"></a>


ダッシュボードで登録したパラメータ値をゲームクライアントから取得します。


>ダッシュボード - 設定 - Remote Config画面でパラメータを追加します。
>追加したパラメータはログイン時にロードされ、その後から呼び出すことができます。




```c++
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
{
    //"test_01"：パラメータFString
    FString value = FGamePotSDKPluginModule::GetSharedGamePotSdk()->getConfig("test_01");

    //ダッシュボードに追加したすべてのパラメータをjson string形式で取得します。
    FString json_value = FGamePotSDKPluginModule::GetSharedGamePotSdk()->getConfigs();
}
```

### 決済キャンセルを悪用するユーザーを自動的に解除する機能<a name="決済キャンセルを悪用するユーザーを自動的に解除する機能"></a>

決済キャンセルを悪用するユーザーを自動的に解除する機能のUIを提供します。各領域別にカスタマイズできます。


Google決済に限って、ユーザーが任意にGoogleにリクエストして決済をキャンセルした場合、「Google決済キャンセル」機能を通じてそのユーザーを利用停止させることができます。
この時、そのユーザーがログインするとSDK内でポップアップを表示して当該決済アイテムを再決済するように誘導し、
決済したら再び正常にアクセスできる機能を提供します。
キャンセルした決済をすべて再決済すると、自動的に利用停止が解除されます。


### NVoidInfoの定義<a name="NVoidInfoの定義"></a>


```c++
USTRUCT()
struct FNVoidInfo
{
    // 基本テーマ
    UPROPERTY()
    FString theme;
    
    // 背景カラー（gradient）
    UPROPERTY()
    TArray<FString> headerBackGradient;
    
    // タイトル
    UPROPERTY()
    FString headerTitle;
    
    // タイトルカラー
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
   
   // 背景カラー（gradient）
    UPROPERTY()
    TArray<FString> footerBackGradient;
    
    // ボタンの背景カラー（gradient）
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
        //テーマの種類
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

### ゲームログの伝送<a name="ゲームログの伝送"></a>


ゲームで使用される情報を入れて呼び出すと、`ダッシュボード` - `ゲーム`で照会できます。

以下は使用できる予約語の定義表です。

|予約語|必須|タイプ|説明|
| :-------------------------------- | :--- | :----- | :----------- |
|FNSendLogCharacter.NAME      |必須|FString |キャラクター名|
|FNSendLogCharacter.LEVEL     |任意|FString |レベル|
|FNSendLogCharacter.SERVER_ID |任意|FString |サーバID|
|FNSendLogCharacter.PLAYER_ID |任意|FString |キャラクターID|
|FNSendLogCharacter.USERDATA  |任意|FString |ETC          |

### FNSendLogCharacterの定義<a name="FNSendLogCharacterの定義"></a>


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

### GDPR規約チェックリスト<a name="GDPR規約チェックリスト"></a>


ダッシュボードで有効化した、GDPR規約項目をリストの形で取得します。

```c++
//リターンされるデータ形式はFStringタイプで、string[]の形式です。ex> "[ gdpr_privacy, gdpr_term ]"
if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FString gdpr_list = FGamePotSDKPluginModule::GetSharedGamePotSdk()->getGDPRCheckedList();

// gdpr_privacy : 個人情報の取扱方針
// gdpr_term : 利用規約
// gdpr_gdpr : GDPR利用規約
// gdpr_push_normal : イベントPush受信に同意
// gdpr_push_night : 夜間イベントPush受信に同意（韓国のみ対象）
// gdpr_adapp_custom : パーソナライズド広告を見るに同意（GDPR適用国）
// gdpr_adapp_nocustom : 非パーソナライズド広告を見るに同意（GDPR適用国）
```

## 付録<a name="付録"></a>


### 3rd party SDK連携サポート<a name="3rdpartySDK連携サポート"></a>


## ログイン<a name="ログイン2"></a>



>自動ログインに対応しない。毎回呼び出しが必要。


|パラメータ名|必須|タイプ|説明|
| :--------- | :--- | :----- | :----------------- |
|userid     |必須|FString |ユーザーの固有ID|

```c++
FString userid = TEXT("memberid of 3rd party sdk");

if (FGamePotSDKPluginModule::IsGamePotSdkAvailable())
    FGamePotSDKPluginModule::GetSharedGamePotSdk()->loginByThirdPartySDK(userid);
```

## 決済<a name="決済"></a>



>決済アイテムがGAMEPOTのダッシュボードに登録されている必要があります。


|パラメータ名|必須|タイプ|説明|
| :------------ | :--- | :----- | :----------------------------------------- |
|productid     |必須|FString |GAMEPOTのダッシュボードに登録されたアイテムID|
|transactionid |必須|FString |決済領収証番号（GPA-xxx-xxxx-xxxx）|
|store         |必須|FString |（決済ストア - Google、Apple、ONE、Galaxy）|
|currency      |任意|FString |通貨（KRW、USD）|
|price         |任意|double |決済アイテム金額|
|paymentid     |任意|FString |決済payment（一般的にはstore_idと同じ）|
|uniqueid      |任意|FString |開発会社で使用する固有ID|

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
