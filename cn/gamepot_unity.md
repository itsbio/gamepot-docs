---
search:
  keyword: ['gamepot']
---

#### **为提供 NAVER CLOUD PLATFORM 产品的详细使用方法和 API 的多种使用方式，分别提供<a href="https://guide.ncloud-docs.com/docs/zh/home" target="_blank">[说明书]</a>和<a href="https://api.ncloud-docs.com/docs/zh/home" target="_blank">[API 参考指南]</a>以供参考。**

<a href="https://api.ncloud-docs.com/docs/zh/game-gamepot" target="_blank">进入 Gamepot API 参考指南 >></a><br />
<a href="https://guide.ncloud-docs.com/docs/zh/game-gamepot-overview" target="_blank">进入 Gamepot 说明书 >></a><br />
<a href="https://guide.ncloud-docs.com/docs/zh/game-gamepotunity" target="_blank">进入 Gamepot Unity SDK 说明书 >></a>

下面将介绍在Unity开发游戏时所需的GAMEPOT Unity SDK使用方法。 通过安装SDK并配置环境，可关联游戏和仪表盘。


## 配置要求<a name="요구사양"></a>

为使用Unity的GAMEPOT SDK，所需的配置要求如下。

* 最低配置：2018.4.0以上
（如需获得低版本Unity的支持，请通过[咨询频道](https://www.ncloud.com/support/question){target=&quot;_blank&quot;}进行咨询。 )
* 若要将v.3.1.0以下版本更新为最新版本， 
请参考[迁移指南](https://docs.gamepot.io/undefined/gamepot_faq#migration){target=&quot;_blank&quot;}进行迁移操作。
* 使用2019.3.X以上版本时，
请务必参考[GAMEPOT FAQ](https://docs.gamepot.io/undefined/gamepot_faq#ver-unity-2.1.1-to-ver-unity-2.1.2-or-new-version){target=&quot;_blank&quot;}中介绍的附加设置事项。 
* 如为使用2019.4.X/2020.3.X/2021.1.X版本的Unity编辑器用户，建议使用2019.4.29f1以上版本、2020.3.36f1以上版本和2021.1.16f1以上版本。 （该版本修复了构建AAB版本时出现的Unity编辑器漏洞，该版本修复了2020.3.35以下版本中在构建Android 31期间连接蓝牙耳机时出现的应用崩溃）


## SDK安装及环境配置<a name="SDK설치및환경구성"></a>

安装GAMEPOT Unity SDK后配置环境并关联GAMEPOT仪表盘和游戏，即可使用游戏开发所需的功能。

GAMEPOT SDK支持的语言如下所示。
 - 韩语、英语、意大利语、泰语、越南语、日语、中文（简体/繁体）、印尼语、德语、西班牙语、法语

运行应用时，将根据设备语言显示SDK内支持的语言，不支持的语言将显示为英语。

以IOS为例）
 - 须将要应用的语言添加至XCode > localization。
 - 构建时，**版本代码**请以整数形式单独增加。
 
### 安装SDK<a name="SDK설치"></a>

安装GAMEPOT Unity SDK后，在Unity配置项目的方法如下。

1. 请使用管理员账户登录仪表盘。
2. 依次点击**下载SDK > Unity**菜单后点击**下载**。
3. 在Unity中依次点击**Assets > Import Package > Custom Package**...菜单后导入GamePotUnityPlugin-xxxx.unitypackage文件。

### Android环境配置<a name="안드로이드환경설정"></a>

如要使用GAMEPOT Unity SDK开发基于Android的游戏，需设置所需环境。

#### 设置最低配置<a name="최소사양설정"></a>
如要设置可安装及运行应用的最低配置，请使用下列代码。

```D
minSDK版本：API 19以上（Kitkat）
```

#### 修改Gradle<a name="Gradle수정"></a>

如要修改Gradle文件，请参考表的内容在下列代码输入值后，使用该代码变更设置。

* 使用编辑器打开 ../Assets/Plugin/Android/mainTemplate.gradle文件。 （从Unity 2019.3.X之后的版本开始修改launcherTemplate.gradle文件）
* 不使用Facebook登录的客户应按如下所示随机设置facebook_app_id / fb_login_protocol_scheme值，或在构建时设置为不包含../Assets/Plugins/Android/libs/gamepot-channel-facebook.aar文件。

gamepot_payment值默认为空。




| 值 | 描述 |
| --- | --- |
|  ```gamepot_project_id``` | 由GAMEPOT发放的项目ID<br>（在仪表盘**项目设置 > 一般**菜单进行确认） |
| ```gamepot_store``` | 商店值输入`google`、`one`或`galaxy` |
| ```gamepot_app_title``` | 应用标题（FCM） |
| ```gamepot_push_default_channel``` | 禁止修改（已添加的默认渠道名称） |
| ```facebook_app_id``` | 由Facebook发放的应用ID |
| ```fb_login_protocol_scheme``` | 由Facebook发放的应用ID |
| ```facebook_client_token``` | Facebook控制台 > 应用 > 设置 > 高级设置 > 客户端Token |
|  ```gamepot_elsa_projectid``` | 使用NAVER Cloud ELSA服务时，输入ELSA项目ID<br>（参考[Effective Log Search &amp; Analytics](https://www.ncloud.com/product/analytics/elsa){target=&quot;_blank&quot;}）  |
| ```gamepot_region``` | 仅在GAMEPOT仪表盘创建区域为新加坡时输入sg |
|  ```gamepot_license_url``` |仅在GAMEPOT仪表盘创建区域为日本时输入https://gamepot.apigw.ntruss.com/fw/jp-v1 |



```java
...
android {
    ...
    defaultConfig {
        ...
        resValue "string", "gamepot_project_id", "" // required
        resValue "string", "gamepot_store", "google" // required
        resValue "string", "gamepot_app_title","@string/app_name" // required (fcm)
        resValue "string", "gamepot_push_default_channel","Default" // required (fcm)
        resValue "string", "facebook_app_id", "0" // optional (facebook)
        resValue "string", "fb_login_protocol_scheme", "fb0" // optional (facebook)
         resValue "string", "facebook_client_token", "" // Facebook控制台 > 应用 > 设置 > 高级设置 > 客户端Token optional（facebook）。
        // resValue "string", "gamepot_elsa_projectid", "" // optional (ncp elsa)
         resValue "string", "gamepot_region", "" // Caution! Only if the gamepot region is Singapore , value as sg
         resValue "string", "gamepot_license_url", "" // Caution! Only if the gamepot region is Japan , value as https://gamepot.apigw.ntruss.com/fw/jp-v1
    }
    ...
}
```

#### 设置推送通知图标<a name="푸시알림아이콘설정"></a>

可设置接收推送消息时要显示于通知栏的图标。 如果不另行设置，则使用包含在SDK的默认图片，也可自行设置适合游戏的图标。

若使用[Android Asset Studio](http://romannurik.github.io/AndroidAssetStudio/icons-notification.html#source.type=clipart&source.clipart=ac_unit&source.space.trim=1&source.space.pad=0&name=ic_stat_gamepot_small){target=&quot;_blank&quot;}制作，将自动按文件夹制作图像，非常方便。

设置推送通知图标的方法如下。

1. 按照以下方法在项目路径下分别创建res/drawable文件夹后，请根据各文件夹大小添加图像文件。
    | 文件夹名| 长度 |
    | --- | ---|
     /Assets/Plugins/Android/GamePotResources/res/drawable-mdpi/ | 24x24 |
     /Assets/Plugins/Android/GamePotResources/res/drawable-hdpi/ | 36x36 |
    /Assets/Plugins/Android/GamePotResources/res/drawable-xhdpi/ | 48x48 |
    /Assets/Plugins/Android/GamePotResources/res/drawable-xxhdpi/ | 72x72 |
    /Assets/Plugins/Android/GamePotResources/res/drawable-xxxhdpi/ | 96x96 |
    
    自Unity Engine 202x开始应放入GamePotResources.androidlib文件夹，并将相应资源文件夹添加到mainTemplate.gradle。 
    ```C#
    ...
        implementation project('GamePotResources.androidlib')
    ...
    ```
2. 请将图像文件名改为ic_stat_gamepot_small。


#### 屏幕方向设置<a name="ScreenOrientation"></a>

按游戏设置屏幕方向的方法如下。

1. 在Unity中打开/Assets/Plugin/Android/AndroidManifest.xml文件。
2. 在Main Activity添加下列代码后，根据游戏情况输入```sensorLandscape```或```sensorPortrait```作为游戏值。
    ```Markup
    ...
        <activity android:screenOrientation="sensorLandscape">
          <intent-filter>
            <action android:name="android.intent.action.MAIN" />
              ...
          </intent-filter>
        </activity>
    ...
    ```


#### Android Resolver、Unity Build设置<a name="AndroidResolverUnityBuild"></a>

为使用SDK，如下设置Android Resolver及Unity Build。

* **Android Resolver**
在Unity的**Assets > Play Services Resolver > Android Resolver > Settings**菜单中选择**Use Jetifier**。
 请取消选择 **Enable Resolution On Build** /  **Enable Auto-Resolution**  / **Patch gradle Template.properties** 项目。

* **Unity Build**
在Unity依次点击**File > Build Settings > Build System**菜单后选择Gradle。


### iOS环境设置<a name="iOS환경설정"></a>

如要使用GAMEPOT Unity SDK开发基于iOS的游戏，需设置所需环境。


#### 配置项目<a name="프로젝트구성"></a>

为设置iOS环境，按以下方法配置项目。 

1. 	将从Google Firebase控制台获取的GoogleService-Info.plist文件添加到Unity项目中。
2. 请参考表的内容在项目的GamePotConfig-Info.plist文件变更以下设置。
    （若不使用Facebook登录，构建时请确保排除GAMEPOTFacebook.framework。）
    环境变量 | 描述|
    --- | ---|
    gamepot_project_id	| 由GAMEPOT发放的项目ID
    gamepot_facebook_app_id |	从Facebook控制台获取的应用ID
    gamepot_facebook_display_name | 在Facebook上显示的名称
    gamepot_facebook_client_token | // Facebook控制台 > 应用 > 设置 > 高级设置 > 客户端Token
    gamepot_google_app_id | GoogleService-Info文件的```CLIENT_ID```值
    gamepot_google_url_schemes | GoogleService-Info文件的```REVERSED_CLIENT_ID```值
    gamepot_elsa_projectid | 使用NAVER Cloud ELSA时项目ID
    gamepot_region | 仅在GAMEPOT仪表盘创建区域为新加坡时输入sg
    gamepot_license_url | 仅在GAMEPOT仪表盘创建区域为日本时输入https://gamepot.apigw.ntruss.com/fw/jp-v1
    
3. 	选择Target后，在**Info > Custom iOS Target Properties**菜单添加下列用户权限获取选项。 （Xcode为准） 
    * 相应用户权限用于GAMEPOT客服中心的文件上传功能。
    ```NSCameraUsageDescription```, ```NSPhotoLibraryUsageDescription```, ```NSMicrophoneUsageDescription```
    * 从iOS 14版本开始，改成了获取IDFA值时必须向用户请求权限才能获取IDFA值。 因此，为了在获取IDFA值时使用向用户请求权限的弹窗，请在Targets >> Info >> Custom iOS Target Properties中添加以下用户权限获取选项。 （必须添加关于收集目的与使用地点的说明。）
    ```NSUserTrackingUsageDescription```

<示例> GAMEPOT样本界面 
在**File > Build Settings**菜单添加GamePotSample>Scene>Login、Main后 > 构建时，可查看样本界面。 


### 重置<a name="초기화"></a>

如要执行重置，在开始游戏时加载的第一个场景中使用的对象中添加以下代码。

```C#
using GamePotUnity;
public class GamePotLoginSampleScene : MonoBehaviour {
    void Awake() {
        GamePot.initPlugin();
    }
    void Start () {
        GamePot.setListener(GamePotInterface.cs继承到的class);
         // ex) GamePot.setListener(new GamePotSampleListener());
    }

}

ex)
public class GamePotSampleListener : MonoBehaviour , IGamePot {
    ....
}
```


### 设置错误代码<a name="오류코드설정"></a>

如要设置错误代码，请使用下列代码。

```C#
public class NError
{
    // 未知错误
    public static readonly int CODE_UNKNOWN_ERROR           = 0;
    // 初始化失败
    public static readonly int CODE_NOT_INITALIZE           = 1;
    // 参数不正确时
    public static readonly int CODE_INVAILD_PARAM           = 2;
    // 没有组成人员ID数据的情况
    public static readonly int CODE_MEMBERID_IS_EMPTY       = 3;
    // 未登录的状态
    public static readonly int CODE_NOT_SIGNIN              = 4;
    // 网络模块未重置的情况
    public static readonly int CODE_NETWORK_MODULE_NOT_INIT = 3000;
    // 发生网络连接错误及超时时
    public static readonly int CODE_NETWORK_ERROR           = 3001;
    // 在server-side发生的错误
    public static readonly int CODE_SERVER_ERROR            = 4000;
    // http response code不成功时
    public static readonly int CODE_SERVER_HTTP_ERROR       = 4001;
    // 发生网络连接错误及超时时
    public static readonly int CODE_SERVER_NETWORK_ERROR    = 4002;
    // 解析由服务器接收的数据时发生的错误
    public static readonly int CODE_SERVER_PARSING_ERROR    = 4003;
    // 支付时发生未知错误并由商店传递错误的情况
    public static readonly int CODE_CHARGE_UNKNOWN_ERROR    = 5000;
    // 未输入product id时
    public static readonly int CODE_CHARGE_PRODUCTID_EMPTY  = 5001;
    // 输入错误的product id时
    public static readonly int CODE_CHARGE_PRODUCTID_WRONG  = 5002;
    // consume时错误
    public static readonly int CODE_CHARGE_CONSUME_ERROR    = 5003;

    // error Code
    public int code { get; set; }
    // error Message
    public string message { get; set; }
}
```


## 登录相关功能<a name="로그인관련기능"></a>

集成Google、Facebook、NAVER等各种登录SDK功能，可在GAMEPOT Unity SDK使用。 


### 使用前设置<a name="사용전설정"></a>

如要使用登录相关SDK功能，需完成控制台设置并声明登录相关代码。


#### 设置Google登录环境<a name="구글로그인환경설정"></a>

为使用登录功能，按以下方法设置Google Firebase控制台。

1. 请将自Google Firebase控制台获取的安卓用google-service.json文件复制到/Assets/Plugins/Android/路径。
2. 将配置APK时使用的Keystore文件的SHA-1值添加到Firebase控制台。

* 尝试Google登录时，如果onCancel响应并无法登录，请按以下方法解决。
    * 确认是否正常应用google-service.json文件
    * 确认配置APK时使用的Keystore和为注册到Firebase控制台导出SHA-1值的Keystore是否相同
    * 确认构建时是否使用了注册到Firebase控制台的包名称


#### 设置Facebook登录环境<a name="페이스북로그인환경설정"></a>

为使用登录功能，按以下方法设置Facebook控制台。

1. 在Facebook for Developers控制台选择**None**、**Consumer**或**Instant Games**作为应用类型后创建应用。
2. 将配置APK时使用的Keystore的密钥哈希值添加到Facebook for Developers控制台。
3. 将从Facebook for Developers控制台获取的应用ID输入到下列代码后，添加到Android专用mainTemplate.gradle文件。
    ```java
    ...
    defaultConfig {
        resValue "string", "facebook_app_id", "{应用ID}"
        resValue "string", "fb_login_protocol_scheme", "fb{应用ID}"
    }
    ...
    ```
4. 请在项目/Assets/Plugins/IOS/Frameworks路径中添加下列框架。
    * FBSDKLoginKit.framework, FBSDKCoreKit.framework, GamePotFacebook.framework




#### 设置Apple登录环境<a name="애플로그인환경설정"></a>

若要设置iOS专用Apple登录环境，在项目中选择Target后，请在**Signing & Capabilities**菜单添加**Sign In with Apple** Capability。



#### 设置游戏中心登录环境 <a name="게임센터로그인환경설정"></a>

iOS专用Game Center登录环境的设置方法如下。

1. 在项目Assets/Plugins/IOS/etcFrameworks/路径下选择GamePotGameCenter.framework后，选择**Select platforms for plugin**列表中的**iOS**设置。
2. 在Xcode中选择Target后，在**Build Phases > Linked Binary With Libraries**菜单下添加Gamekit.framework。
3. 请在 **Signing & Capabilities** 菜单中添加 **GameCenter** Capability。


### 登录功能<a name="로그인기능"></a>

如要使用根据开发商实现的登录UI点击登录按钮时操作的SDK登录功能，请使用下列代码。

* 方式1

    ```Csharp 
    GamePot.login(NCommon.LoginType);

    // 登录成功
    public void onLoginSuccess(NUserInfo userInfo)
    {
    }
    // 登录失败
    public void onLoginFailure(NError error)
    {
        // 请使用error.message显示错误消息。
    }
    // 取消登录
    public void onLoginCancel()
    {
        // 用户取消登录
    }
    // 强制更新（商店版本和客户端版本不一致时调用）
    public void onNeedUpdate(NAppStatus status)
    {
        // 须基于参数传递的status信息创建并显示弹窗。 请从下列两种方式中选择一种配置弹窗。
        // 方式1：使用开发商自行实现UI的游戏内弹窗
        // 方式2：调用下列代码后使用SDK自主弹窗
        // GamePot.showAppStatusPopup(status.ToJson());
    }
    // 维护（仪表盘的维护选项处于激活状态时调用）
    public void onMainternance(NAppStatus status)
    {
         // 须基于参数传递的status信息创建并显示弹窗。 请从下列两种方式中选择一种配置弹窗。
        // 方式1：使用开发商自行实现UI的游戏内弹窗
        // 方式2：调用下列代码后使用SDK自主弹窗
        // GamePot.showAppStatusPopup(status.ToJson());
    }
    // 结束应用
    public void onAppClose()
    {
        // 如果使用方式2实现强制更新或维护功能时，因有可能强制结束应用，请在此处可执行结束应用。
    }
    ```

* 方式2

    ```C#
    GamePot.login(NCommon.LoginType, GamePotCallbackDelegate.CB_Login);

    GamePot.login(NCommon.LoginType, (resultState, userInfo, appStatus, error) => {
        switch (resultState)
        {
            case NCommon.ResultLogin.SUCCESS:
            // login success
            break;
            case NCommon.ResultLogin.CANCELLED:
            // login cancel
            break;
            case NCommon.ResultLogin.FAILED:
            // login fail
            break;
            case NCommon.ResultLogin.NEED_UPDATE:
                // 须基于参数返回的appStatus信息创建和显示弹窗。 请从下列两种方式中选择一种配置弹窗。
                // 方式1：使用开发商自行实现UI的游戏内弹窗
                // 方式2：调用下列代码后使用SDK自主弹窗
                // GamePot.showAppStatusPopup(status.ToJson());
            break;
            case NCommon.ResultLogin.MAINTENANCE:
                // 须基于参数返回的appStatus信息创建和显示弹窗。 请从下列两种方式中选择一种配置弹窗。
                // 方式1：使用开发商自行实现UI的游戏内弹窗
                // 方式2：调用下列代码后使用SDK自主弹窗
                // GamePot.showAppStatusPopup(status.ToJson());
            break;
            case NCommon.ResultLogin.APP_CLOSE:
                // 如果使用方式2实现强制更新或维护功能时，因有可能强制结束应用，请在此处可执行结束应用。
            break;
            default:
            break;
        }
    });
    ```


#### 定义LoginType、NUserInfo、NAppStatus<a name="LoginTypeNUserInfo,NAppStatus"></a>

如要设置登录功能的各个参数，请使用下列代码。

* **```LoginType```**
    ```C#
    public enum LoginType
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
        THIRDPARTYSDK
    }
    ```
* **```NUserInfo```**
    ```C#
    public class NUserInfo
    {
        public string memberid { get; set; }        // 用户唯一ID
        public string name { get; set; }            // 姓名
        public string profileUrl { get; set; }      // 简介URL（如有）
        public string email { get; set; }          // 邮件（如有）
        public string token { get; set; }           //用户有效性验证Token（在Token Authentication API中使用）
        public string userid { get; set; }          // 社交媒体ID
    }
    ```
* **```NAppStatus```**
    ``` C#
    public class NAppStatus
    {
        public string type { get; set; }        // 按AppStatus类型“maintenance”：维护，“needupdate”：更新
        public string message { get; set; }     // 维护设置：在仪表盘输入的消息
        public string url { get; set; }         // 维护设置：在仪表盘输入的URL
        public string currentAppVersion { get; set; }   // 更新：当前的应用版本
        public string updateAppVersion { get; set; }    // 更新：在仪表盘输入的应用版本
        public int currentAppVersionCode { get; set; }  // 更新：当前的应用代码
        public int updateAppVersionCode { get; set; }   // 更新：在仪表盘输入的应用版本代码
        public bool isForce { get; set; }           // 更新：在仪表盘设置强制更新时，为true
        public string resultPayload { get; set; }   // 由客户端SDK传递的JSON值，可忽略。
        public double startedAt { get; set; }       // 维护：开始时间
        public double endedAt { get; set; }        // 维护：结束时间
    }
    ```

#### 设置用于获取IDFA值的权限请求弹窗 <a name="IDFA값획득을위한권한요청팝업설정"></a>
如果要在iOS平台使用权限请求弹窗以获取用户IDFA值，请使用下列代码。

```C#
// 可随机弹出IDFA值获取权限请求弹窗。
// 获取权限后，即使调用方法也不会显示弹窗。

GamePot.requestTrackingAuthorization((NResultTrackingAuthorizationresultState) =>
{
   // 正在处理获得的NResultTrackingAuthorizationresultState..
});
```
<!--

<br>
* **变更弹窗请求时间**

权限请求弹窗用于获取iOS平台的IDFA值，将在调用登录API时请求。 如果不想在登录时调用相应弹窗请求，请在Assets/GamePot/SDK/Scripts/GamePot.cs文件中修改Method，如下所示。
 
```
...
public static void login(NCommon.LoginType loginType)
{
    // Assets/GamePot/SDK/Scripts/GamePot.cs
    ...
    #elif UNITY_IOS
        //如为IOS平台，先弹出允许获取IDFA的弹窗，然后进行登录处理
        requestTrackingAuthorization((NResultTrackingAuthorizationresultState) =>
        {
            GamePotUnityPluginiOS.login(loginType);
        });
    ...
}
 ```
<br>

-->

* ```NResultTrackingAuthorizationresultState```定义
    ```C#
    public class NResultTrackingAuthorization
    {
        public NCommon.ResultTrackingAuthorization authorization { get; set; }
    }

    public enum ResultTrackingAuthorization
    {
        ATTrackingManagerAuthorizationStatusNotDetermined,
        ATTrackingManagerAuthorizationStatusRestricted,
        ATTrackingManagerAuthorizationStatusDenied,
        ATTrackingManagerAuthorizationStatusAuthorized,
        ATTrackingManagerAuthorizationStatusUnknown
    }
    ```


#### 获得会员唯一ID<a name="회원고유아이디획득"></a>

如要获得游戏会员的唯一ID值，请使用下列代码。

```C#
GamePot.getMemberId();
```


### 使用第三方账户登录功能<a name="계정별로그인기능사용"></a>

如要使用第三方账户登录功能，请使用下列代码应用设置。


#### NAVER登录<a name="네이버로그인"></a>

若要使用NAVER登录功能，在NAVER Developers控制台中选择```Naver ID Login```作为使用API，然后注册应用并使用下方代码。


* **Android**
    * 修改mainTemplate.gradle
    ```java
    ...
    defaultConfig {
        resValue "string", "gamepot_naver_clientid", "abcdefg1234567890"
        resValue "string", "gamepot_naver_secretid", "hijklmn"
    }
    ...
    
    // 请将从NAVER Developers控制台获取的Client ID输入到gamepot_naver_clientid值中，并在gamepot_naver_secretid值中输入客户端密钥。
        ```
<br>
* **iOS**
    * 修改GamepotConfig-info.plist文件
    ```text
    gamepot_naver_clientid // 拟在NAVER使用的Client ID
    gamepot_naver_secretid // 拟在NAVER使用的Secret ID
    gamepot_naver_urlscheme // 拟在NAVER使用的URL Scheme
    ```
   用SourceCode确认时，如下进行添加
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
    * 在项目**Info  >  URL Types** 菜单添加用NAVER ID登录设置中添加的URL Schemes。
    
#### LINE登录<a name="라인로그인"></a>
如要使用LINE登录功能，需将配置APK时使用的包名称、Keystore的SHA-1值、URL Scheme值添加到LINE Developers控制台后使用下列代码。
    
 * **Android**
    * 修改mainTemplate.gradle
    ```java
    ...
    defaultConfig {
        resValue "string", "gamepot_line_channelid","xxxxxxx"
    }
    ...
    
    // 请在gamepot_line_channelid值中输入从LINE Developers控制台获取的Client ID。
     ```
<br>
* **iOS**
    * 修改GamepotConfig-info.plist文件
    ```text
    gamepot_line_channelid // 拟在NAVER使用的Client ID
    ggamepot_line_url_schemes // Line URL Scheme （line3rdp.{项目绑定identifier}）
    ```
   用SourceCode确认时，如下进行添加
   ```markup
   ...
    <key>gamepot_line_channelid</key>
    <string>xxxxxx</string>
    <key>gamepot_line_url_schemes</key>
    <string>xxxxxx</string>
    ...
    ```
<!--
#### Twitter登录<a name="트위터로그인"></a>
如要使用Twitter登录功能，请使用下列代码。

* **Android**
    * 修改mainTemplate.gradle
    ```java
    ...
    defaultConfig {
            resValue "string", "gamepot_twitter_consumerkey","xxxxx" // 从Twitter开发人员控制台获取
            resValue "string", "gamepot_twitter_consumersecret","xxx" // 从Twitter开发人员控制台获取
    }
    ...
   ```
<br>
* **iOS**
    * 修改GamepotConfig-info.plist文件
    ```text
    gamepot_twitter_consumerkey : Twitter Consumer Key
    gamepot_twitter_consumersecret :  Twitter Consumer Secret
    ```
   用SourceCode确认时，如下进行添加
   ```markup
  ...
    <key>gamepot_twitter_consumerkey</key>
    <string>xxxxxx</string>
    ...
    ```
-->


#### Apple Web登录<a name="애플웹로그인"></a>

若要使用Apple网页登录功能，在仪表盘的**项目设置 > 一般**菜单中设置Apple ID登录后，在项目/Assets/Plugins/Android/libs路径下添加gamepot-channel-apple-signin.aar文件。


### 自动登录功能<a name="자동로그인기능"></a>

如要使用通过传输会员最后一次登录信息的API自动登录功能时，请使用下列代码。

```C#
NCommon.LoginType type = GamePot.getLastLoginType();
if(type != NCommon.LoginType.NONE) {
{
    // 以最后一次登录的类型登录的方式。
    GamePot.login(type);
}
else
{
    // 第一次运行游戏或已退出登录的状态。 请跳转到可以进行登录的登录界面。
}
```


### 退出功能<a name="로그아웃기능"></a>

如要使用退出功能，请使用下列代码。

* 方式1

```C#
GamePot.logout();

/// 成功退出登录
public void onLogoutSuccess()
{
}

/// 退出登录失败
public void onLogoutFailure(NError error)
{
    // 请使用error.message显示错误消息。
}
```

* 方式2


```
GamePot.logout(GamePotCallbackDelegate.CB_Common);

GamePot.logout((success, error) => {
   if(success)
   {
       // 成功退出登录
   }
   else
   {
        // 退出登录失败
        // 请使用error.message显示错误消息。
   }
});

```


### 会员注销功能<a name="회원탈퇴기능"></a>

如要使用会员注销功能，请使用下列代码。

* 方式1


```C#
GamePot.deleteMember();

/// 会员注销成功
public void onDeleteMemberSuccess() {
}

/// 会员注销失败
public void  onDeleteMemberFailure(NError error) {
    // 请使用error.message显示错误消息。
}
```

* 方式2


```
GamePot.deleteMember(GamePotCallbackDelegate.CB_Common);

GamePot.deleteMember((success, error) => {
   if(success)
   {
        // 会员注销成功
   }
   else
   {
        // 会员注销失败
        // 请使用error.message显示错误消息。
   }
});
```


### 登录验证功能<a name="로그인검증기능"></a>

登录成功并由开发商服务器向GAMEPOT服务器传递登录信息后，即可进行登录验证。

详细说明请参考[登录验证请求](/docs/zh/game-gamepotserver#로그인검증요청)。



## 第三方账户关联<a name="외부계정연동"></a>

可以在一个游戏账户中关联或解除关联多个第三方账户。


### 账户关联功能<a name="계정연동기능"></a>

如要使用Google、Facebook、NAVER等第三方账户的关联功能，请使用下列代码。

* 方式1



```C#
public enum LinkingType
{
    GOOGLEPLAY,
    GAMECENTER,
    GOOGLE,
    FACEBOOK,
    NAVER,
    TWITTER,
    LINE,
    APPLE
}

void GamePot.createLinking(NCommon.LinkingType.XXXXX);

/// 取消账户关联
public void onCreateLinkingCancel() {
    // 用户取消账户关联
}

/// 账户关联成功
public void onCreateLinkingSuccess(NUserInfo userInfo) {
}

/// 账户关联失败
public void onCreateLinkingFailure(NError error) {
    // 请使用error.message显示错误消息。
}
```

* 方式2


```C#
public enum LinkingType
{
    GOOGLEPLAY,
    GAMECENTER,
    GOOGLE,
    FACEBOOK,
    NAVER,
    TWITTER,
    LINE,
    APPLE
}

void GamePot.createLinking(NCommon.LinkingType.XXXXX, GamePotCallbackDelegate.CB_CreateLinking);

GamePot.createLinking(NCommon.LinkingType.XXXXX, (resultState, userInfo, error) => {
      switch (resultState)
    {
        case NCommon.ResultLinking.SUCCESS:
        // 账户关联成功
        break;
        case NCommon.ResultLinking.CANCELLED:
        // 取消账户关联
        break;
        case NCommon.ResultLinking.FAILED:
        // 账户关联失败
        break;
        default:
        break;
    }
});
```


### 关联列表确认功能<a name="연동리스트확인기능"></a>

如要确认与账户关联的第三方账户列表，请使用下列代码。

```C#
List<NLinkingInfo> linkedList = GamePot.getLinkedList();

// 定义链接信息
public class NLinkingInfo
{
    public LinkingType provider { get; set; }  // google, facebook, naver, apple..
}
```


### 解除关联功能<a name="연동해제기능"></a>

如要使用解除与第三方账户的关联功能，请使用下列代码。

* 方式1

```C#
void GamePot.deleteLinking(NCommon.LinkingType.XXXXX);

/// 账户关联解除成功
public void onDeleteLinkingSuccess() {
}

/// 账户关联解除失败
public void onDeleteLinkingFailure(NError error) {
    // 解除关联失败时
    // 请使用error.message显示错误消息。
}
```

* 方式2


```C#
void GamePot.deleteLinking(NCommon.LinkingType.XXXXX, GamePotCallbackDelegate.CB_Common);

GamePot.deleteLinking(NCommon.LinkingType.XXXXX, (success, error) => {
    if(success)
    {
       // 账户关联解除成功
    }
   else
   {
        // 解除关联失败时
        // 请使用error.message显示错误消息。
    }
});
```

## 支付功能<a name="결제기능"></a>

:::(Info) (参考)

GAMEPOT结算仅支持游戏内消耗性商品类型的结算，One Store应用内SDK仅支持V17版本。
* 包含One Store应用内SDK：gamepot-billing-onestore.aar
* 包含Galaxy Store应用内SDK：gamepot-billing-galaxystore.aar
* 包含My Card应用内SDK：gamepot-billing-mycard.aar（请通过相应措施将其在Google Store构建中除外。）
:::

可使用应用内购买所需的支付功能。 



### 应用内商品查询功能<a name="인앱상품조회기능"></a>

如要使用查询商店内商品信息的功能，请使用下列代码。

如果登录成功后需要调用的API是getPurchaseItems API，由于它是异步提供从商店应用内SDK接收的内容的API，因此也可根据调用时间以空白值进行传递。 （以可支付的环境为准） 

```C#
[Case1]:

NPurchaseItem[] items = GamePot.getPurchaseItems();
foreach(NPurchaseItem item in items) {
    Debug.Log(item.productId);        // 产品ID
    Debug.Log(item.price);            // 价格
    Debug.Log(item.title);            // 标题
    Debug.Log(item.description);    // 概述
}

[Case2]:

GamePot.getPurchaseDetailListAsync((bool success, NPurchaseItem[] purchaseInfoList, NError error) =>
{
   // string result = "data is empty!";
    if (success)
    {
         //PurchaseDetailList API Success
        // if (purchaseInfoList != null)
        //     result = purchaseInfoList[0].productId;
        //if (purchaseInfoList.Length > 1)
        //{
        //    for (int i = 1; i < purchaseInfoList.Length; i++)
        //        result += "\n" + purchaseInfoList[i].productId;
        //}
    }
    else
    {
        // API错误 
        // result = error.ToJson();
    }

});


public class NPurchaseItem
{
    public string productId { get; set; }   // 商品ID
    public string type { get; set; }        // 商品类型 固定为"inapp"
    public string price { get; set; }       // 价格 Google商店：$0.99，其他商店：0.99
    public string price_amount { get; set; }
    public string price_amount_micros { get; set; }
    public string price_currency_code { get; set; } // 货币代码 例）KRW、USD
    public string price_with_currency { get; set; } // （在UI中显示时推荐）货币与价格合并后的值。 One Store不会传输货币单位。例如）$0.99
    public string title { get; set; }       // 商品名称
    public string description { get; set; } // 商品描述
}
```



```C#
[Case3]:

GamePot.getPurchaseDetailListAsync();

public void onPurchaseDetailListSuccess(NPurchaseItem[] purchaseInfoList)
{
    //PurchaseDetailList API Success
}

public void onPurchaseDetailListFailure(NError error)
{
       // API错误 
}
```




### 支付尝试功能<a name="결제시도기능"></a>

可以通过一个支付API，在Google Play商店、Apple App Store均可使用支付尝试功能。
（如为One Store版本，uniqueId+serverId+playerId+etc的长度小于85byte方可进行支付。）

如要使用支付尝试功能，请使用下列代码。

* 方式1

// productId：商店中添加的商品ID
// uniqueId：单独管理的发票号
// serverId：付费角色的服务器ID
// playerId：付费角色的角色ID
// etc       ： 付费角色的其他信息



```C#

GamePot.purchase(string productId);

GamePot.purchase(string productId, string uniqueId);

GamePot.purchase(string productId, string uniqueId, string serverId, string playerId, string etc);

/// 应用内支付成功
public void onPurchaseSuccess(NPurchaseInfo purchase) {
}

/// 应用内支付失败
public void onPurchaseFailure(NError error) {
    // 应用内支付失败
    // 请使用error.message显示错误消息。
}

/// 应用内支付失败
public void onPurchaseCancel() {
}
```


* 方式2

```C#
// productId：商店中添加的商品ID
GamePot.purchase(string productId, GamePotCallbackDelegate.CB_Purchase);

GamePot.purchase(string productId, string uniqueId, GamePotCallbackDelegate.CB_Purchase);

GamePot.purchase(string productId, string uniqueId, string serverId, string playerId, string etc, GamePotCallbackDelegate.CB_Purchase);

GamePot.purchase(productId, (resultState, purchaseInfo, error) => {
      switch (resultState)
    {
        case NCommon.ResultPurchase.SUCCESS:
        // purchase success
        break;
        case NCommon.ResultPurchase.CANCELLED:
        // purchase cancel
        break;
        case NCommon.ResultPurchase.FAILED:
        // purchase fail
        break;
        default:
        break;
    }
});
```

### 获取付费道具信息的功能<a name="결제아이템정보획득기능"></a>

如要使用获取由商店传递的应用内付费道具信息功能，请使用下列代码。

```C#
public class NPurchaseInfo
{
    public string price { get; set; }               // 付费道具的价格
    public string productId { get; set; }           // 付费道具ID
    public string currency { get; set; }            // 支付价格货币（KRW/USD）
    public string orderId { get; set; }            // 商店Order ID
    public string productName { get; set; }        // 付费道具名称
    public string gamepotOrderId { get; set; }      // 在GAMEPOT中创建的Order ID（不提供相应值） 
    public string uniqueId { get; set; }            // 开发商单独管理的发票ID
    public string serverId { get; set; }            // 付费角色的服务器ID
    public string playerId { get; set; }            // 付费角色的角色ID
    public string etc { get; set; }                 // 付费角色的其他信息
    public string signature { get; set; }           // 支付签名
    public string originalJSONData { get; set; }    // 发票数据
}
```

### 发放付费道具的功能<a name="결제아이템지급기능"></a>

可设置为与支付商店的发票明细进行对照并完成所有验证后向开发商服务器传递发放请求。
详细说明请参考[道具发放请求](/docs/zh/game-gamepotserver#아이템지급요청)。


### My Card支付<a name="Mycard결제"></a>

Mycard库：[gamepot-billing-mycard.aar](https://xyuditqzezxs1008973.cdn.ntruss.com/patch/gamepot-billing-mycard.aar){target=&quot;_blank&quot;}

:::(Info) (参考)

请通过Mycard确认用于和Mycard关联的FacServiceID/KEY值。 
:::

1. 在仪表盘 >> 支付 >> IAP的商店类型：Google项目 > 添加价格 > 货币（例如：TWD）/输入价格信息后保存。 

2. 在Dashboard >> 项目设置 >> 外部支付项目中添加MyCard，并确认是否正常输入相应FacService ID / Sign Key。

3. 支付时调用以下SDK代码。 
   GamePot.getInstance().purchase("product id");
   * 在MyCard使用过程中，付费道具调用形式在调用现有的GamePot.getInstance().getPurchaseDetailList();时发生错误。 
     为进行替代，请调用GamePot.getInstance().getPurchaseThirdPaymentsDetailList();。 

4.  在../Assets/Plugins/Android/AndroidManifest.xml文件中移除<application>级别的名称。

  ``` java
    <supports-screens android:smallScreens="true" android:normalScreens="true" android:largeScreens="true" android:xlargeScreens="true" android:anyDensity="true" />
    <application android:icon="@drawable/app_icon"
        android:label="@string/app_name"
        android:allowBackup="false"
        tools:replace="android:allowBackup"
        >
  ```

5.  在../Assets/Plugins/Android/mainTemplate.gradle文件中按照以下方法进行设置。
（从Unity 2019.3.X之后的版本开始修改launcherTemplate.gradle文件）

  ``` java
  resValue "string", "gamepot_store", "google"
  仅在resValue "string"、"gamepot_payment"、"mycard" //商店为Google时运行。
  ```

6. 确认../Assets/Plugins/Android/libs文件夹内是否包含gamepot-billing-mycard.aar。

        
        
### 第三方支付<a name="외부결제"></a>
        
如要关联第三方支付模块，首先参考[第三方支付服务关联](/docs/zh/game-gamepot-projectmgmt#외부결제서비스연동)完成设置后使用下列代码。

* 方式1



```C#
GamePot.purchaseThirdPayments(string productId);

// 返回的数据格式与getPurchaseItems()相同。
GamePot.getPurchaseThirdPaymentsItems();
```
        
* 方式2

```C#
GamePot.purchaseThirdPayments(string productId, GamePotCallbackDelegate.CB_Purchase);

// 返回的数据格式与getPurchaseItems()相同。
GamePot.purchase(productId, (resultState, purchaseInfo, error) => {
      switch (resultState)
    {
        case NCommon.ResultPurchase.SUCCESS:
        // purchase success
        break;
        case NCommon.ResultPurchase.CANCELLED:
        // purchase cancel
        break;
        case NCommon.ResultPurchase.FAILED:
        // purchase fail
        break;
        default:
        break;
    }
});
```
        

## SDK自主提供的登录UI<a name="SDK자체제공로그인UI"></a>
        
可以使用GAMEPOT Unity SDK提供的完整的登录UI。

        
### 调用SDK自主提供的登录UI<a name="SDK자체제공로그인UI호출"></a>
        
如要调用GAMEPOT Unity SDK提供的登录UI，请使用下列代码。

* 方式1
```C#
public class NLoginUIInfo
{
    public NCommon.LoginType[] loginTypes { get; set; }     // 拟显示的Login UI类型（排列）
    public bool showLogo { get; set; }                      // 是否显示图片标志
}
 NLoginUIInfo info = new NLoginUIInfo();

//待调用登录UI类型
 info.loginTypes = new NCommon.LoginType[]
 {
     NCommon.LoginType.GOOGLE,
     NCommon.LoginType.FACEBOOK,
     NCommon.LoginType.GUEST
     ...
 };
 info.showLogo = true;
```

 ```C#
 GamePot.showLoginWithUI(info);
 
 // 与一般登录API响应逻辑相同。 但时，响应结果为onLoginCancel/onLoginFailure时，将在Native级别上以提醒消息形式进行处理。
 
 // 登录成功
public void onLoginSuccess(NUserInfo userInfo)
{
}
// 强制更新（商店版本和客户端版本不一致时调用）
public void onNeedUpdate(NAppStatus status)
{
    // 须基于参数传递的status信息创建并显示弹窗。 请从下列两种方式中选择一种配置弹窗。
    // 方式1：使用开发商自行实现UI的游戏内弹窗
    // 方式2：调用下列代码后使用SDK自主弹窗
    // GamePot.showAppStatusPopup(status.ToJson());
}
// 维护（仪表盘的维护选项处于激活状态时调用）
public void onMainternance(NAppStatus status)
{
    // 须基于参数传递的status信息创建并显示弹窗。 请从下列两种方式中选择一种配置弹窗。
    // 方式1：使用开发商自行实现UI的游戏内弹窗
    // 方式2：调用下列代码后使用SDK自主弹窗
    // GamePot.showAppStatusPopup(status.ToJson());
}
// 结束应用
public void onAppClose()
{
    // 如果使用方式2实现强制更新或维护功能时，因有可能强制结束应用，请在此处可执行结束应用。
}

 public void onLoginExit()
{
    // 关闭系统自主提供的登录UI时
 }       
        
```

* 方式2



```C#
GamePot.showLoginWithUI(NLoginUIInfo, GamePotCallbackDelegate.CB_Login);

 GamePot.showLoginWithUI(NLoginUIInfo, (resultState, userInfo, appStatus, error) => {
    switch (resultState)
    {
        case NCommon.ResultLogin.SUCCESS:
          // login success
        break;
        case NCommon.ResultLogin.EXIT:
            // 关闭系统自主提供的登录UI时
        break;
         case NCommon.ResultLogin.NEED_UPDATE:
            // 须基于参数传递的status信息创建并显示弹窗。 请从下列两种方式中选择一种配置弹窗。
            // 方式1：使用开发商自行实现UI的游戏内弹窗
            // 方式2：调用下列代码后使用SDK自主弹窗
            // GamePot.showAppStatusPopup(appStatus.ToJson());
        break;
         case NCommon.ResultLogin.MAINTENANCE:
             // 须基于参数传递的status信息创建并显示弹窗。 请从下列两种方式中选择一种配置弹窗。
            // 方式1：使用开发商自行实现UI的游戏内弹窗
            // 方式2：调用下列代码后使用SDK自主弹窗
            // GamePot.showAppStatusPopup(appStatus.ToJson());
        break;
         case NCommon.ResultLogin.APP_CLOSE:
            // 如果使用方式2实现强制更新或维护功能时，因有可能强制结束应用，请在此处可执行结束应用。
        break;
        default:
        break;
    }
});
```

### 设置自主提供的登录UI图片标志<a name="자체제공로그인UI이미지로고설정"></a>
可设置自主提供的登录UI上方显示的图片。 如果不另行设置，则使用包含在SDK的默认图片，也可自行设置适合游戏的图片。

#### 设置Android专用图片标志<a name="안드로이드용이미지로고설정"></a>
Android专用自主提供的登录UI图片的设置方法如下。

1. 在下列路径分别创建res/drawable文件夹后，请按照大小添加图像文件。
    | 文件夹名 | 长度 |
    | --- | ---|
     /Assets/Plugins/Android/GamePotResources/res/drawable-mdpi/ | 78x55 |
     /Assets/Plugins/Android/GamePotResources/res/drawable-hdpi/ | 116x82 |
    /Assets/Plugins/Android/GamePotResources/res/drawable-xhdpi/ | 155x110 |
    /Assets/Plugins/Android/GamePotResources/res/drawable-xxhdpi/ | 232x165 |
    /Assets/Plugins/Android/GamePotResources/res/drawable-xxxhdpi/ | 310x220 |
2. 请将图片文件名变更为 ic_stat_gamepot_login_logo.png。

#### 设置iOS专用图片标志<a name="iOS용이미지로고설정"></a>
如要设置自主提供的iOS专用登录UI图片，需将拟设置的图片（推荐大小310x220）的文件名变更为 ic_stat_gamepot_login_logo.png后，与在GamePot.bundle中存在的同名文件进行替换。


## 优惠券功能<a name="쿠폰기능"></a>
如要使用用户输入优惠券即处理为已使用的功能，请使用下列代码。

* 方式1

```C#
GamePot.coupon(string couponNumber); // 优惠券编号

GamePot.coupon(string couponNumber, string userData);; // 优惠券编号、用户信息

/// 优惠券使用成功
public void onCouponSuccess() {
}

/// 优惠券使用失败
public void onCouponFailure(NError error) {
    // 请使用error.message显示错误消息。
}
```

* 方式2

```C#
GamePot.coupon(string couponNumber, GamePotCallbackDelegate.CB_Common); // 优惠券编号

GamePot.coupon(string couponNumber, string userData, GamePotCallbackDelegate.CB_Common);    // 优惠券编号、用户信息

GamePot.coupon(couponNumber, (success, error) => {
   if(success)
   {
       // 优惠券使用成功
   }
   else
   {
        // 优惠券使用失败
        // 请使用error.message显示错误消息。
   }
});
```

        
        
### 发放道具<a name="아이템지급"></a>
        
优惠券使用成功时，向开发商服务器请求发放道具。

详细说明请参考[道具发放请求](/docs/zh/game-gamepotserver#아이템지급요청)。

        
        
## 推送功能<a name="푸시기능"></a>
        
可允许或禁用一般推送、夜间推送、广告推送功能，可使用本地推送功能。
若使用推送功能，请将广告推送设置为true（广告推送值为false时，无论是否设置一般/夜间推送，皆不会推送通知。）

        
        
### 一般推送设置<a name="일반푸시설정"></a>
        
如要设置一般推送，请使用下列代码。

* 方式1
        
```C#
    GamePot.setPushStatus(bool pushEnable);

    /// 对推送状态变更的服务器通信成功
    public void onPushSuccess() {
    }

    /// 对推送状态变更的服务器通信失败
    public void onPushFailure(NError error) {

        // 推送状态变更失败时，请使用error.message显示错误消息。
    }
```

* 方式2

```C#
void GamePot.setPushStatus(bool pushEnable, GamePotCallbackDelegate.CB_Common);

    GamePot.setPushStatus(pushEnable, (success, error) => {
        if(success)
        {
            // 对推送状态变更的服务器通信成功
        }
       else
       {
            // 推送状态变更失败。请使用error.message显示错误消息。
        }
    });
    
 ```

### 夜间推送设置<a name="야간푸시설정"></a>
如要设置夜间推送，请使用下列代码。

* 方式1

```C#
GamePot.setPushNightStatus(bool nightPushEnable);

    /// 对夜间推送状态变更的服务器通信成功
    public void onPushNightSuccess() {
    }

    /// 对夜间推送状态变更的服务器通信失败
    public void onPushNightFailure(NError error) {

        // 夜间推送状态变更失败时，请使用error.message显示错误消息。
    }
```

* 方式2

```C#
    void GamePot.setPushNightStatus(bool nightPushEnable, GamePotCallbackDelegate.CB_Common);

    GamePot.setPushNightStatus(nightPushEnable, (success, error) => {
        if(success)
        {
            // 对夜间推送状态变更的服务器通信成功
        }
       else
       {
            // 夜间推送状态变更失败。请使用error.message显示错误消息。
        }
    });
```

<!--

### 广告推送设置<a name="광고푸시설정"></a>
如要设置广告推送，请使用下列代码。

* 方式1

```C#
    GamePot.setPushADStatus(bool adPushEnable);

    /// 对广告推送状态变更的服务器通信成功
    public void onPushAdSuccess() {
    }

    /// 对广告推送状态变更的服务器通信失败
    public void onPushAdFailure(NError error) {

        // 广告推送状态变更失败时，请使用error.message显示错误消息。
    }
```

* 方式2

```C#
    void GamePot.setPushADStatus(bool adPushEnable, GamePotCallbackDelegate.CB_Common);

    GamePot.setPushADStatus(adPushEnable, (success, error) => {
        if(success)
        {
            // 对广告推送状态变更的服务器通信成功
        }
       else
       {
            // 广告推送状态变更失败。请使用error.message显示错误消息。
        }
    });
```
-->


#### 一般/夜间/广告推送同时设置<a name="일반야간광고푸시한번에설정"></a>
如果是登录前需要确认是否允许推送的游戏，登录后必须调用以下代码。

* 方式1

```C#
GamePot.setPushStatus(bool pushEnable, bool nightPushEnable, bool adPushEnable);

/// 对推送状态变更的服务器通信成功
public void onPushStatusSuccess() {
}

/// 对推送状态变更的服务器通信失败
public void onPushStatusFailure(NError error) {

    // 推送状态变更失败时，请使用弹窗等方式告知玩家error.message。
}
```

* 方式2


```C#
void GamePot.setPushStatus(bool pushEnable, bool nightPushEnable, bool adPushEnable, GamePotCallbackDelegate.CB_Common);

GamePot.setPushStatus(pushEnable, nightPushEnable, adPushEnable, (success, error) => {
    if(success)
    {
        // 对推送状态变更的服务器通信成功
    }
   else
   {
        // 推送状态变更失败。请使用弹窗等方式告知玩家error.message。
    }
});
```

### 确认推送状态<a name="푸시상태확인"></a>
如要确认当前推送状态，请使用下列代码。

```C#
NPushInfo pushInfo = GamePot.getPushStatus();

// 是否允许pushInfo.enable
// pushInfo.night   是否允许夜间推送
```

### 图片推送功能<a name="이미지푸시기능"></a>
为在iOS应用中接收并处理通知图片，按以下方法添加通知服务扩展程序。

1. 在项目中点击 **Target** 菜单后，请选择 **Notification Service Extension** ，然后点击 **Next** 。
2. 输入**Project Name**后点击**Finish**。
3. 对已创建的Notification Service Extension模块的NotificationService.h文件作出如下修改。
    ```C
    // 导入GamePot/GamePotNotificationServiceExtension.h
    // #import <UserNotifications/UserNotifications.h>
    #import <GamePot/GamePotNotificationServiceExtension.h
    // 继承GamePotNotificationServiceExtension代替UNNotificationServiceExtension
    // @interface NotificationService : UNNotificationServiceExtension
    @interface NotificationService : GamePotNotificationServiceExtension
    @end
    ```
4. 请对已创建的Notification Service Extension模块的NotificationService.m文件作出如下修改。
    ```C
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
5. 请在已创建的Notification Service Extension模块中依次点击**Targets > Build Phases > Link Binary With Libraries**菜单，然后添加GamePot.framework。


### 本地推送功能<a name="로컬푸시기능"></a>
可以不通过推送消息服务器，直接在设备自主显示推送。

如要通过注册推送在规定时间显示本地推送时，请使用下列代码。

```C#
int pushId = GamePot.sendLocalPush(DateTime.Parse("2018-01-01 00:00:00"), "title", "content");

// pushid的返回值由开发商管理 
```

#### 取消已注册的本地推送<a name="등록한로컬푸시취소"></a>
若要使用注册本地推送时获得的```pushid```值取消当前已注册的推送，请使用下列代码。

```C#
GamePot.cancelLocalPush(/*注册推送时获得的pushId*/);
```

## 显示公告事项图片的功能<a name="공지사항이미지표시기능"></a>
可设置为在仪表盘**公告事项**菜单显示上传的图片。 推荐图片大小如下。

* 大小：720x1200（Portrait）、1280x640（Landscape）
* 容量：250KB以下

如要在仪表盘**公告事项**菜单显示上传的图片，请使用下列代码。

```C#
GamePot.showNotice(bool Flag = true);

// true：应用“今日不再显示”
// false：与“今日不再显示”无关，强制显示

GamePot.showEvent(string Type)

// Type：仅显示与仪表盘公告事项 > 分类菜单中设置的分类名称相对应的图片

public void onReceiveScheme(string scheme)
{
    // 传递在GAMEPOT仪表盘设置的scheme值
}
```

## 客户支持功能<a name="고객지원기능"></a>
通过与仪表盘关联，可使用客户咨询、调用政策及条款UI、同意收集等功能。


### 客户咨询功能<a name="고객문의기능"></a>
可使用会员发送咨询，由负责人回复的客户咨询功能。 与仪表盘的**客户支持 > 客户咨询**菜单关联。

客户咨询UI根据设备语言将变更为韩语、英语、日语、中文（简体、繁体）中的一个语言，除此之外的设备语言，则变更为英语。

如要与仪表盘关联使用客户咨询功能，请使用下列代码。

```C#
GamePot.showCSWebView();
```

#### 外部链接客户咨询<a name="외부링크고객문의"></a>
如要允许通过外部链接访问的未登录客户也能提交咨询，请使用下列代码。

```C#
// url：GAMEPOT发放的外部客户支持URL

GamePot.showWebView(string url);
```


### 条款及政策UI调用功能<a name="약관및정책UI호출기능"></a>
可在仪表盘的**客户支持**菜单以UI形式调用已撰写的各种条款、政策。

如要调用条款及政策UI，请使用下列代码。

* **使用条款**
    ```C#
    GamePot.showTerms();
    ```

* **隐私政策**
    ```C#
    GamePot.showPrivacy();
    ```
* **退款政策**
    ```C#
    GamePot.showRefund();
    ```

### 条款同意功能（含GDPR）<a name="약관동의기능GDPR포함"></a>
可使用提供的弹窗UI功能收集在仪表盘已撰写的各种政策及条款的同意。 也可以收集GDPR政策的同意。

#### 自动调用条款同意<a name="약관동의자동호출"></a>
如果使用GAMEPOT Unity SDK v3.3.0以上版本，当会员登录时将自动显示条款同意弹窗。

如要变更登录时是否自动调用条款同意，请使用下列代码。 

```C#
// 默认值为true
// 自动弹出弹窗时，应用MATERIAL_BLUE主题 
// 若设置为false，登录时不显示条款同意弹窗。
GamePot.setAutoAgree(true);

// 自定义应用MATERIAL_ORANGE主题时
NAgreeInfo bulider = new NAgreeInfo(); 
bulider.theme = "MATERIAL_ORANGE";
GamePot.setAutoAgreeBuilder(bulider);

...

GamePot.login(NCommon.LoginType);

...
```

#### 手动调用条款同意<a name="수동약관동의호출"></a>
如要手动执行条款调用，请使用下列代码。

* 选择主题
    ```java
    // 默认主题
    BLUE
    GREEN

    // 改进主题
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
    MATERIAL_PEACH,
    ```

* 调用 - 方式1



    ```C#
     // 默认调用（应用MATERIAL_BLUE主题）
    GamePot.showAgreeDialog();

    // 应用其他主题时
    NAgreeInfo info = new NAgreeInfo();
    info.theme = "MATERIAL_RED";
    GamePot.showAgreeDialog(info);
    // 同意条款时
    public void onAgreeDialogSuccess(NAgreeResultInfo info)
    {
        // info.agree：全部同意必要条款时为true
        // info.agreePush：勾选同意接收一般广告类消息时为true，否则为false
        // info.agreeNight：勾选同意接收夜间广告推送时为true，否则为false
        // agreePush/agreeNight值请在登录成功后通过setPushStatus API一次性设置。
    }

    // 发生错误
    public void onAgreeDialogFailure(NError error)
    {
        // 请使用error.message显示错误消息。
    }
   ```


* 调用 - 方式2


```C#
        // 默认调用（应用蓝色主题）
    showAgreeDialog(GamePotCallbackDelegate.CB_ShowAgree);

    // 应用其他主题时
    NAgreeInfo info = new NAgreeInfo();
    info.theme = "MATERIAL_RED";
    GamePot.showAgreeDialog(info,GamePotCallbackDelegate.CB_ShowAgree);
    
    GamePot.showAgreeDialog( info, (success, NAgreeResultInfo agreeInfo, NError error) => {
       if(success)
       {
            // 同意条款时
            // info.agree：全部同意必要条款时为true
             // info.agreePush：勾选同意接收一般广告类消息时为true，否则为false
             // info.agreeNight：勾选同意接收夜间广告推送时为true，否则为false
             // agreePush/agreeNight值请在登录成功后通过setPushStatus API一次性设置。
       }
       else
       {
            // 发生错误
            // 请使用error.message显示错误消息。
       }
    });
    ```

#### 自行配置条款同意UI主题<a name="약관동의UI테마직접구성"></a>
可使用自行配置的条款同意UI主题替代SDK提供的主题。

如要使用自行设置的条款同意UI主题，调用条款同意前请使用下列代码配置主题。

```C#
NAgreeInfo info = new NAgreeInfo();
info.theme = "MATERIAL_RED";
info.headerBackGradient = new string[] { "0xFF00050B", "0xFF0F1B21" };
info.headerTitleColor = "0xFFFF0000";
info.headerBottomColor = "0xFF00FF00";
// 未使用时设置为""
info.headerTitle = "同意使用条款";
// Android：res/drawable对象ID（文件名）
// iOS：asset对象ID（文件名）
info.headerIconDrawable = "ic_stat_gamepot_agree";

info.contentBackGradient = new string[] { "0xFFFF2432", "0xFF11FF32" };
info.contentIconColor = "0xFF0429FF";
info.contentCheckColor = "0xFFFFADB5";
info.contentTitleColor = "0xFF98FFC6";
info.contentShowColor = "0xFF98B3FF";
// Android：res/drawable对象ID（文件名）
// iOS：asset对象ID（文件名）
info.contentIconDrawable = "ic_stat_gamepot_small";

info.footerBackGradient = new string[] { "0xFFFFFFFF", "0xFF112432" };
info.footerButtonGradient = new string[] { "0xFF1E3A57", "0xFFFFFFFF" };
info.footerButtonOutlineColor = "0xFFFF171A";
info.footerTitleColor = "0xFFFF00D5";
info.footerTitle = "开始游戏";

// 是否显示“同意接收一般广告类消息”按钮
info.showPush = true;

// 是否显示“同意夜间接收广告类消息”按钮
info.showNightPush = true;

// 设置同意接受一般广告类链接按钮（不使用时无需输入）
info.pushDetailURL = "https://...";

// 设置同意接受夜间广告类链接按钮（不使用时无需输入）
info.nightPushDetailURL = "https://...";

// 更改语句
info.allMessage = "全部同意";
info.termMessage = "必选）使用条款";
info.privacyMessage = "必选）隐私政策";
info.pushMessage = "可选）同意接收一般推送";
info.nightPushMessage = "可选）同意接收夜间推送";


//勾选接收广告推送（一般/夜间）后，游戏开始时是否显示Toast消息（同意时间）
GamePot.setShowToastPushStatus(true);
GamePot.showAgreeDialog(info);

//是否激活条款弹窗内年龄限制相关选项（默认禁用/激活时，GAMEPOT仪表盘 > 客户支持 > 设置 > GDPR > 邮件验证项目为必填项）
info.ageCertificationShow = false;  // true：激活年龄限制 false：禁用
```
* 各个变量将应用到如下图片所显示的区域中。
  - **AgeView**
    ![gamepotandroid09ko](./images/gamepot_android_09_ko.png)
  - **EmailView**
    ![gamepotandroid091ko](./images/gamepot_android_09_1_ko.png)
  - **AgreeView**
    ![gamepotandroid092ko](./images/gamepot_android_09_2_ko.png)
    
#### GDPR条款确认列表功能<a name="GDPR약관체크리스트기능"></a>
如要以列表形式导入在仪表盘激活的GDPR条款项目，请使用下列代码。

```C#a
//返回的数据格式为string[]。
GamePot.getGDPRCheckedList();

//返回的各项参数对应仪表盘的下列设置。
gdpr_privacy：隐私政策
gdpr_term：使用条款
gdpr_gdpr：GDPR使用条款
gdpr_push_normal：同意接收事件推送
gdpr_push_night：同意接收夜间事件推送（仅限韩国）
gdpr_adapp_custom：同意查看个性化广告（GDPR实施国家和地区）
gdpr_adapp_nocustom：同意查看非个性化广告（GDPR实施国家和地区）
```

## 恶意使用支付取消的用户重新支付弹窗功能<a name="결제취소악용자재결제팝업기능"></a>
对通过仪表盘的**支付取消**菜单恶意取消Google支付的用户进行了自动停用设置时，会向该恶意用户显示SDK提供的重新支付弹窗UI，当用户通过UI对取消支付的项目进行重新支付时，将自动取消停用。

如要修改恶意取消支付用户重新支付的弹窗默认文本，请使用下列代码。

```C#

NVoidInfo info = new NVoidInfo();

//主题种类
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

//主题变更
info.theme = "MATERIAL_ORANGE";

// 更改语句
info.headerTitle = "Header Title Section!";

info.descHTML = "descHTML Section!";

info.listHeaderTitle = "listHeaderTitle Section!";

info.footerTitle = "footerTitle Section!";

GamePot.setVoidBuilder(info);
```


## 远程配置功能<a name="원격구성기능"></a>
可导入注册在仪表盘**游戏 > 远程配置**菜单的服务器参数值。 如果在SDK使用导入的参数值，无需更新游戏可对各个要素进行修改及控制。 

导入的参数值会在登录时加载，之后可以被调用。

如要使用远程配置功能，请使用下列代码。

```C#
//“test_01”：参数string
var str_value = GamePot.getConfig("test_01");

//以json字符串形式获取仪表盘中添加的所有参数。
var json_value = GamePot.getConfigs();
```

## 游戏日志传输功能<a name="게임로그전송기능"></a>
调用游戏日志后，可在仪表盘的**游戏 > 玩家**菜单中查看。

如要使用游戏日志传输功能，请参考表的内容在下列代码输入保留字后调用代码。

* **保留字及代码**
     保留字	| 是否为必填 |	类型 |	描述 |	最大长度|
     --- | --- | --- | --- | ---|
    ```GamePotSendLogCharacter.NAME```	| 必填	| ```String``` | 角色名称	| 128|
    ```GamePotSendLogCharacter.LEVEL```	| 选择	| ```String```	| 级别	| 128|
    ```GamePotSendLogCharacter.SERVER_ID```	| 选择	| ```String``` |	服务器ID |	128|
    ```GamePotSendLogCharacter.PLAYER_ID```	| 选择	| ```String``` | 角色ID |128|
    ```GamePotSendLogCharacter.USERDATA```	| 选择	| ```String``` |	ETC |	128 |
    ```C#
    String name = "角色名称";
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

    // 结果值true：验证成功。 日志将发送到GAMEPOT服务器。
    // 结果值false：验证失败。请确认logcat。
    ```

## 确认AppStatus <a name="AppStatus확인"></a>
若要确认当前客户端的AppStatus，请使用下列代码。

```C#
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
        // 未维护/更新相关的设置时
        break;

        case NCommon.ResultCheckAppStatus.FAILED:
        // Handling error
        break;

        case NCommon.ResultCheckAppStatus.NEED_UPDATE:
        // 更新
        // Handling appStatus
        break;

        case NCommon.ResultCheckAppStatus.MAINTENANCE:
        // 维护
        // Handling appStatus
        break;
        
        default:
        break;
    }
});
```

### 设置setUserData <a name="setUserData설정"></a>
登录后想给相应会员添加附加信息时使用。
密钥数量上限为50个
值长度上限为1024字节
相应信息只能在会员详细项目中确认。

* 方式1



```C#
JSONNode _json = new JSONObject();
_json.Add("appversion", "1.0.23");
_json.Add("server", "s1");
string json = _json.ToString();
GamePot.setUserData(_json);

// setUserData成功
public void onSetUserDataSuccess() {

}

// setUserData失败
public void onSetUserDataFailure(NError error) {

}
```

* 方式2


```C#
void setUserData(JSONNode userData, GamePotCallbackDelegate.CB_SetUserData cbSetUserData);

JSONNode _json = new JSONObject();
_json.Add("appversion", "1.0.23");
_json.Add("server", "s1");
string json = _json.ToString();

GamePot.setUserData(_json, (success,  error) => {
    if(success)
    {
        // setUserData成功
    }
   else
   {
        // setUserData失败
    }
});
```


## 第三方SDK关联<a name="3rdPartySDK연동"></a>
GAMEPOT Unity SDK支持与第三方SDK关联。 

### 第三方SDK登录关联<a name="3rdPartySDK로그인연동"></a>
如要通过第三方SDK关联使用登录功能，请参考表的内容在下列参数输入值后使用代码。

* **参数及代码**
    * 由于不支持自动登录，因此需要每次调用。
   
    参数名 |	是否为必填 |	类型 | 描述
    --- | --- | --- | ---
    ```userid```	| 必填	| ```String```	| 用户唯一ID<br>值无法使用“:”（冒号）
    ```C#
    String userid = "memberid of 3rd party sdk";

    GamePot.loginByThirdPartySDK("userid");
    ```
    
### 第三方SDK支付关联<a name="3rdParty결제연동"></a>
如要通过第三方SDK关联使用支付功能，请参考表的内容在下列代码输入参数值后使用代码。

* **参数及代码**
    参数名 |	是否为必填 |	类型 |	描述
    --- | --- | --- | ---
    ```productid``` |	必填 |	```String``` | 在仪表盘添加的道具ID
    ```transactionid```	| 必填	| ```String```	| 支付收据编号（GPA-xxx-xxxx-xxxx）
    ```store``` | 必填 | 支付商店（```google```, ```apple```, ```one```, ```galaxy```)
    ```currency```	| 选择	| ```String```	| 货币（KRW、USD）
    ```price``` |	选择 |	```double``` | 付费道具的金额
    ```paymentid``` |	选择 |	```String``` | 支付ID<br>一般与store_id相同
    ```uniqueid``` |	选择 |	```String``` | 开发商使用的唯一ID
    ```C
    String productId = "purchase_001";
    String transactionId = "GPA-xxx-xxxx-xxxx";
    String currency = "KRW";
    double price = 1200;
    String paymentId = "google";
    String uniqueId = "developer unique id";

    sendPurchaseByThirdPartySDK(string productId, string transactionId, string currency, double price, string store, string paymentId, string uniqueId);
    ```

## 关联Firebase SDK时注意事项<a name="FirebaseSDK연동시주의사항"></a>
如要正常关联Firebase SDK ，包括首次关联在内，每当包名称变更时需在**Assets > External Dependency Manager > Android Resolver > Settings**菜单取消勾选Patch mainTemplate.gradle选项后进行Resolve。

Firebase库按照输入至Unity编辑器中的包名称进行重新打包时，若包名称有误，将导致应用安装失败。 这种情况，需正确修改包名称。

如要确认并修改包名称，请使用下列代码。

```C#
// 进行域名解析后，确保com.google.firebase.firebase-common-[Firebase库版本].aar内
AndroidManifest.xml的android:authorities值为与版本匹配的包名称形式（[包名称].firebaseinitprovider）。

<provider>
            android:name="com.google.firebase.provider.FirebaseInitProvider"
            android:exported="false"
            android:authorities = "[应用包名称].firebaseinitprovider"
```

## 在Native环境下修改项目 <a name="Native환경에서프로젝트수정"></a>
                                                 
如果使用GAMEPOT Unity SDK期间需要在Native环境下修改项目，须创建继承MainActivity的io.gamepot.unity.plugin.GamePotSDKActivity的Class后单独处理的MainActivity。

使用GAMEPOT Unity SDK在Native环境修改项目的方法如下。 本指南以[示例文件](https://xyuditqzezxs1008973.cdn.ntruss.com/patch/UnityGameActivityBridge_sample.zip){target=&quot;_blank&quot;}为准进行说明。

1. 	请删除位于已下载的示例项目的/app/libs路径中的示例Bridge文件。
2.  请在已下载的示例项目的/app/libs路径中添加当前项目的gamepot-bridge.aar文件。
3. 	请将构建后创建的.aar文件添加至项目路径下的/Android/libs路径。
4. 	使用下列代码修改AndroidManifest.xml，以便替换MainActivity。
    ```C#
    修改前：
            <activity android:theme="@style/UnityThemeSelector"
                android:name="io.gamepot.unity.plugin.GamePotSDKActivity"

    修改后： 
                android:name="io.gamepot.unity.plugin.Game.GameActivity"   //示例基准：变更为构建时继承的Activity
    ```