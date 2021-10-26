## 1. 始める<a name="1始める"></a>


### Step 1. GAMEPOT プラグインをダウンロードする<a name="Step1GAMEPOTプラグインをダウンロードする"></a>


作成した GAMEPOT ダッシュボードにアクセスして、最新プラグインをダウンロードします。

### Step 2. プラグインをインポートする<a name="Step2プラグインをインポートする"></a>


**Assets > Import Package > Custom Package**メニューでダウンロードした GamePotUnityPlugin-xxxx.unitypackage ファイルを選択します。

![gamepot_unity_01.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_unity_01%2812%29.png)

プラグインを確認してインポートすると、当該プロジェクトに追加されます。

![gamepot_unity_02.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_unity_02%2812%29.png)

### Step 3. Android<a name="Step3Android"></a>


#### 基本環境設定<a name="基本環境設定"></a>


```d
minSdkVersion : API 17 (Jelly Bean, 4.2) 以上
```

**Gradle 環境の設定方法**

/Assets/Plugin/Android/mainTemplate.gradle ファイルをエディタで開きます。

```java
...
android {
    ...
    defaultConfig {
        ...
        resValue "string", "gamepot_project_id", "" // required
        resValue "string", "gamepot_store", "google" // required
        resValue "string", "gamepot_payment", "[storeId]" // optional
        resValue "string", "gamepot_app_title","@string/app_name" // required (fcm)
        resValue "string", "gamepot_push_default_channel","Default" // required (fcm)
        resValue "string", "facebook_app_id", "0" // optional (facebook)
        resValue "string", "fb_login_protocol_scheme", "fb0" // optional (facebook)
        // resValue "string", "gamepot_elsa_projectid", "" // optional (ncp elsa)
    }
    ...
}
```

以下の必須値を探して修正します。以下の値を修正しないと正常に動作しません。

```java
resValue "string", "[key]", "[value]"
```

| 値                           | 説明                                                         |
| :--------------------------- | :----------------------------------------------------------- |
| gamepot_project_id           | GAMEPOT から発行されたプロジェクト ID を入力してください。   |
| gamepot_store                | ストア値 （`Google`または`One`または`Galaxy`）               |
| gamepot_payment              | 決済方法値 \(ストアがgoogleである場合のみ該当し、現在は `mycard`に対応\) |
| gamepot_app_title            | アプリのタイトル （FCM）                                     |
| gamepot_push_default_channel | 登録された基本チャンネル名 （Default） - 変更しないでください。 |
| facebook_app_id              | Facebook で発行されたアプリ ID                               |
| fb_login_protocol_scheme     | Facebook で発行された protocol scheme fb\[app_id\]           |
| gamepot_elsa_projectid       | NCLOUD ELSA 使用時のプロジェクト ID （[詳しく見る](https://www.ncloud.com/product/analytics/elsa)） |

**Notibar のプッシュアイコン変更方法**

![gamepot_unity_03.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_unity_03%2813%29.png)



プッシュ通知を受ける際に Android Notification bar に表示する Small icon は SDK 内部の基本画像が用いられ、直接追加することもできます。

直接追加するには`drawable`フォルダ別に画像を作成する必要があります。[（Android Asset Studio](http://romannurik.github.io/AndroidAssetStudio/icons-notification.html#source.type=clipart&source.clipart=ac_unit&source.space.trim=1&source.space.pad=0&name=ic_stat_gamepot_small)を用いて作成すると、自動的にフォルダ別に画像が追加されるため便利です。）

画像ファイル名は ic_stat_gamepot_small にしてください。

| フォルダ名                                                   | サイズ |
| :----------------------------------------------------------- | :----- |
| /Assets/Plugins/Android/GamePotResources/res/drawable-mdpi/  | 24x24  |
| /Assets/Plugins/Android/GamePotResources/res/drawable-hdpi/  | 36x36  |
| /Assets/Plugins/Android/GamePotResources/res/drawable-xhdpi/ | 48x48  |
| /Assets/Plugins/Android/GamePotResources/res/drawable-xxhdpi/ | 72x72  |
| /Assets/Plugins/Android/GamePotResources/res/drawable-xxxhdpi/ | 96x96  |

**Screen Orientation の設定方法**

/Assets/Plugin/Android/AndroidManifest.xml ファイルをエディタで開きます。

```markup
...
    <activity android:screenOrientation="sensorLandscape">
      <intent-filter>
        <action android:name="android.intent.action.MAIN" />
          ...
      </intent-filter>
    </activity>
...
```

Main Activity に screenOrientation を追加し、ゲームに応じて`sensorLandscape`もしくは`sensorPortrait`を入力してください。

**Android Resolver Settings**

`Assets > Play Services Resolver > Android Resolver > Settings`メニューに移動します。

![gamepot_unity_04.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_unity_04%2812%29.png)


`Enable Resolution On BuildチェックボックスのチェックをOFF`にしてください。

![gamepot_unity_05.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_unity_05%2812%29.png)

**Unity Build Settings**

`File > Build Settings > Build System`メニューで Gradle を選択します。

![gamepot_unity_06.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_unity_06%2812%29.png)

### Step 4. iOS<a name="Step4iOS"></a>



>GameCenter Login を`使用しない場合`は、以下の位置から当該ファイルを削除してください。>
`Assets/Plugins/IOS/Frameworks/GamePotGameCenter.framework`
当該ライブラリが含まれている場合、`Capabilities設定でGameCenterを必ず有効化`してください。


Google Firebase からダウンロードした`GoogleService-Info.plist`ファイルを`/Assets/Plugins/IOS/`にコピーします。

`/Assets/Plugin/IOS/GamePotConfig-Info.plist`に必要な環境変数を追加してください。

![gamepot_unity_07.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_unity_07%2812%29.png)



| 環境変数                      | 説明                                                       |
| :---------------------------- | :--------------------------------------------------------- |
| gamepot_project_id            | GAMEPOT から発行されたプロジェクト ID を入力してください。 |
| gamepot_facebook_app_id       | Facebook で発行されたアプリ ID                             |
| gamepot_facebook_display_name | Facebook に表示される名前                                  |
| gamepot_google_app_id         | GoogleService-Info ファイルの CLIENT_ID 値                 |
| gamepot_google_url_schemes    | GoogleService-Info ファイルの REVERSED_CLIENT_ID 値        |
| gamepot_elsa_projectid        | NCLOUD ELSA 利用時のプロジェクト ID                        |

scenes を追加してから**File > Build Settings > Build And Run**を実行すると完了します。

![gamepot_unity_08.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_unity_08%2812%29.png)

XCode をビルドしてから

Targets >> Info >> Custom iOS Target Properties に以下の`ユーザー権限取得オプションを追加`してください。

このユーザー権限は GAMEPOT サポートセンター内のファイルアップロード機能で使用されます。

```text
NSCameraUsageDescription
NSPhotoLibraryUsageDescription
```

iOS14 以降

iOS14 バージョンから IDFA 値獲得時にユーザーに権限を獲得しなければなら

IDFA 値獲得が可能なように変更されました。

したがって IDFA 値獲得時にユーザーに権限獲得するポップアップを使用している場合
**Targets > Info > Custom iOS Target Properties** 内の下のユーザーの権限獲得オプションを追加お願いします。



>2020.09.11
Apple の IDFA 値獲得時にユーザーに権限獲得するポップアップ必須適用は 2021 年初めまで延期された
下のリンク参照してお願いします。
[https://developer.apple.com/news/?id=hx9s63c5](https://developer.apple.com/news/?id=hx9s63c5)


```text
NSUserTrackingUsageDescription
```

## 2. 初期化<a name="2初期化"></a>



ゲームを始める際にロードされる最初の画面に使用されるインスタンスに、次のコードを追加します。

```csharp
using GamePotUnity;
public class GamePotLoginSampleScene : MonoBehaviour {
    void Awake() {
        GamePot.initPlugin();
    }
    void Start () {
        GamePot.setListener(  GamePotInterface.cs 継承されたclass );
         // ex) GamePot.setListener(new GamePotSampleListener());
    }

}

ex)
public class GamePotSampleListener : MonoBehaviour , IGamePot {
    ....
}
```

## 3. エラーコード<a name="3エラーコード"></a>


```csharp
public class NError
{
    // 不明なError
    public static readonly int CODE_UNKNOWN_ERROR           = 0;
    // 初期化失敗
    public static readonly int CODE_NOT_INITALIZE           = 1;
    // パラメータが正しくない場合
    public static readonly int CODE_INVAILD_PARAM           = 2;
    // メンバーIDデータがない場合
    public static readonly int CODE_MEMBERID_IS_EMPTY       = 3;
    // ログインされていない状態
    public static readonly int CODE_NOT_SIGNIN              = 4;
    // ネットワークモジュールが初期化されなかった場合
    public static readonly int CODE_NETWORK_MODULE_NOT_INIT = 3000;
    // ネットワークコネクションエラー及びタイムアウト発生時
    public static readonly int CODE_NETWORK_ERROR           = 3001;
    // server-sideで発生するエラー
    public static readonly int CODE_SERVER_ERROR            = 4000;
    // http response codeが成功していない場合
    public static readonly int CODE_SERVER_HTTP_ERROR       = 4001;
    // ネットワークコネクションエラー及びタイムアウト発生時
    public static readonly int CODE_SERVER_NETWORK_ERROR    = 4002;
    // サーバから取得したデータをパースする際のエラー
    public static readonly int CODE_SERVER_PARSING_ERROR    = 4003;
    // 決済で不明なエラー発生及びストア側からError伝達時
    public static readonly int CODE_CHARGE_UNKNOWN_ERROR    = 5000;
    // product idを入力しなかった場合
    public static readonly int CODE_CHARGE_PRODUCTID_EMPTY  = 5001;
    // product idを正しく入力しなかった場合
    public static readonly int CODE_CHARGE_PRODUCTID_WRONG  = 5002;
    // consume時のエラー
    public static readonly int CODE_CHARGE_CONSUME_ERROR    = 5003;

    // error Code
    public int code { get; set; }
    // error Message
    public string message { get; set; }
}
```

## 4. ログイン環境設定<a name="4ログイン環境設定"></a>

### Google ログイン<a name="Googleログイン"></a>


#### Google Firebase Console<a name="GoogleFirebaseConsole"></a>


1.Google Firebase Console で Android 用 google-service.json ファイルをダウンロードしてから`/Assets/Plugins/Android/`にコピーします。
2.APK をビルドする際に使用した Keystore の SHA-1 値を Google Firebase console に追加します。
3.Google Firebase Console で iOS 用 GoogleService-Info.plist ファイルをダウンロードしてから`/Assets/Plugins/IOS/`にコピーします。

**Google ログイン時に onCancel がレスポンスしてログインできない場合、** 以下の内容をチェックしてください。

1.上記で適用リクエストした google-service.json ファイルを正常に適用したか確認 2.ビルドする際に使用したキーストアが、Firebase console に登録した sha-1 を抽出したキーストアなのか確認
3.Firebase console に登録したパッケージ名でビルドしたか確認

### Facebook ログイン<a name="Facebookログイン"></a>


#### Facebook Developer Console<a name="FacebookDeveloperConsole"></a>

Facebookコンソールからアプリ作成の際のアプリタイプ : なし、またはユーザー、またはインスタンスゲーム選択後にアプリ作成


>ライブ展開が可能なアプリチェック > 権限および機能 > public_profile / email 権限が必要です。 


APK をビルドする際に使用した Keystore のキーハッシュ値を Facebook コンソールに追加します。

#### Android<a name="Android1"></a>


mainTemplate.gradle 修正

```java
...defaultConfig {    resValue "string", "facebook_app_id", "1234567890"    resValue "string", "fb_login_protocol_scheme", "fb1234567890"}...
```

Facebook 開発者センターで発行されたアプリ ID を`facebook_app_id`値に入力し、`fb_login_protocol_scheme`値に`fb{facebook_app_id}`を入力します。



>app_id が 1234567890 である場合、fb1234567890 が`fb_login_protocol_scheme`値です。


#### iOS<a name="iOS1"></a>

/Assets/Plugins/IOS/Frameworks のパスに以下のフレームワークを追加します。

FBSDKLoginKit.framework FBSDKCoreKit.framework GamePotFacebook.framework

### APPLE ログイン<a name="APPLEログイン"></a>


>iOSにのみ該当する機能です。(Androidの場合、Web Loginの形でサポート- 8. その他のAPIを参考)


**Xcode > TARGETS > Signing & Capabilities > + Capability > Sign In with Apple を追加します。**

![gamepot_unity_24.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_unity_24%288%29.png)


### ゲームセンターログイン<a name="ゲームセンターログイン"></a>


 >iOS にのみ該当する機能です。
GameCenter Login を使用する場合は、以下の画像のように設定してください。>
`Assets/Plugins/IOS/etcFrameworks/GamePotGameCenter.framework`


![gamepot_unity_25.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_unity_25%2810%29.png)



>当該ライブラリが含まれている場合、`Capabilities設定でGameCenterを必ず有効化`してください。



**Xcode > Build Phases > Linked Binary With Libraries**に Gamekit.framework を追加します。

![gamepot_unity_26.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_unity_26%289%29.png)

**Xcode > TARGETS > Signing & Capabilities > + Capability > GameCenter を追加します。**

![gamepot_unity_09.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_unity_09%2812%29.png)

## 5. ログイン/ログアウト/退会/検証<a name="5ログインログアウト退会検証"></a>



### ログイン<a name="ログイン1"></a>


別途の登録なしにユーザーアカウントが作成されます。すべての身元確認のための MemberId が作成され、作成された情報は NUserInfo 構造体に保存され、返却されます。

- Case 1

Request:

```csharp
GamePot.login(NCommon.LoginType);
```

Response:

```csharp
// ログイン成功public void onLoginSuccess(NUserInfo userInfo){}// ログイン失敗public void onLoginFailure(NError error){    // ログインに失敗した場合    // error.messageをポップアップなどでユーザーに知らせてください。}// ログインキャンセルpublic void onLoginCancel(){    // ユーザーが任意にログインをキャンセルした場合}// 強制アップデート(ストアバージョンとゲームクライアントバージョンが異なる場合に呼び出す)public void onNeedUpdate(NAppStatus status){    // TODO: パラメータに渡されたstatus情報をもとにポップアップを作り、ユーザーに知らせてください。    // TODO: 以下の二つの方式のうち一つを選択してください。    // case 1：ゲーム内ポップアップを通じて開発会社で直接UIを実装    // case 2：SDKのポップアップを使用(この場合は以下のコードを呼び出してください。)    // GamePot.showAppStatusPopup(status.ToJson());}// メンテナンス(ダッシュボードでメンテナンスが有効化している場合に呼び出す)public void onMainternance(NAppStatus status){       // TODO: パラメータに渡されたstatus情報をもとにポップアップを作り、ユーザーに知らせてください。    // TODO: 以下の二つの方式のうち一つを選択してください。    // case 1：ゲーム内ポップアップを通じて開発会社で直接UIを実装    // case 2：SDKのポップアップを使用(この場合は以下のコードを呼び出してください。)    // GamePot.showAppStatusPopup(status.ToJson());}// アプリ終了public void onAppClose(){    // TODO: 強制アップデートやメンテナンス機能をcase 2の方式で実装する場合    // TODO: アプリを強制終了できるため、ここでアプリを終了できるように実装してください。}
```

- Case 2

Request:

```csharp
GamePot.login(NCommon.LoginType, GamePotCallbackDelegate.CB_Login);
```

```csharp
GamePot.login(NCommon.LoginType, (resultState, userInfo, appStatus, error) => {    switch (resultState)    {        case NCommon.ResultLogin.SUCCESS:        // login success        break;        case NCommon.ResultLogin.CANCELLED:        // login cancel        break;        case NCommon.ResultLogin.FAILED:        // login fail        break;	case NCommon.ResultLogin.NEED_UPDATE:            // やる事：パラメータに渡されたappStatus情報をもとにポップアップを作り、ユーザーに知らせてください。            // やる事：以下の二つの方式の中から一つを選択してください。                // ケース1：ゲーム内ポップアップを通じて開発会社で直接UIを実装                // ケース2：SDKのポップアップを使用(この場合は以下のコードを呼び出してください。)                // GamePot.showAppStatusPopup(status.ToJson());        break;        case NCommon.ResultLogin.MAINTENANCE:            // やる事：パラメータに渡されたappStatus情報をもとにポップアップを作り、ユーザーに知らせてください。            // やる事：以下の二つの方式の中から一つを選択してください。                // ケース1：ゲーム内ポップアップを通じて開発会社で直接UIを実装                // ケース2：SDKのポップアップを使用(この場合は以下のコードを呼び出してください。)                // GamePot.showAppStatusPopup(status.ToJson());        break;        case NCommon.ResultLogin.APP_CLOSE:            // やる事：強制アップデートやメンテナンス機能をケース2の方式(SDKポップアップ)で実装する場合に使用            // やる事：アプリを強制終了できるため、ここでアプリを終了できるように実装してください。        break;        default:        break;    }});
```

LoginType の定義

```csharp
public enum LoginType{    NONE,    GOOGLE,    GOOGLEPLAY,    FACEBOOK,    NAVER,    GAMECENTER,    TWITTER,    LINE,    APPLE,    GUEST,    THIRDPARTYSDK}
```

NUserInfo の定義

```csharp
public class NUserInfo{    public string memberid { get; set; }        // メンバーID(ユーザーの固有ID)    public string name { get; set; }            // 名前    public string profileUrl { get; set; }      // プロフィールURL(ある場合)    public string email { get; set; }           // メール(ある場合)    public string token { get; set; }           // ユーザーの有効性チェック用のトークン（Token Authentication APIで使用）    public string userid { get; set; }          // Social ID（Google、Facebook...）}
```

NAppStatus の定義

```csharp
public class NAppStatus{    public string type {get; set; } // AppStatusタイプに "maintenance"：点検、「needupdate "：更新    public string message {get; set; } //点検設定：Dashboardで入力したメッセージ    public string url {get; set; } //点検設定：Dashboardで入力したURL    public string currentAppVersion {get; set; } //更新：現在のApp Version    public string updateAppVersion {get; set; } //更新：Dashboardで入力されたApp Version    public int currentAppVersionCode {get; set; } //更新：現在のApp Code    public int updateAppVersionCode {get; set; } //更新：Dashboardで入力したApp Version code    public bool isForce {get; set; } //更新：Dashboardで強制的に更新設定時true    public string resultPayload {get; set; } //クライアントSDKから渡されたJson値として無視してもされます。    public double startedAt {get; set; } //点検：開始時間    public double endedAt {get; set; } //点検：終了時間}
```

**(2021.03.04) SDK v3.2.0以上から適用**

> `iOSプラットフォームの場合、`ログインAPI呼び出しの際に、IDFA値の取得権限をリクエストするポップアップをまず明示的にリクエストします。

> そのポップアップリクエストをログインの際に呼び出したくない場合、GamePot.login(NCommon.LoginType loginType)メソッドを修正します。(Assets/GamePot/SDK/Scripts/GamePot.cs )

```csharp
...public static void login(NCommon.LoginType loginType){    // Assets/GamePot/SDK/Scripts/GamePot.cs    ...    #elif UNITY_IOS        //iOSプラットフォームの場合、IDFA取得を許可するポップアップを先に表示してlogin処理        requestTrackingAuthorization((NResultTrackingAuthorizationresultState) =>        {            GamePotUnityPluginiOS.login(loginType);        });    ...}
```

Request:

```csharp
// IDFAの取得権限をリクエストするポップアップを任意で表示できます。// 権限を取得した後は、メソッドを呼び出してもポップアップは表示されません。GamePot.requestTrackingAuthorization((NResultTrackingAuthorizationresultState) =>{   // 取得したNResultTrackingAuthorizationresultStateのハンドリング});
```

NResultTrackingAuthorizationresultStateの定義

```csharp
public class NResultTrackingAuthorization{    public NCommon.ResultTrackingAuthorization authorization { get; set; }}
```

```csharp
public enum ResultTrackingAuthorization{    ATTrackingManagerAuthorizationStatusNotDetermined,    ATTrackingManagerAuthorizationStatusRestricted,    ATTrackingManagerAuthorizationStatusDenied,    ATTrackingManagerAuthorizationStatusAuthorized,    ATTrackingManagerAuthorizationStatusUnknown}
```

### ログイン情報をインポートする

```csharp
GamePot.getMemberId(); // メンバーID(ユーザーの固有ID)
```

### 自動ログイン<a name="自動ログイン"></a>


```csharp
NCommon.LoginType type = GamePot.getLastLoginType();if(type != NCommon.LoginType.NONE) {{    // 最後にログインしたログインタイプでログインする方式です。    GamePot.login(type);}else{    // 初めてゲームを実行したか、ログアウトした状態。ログインできるログイン画面に移動してください。}
```

### ログアウト<a name="ログアウト"></a>


ユーザーをログアウトさせます。アカウントは削除されず、同じアカウントでログインできます。

- Case 1

Request:

```csharp
GamePot.logout();
```

Response:

```csharp
/// ログアウト成功public void onLogoutSuccess(){}/// ログアウト失敗public void onLogoutFailure(NError error){    // ログアウトに失敗した場合    // error.messageをポップアップなどでユーザーに知らせてください。}
```

- Case 2

Request:

```csharp
GamePot.logout(GamePotCallbackDelegate.CB_Common);
```

```csharp
GamePot.logout((success, error) => {   if(success)   {       // ログアウト成功   }   else   {        // ログアウトに失敗した場合        // error.messageをポップアップなどでユーザーに知らせてください。   }});
```

### 退会<a name="退会"></a>


会員退会します。復旧はできません。

- Case 1

Request:

```text
GamePot.deleteMember();
```

Response:

```csharp
/// 会員退会成功public void onDeleteMemberSuccess() {}/// 会員退会失敗public void  onDeleteMemberFailure(NError error) {    // 会員退会に失敗した場合    // error.messageをポップアップなどでユーザーに知らせてください。}
```

- Case 2

Request:

```csharp
GamePot.deleteMember(GamePotCallbackDelegate.CB_Common);
```

```csharp
GamePot.deleteMember((success, error) => {   if(success)   {        // 会員退会成功   }   else   {        // 会員退会に失敗した場合        // error.messageをポップアップなどでユーザーに知らせてください。   }});
```

### 検証<a name="検証"></a>


ログイン完了後、ログイン情報を開発会社のサーバから GAMEPOT サーバに伝達するとログイン検証が行われます。

詳しい説明は Server to server api メニューの`Token Authentication`項目を参考にしてください。

## 6. アカウント連携<a name="6アカウント連携"></a>


一つのゲームアカウントに複数のソーシャルアカウント（Google/Facebook など）を連携/解除できる機能です。（最小連携ソーシャルアカウント数は一つです。）


>連携画面の UI は開発会社で実装してください。



```csharp
public enum LinkingType{    GOOGLEPLAY,    GAMECENTER,    GOOGLE,    FACEBOOK,    NAVER,    TWITTER,    LINE,    APPLE}
```

### 連携<a name="連携"></a>


Google / Facebook などの ID でアカウントを連携できます。

- Case 1

Request:

```csharp
void GamePot.createLinking(NCommon.LinkingType.XXXXX);
```

Response:

```csharp
/// アカウント連携キャンセルpublic void onCreateLinkingCancel() {    // ユーザーがアカウント連携をキャンセルした場合}/// アカウント連携成功public void onCreateLinkingSuccess(NUserInfo userInfo) {}/// アカウント連携失敗public void onCreateLinkingFailure(NError error) {    // アカウント連携に失敗した場合    // error.messageをポップアップなどでユーザーに知らせてください。}
```

- Case 2

Request:

```csharp
void GamePot.createLinking(NCommon.LinkingType.XXXXX, GamePotCallbackDelegate.CB_CreateLinking);
```

```csharp
GamePot.createLinking(NCommon.LinkingType.XXXXX, (resultState, userInfo, error) => {      switch (resultState)    {        case NCommon.ResultLinking.SUCCESS:        // アカウント連携成功        break;        case NCommon.ResultLinking.CANCELLED:        // アカウント連携キャンセル        break;        case NCommon.ResultLinking.FAILED:        // アカウント連携失敗        break;        default:        break;    }});
```

現在連携されているすべてのアカウント情報を取得できます。

```csharp
List<NLinkingInfo> linkedList = GamePot.getLinkedList();
```

リンク情報の定義

```csharp
public class NLinkingInfo{    public LinkingType provider { get; set; }  // google, facebook, naver, apple..}
```

### 連携解除<a name="連携解除"></a>


現在連携されているアカウントを解除します。

- Case 1

Request :

```csharp
void GamePot.deleteLinking(NCommon.LinkingType.XXXXX);
```

Response:

```csharp
/// アカウント連携の解除成功public void onDeleteLinkingSuccess() {}/// アカウント連携の解除失敗public void onDeleteLinkingFailure(NError error) {    // 連携解除に失敗した場合    // error.messageをポップアップなどでユーザーに知らせてください。}
```

- Case 2

Request:

```csharp
void GamePot.deleteLinking(NCommon.LinkingType.XXXXX, GamePotCallbackDelegate.CB_Common);
```

```csharp
GamePot.deleteLinking(NCommon.LinkingType.XXXXX, (success, error) => {    if(success)    {       // アカウント連携の解除成功    }   else   {        // 連携解除に失敗した場合        // error.messageをポップアップなどでユーザーに知らせてください。    }});
```

#### アカウント連携状況に関する結果処理の例<a name="アカウント連携状況に関する結果処理の例"></a>

createLinking / deleteLinking の結果に応じて現在連携されているアカウント情報を取得し、連携状態に対する UI をアップデートします。

```csharp
public void onInit(){    UI_Update();}public void onCreateLink_GAMECENTER_Click(){    GamePot.createLinking(NCommon.LinkingType.GAMECENTER);}public void onCreateLink_GOOGLE_Click(){    GamePot.createLinking(NCommon.LinkingType.GOOGLE);}public void onCreateLinkingSuccess(NUserInfo userInfo){    UI_Update();}public void onCreateLinkingFailure(NError error){    UI_Update();}public void onDeleteLinkingSuccess(NUserInfo userInfo){    UI_Update();}public void onDeleteLinkingFailure(NError error){    UI_Update();}Public void UI_Update(){    // Ui Update in GAME    CreateLinkManager.instance._IOS_google_state  = false;    CreateLinkManager.instance._IOS_gamecenter_state  = false;    List<NLinkingInfo> linkedList = GamePot.getLinkedList();    foreach ( NLinkingInfo item in linkedList)    {        switch(item.provider)        {        case NCommon.LinkingType.GOOGLE :            CreateLinkManager.instance._IOS_google_state  = true;            break;        case NCommon.LinkingType.GAMECENTER :            CreateLinkManager.instance._IOS_gamecenter_state  = true;            break;        ...        }    }}
```

## 7. 決済<a name="7決済"></a>


>支払いは消耗アプリ内商品タイプのみをサポートしており、ワンストアアプリ内SDKはV17バージョンのみをサポートします。

>ワンストアアプリ内SDKを含む : gamepot-billing-onestore.aar

>ギャラクシーストアアプリ内SDKを含む: gamepot-billing-galaxystore.aar

>マイカードアプリ内SDKを含む : gamepot-billing-mycard.aar ( Googleストアビルドには含まれていないように措置してください。)


### In-App 商品照会<a name="InApp商品照会"></a>


ストアに登録された商品情報を伝達します。

この機能を用いると、各ユーザに応じた料金、通貨、商品名が表示されます。

```csharp
NPurchaseItem[] items = GamePot.getPurchaseItems();foreach(NPurchaseItem item in items) {    Debug.Log(item.productId);        // 商品ID    Debug.Log(item.price);            // 料金    Debug.Log(item.title);            // タイトル    Debug.Log(item.description);    // 説明}
```

NPurchaseItemの定義

```csharp
public class NPurchaseItem{    public string productId { get; set; }   // 商品ID    public string type { get; set; }        // 商品タイプで、「inapp」に固定    public string price { get; set; }       // 価格 Googleストア：$0.99、その他のストア：0.99    public string price_amount { get; set; }    public string price_amount_micros { get; set; }    public string price_currency_code { get; set; } // 通貨コード ex） KRW、USD    public string price_with_currency { get; set; } // （UIに表示する場合に推奨） 通貨と価格が合算された値は、ONE Storeの場合、通貨単位が伝達されません。ex） $0.99    public string title { get; set; }       // 商品名    public string description { get; set; } // 商品説明}
```

### In-App 商品決済<a name="InApp商品決済"></a>


以下の関数一つで Google、Apple、APPSTORE 決済が可能になります。

- Case 1

Request:

```csharp
// productId：ストアに登録されている商品IDを入力してください。// uniqueId：別途管理する領収証番号を入力します。// serverId：決済を行ったキャラクターのサーバIDを入力します。// playerId ：決済を行ったキャラクターのキャラクターIDを入力します。// etc      ：決済を行ったキャラクターのその他の情報を入力します。GamePot.purchase(string productId);GamePot.purchase(string productId, string uniqueId);GamePot.purchase(string productId, string uniqueId, string serverId, string playerId, string etc);
```

Response:

```csharp
/// In-App決済成功public void onPurchaseSuccess(NPurchaseInfo purchase) {}/// In-App決済失敗public void onPurchaseFailure(NError error) {    // 決済に失敗した場合    // error.messageをポップアップなどでユーザーに知らせてください。}/// In-App決済失敗public void onPurchaseCancel() {}
```

- Case 2

Request:

```csharp
// productId：マーケットに登録された商品IDGamePot.purchase(string productId, GamePotCallbackDelegate.CB_Purchase);GamePot.purchase(string productId, string uniqueId, GamePotCallbackDelegate.CB_Purchase);GamePot.purchase(string productId, string uniqueId, string serverId, string playerId, string etc, GamePotCallbackDelegate.CB_Purchase);
```

```csharp
GamePot.purchase(productId, (resultState, purchaseInfo, error) => {      switch (resultState)    {        case NCommon.ResultPurchase.SUCCESS:        // purchase success        break;        case NCommon.ResultPurchase.CANCELLED:        // purchase cancel        break;        case NCommon.ResultPurchase.FAILED:        // purchase fail        break;        default:        break;    }});
```

### NPurchaseInfo の定義<a name="NPurchaseInfoの定義"></a>


決済成功後に決済したアイテム情報です。参考用にしてください。

```csharp
public class NPurchaseInfo{    public string price { get; set; }               // 決済アイテムの料金    public string productId { get; set; }           // 決済アイテムID    public string currency { get; set; }            // 決済料金の通貨(KRW/USD)    public string orderId { get; set; }             // ストアOrder ID    public string productName { get; set; }         // 決済アイテム名    public string gamepotOrderId { get; set; }      // GAMEPOTで作成したorder id    public string uniqueId { get; set; }            // 開発会社のunique ID    public string serverId { get; set; }            //(決済を行ったキャラクターの)サーバID    public string playerId { get; set; }            //(決済を行ったキャラクターの)キャラクターID    public string etc { get; set; }                 //(決済を行ったキャラクターの)その他の情報    public string signature { get; set; }           // 決済Signature    public string originalJSONData { get; set; }    // 領収証Data}
```

### 決済アイテム支給<a name="決済アイテム支給"></a>


GAMEPOT は、Server to server api を通じて決済ストアの領収証検証まですべて完了してから開発会社のサーバに支給リクエストをするため、不正決済はできません。

このためには`Server to server api`メニューの`Purchase Webhook`項目を参考にして処理してください。

### 外部決済<a name="外部決済"></a>


外部決済を許可しているストアと、公式ストアではないところで決済を使用できる機能です。


>呼び出し api だけが異なり、レスポンスや purchase webhook などその他は一般決済と同じです。
>機能を使用するには設定が必要です。ダッシュボードマニュアルの｢外部決済｣項目を参考にしてください。


- Case 1

Request:

```csharp
// productId：マーケットに登録された商品IDGamePot.purchaseThirdPayments(string productId);
```

外部決済を利用する場合、商品情報リストは以下の api を使用してください。

Request:

```csharp
// 返却されるデータ形式はgetPurchaseItems()と同じです。GamePot.getPurchaseThirdPaymentsItems();
```

- Case 2

Request:

```csharp
// productId：マーケットに登録された商品IDGamePot.purchaseThirdPayments(string productId, GamePotCallbackDelegate.CB_Purchase);
```

```csharp
// 返却されるデータ形式はgetPurchaseItems()と同じです。GamePot.purchase(productId, (resultState, purchaseInfo, error) => {      switch (resultState)    {        case NCommon.ResultPurchase.SUCCESS:        // purchase success        break;        case NCommon.ResultPurchase.CANCELLED:        // purchase cancel        break;        case NCommon.ResultPurchase.FAILED:        // purchase fail        break;        default:        break;    }});
```

## 8. その他の API<a name="8その他のAPI"></a>

### SDKサポートログインUI<a name="SDKサポートログインUI"></a>


SDK内で、独自に(完成した形の) Login UIを提供します。

```csharp
public class NLoginUIInfo{    public NCommon.LoginType[] loginTypes { get; set; }     // 表示するLogin UIタイプ(配列)    public bool showLogo { get; set; }                      // 画像ロゴ表示の有無}
```

#### SDKログインUIの呼び出し<a name="SDKログインUIの呼び出し"></a>


- Case 1

Request:

```csharp
 NLoginUIInfo info = new NLoginUIInfo();//呼び出すログインUIタイプ info.loginTypes = new NCommon.LoginType[] {     NCommon.LoginType.GOOGLE,     NCommon.LoginType.FACEBOOK,     NCommon.LoginType.GUEST     ... }; info.showLogo = true; GamePot.showLoginWithUI(info);
```

Response:

 **一般ログインAPIレスポンスロジックと同じです。(ただし、onLoginCancel / onLoginFailureの場合、Nativeレベルでトーストメッセージで処理されます。)**

```csharp
// ログイン成功public void onLoginSuccess(NUserInfo userInfo){}// 強制アップデート(ストアバージョンとゲームクライアントバージョンが異なる場合に呼び出す)public void onNeedUpdate(NAppStatus status){    // TODO：パラメータに渡されたstatus情報をもとにポップアップを作り、ユーザーに知らせてください。    // TODO：以下の二つの方式のうち一つを選択してください。    // case 1：ゲーム内ポップアップを通じて開発会社で直接UIを実装    // case 2：SDKのポップアップを使用(この場合は以下のコードを呼び出してください。)    // GamePot.showAppStatusPopup(status.ToJson());}// メンテナンス(ダッシュボードでメンテナンスが有効化している場合に呼び出す)public void onMainternance(NAppStatus status){       // TODO：パラメータに渡されたstatus情報をもとにポップアップを作り、ユーザーに知らせてください。    // TODO：以下の二つの方式のうち一つを選択してください。    // case 1：ゲーム内ポップアップを通じて開発会社で直接UIを実装    // case 2：SDKのポップアップを使用(この場合は以下のコードを呼び出してください。)    // GamePot.showAppStatusPopup(status.ToJson());}// アプリ終了public void onAppClose(){    // TODO：強制アップデートやメンテナンス機能をcase 2の方式で実装する場合    // TODO：アプリを強制終了できるため、ここでアプリを終了できるように実装してください。}
```

- Case 2

Request:

```csharp
 GamePot.showLoginWithUI(NLoginUIInfo, GamePotCallbackDelegate.CB_Login);
```

```csharp
 GamePot.showLoginWithUI(NLoginUIInfo, (resultState, userInfo, appStatus, error) => {    switch (resultState)    {        case NCommon.ResultLogin.SUCCESS:        // login success        break;        default:        break;    }});
```

#### Customizing<a name="Customizing1"></a>


**ログインUI画像ロゴの変更方法**

ログインUI上段に表示される画像ロゴは、SDKの内部で基本画像が表示され、直接追加することもできます。

**[Android]**


>直接追加するには`drawable`フォルダ別に画像を追加する必要があります。[（Android Asset Studio](http://romannurik.github.io/AndroidAssetStudio/icons-notification.html#source.type=clipart&source.clipart=ac_unit&source.space.trim=1&source.space.pad=0&name=ic_stat_gamepot_login_logo)を利用して作成すると、自動的にフォルダ別に画像が作成されるため便利です。）


画像ファイル名はic_stat_gamepot_login_logo.pngにしてください。

| フォルダ名                                                   | サイズ  |
| :----------------------------------------------------------- | :------ |
| /Assets/Plugins/Android/GamePotResources/res/drawable-mdpi/  | 78x55   |
| /Assets/Plugins/Android/GamePotResources/res/drawable-hdpi/  | 116x82  |
| /Assets/Plugins/Android/GamePotResources/res/drawable-xhdpi/ | 155x110 |
| /Assets/Plugins/Android/GamePotResources/res/drawable-xxhdpi/ | 232x165 |
| /Assets/Plugins/Android/GamePotResources/res/drawable-xxxhdpi/ | 310x220 |

 **[iOS]**


>画像ロゴはGamePot.bundle内に、ic_stat_gamepot_logo.pngファイルとして存在します。


画像ファイル名を`ic_stat_gamepot_login_logo.png`に変更した後、交換します。

(推奨サイズ：310x220)

**Screen Orientationの設定方法**

**[Android]**

/Assets/Plugin/Android/AndroidManifest.xmlファイルをエディタで開きます。

```markup
...e    <activity android:screenOrientation="sensorLandscap">      <intent-filter>        <action android:name="android.intent.action.MAIN" />          ...      </intent-filter>    </activity>...
```

Main ActivityにscreenOrientationを追加し、ゲームに応じて`sensorLandscape`または`sensorPortrait`を入力してください。


### Appleログイン(for Android - Web Login)<a name="AppleログインforAndroid-WebLogin"></a>


#### GAMEPOT Dashboard<a name="GAMEPOTDashboard"></a>


ダッシュボードのプロジェクトの設定 >> 一般 >> Apple ID Loginの設定


>機能を使用するには、Apple Developer Consoleの設定が必要です。
>ダッシュボードで当該項目の**ヘルプを見る**を参考にしてください。


/Assets/Plugins/Android/libsパスに以下のaarファイルを追加します。(Select platforms for plugin - Androidチェック確認)

- gamepot-channel-apple-signin.aar

### NAVER ログイン<a name="NAVERログイン"></a>


#### Naver Developers<a name="NaverDevelopers"></a>


使用 API を`ネアロ(NAVER IDでログイン)`にしてからアプリケーション登録

#### Android<a name="Android2"></a>

mainTemplate.gradle 修正

```java
...defaultConfig {    resValue "string", "gamepot_naver_clientid", "abcdefg1234567890"    resValue "string", "gamepot_naver_secretid", "hijklmn"}...
```

Console で発行された Client ID を`gamepot_naver_clientid`値に入力し、Client Secret は`gamepot_naver_secretid`値に入力します。

#### iOS<a name="iOS2"></a>


GamePotConfig-Info.plist ファイルに以下の項目を追加してその値を入力します。

```text
gamepot_naver_clientid // NAVERで使用するClient IDgamepot_naver_secretid // NAVERで使用するSecret IDgamepot_naver_urlscheme // NAVERで使用するurlscheme
```

GamePotConfig-Info.plist ファイルを SourceCode で表示する場合は以下のとおり追加

```markup
...<key>gamepot_naver_clientid</key><string>xxxxxx</string><key>gamepot_naver_secretid</key><string>xxxxxx</string><key>gamepot_naver_urlscheme</key><string>xxxxxx</string>...
```

**Targets > Info > URL Types に NAVER ID** でログイン設定に登録した URL Schemes を追加します。

URL Schemes を作成する際に`アルファベットの小文字`、`ピリオド(.)`、`アンダースコア(_)`以外の文字を使用すると認識できない場合があるため、ご注意ください。

### LINE ログイン<a name="LINEログイン"></a>


#### LINE Developers<a name="LINEDevelopers"></a>


APK にビルドする際に使用したパッケージ名と keystore の SHA 値、url Scheme 値を LINE のコンソールに追加します。

#### Android<a name="Android3"></a>


mainTemplate.gradle 修正

発行された Client ID を`gamepot_line_channelid`値に入力します。

```java
...defaultConfig {    resValue "string", "gamepot_line_channelid","xxxxxxx"}...
```

#### iOS<a name="iOS3"></a>


/Assets/Plugins/IOS/GamePotConfig-Info.plist ファイルに以下の項目を追加してその値を入力します。

```text
gamepot_line_channelid // NAVERで使用するClient IDgamepot_line_url_schemes // Line URL Scheme (line3rdp.{プロジェクトバンドルidentifier})
```

GamePotConfig-Info.plist ファイルを SourceCode で表示する場合は以下のとおり追加します。

```markup
...<key>gamepot_line_channelid</key><string>xxxxxx</string><key>gamepot_line_url_schemes</key><string>xxxxxx</string>...
```

### Twitter ログイン<a name="Twitterログイン"></a>


#### Twitter Developers<a name="TwitterDevelopers"></a>


#### Android<a name="Android4"></a>

mainTemplate.gradle 修正

```java
...defaultConfig {        resValue "string", "gamepot_twitter_consumerkey","xxxxx" // Twitter開発者コンソールで取得        resValue "string", "gamepot_twitter_consumersecret","xxx" // Twitter開発者コンソールで取得}...
```

#### iOS<a name="iOS4"></a>


GamePotConfig-Info.plist ファイルに以下の項目を追加してその値を入力します。

```text
gamepot_twitter_consumerkey : Twitter Consumer Keygamepot_twitter_consumersecret :  Twitter Consumer Secret
```

GamePotConfig-Info.plist ファイルを SourceCode で表示する場合は以下のとおり追加

```markup
...<key>gamepot_twitter_consumerkey</key><string>xxxxxx</string>...
```

### クーポン<a name="クーポン"></a>


#### クーポン使用<a name="クーポン使用"></a>


>クーポンを入力する UI は開発会社で実装してください。


- Case 1

Request:

```csharp
GamePot.coupon(string couponNumber); // クーポン番号GamePot.coupon(string couponNumber, string userData); // クーポン番号、ユーザー情報
```

Response:

```csharp
/// クーポン使用に成功public void onCouponSuccess() {}/// クーポン使用に失敗public void onCouponFailure(NError error) {    // クーポン使用に失敗した場合    // error.messageをポップアップなどでユーザーに知らせてください。}
```

- Case 2

Request:

```csharp
GamePot.coupon(string couponNumber, GamePotCallbackDelegate.CB_Common); // クーポン番号GamePot.coupon(string couponNumber, string userData, GamePotCallbackDelegate.CB_Common);    // クーポン番号、ユーザー情報
```

```csharp
GamePot.coupon(couponNumber, (success, error) => {   if(success)   {       // クーポン使用に成功   }   else   {        // クーポン使用に失敗した場合        // error.messageをポップアップなどでユーザーに知らせてください。   }});
```

#### アイテム支給<a name="アイテム支給"></a>


クーポンの使用に成功すると、開発会社のサーバに Server to server api を通じてアイテム支給をリクエストします。

このためには Server to server api メニューの`Item Webhook`項目を参考にして処理してください。

### Push on/off<a name="Pushonoff"></a>


プッシュ、夜間プッシュ通知をそれぞれ on/off にできます。


>on/off を設定する UI は開発会社で実装してください。


#### プッシュ通知設定<a name="プッシュ通知設定"></a>


- Case 1

Request:

```csharp
GamePot.setPushStatus(bool pushEnable);
```

Response:

```csharp
/// プッシュ通知の状態変更に関するサーバ通信成功public void onPushSuccess() {}/// プッシュ通知の状態変更に関するサーバ通信失敗public void onPushFailure(NError error) {    // プッシュ通知の状態変更に失敗した場合    // error.messageをポップアップなどでユーザーに知らせてください。}
```

- Case 2

Request:

```csharp
void GamePot.setPushStatus(bool pushEnable, GamePotCallbackDelegate.CB_Common);
```

```csharp
GamePot.setPushStatus(pushEnable, (success, error) => {    if(success)    {        // プッシュ通知の状態変更に関するサーバ通信成功    }   else   {        // プッシュ通知の状態変更に失敗した場合        // error.messageをポップアップなどでユーザーに知らせてください。    }});
```

#### 夜間プッシュ通知設定<a name="夜間プッシュ通知設定"></a>

- Case 1

Request:

```csharp
GamePot.setPushNightStatus(bool nightPushEnable);
```

Response:

```csharp
/// 夜間プッシュ通知の状態変更に関するサーバ通信成功public void onPushNightSuccess() {}/// 夜間プッシュ通知の状態変更に関するサーバ通信失敗public void onPushNightFailure(NError error) {    // 夜間プッシュ通知の状態変更に失敗した場合    // error.messageをポップアップなどでユーザーに知らせてください。}
```

- Case 2

Request:

```csharp
void GamePot.setPushNightStatus(bool nightPushEnable, GamePotCallbackDelegate.CB_Common);
```

```csharp
GamePot.setPushNightStatus(nightPushEnable, (success, error) => {    if(success)    {        // 夜間プッシュ通知の状態変更に関するサーバ通信成功    }   else   {        // 夜間プッシュ通知の状態変更に失敗した場合        // error.messageをポップアップなどでユーザーに知らせてください。    }});
```

#### プッシュ型広告設定<a name="プッシュ型広告設定"></a>


- Case 1

Request:

```csharp
GamePot.setPushADStatus(bool adPushEnable);
```

Response:

```csharp
/// プッシュ型広告の状態変更に関するサーバ通信成功public void onPushAdSuccess() {}/// プッシュ型広告の状態変更に関するサーバ通信失敗public void onPushAdFailure(NError error) {    // プッシュ型広告の状態変更に失敗した場合    // error.messageをポップアップなどでユーザーに知らせてください。}
```

- Case 2

Request:

```csharp
void GamePot.setPushADStatus(bool adPushEnable, GamePotCallbackDelegate.CB_Common);
```

```csharp
GamePot.setPushADStatus(adPushEnable, (success, error) => {    if(success)    {        // プッシュ型広告の状態変更に関するサーバ通信成功    }   else   {        // プッシュ型広告の状態変更に失敗した場合        // error.messageをポップアップなどでユーザーに知らせてください。    }});
```

#### プッシュ通知 / 夜間プッシュ通知 / プッシュ型広告を一度に設定<a name="プッシュ通知/夜間プッシュ通知/プッシュ型広告を一度に設定"></a>


ログイン前にプッシュ/夜間プッシュ通知の On/Off を設定するゲームの場合、ログインの後に以下のコードを必ず呼び出します。

- Case 1

Request:

```csharp
GamePot.setPushStatus(bool pushEnable, bool nightPushEnable, bool adPushEnable);
```

Response:

```csharp
/// プッシュ通知の状態変更に関するサーバ通信成功public void onPushStatusSuccess() {}/// プッシュ通知の状態変更に関するサーバ通信失敗public void onPushStatusFailure(NError error) {    // プッシュ通知の状態変更に失敗した場合    // error.messageをポップアップなどでユーザーに知らせてください。}
```

- Case 2

Request:

```csharp
void GamePot.setPushADStatus(bool pushEnable, bool nightPushEnable, bool adPushEnable, GamePotCallbackDelegate.CB_Common);
```

```csharp
GamePot.setPushADStatus(pushEnable, nightPushEnable, adPushEnable, (success, error) => {    if(success)    {        // プッシュ通知の状態変更に関するサーバ通信成功    }   else   {        // プッシュ通知の状態変更に失敗した場合        // error.messageをポップアップなどでユーザーに知らせてください。    }});
```

#### プッシュ通知の状態照会<a name="プッシュ通知の状態照会"></a>


```csharp
NPushInfo pushInfo = GamePot.getPushStatus();// pushInfo.enable プッシュ通知のOn/Off// pushInfo.night 夜間のプッシュ通知のOn/Off
```

### 案内事項<a name="案内事項"></a>


GAMEPOT ダッシュボードで｢案内事項｣に追加した画像を順番に表示する機能です。

画像推奨スペックは以下のとおりです。

- サイズ : 720 _1200（Portrait） / 1280_ 640（Landscape）

  > 上記のサイズを守らない場合、center crop で画像を処理します。

- 容量：250KB 以下

Request:

```csharp
GamePot.showNotice(bool Flag = true);// true：「今日は表示しない」を適用// false：「今日は表示しない」とは関係なしに強制表示GamePot.showEvent(string Type)// Type：ダッシュボードの案内事項 >> 分類で設定した分類名に該当する画像のみ表示
```

Response:

GAMEPOT ダッシュボードで`クリックアクション`を`SCHEME`に設定した場合、当該画像をクリックすると`SCHEME`値を伝達します。

```csharp
public void onReceiveScheme(string scheme){    // GAMEPOTダッシュボードで設定したscheme値を伝達}
```

### サポートセンター<a name="サポートセンター"></a>


顧客が運営者に問い合わせを登録して返答を受け取れる機能です。

問い合わせの UI はデバイスの言語に応じて変更されます。韓国語、英語、日本語、中国語(簡体字、繁体字)に対応し、その他の言語は英語で表示されます。

#### 呼び出し<a name="呼び出し1"></a>


```csharp
GamePot.showCSWebView();
```

外部リンクをサポートし、ログインしていない顧客も問い合わせを登録できます。

#### 呼び出し<a name="呼び出し2"></a>

```csharp
// url：GAMEPOTから発行された外部サポートセンターURLGamePot.showWebView(string url);
```

### ローカルプッシュ（Local Push notification）<a name="ローカルプッシュLocalPushnotification"></a>


プッシュサーバを介さずに端末にプッシュを表示する機能です。

#### プッシュ登録<a name="プッシュ登録"></a>


決められた時間にローカルプッシュを表示する方法は以下のとおりです。


>戻り値として返ってくる pushId は開発会社で管理します。



```csharp
int pushId = GamePot.sendLocalPush(DateTime.Parse("2018-01-01 00:00:00"), "title", "content");
```

#### 登録プッシュキャンセル<a name="登録プッシュキャンセル"></a>


プッシュ登録の際に取得した pushId をもとに、これまでに登録したプッシュをキャンセルできます。

```csharp
GamePot.cancelLocalPush(/*プッシュ登録の際に取得したpushId*/);
```


### Image Push

iOSアプリで通知画像を受信して処理するには、Xcodeで通知サービス拡張プログラムを追加する必要があります。

- Notification Service Extensionをプロジェクトに追加する
  1. Xcode > File > New > Target...メニューをクリック
  2. Targetをクリックすると表示される画面でNotification Service Extensionを選択し、Nextをクリック
  3. 追加するTarget(Notification Service Extension)のProject Nameを指定し、Finishをクリック > Notification Service Extensionモジュールが追加されたことを確認

- 通知サービス拡張プログラムを追加する

1. 作成されたNotification Service ExtensionモジュールのNotificationService.hファイルを以下のように修正


```c++
// GamePot/GamePotNotificationServiceExtension.hを読み込む// #import <UserNotifications/UserNotifications.h>#import <GamePot/GamePotNotificationServiceExtension.h// UNNotificationServiceExtensionの代わりにGamePotNotificationServiceExtensionを継承// @interface NotificationService : UNNotificationServiceExtension@interface NotificationService : GamePotNotificationServiceExtension@end
```

2. 作成されたNotification Service ExtensionモジュールのNotificationService.mファイルを以下のように修正

```c++
    ...    - (void)didReceiveNotificationRequest:(UNNotificationRequest *)request withContentHandler:(void (^)(UNNotificationContent * _Nonnull))contentHandler {        // self.contentHandler = contentHandler;        // self.bestAttemptContent = [request.content mutableCopy];        // Modify the notification content here...        // self.bestAttemptContent.title = [NSString stringWithFormat:@"%@ [modified]", self.bestAttemptContent.title];        // self.contentHandler(self.bestAttemptContent);        [super didReceiveNotificationRequest:request withContentHandler:contentHandler];    }    ...
```

3. 作成されたNotification Service ExtensionモジュールのTargets >> Build Phases >> Link Binary With LibrariesにGamePot.frameworkを追加



### 規約同意<a name="規約同意"></a>


｢利用規約｣と｢個人情報の取扱方針｣の同意をスムーズに行えるように UI を提供します。

`BLUE`テーマと`GREEN`テーマの2種類の`基本テーマ`の他にも、新たに追加された11種類の`改善テーマ`を提供します。

各領域別にCustomizingも可能です。

#### 規約同意を呼び出す<a name="規約同意を呼び出す"></a>

`GAMEPOT SDK V3.3.0`から、**ログイン時に自動的に規約同意のポップアップが表示**されます。

ログインの前に、フラグ値を通じてこれを変更できます。

```csharp
// デフォルト値はtrue// 自動ポップアップ時はMATERIAL_BLUEテーマを適用// falseに設定すると、ログイン時に規約同意のポップアップが表示されません。GamePot.setAutoAgree(true);// MATERIAL_ORANGEテーマでカスタム適用する場合NAgreeInfo bulider = new NAgreeInfo(); bulider.theme = "MATERIAL_ORANGE";GamePot.setAutoAgreeBuilder(bulider);...GamePot.login(NCommon.LoginType);...
```

#### 規約同意を呼び出す(手動)


```csharp
// 基本テーマBLUEGREEN// 改善テーマMATERIAL_RED,MATERIAL_BLUE,MATERIAL_CYAN,MATERIAL_ORANGE,MATERIAL_PURPLE,MATERIAL_DARKBLUE,MATERIAL_YELLOW,MATERIAL_GRAPE,MATERIAL_GRAY,MATERIAL_GREEN,MATERIAL_PEACH,
```


>規約同意のポップアップ表示の有無は、開発会社でゲームに合わせて処理してください。
>**[見る]** ボタンをクリックすると表示される内容は、ダッシュボードで適用及び修正できます。


- Case 1

Request:

```csharp
// 基本呼び出し(BLUEテーマを適用)GamePot.showAgreeDialog();// その他のテーマを適用時NAgreeInfo info = new NAgreeInfo();info.theme = "MATERIAL_RED";GamePot.showAgreeDialog(info);
```


Response:

```csharp
// 規約に同意した場合public void onAgreeDialogSuccess(NAgreeResultInfo info){    // info.agree：規約の必須事項にすべて同意した場合、true    // info.agreeNight：夜間プッシュ型広告の通知を許可した場合はtrue、そうでない場合はfalse    // agreeNight値はログイン完了後、setPushNightStatus apiを通じて伝達してください。}// エラー発生public void onAgreeDialogFailure(NError error){    // error.messageをポップアップなどでユーザーに知らせてください。}
```

- Case 2

Request:

```csharp
// 基本呼び出し(BLUEテーマを適用)showAgreeDialog(GamePotCallbackDelegate.CB_ShowAgree);// GREENテーマ適用時NAgreeInfo info = new NAgreeInfo();info.theme = "MATERIAL_RED";GamePot.showAgreeDialog(info,GamePotCallbackDelegate.CB_ShowAgree);
```

```csharp
GamePot.showAgreeDialog(bool info, (success, NAgreeResultInfo agreeInfo, NError error) => {   if(success)   {        // 規約に同意した場合   }   else   {        // エラー発生        // error.messageをポップアップなどでユーザーに知らせてください。   }});
```

#### Customizing<a name="Customizing2"></a>

テーマを使わずにゲームに合わせてカラーを変更します。

規約同意を呼び出す前に、`NAgreeInfo`で各領域別にカラーを指定できます。

```csharp
NAgreeInfo info = new NAgreeInfo();info.theme = "MATERIAL_RED";info.headerBackGradient = new string[] { "0xFF00050B", "0xFF0F1B21" };info.headerTitleColor = "0xFFFF0000";info.headerBottomColor = "0xFF00FF00";// 未使用時は""に設定info.headerTitle = 「規約同意」;// Android：res/drawableオブジェクトID(ファイル名)// iOS：assetオブジェクトID(ファイル名)info.headerIconDrawable = "ic_stat_gamepot_agree";info.contentBackGradient = new string[] { "0xFFFF2432", "0xFF11FF32" };info.contentIconColor = "0xFF0429FF";info.contentCheckColor = "0xFFFFADB5";info.contentTitleColor = "0xFF98FFC6";info.contentShowColor = "0xFF98B3FF";// Android：res/drawableオブジェクトID(ファイル名)// iOS：assetオブジェクトID(ファイル名)info.contentIconDrawable = "ic_stat_gamepot_small";info.footerBackGradient = new string[] { "0xFFFFFFFF", "0xFF112432" };info.footerButtonGradient = new string[] { "0xFF1E3A57", "0xFFFFFFFF" };info.footerButtonOutlineColor = "0xFFFF171A";info.footerTitleColor = "0xFFFF00D5";info.footerTitle = 「ゲームを始める」;// 一般プッシュ型広告通知許可ボタンの表示の有無info.showPush = true;// 夜間プッシュ型広告通知許可ボタンの表示の有無info.showNightPush = true;// 一般プッシュ型広告通知許可リンクボタンの設定（使用しない場合、入力しない）info.pushDetailURL = "https://...";// 夜間プッシュ型広告通知許可リンクボタンの設定（使用しない場合、入力しない）info.nightPushDetailURL = "https://...";// メッセージ変更info.allMessage = 「すべて同意」;info.termMessage = 「必須) 利用規約」;info.privacyMessage = 「必須) 個人情報の取扱方針」;info.pushMessage = "任意） 一般プッシュ通知を許可";info.nightPushMessage = 「任意) 夜間プッシュ通知を許可」;//プッシュ型広告通知許可(一般/夜間)にチェックを入れた場合、ゲームを始める際のToastメッセージ(同意時間)表示の有無GamePot.setShowToastPushStatus(true);GamePot.showAgreeDialog(info);
```

それぞれの変数は以下の領域に適用されます。


>contentIconDrawable は AOS でのみ表示され、基本値はプッシュアイコンとして設定されます。


- AgeView

![gamepot_unity_15.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_unity_15%2814%29.png)

- EmailView

![gamepot_unity_15_1.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_unity_15_1.png)

- AgreeView

![gamepot_unity_15_2.png](https://cdn.document360.io/6998976f-9d95-4df8-b847-d375892b92c2/Images/Documentation/gamepot_unity_15_2.png)

### 利用規約<a name="利用規約"></a>


利用規約 UI を呼び出します。


>ダッシュボード - サポートセンター - 利用規約の設定項目にまず内容を入力してください。



```csharp
GamePot.showTerms();
```

### 個人情報の取扱方針<a name="個人情報の取扱方針"></a>


個人情報の取扱方針 UI を呼び出します。


>ダッシュボード - サポートセンター - 個人情報の取扱方針の設定項目にまず内容を入力してください。



```csharp
GamePot.showPrivacy();
```

### 払い戻し規約<a name="払い戻し規約"></a>


払い戻し規約 UI を呼び出します。


>ダッシュボード - サポートセンター - 払い戻し規約の設定項目にまず内容を入力してください。



```csharp
GamePot.showRefund();
```

### Remote Config<a name="RemoteConfig"></a>


ダッシュボードで登録したパラメータ値をゲームクライアントから取得します。


>ダッシュボード - 設定 - Remote Config 画面でパラメータを追加します。
>追加したパラメータはログイン時にロードされ、その後から呼び出すことができます。


```csharp
//"test_01"：パラメータstringvar str_value = GamePot.getConfig("test_01");//ダッシュボードに追加したすべてのパラメータをjson string形式で取得します。var json_value = GamePot.getConfigs();
```

### 決済キャンセルを悪用するユーザーを自動的に解除する機能<a name="決済キャンセルを悪用するユーザーを自動的に解除する機能"></a>

決済キャンセルを悪用するユーザーを自動的に解除する機能の UI を提供します。各領域別にカスタマイズできます。


>Google 決済に限って、ユーザーが任意に Google にリクエストして決済をキャンセルした場合、｢Google 決済キャンセル｣機能を通じてそのユーザーを利用停止させることができます。
この時、当該ユーザーがログインすると SDK 内でポップアップを表示し、当該決済アイテムを再決済するように誘導し、
決済したら再び正常にアクセスできるようにする機能を提供します。
キャンセルした決済をすべて再決済すると、自動的に利用停止が解除されます。


```csharp
NVoidInfo info = new NVoidInfo();

//テーマの種類
MATERIAL_RED,
MATERIAL_BLUE,
MATERIAL_CYAN,
MATERIAL_ORANGE,
MATERIAL_PURPLE,
MATERIAL_DARKBLUE,
MATERIAL_YELLOW,
MATERIAL_GRAPE,
MATERIAL_GRAY,
MATERIAL_GREEN,
MATERIAL_PEACH

//テーマの変更
info.theme = "MATERIAL_ORANGE";

// メッセージ変更
info.headerTitle = "Header Title Section!";

info.descHTML = "descHTML Section!";

info.listHeaderTitle = "listHeaderTitle Section!";

info.footerTitle = "footerTitle Section!";

GamePot.setVoidBuilder(info);

```

### ゲームログ伝送<a name="ゲームログ伝送"></a>


ゲームで使用される情報を入れて呼び出すと、`ダッシュボード` - `ゲーム`で照会できます。

以下は使用できる予約語の定義表です。

| 予約語                            | 必須 | タイプ | 説明           | 最大文字数 |
| :-------------------------------- | :--- | :----- | :------------- | ---------- |
| GamePotSendLogCharacter.NAME      | 必須 | String | キャラクター名 | 128        |
| GamePotSendLogCharacter.LEVEL     | 任意 | String | レベル         | 128        |
| GamePotSendLogCharacter.SERVER_ID | 任意 | String | サーバID       | 128        |
| GamePotSendLogCharacter.PLAYER_ID | 任意 | String | キャラクターID | 128        |
| GamePotSendLogCharacter.USERDATA  | 任意 | String | ETC            | 128        |


```csharp
String name = 「キャラクター名」;
String level = "10";
String serverid = "svn_001";
String playerid = "283282191001";
String userdata = "";

GamePotSendLogCharacter characterLog = new GamePotSendLogCharacter();
characterLog.put(GamePotSendLogCharacter.NAME, name);
characterLog.put(GamePotSendLogCharacter.PLAYER_ID, playerid);
characterLog.put(GamePotSendLogCharacter.LEVEL, level);
characterLog.put(GamePotSendLogCharacter.SERVER_ID, serverid);
characterLog.put(GamePotSendLogCharacter.USERDATA, userdata);

Boolean result = GamePot.characterInfo(characterLog);

// Result is TRUE : validation success.Logs will send to GamePot Server
// Result is FALSE : validation was failed.Please check logcat
```

### GDPR規約チェックリスト<a name="GDPR規約チェックリスト"></a>


ダッシュボードで有効化した、GDPR規約項目をリストの形で取得します。

```csharp
//リターンされるデータ形式はstring[]です。
GamePot.getGDPRCheckedList();

//リターンされるパラメータは、それぞれダッシュボードの次の設定に該当します。
gdpr_privacy：個人情報の取扱方針
gdpr_term：利用規約
gdpr_gdpr：GDPRの利用規約
gdpr_push_normal：イベントPush受信に同意
gdpr_push_night：夜間イベントPush受信に同意(韓国のみ対象)
gdpr_adapp_custom：パーソナライズド広告を見るに同意 (GDPR適用国)
gdpr_adapp_nocustom：非パーソナライズド広告を見るに同意 (GDPR適用国)
```

### AppStatus確認

現在のクライアントのAppStatusを確認できます。

```csharp
public enum ResultCheckAppStatus
{
    SUCCESS,
    FAILED,
    NEED_UPDATE,
    MAINTENANCE
}

GamePot.checkAppStatus((NCommon.ResultCheckAppStatus resultState , NAppStatus appStatus, NError error) =>
{
    switch(resultState)
    {
        case NCommon.ResultCheckAppStatus.SUCCESS:
        // ログインに成功
        break;

        case NCommon.ResultCheckAppStatus.FAILED:
        // Handling error
        break;

        case NCommon.ResultCheckAppStatus.NEED_UPDATE:
        // アップデート
        // Handling appStatus
        break;

        case NCommon.ResultCheckAppStatus.MAINTENANCE:
        // メンテナンス
        // Handling appStatus
        break;
        
        default:
        break;
    }
```

## 付録<a name="付録"></a>

### 3rd party SDK 連携サポート<a name="3rdpartySDK連携サポート"></a>


## ログイン<a name="ログイン2"></a>


>自動ログインに対応しない。毎回呼び出しが必要。
>userid 값에 :(colon) 이 들어가면 안됩니다.


| パラメータ名 | 必須 | タイプ | 説明              |
| :----------- | :--- | :----- | :---------------- |
| userid       | 必須 | String | ユーザーの固有 ID |

```csharp
String userid = "memberid of 3rd party sdk";

GamePot.loginByThirdPartySDK("userid");
```

## 決済<a name="決済"></a>


>決済アイテムが GAMEPOT のダッシュボードに登録されている必要があります。


| パラメータ名  | 必須 | タイプ | 説明                                            |
| :------------ | :--- | :----- | :---------------------------------------------- |
| productid     | 必須 | String | GAMEPOT のダッシュボードに登録されたアイテム ID |
| transactionid | 必須 | String | 決済領収証番号(GPA-xxx-xxxx-xxxx)               |
| store         | 必須 | String | (決済ストア - Google、Apple、ONE、Galaxy)       |
| currency      | 任意 | String | 通貨(KRW、USD)                                  |
| price         | 任意 | double | 決済アイテム金額                                |
| paymentid     | 任意 | String | 決済 payment (一般的には store_id と同じ)       |
| uniqueid      | 任意 | String | 開発会社で使用する固有 ID                       |

```csharp
String productId = "purchase_001";
String transactionId = "GPA-xxx-xxxx-xxxx";
String currency = "KRW";
double price = 1200;
String paymentId = "google";
String uniqueId = "developer unique id";

sendPurchaseByThirdPartySDK(string productId, string transactionId, string currency, double price, string store, string paymentId, string uniqueId);
```

## Firebase Unity SDKを別途付けた場合の注意点

> 最初の1回、またはパッケージ名が変更されるたびにAssets > External Dependency Manager > Android Resolver > Settings内のPatch mainTemplate.gradleオプションを解除し、(設定変更後はOKボタンをクリック) > Resolveを行ってください。

Resolveが行われる際、FirebaseライブラリがUnityエディタ上に入力されたパッケージ名でリパッケージングされる過程が行われます。そのとき、パッケージ名が正しくないとアプリはインストールされません。

```csharp
反映事項の確認方法：

Resolve作業後、com.google.firebase.firebase-common-[Firebaseライブラリバージョン].aar内の
AndroidManifest.xmlでandroid:authorities値が
バージョンに合ったパッケージ名形式([パッケージ名].firebaseinitprovider)になっているかを見て確認できます。

<provider
            android:name="com.google.firebase.provider.FirebaseInitProvider"
            android:exported="false"
            android:authorities=“[アプリのパッケージ名].firebaseinitprovider"

ex)アプリのパッケージ名がcom.itsb.gamepotの場合
(com.itsb.gamepotはGAMEPOTのサンプルパッケージ名であるため、例のようなパッケージ名にならないようにします。)

<provider
            android:name="com.google.firebase.provider.FirebaseInitProvider"
            android:exported="false"
            android:authorities=“com.itsb.gamepot.firebaseinitprovider"
            .......

```

## Native 環境での修正が必要なとき 

>ユニティプラグインパッケージをご利用の場合Android環境のときにio.gamepot.unity.plugin.GamePotSDKActivityがMainActivityにする必要が動作します。
ただし、特定の広告ツールの機能のために、ネイティブ環境賞の修正をしなければならない場合があるときは、上記Classを継承受けて、別の処理するMainActivityを作成して適用する必要があります。


継承の例ブリッジファイル : [ダウンロード](https://xyuditqzezxs1008973.cdn.ntruss.com/patch/UnityGameActivityBridge_sample.zip)
(GAMEPOT SDK 3.2.0 基準の例)

上記の例に基づいた説明は以下の通りです。

1. プロジェクトに適用されたプロジェクト内../Assets/Plugins/Android/libs/gamepot-bridge.aarファイルを
ダウンロードしたプロジェクト（継承の例ブリッジファイル）の中にある../app/libsパスのファイルと置き換えます。

2. 作業を完了した後、ビルドをして生成されたarr（例：GameActivity-bridge.aar）を../Assets/Plugins/Android/libsフォルダに配置します。
ex)
../Assets/Plugins/Android/libs/GameActivity-bridge.aar 

3. メインアクティビティ交換のためにAndroidManifest.xmlファイルを変更します。

```csharp
既存 :
        <activity android:theme="@style/UnityThemeSelector"
            android:name="io.gamepot.unity.plugin.GamePotSDKActivity"

修正 : 
            android:name="io.gamepot.unity.plugin.Game.GameActivity"   //目安: ビルド時の継承されたアクティビティに変更
```
