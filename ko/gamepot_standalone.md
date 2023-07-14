---
search:
  keyword: ['gamepot']
---

#### **네이버 클라우드 플랫폼의 상품 사용 방법을 보다 상세하게 제공하고, 다양한 API의 활용을 돕기 위해 <a href="https://guide.ncloud-docs.com/docs/ko/home" target="_blank">[설명서]</a>와 <a href="https://api.ncloud-docs.com/docs/ko/home" target="_blank">[API 참조서]</a>를 구분하여 제공하고 있습니다.**

<a href="https://api.ncloud-docs.com/docs/ko/game-gamepot" target="_blank">Gamepot API 참조서 바로가기 >></a><br />
<a href="https://guide.ncloud-docs.com/docs/game-gamepot-overview" target="_blank">Gamepot 설명서 바로가기 >></a>

# GamePot Unity SDK (Standalone)

## 0. Project Setting

(빌드 시 필요한) 게임팟 프로젝트와 관련된 각종 셋팅값을 입력합니다.

1.  유니티 에디터 상단의 GAMEPOT >> GAMEPOT CONFIG 메뉴를 클릭합니다.

![gamepot_standalone_01](./images/gamepot_standalone_01.png)

2.  해당 메뉴를 클릭 후, 인스펙터창에 게임팟 프로젝트와 관련된 각종 셋팅값을 입력하고, 하단의 **Confirm** 버튼을 클릭합니다.

| ID         | type   | desc                                                                    |
| :--------- | :----- | :---------------------------------------------------------------------- |
| PROJECT_ID | string | 게임팟 Project ID                                                       |
| STORE      | string | 스토어 ID                                                               |
| API_URL    | string | ~~게임팟 api 서버 url (default)~~ 빈 값으로 유지해주세요. (v2.4.0 이후) |

|

![gamepot_standalone_02](./images/gamepot_standalone_02.png)

3.  **Confirm** 버튼을 누르면, **/Assets/** 의 경로에 GamePotStandalone_Config.json 파일이 생성된 것을 확인 할 수 있습니다.
4.  Windows 플랫폼 빌드 시, 초기화 시점에 해당 config정보를 읽어올 수 있도록 **~/build/bin/{Build_Name}\_Data** 경로에 해당 json 파일을 위치시켜주세요.

![gamepot_standalone_03](./images/gamepot_standalone_03.png)

## 1. 초기화

게임을 시작할때 로드되는 첫 장면에 사용되는 개체에 다음 코드를 추가합니다.

```csharp

using GamePotUnity;
using GamePotUnity.Standalone.Networking;

public class GamePotLoginSampleScene : MonoBehaviour {

    bool isPaused = false;

    void Awake() {

        // GamePot 인스턴스 초기화
        GamePot.initPlugin();
    }
    void Start () {
        GamePot.setListener(  GamePotInterface.cs 상속받은 class );
         // ex) GamePot.setListener(new GamePotSampleListener());
    }

   void OnApplicationPause(bool pauseStatus)
    {
       if(pauseStatus == true)
       {
           GamePotChat.start();    //(re)connect to socket server
       }
       else
       {
           GamePotChat.stop();    //disconnect from socket server
       }
       pauseStatus != isPaused
    }
}

ex)
public class GamePotSampleListener : MonoBehaviour , IGamePot {
    ....
}
```

## 2. MemberInfo 셋팅

- **로그인 API를 호출하기 전**, (GAMEPOT JS SDK로부터 획득한) UserInfo 값을 셋팅해주세요.

- 다음과 같이, MemberID(GamePot) / Token(GamePot) 값을 GamePotSettings.MemberInfo에 저장합니다.

```csharp

//전달받은 memberId / token 값을 GamePotSettings.MemberInfo에 넣어줍니다.
***************************************************

[Step 1] - Setting MemberInfo

NUserInfo userInfo = new NUserInfo
{
     memberid = (string) GAMEPOT_MEMBER_ID,
     token = (string) GAMEPOT_TOKEN
};
GamePotSettings.MemberInfo = userInfo;

***************************************************

[Step 2]

....
//GamePotSettings.MemberInfo 값을 셋팅한 다음, Login API를 호출해주세요.
GamePot.login(NCommon.LoginType.STANDALONE);
....

```

| Struct                    | ID       | type   | desc             |
| :------------------------ | :------- | :----- | :--------------- |
| GamePotSetting.MemberInfo |          |        |                  |
|                           | memberid | string | 게임팟 Member ID |
|                           | token    | string | 게임팟 Token     |

|

## 3. 로그인 (점검 체크)

- Login API를 호출하면, 내부적으로 점검 여부를 체크하여 Callback 이벤트가 호출됩니다. 이 때, Windows 플랫폼의 경우 NCommon.LoginType.STANDALONE을 파라메터로 넣어주세요.

- 로그인 성공 시, GamePotSettings.MemberInfo에 셋팅된 정보가 NUserInfo 구조체에 저장되어 onLoginSuccess 이벤트 파라메터로 return 됩니다.

Case 1 )

Request:

```csharp
GamePot.login(NCommon.LoginType.STANDALONE);
```

Response:

```csharp
// 로그인 성공
public void onLoginSuccess(NUserInfo userInfo)
{
}

// 로그인 실패
public void onLoginFailure(NError error)
{
    // 로그인을 실패하는 경우
    // error.message를 팝업 등으로 유저에게 알려주세요.
}

// 점검(대시보드에 점검이 활성화되어 있는 경우 호출)
public void onMainternance(NAppStatus status)
{
    // TODO: 파라미터로 넘어온 status 정보를 토대로 팝업을 만들어 사용자에게 알려줘야 합니다.
    // ex) 인게임 팝업을 통해 개발사에서 직접 UI 구현
}

```

- Case 2

Request:

```csharp
GamePot.login(NCommon.LoginType, GamePotCallbackDelegate.CB_Login);
```

```csharp
GamePot.login(NCommon.LoginType, (resultState, userInfo, appStatus, error) => {
    switch (resultState)
    {
        case NCommon.ResultLogin.SUCCESS:
        // login success
        break;
        case NCommon.ResultLogin.FAILED:
        // login fail
        break;
        case NCommon.ResultLogin.MAINTENANCE:
        // onMaintenance
        break;
        default:
        break;
    }
});
```

NUserInfo 정의

```csharp
public class NUserInfo
{
    public string memberid { get; set; }        // 맴버 ID(유저의 유니크 아이디)
    public string name { get; set; }            // 이름
    public string profileUrl { get; set; }      // 프로필 URL(존재 시)
    public string email { get; set; }           // 이메일(존재 시)
    public string token { get; set; }           // 유저 광고 ID
    public string userid { get; set; }          // Social ID(google, facebook ...)
}
```

<!-- ### Step 4
(setup 이후,) 소켓 서버에 대해 핸들링(connect / disconnect) 할 수 있습니다.

```csharp
GamePotChat.start();    //connect
GamePotChat.stop();    //disconnect
​``` -->

## 4. 기타 API

### 4-1. 고객지원 / FAQ (웹뷰)

- ref. 현재 유니티 엔진 상에서, **웹뷰에 대한 Event 수신 / 한글 유니코드 입력이 불가한 이슈** 가 있습니다. 이에 따라, 아직 (공식적으로) 고객지원 메뉴에 대한 Native API는 제공되지 않는 상태입니다.

Case 1 ) 사용자 아이디로 고객문의 UI를 연동할때 


```csharp

//대시보드 주소 및 각 파라메터 값을, 생성한 GamePot 대시보드에 대한 값으로 수정하여 접근이 가능합니다.

[url]
"https://{domain}/cs/question?projectid={projectid}&store={store}&memberid={memberid}&device={device}&sdkversion={sdkversion}&language={language}"

/* Example
https://dashboard.gamepot.ntruss.com/demo/cs/question?projectid=XXXXXXXXX&store=XX&memberid=XXXXXXX&device=android&sdkversion=3.4.0&language=ko
*/

```

| ID         | desc                        | example                                  |
| :--------- | :-------------------------- | :--------------------------------------- |
| domain     | 게임팟 대시보드 domain 주소 | https://dashboard.gamepot.ntruss.com/demo  |
| projectid  | 게임팟 Project ID           | XXXXXXX     |
| store      | 스토어 명                   | android ,ios , one , pc                                  |
| memberid   | 게임팟 Member ID            | XXXXXXXXX     |
| device     | 플랫폼                      | android ,ios , one , pc                        |
| sdkversion | 게임팟 SDK Version          | 3.4.0                                    |
| language   | 언어                        | (ISO 639-1코드) ex) ko                                       |





<!--

Case 2 ) 로그인 성공 후 발생하는 토큰으로 고객문의 UI를 연동할때 

​```csharp
파라미터  정의:
projectid : 게임팟 프로젝트 아이디 (ex. 807db37b-99dd-4628-9b63-1077ded8155d
store : pc 
language : 문의자 언어 (ex. 한국어 - ko ) 
token : 로그인 후 획득한 토큰 
sdkversion : 3.4.0 ( 고정 값 )

정보가 맞지 않는 경우 400 에러 화면으로 이동합니다.
sdkversion 정보가 없는 경우 파일 업로드 메뉴가 보이지 않습니다.


[url]
"https://{domain}/cs/question?projectid={projectid}&store={store}&sdkversion={sdkversion}&language={language}&token={로그인 성공 후 토큰}"

https://dashboard.gamepot.ntruss.com/demo/cs/question?projectid=XXXXXX&sdkversion=3.4.0&store=pc&language=ko&token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhZ3JlZSI6eyJ0ZXJtc29mdXNlIjoiTiIsInByaXZhY3lwb2xpY3kiOiJOIn0sImdkcHIiOnsic3RhdHVzIjowLCJjaGVja2VkX3N0b3J5X2NhdGVnb3J5X2lkcyI6W119LCJsb2NhbCI6eyJzdGF0dXMiOjB9LCJwdXNoIjp0cnVlLCJuaWdodCI6ZmFsc2UsImFkIjp0cnVlLCJkZWxldGVkIjpmYWxzZSwibWFuYWdlciI6ZmFsc2UsInNhbmRib3giOmZhbHNlLCJfaWQiOiI2MWJjMWE1NjU0ZjliMTY3MThjNWM4NDIiLCJ1c2VybmFtZSI6IiIsInBhc3N3b3JkIjoiJDJiJDA0JEhzbXFELi5KMEdDZmtIa0hhdE5XYXVMRHhFNGRPamZBUW9rT3ZLOFJWNmt6cDNYNVZYYS5hIiwicHJvamVjdF9pZCI6IjgwN2RiMzdiLTk5ZGQtNDYyOC05YjYzLTEwNzdkZWQ4MTU1ZCIsInN0b3JlX2lkIjoiZ29vZ2xlIiwiaWQiOiIyNTJjZGQ5Ni1hYjkwLTQ1ODItOTIwYy1iZmU5YjJhNzMzNGYiLCJyZW1vdGVpcCI6IjYxLjQzLjU0LjMiLCJsb2dpbmVkQXQiOiIyMDIxLTEyLTE3VDA1OjA0OjIyLjIzOVoiLCJjb3VudHJ5IjoiS1IiLCJjcmVhdGVkQXQiOiIyMDIxLTEyLTE3VDA1OjA0OjIyLjI1MVoiLCJ1cGRhdGVkQXQiOiIyMDIxLTEyLTE3VDA1OjA0OjIyLjI1MVoiLCJfX3YiOjAsImlhdCI6MTYzOTcxNzQ2MiwiZXhwIjoxNjQ3NDkzNDYyfQ.__fyXqmw567Ilf2_blMhLJo_g6FwsWnRtWUI_Iiab6Y

```
-->

### 4-2. 쿠폰

> 쿠폰 번호를 입력받는 UI는 개발사에서 구현해주세요.

- Case 1

Request:

```csharp
GamePot.coupon(string couponNumber); // 쿠폰번호

GamePot.coupon(string couponNumber, string userData); // 쿠폰번호, 사용자정보
```

Response:

```csharp
/// 쿠폰 사용 성공
public void onCouponSuccess() {
}

/// 쿠폰 사용 실패
public void onCouponFailure(NError error) {
    // 쿠폰 사용을 실패하는 경우
    // error.message를 팝업 등으로 유저에게 알려주세요.
}
```

- Case 2

Request:

```csharp
GamePot.coupon(string couponNumber, GamePotCallbackDelegate.CB_Common); // 쿠폰번호

GamePot.coupon(string couponNumber, string userData, GamePotCallbackDelegate.CB_Common);    // 쿠폰번호, 사용자정보
```

```csharp
GamePot.coupon(couponNumber, (success, error) => {
   if(success)
   {
       // 쿠폰 사용 성공
   }
   else
   {
        // 쿠폰 사용을 실패하는 경우
        // error.message를 팝업 등으로 유저에게 알려주세요.
   }
});
```

#### - 아이템 지급

쿠폰 사용이 성공하면 개발사 서버에 Server to server api를 통해 아이템 지급을 요청합니다.

이를 위해선 Server to server api 메뉴에 `Item Webhook` 항목을 참고하여 처리하셔야 합니다.

### 4-3. 게임 로그 전송

게임에서 사용되는 정보를 담아 호출하면 `대시보드` - `게임`에서 조회가 가능합니다.

아래는 사용할 수 있는 예약어 정의 표 입니다.

| 예약어                            | 필수 | 타입   | 설명         | 최대 길이 |
| :-------------------------------- | :--- | :----- | :----------- | --------- |
| GamePotSendLogCharacter.NAME      | 필수 | String | 케릭터명     | 128       |
| GamePotSendLogCharacter.LEVEL     | 선택 | String | 레벨         | 128       |
| GamePotSendLogCharacter.SERVER_ID | 선택 | String | 서버아이디   | 128       |
| GamePotSendLogCharacter.PLAYER_ID | 선택 | String | 케릭터아이디 | 128       |
| GamePotSendLogCharacter.USERDATA  | 선택 | String | ETC          | 128       |

|

```csharp
String name = "케릭터명";
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
```

Request:

```csharp
GamePot.characterInfo(characterLog, GamePotCallbackDelegate.CB_Common);

GamePot.characterInfo(characterLog, (success, error) => {
    if(success)
    {
        //게임 로그 전송 성공
    }
    else
    {
        //게임 로그 전송 실패
    }
});
```

# 부록

### 3rd party SDK 연동 지원


## 3rd party SDK 로그인

> userid 값에 :(colon) 이 들어가면 안됩니다.

```csharp
String memberId = "memberid of 3rd party sdk";
GamePot.loginByThirdPartySDK(memberId);
```

Response:

```csharp
// 로그인 성공
public void onLoginSuccess(NUserInfo userInfo)
{
}

// 로그인 실패
public void onLoginFailure(NError error)
{
    // 로그인을 실패하는 경우
    // error.message를 팝업 등으로 유저에게 알려주세요.
}

// 점검(대시보드에 점검이 활성화되어 있는 경우 호출)
public void onMainternance(NAppStatus status)
{
    // TODO: 파라미터로 넘어온 status 정보를 토대로 팝업을 만들어 사용자에게 알려줘야 합니다.
    // ex) 인게임 팝업을 통해 개발사에서 직접 UI 구현
}

```


## 3rdParty_Purchase API 

3자 SDK를 통해 발생한 결제 이력을 게임팟 대시보드이 이력을 남기기 위한 기능 ( 보안상 서버에서 발송하는 방식으로 진행을 권장합니다.)

x-api-key는 게임팟에 문의 부탁드립니다.

#### Request

 - Method : POST
 - URI : https://gamepot.apigw.ntruss.com/gpapps/v2/thirdparty/purchase

```text
PUT
url : https://gamepot.apigw.ntruss.com/gpapps/v2/thirdparty/purchase
Header : 'Content-Type: application/json'
Header : 'x-api-key: XXXXXXXX'
data:
{
     "projectId": "XXXXXXXX",
     "store": "pc",
     "productId": "XXXXX",
     "transactionId": "XXXXXXX",
     "memberId":"XXXXXXX",
     "currency": "KRW",
     "price":1000,
     "paymentId": "XXXX",
     "uniqueId": ""

}
```
| Attribute    | Type   | Required | Description                  |
| :-------- | :----- | :------- | :--------------------------- |
| projectId  | String | O        |   GamePot SDK의 projectId   |
| store  | String | O        |   결제 스토어   |
| productId  | String | O        |   결제 아이템 아이디   |
| transactionId  | String | O        |   결제 고유 아이디   |
| memberId  | String | O        |   GamePot SDK의 memberId   |
| currency  | String | X        |   결제 통화   |
| price  | String | X        |   결제 금액   |
| paymentId  | String | X        |   결제 수단   |
| uniqueId  | String | X        |   게임내 결제 고유 아이디   |



#### Response

성공

```javascript
{
  "status": 1,
  "message" : ""
}
```

| Attribute       | Type    | Description                                     |
| :---------------| :------ | :---------------------------------------------- |
| status          | Int     | 결과값 \(1: 성공, 실패는 Error code 참고\)            |
| message        | String  | 오류 내용    |


실패
```javascript
{
  "status": -5,
  "message": "The order id already exist"
}
```

| Attribute | Type   | Description                                     |
| :-------- | :----- | :---------------------------------------------- |
| status    | Int    | 결과값 \(1: 성공, 실패시 Error code 참고\)            |
| message   | String | 오류 내용                                         |



#### Error code

| Code | Description                                                       |
| :--- | :---------------------------------------------------------------- |
| -1  | Body에 누락된 데이터가 있는 경우 projectId, transactionId, productId, store, memberId을 모두 었는지 확인하세요.                    |
| -2  | price 값이 number타입이 아닌 경우 number타입으로 넣으세요.        |
| -3  | projectId가 없는 경우 입력한 projectId를 다시 확인하세요.         |
| -4  | 프로젝트가 해당 api를 지원하지 않는 경우 GAMEPOT에 문의해주세요.         |
| -5  | transactionId가 이미 존재하는 경우         |
| -6  | DB오류. GAMEPOT에 문의해주세요.        |
| -99  | x-api-key 권한 오류         |


### 사용자 토큰 확인 API

사용자 토큰 확인 API

#### Request

 - Method : POST
 - URI : https://gamepot.apigw.ntruss.com/gpapps/v2/api/project/{projectid}/auth/token

```text
POST
url : https://gamepot.apigw.ntruss.com/gpapps/v2/api/project/{projectid}/auth/token
Header : 'accept-language: ko'
Header : 'Content-Type: application/json'
body : 
{
	"memberId":"XXXXXX",
	"token":"{GamePot SDK의 login token }"
}


```

| Attribute | Type   | Description                             |
| :-------- | :----- | :---------------------------------------|
| projectId | String | GamePot SDK의 projectId                  |

| body | Type   | Description                             |
| :-------- | :----- | :---------------------------------------|
| memberId | String | 사용자 아이디                  |
| token | String | 로그인 이후 획득한 토큰                  |





#### Response

성공

```javascript
{
    "status": 1,
    "decoded": {
        "agree": {
            "termsofuse": "N",
            "privacypolicy": "N"
        },
        "verify": {
            "key": "XXXXXXX",
            "updatedAt": "20XX-09-22T05:13:53.721Z"
        },
        "gdpr": {
            "status": 0,
            "checked_story_category_ids": [],
            "checked_category_ids": []
        },
        "local": {
            "status": 2,
            "email_cert_expired_at": null,
            "email_cert_key": null
        },
        "push": true,
        "night": false,
        "ad": true,
        "deleted": false,
        "manager": false,
        "sandbox": false,
        "username": "",
        "password": "$2b$04$kDY9HijwxPd5qHVCbkCJXexS8IpcsNmrKIfXH1gXnwWEtcQNOKvDy",
        "project_id": "{GamePot SDK의 projectId }",
        "store_id": "pc",
        "id": "XXXXX",
        "remoteip": "220.76.XX.XX",
        "loginedAt": "20XX-09-22T08:29:29.003Z",
        "country": "KR",
        "createdAt": "20XX-09-22T05:11:54.617Z",
        "updatedAt": "20XX-09-22T08:29:29.003Z",
        "iat": 1615186937,
        "exp": 1622962937
    }
}
```

| Attribute       | Type    | Description                                     |
| :---------------| :------ | :---------------------------------------------- |
| status          | Int     | 결과값 \(1: 성공, 실패는 Error code 참고\)            |
| agree           | String | 약관동의    (termsofuse/privacypolicy 값은 동일한 값 - Y : 동의 / N : 미동의)   |
| verify          | String | 본인인증     (해당 항목이 있는 경우 본인인증을 진행한 케이스)      |
| id              | String | 사용자 아이디           |
| project_id      | String | 프로젝트 아이디           |

실패
```javascript
{
    "status": -2,
    "message": "Token authentication failed."
}
```

| Attribute | Type   | Description                                     |
| :-------- | :----- | :---------------------------------------------- |
| status    | Int    | 결과값 \(1: 성공, 실패는 Error code 참고\)        |
| message   | String | 오류 내용                                         |

#### Error code

| Code | Description                                                       |
| :--- | :---------------------------------------------------------------- |
| -1   | 토큰 정보가 올바르지 않을 때                              |
| -2   | 토큰 정보가 올바르지 않을 때                              |