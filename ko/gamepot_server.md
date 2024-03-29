---
search:
  keyword: ['gamepot']
---

#### **네이버 클라우드 플랫폼의 상품 사용 방법을 보다 상세하게 제공하고, 다양한 API의 활용을 돕기 위해 <a href="https://guide.ncloud-docs.com/docs/ko/home" target="_blank">[설명서]</a>와 <a href="https://api.ncloud-docs.com/docs/ko/home" target="_blank">[API 참조서]</a>를 구분하여 제공하고 있습니다.**

<a href="https://api.ncloud-docs.com/docs/ko/game-gamepot" target="_blank">Gamepot API 참조서 바로가기 >></a><br />
<a href="https://guide.ncloud-docs.com/docs/game-gamepot-overview" target="_blank">Gamepot 설명서 바로가기 >></a>

# Server API

## GAMEPOT 서버 &gt; 게임 서버

### Purchase Webhook\(required\)

결제 완료 후에 GAMEPOT서버에서 게임 서버로 아이템 지급을 위해 HTTP 요청을 합니다.

> GAMEPOT은 클라이언트로부터 전달받은 결제 정보를 토대로 스토어 영수증 검증까지 진행하여 불법 결제 시도를 막고 있습니다.

#### Request

HTTP 요청 시 정보는 아래와 같은 내용으로 전달드리고 해당 정보를 바탕으로 유저에게 아이템을 지급하시면 됩니다.

> `{domain}` 항목은 개발사에서 작업 완료 후 알려주어야 하며, 이 값은 GAMEPOT 대시보드 - 프로젝트 설정 - 일반 - Webhook 항목에 추가해야 합니다.

```java
https://{domain}?
userId={uuid}&orderId={orderId}&projectId={projectId}&platform={platform}&productId={productId}&store={store}&payment={payment}&transactionId={transactionId}&gamepotOrderId={gamepotOrderId}&uniqueId={uniqueId}&tp={tp}
```

| Attribute      | Type    | Max Length | Description                                                |
| :------------- | :------ | :--------- | :--------------------------------------------------------- |
| userId         | String  | 128        | 사용자ID                                                   |
| transactionId  | String  | 512        | 주문번호\(GPA-xxxx-xxxx-\)                                 |
| store          | String  | 64         | 스토어 정보\(apple, google, one\)                          |
| projectId      | String  | 128        | 프로젝트ID                                                 |
| productId      | String  | 256        | 구글/애플/원스토어에 등록된 상품ID                         |
| platform       | String  | 128        | 운영 Platform 정보 \(android, ios\)                        |
| payment        | String  | 64         | 결제 방식 \( apple, google, one, danal, mycard, mol ... \) |
| uniqueId       | String  | 512        | Unique id \(purchase api 호출 시 넣은 unique id\)          |
| gamepotOrderId | String  | 512        | GAMEPOT Order id                                           |
| serverId       | String  | -          | serverId \(purchase api 호출 시 넣은 serverId\)            |
| playerId       | String  | -          | playerId \(purchase api 호출 시 넣은 playerId\)            |
| tp             | Integer | -          | 1: 테스트 결제<br />0: 일반 결제                           |
| etc            | String  | -          | etc \(purchase api 호출 시 넣은 etc\)                      |

#### Response

응답은 아래와 같은 형식으로 해주세요.

```javascript
{
    "status": 1,
    "message" : ""
}
```

| Attribute | Type   | Description                   |
| :-------- | :----- | :---------------------------- |
| status    | Int    | 결과값 \( 0: 실패, 1: 성공 \) |
| message   | String | 오류 내용                     |

### Item Webhook\(required\)

쿠폰 사용 후 GAMEPOT서버에서 게임 서버로 아이템 지급을 위해 HTTP 요청을 합니다.

#### Request

HTTP 요청 시 정보는 아래와 같은 내용으로 전달드리고 해당 정보를 바탕으로 유저에게 아이템을 지급하시면 됩니다.

> `{domain}` 항목은 개발사에서 작업 완료 후 알려주어야 하며, 이 값은 GAMEPOT 대시보드 - 프로젝트 설정 - 일반 - Webhook 항목에 추가해야 합니다.

```text
https://{domain}?
userId={userId}&projectId={projectId}&platform={platform}&store={store}&userData={userData}&itemId=[{itemData}, {itemData}, ...]
```

| Attribute | Type   | Max Length | Description                                                                                        |
| :-------- | :----- | :--------- | :------------------------------------------------------------------------------------------------- |
| userId    | String | 128        | 사용자ID ( 게임팟 대시보드 > 게임 > 선물하기 > 대상 값이 전체인 경우 all )                         |
| projectId | String | 128        | Project ID                                                                                         |
| platform  | String | 128        | 운영 Platform 정보 \(Android, IOS\)                                                                |
| store     | String | 64         | 스토어 정보\(apple, google, one\)                                                                  |
| title     | String | -          | 게임팟 대시보드 > 게임 > 선물하기 > 제목 에 넣은 값                                                |
| content   | String | -          | 게임팟 대시보드 > 게임 > 선물하기 > 설명 에 넣은 값                                                |
| target    | String | -          | 게임팟 대시보드 > 게임 > 선물하기 > 대상 값 - 전체 : all / 사용자ID : user                         |
| expireMs  | String | -          | 게임팟 대시보드 > 게임 > 선물하기 > 만료일 값의 Timestamp ( GMT+9)                                                     |
| userData  | String | -          | coupon api 호출 시 두 번째 파라미터에 넣은 값                                                      |
| itemId    | Array  | -          | itemData Array - itemData\(JSON\) {"item_id" : String, "store_item_id" : String, "count" : Number} |
|     |   |           | item_id : 게임팟 > 게임 > 게임팟에서 생성한 아이템 항목의 고유아이디 / store_item_id : 아이템을 지급하고자 하는 아이템 아이디 / count : 지급할 아이템 수 |

> ex\)
>
> https://{domain}?itemId=\[{"item_id":"d0781c4e-df52-465b-ab93-0ee16fbf445d","store_item_id":"ttt","count":1}\]&platform=android&projectId=f1df9464-40a8-4a66-8421-196c7c661002&store=google&userId=2d485044-06c2-48c4-a6ed-4ab53dea88bb

#### Response

응답은 아래와 같은 형식으로 해주세요.

```javascript
{
    "status": 1,
    "message" : ""
}
```

| Attribute | Type   | Description                   |
| :-------- | :----- | :---------------------------- |
| status    | Int    | 결과값 \( 0: 실패, 1: 성공 \) |
| message   | String | 오류 내용                     |

## 게임 서버 &gt; GAMEPOT 서버

### Gamepot user ID verification\(optional\)

해당 Api는 로그인과는 상관없이 게임팟 사용자 아이디의 유효성 체크하는 과정입니다.

게임에서 로그인 완료 후 얻은 정보로 GAMEPOT 서버에 로그인 검증을 할 수 있습니다.

토큰 검증은 2 단계로 진행되며, 1단계 GAMEPOT 토큰 검증 후 2단계 소셜 토큰 검증이 진행됩니다.

> 2단계 검증은 GAMEPOT 대시보드 - 프로젝트 설정 - Auth key에 값이 입력되어 있어야 합니다.

1단계 GAMEPOT 토큰 검증은 로그인 후 얻은 MemberID(사용자ID), Token으로 동기 토큰 검증을 진행하며,

2단계 소셜 토큰 검증은 구글 로그인이나 페북 로그인을 통해 얻은 소셜 계정의 토큰으로 소셜 비동기 토큰 검증을 진행합니다.

2단계에서 검증 실패한 경우에는 GAMEPOT 이용정지 기능이 동작되어 이후 재 로그인 시 로그인이 불가합니다.

> 검증 실패에 따른 이용정지는 GAMEPOT 대시보드 - 프로젝트 설정 - Auth key 항목에서 스위치가 ON되어 있는 경우에만 동작하며, 이용정지 대상자는 GAMEPOT 대시보드 - 회원 - 이용정지 메뉴에서 확인이 가능합니다.

**1단계 검증을 동기처리하지 마세요!**

유저가 로그인하는 과정인데 이 기능을 동기 처리하면 네트웍 통신에 따른 지연이 발생하여 게임 이용에 허들이 됩니다. 또한, 해당 네트웍 통신이 물리적으로 분리된 상황이므로 그로 인한 네트웍 통신이 원할하지 않을 경우가 많습니다.

해당 기능은 비동기로 처리한 후 이후에 게임 이용을 제한하는 형태로 기능구현을 해주시기 바랍니다.

#### Request

데이터 무결성을 위해 클라이언트가 아닌 개발사 서버에서 진행 해주세요.

```text
POST
url : https://gamepot.apigw.ntruss.com/gpapps/v1/loginauth
Header : 'content-type: application/json'
data:
{
    "projectId": {GamePot SDK의 projectId},
    "memberId": {GamePot SDK의 memberid(사용자ID)},
    "token": {GamePot SDK의 Token}
}
```

| Attribute | Type   | Max Length | Description                      |
| :-------- | :----- | :--------- | :------------------------------- |
| projectId | String | 128        | GamePot SDK의 projectId          |
| memberId  | String | 128        | GamePot SDK의 memberid(사용자ID) |
| token     | String | 2048       | GamePot SDK의 Token              |

#### Response

1단계 검증에서 검증 실패하는 경우 status가 1이 아닌 값이 입력됩니다.

이 경우는 게임 진입을 제한 해주세요.

```javascript
{
    "status": 1,
    "message" : ""
}
```

| Attribute | Type   | Description                                     |
| :-------- | :----- | :---------------------------------------------- |
| status    | Int    | 결과값 \(1: 성공, 실패는 아래 Error code 참고\) |
| message   | String | 오류 내용                                       |

#### Error code

| Code | Description                                                                                                     |
| :--- | :-------------------------------------------------------------------------------------------------------------- |
| 0    | Body에 누락된 데이터가 있는 경우 HTTP 요청 시 projectId, memberId, token을 모두 넣었는지 확인해 주세요.         |
| -1   | Token 검증 실패 Token이 조작된 경우                                                                             |
| -2   | MemberId 검증 실패 Token의 MemberId 정보와 body의 MemberId가 일치하지 않은 경우                                 |
| -3   | Token 만료 SDK login api가 성공한 시각과 해당 Authentication check를 요청한 시각이 10분 이상 차이가 발생한 경우 |

### ThirdParty Purchase

> 이 기능은 일반적으로 사용되지 않는 기능이므로 적용 전 GAMEPOT에 문의해주세요.

#### Request

```text
POST
url : https://gamepot.apigw.ntruss.com/gpapps/v2/thirdparty/purchase
Header : 'content-type: application/json'
Header : 'x-api-key: xxxxxxxxxxx'
data:
{
	"projectId": "e948e5bc-dccd-4729-b9b0-b547ae34b85d",
	"store": "tpay",
	"productId": "purchase_001",
	"transactionId": "t-123412812-sadl-2384-75847",
	"memberId":"89a907ed-0e1d-42fb-ae4d-75e95581220d",
	"currency": "KRW",
	"price":1000,
	"paymentId": "prepaid",
	"uniqueId": ""
}
```

| Header    | Type   | Required | Description                  |
| :-------- | :----- | :------- | ---------------------------- |
| x-api-key | String | O        | GamePot에서 발급하는 인증 키 |

<br/>

| Attribute     | Type   | Max Length | Required | Description                      |
| :------------ | :----- | :--------- | :------- | :------------------------------- |
| projectId     | String | 128        | O        | GamePot SDK의 projectId          |
| store         | String | 64         | O        | 결제 스토어                      |
| productId     | String | 256        | O        | 결제 아이템 아이디               |
| transactionId | String | 512        | O        | 결제 고유 아이디                 |
| memberId      | String | 128        | O        | GamePot SDK의 memberid(사용자ID) |
| currency      | String | 64         | X        | 결제 통화                        |
| price         | Number | -          | X        | 결제 금액                        |
| paymentId     | String | 64         | X        | 결제 수단                        |
| uniqueId      | String | 512        | X        | 게임내 결제 고유 아이디          |

#### Response

```javascript
{
    "status": 1,
    "message" : ""
}
```

| Attribute | Type   | Description                                     |
| :-------- | :----- | :---------------------------------------------- |
| status    | Int    | 결과값 \(1: 성공, 실패는 아래 Error code 참고\) |
| message   | String | 오류 내용                                       |

#### Error code

| Code | Description                                                                                                              |
| :--- | :----------------------------------------------------------------------------------------------------------------------- |
| -1   | Body에 누락된 데이터가 있는 경우 <br/> projectId, transactionId, productId, store, memberId을 모두 넣었는지 확인하세요.  |
| -2   | price 값이 number타입이 아닌 경우<br/> number타입으로 넣으세요.                                                          |
| -3   | projectId가 없는 경우<br/> 입력한 projectId를 다시 확인하세요.                                                           |
| -4   | 프로젝트가 해당 api를 지원하지 않는 경우<br/> GAMEPOT에 문의해주세요.                                                    |
| -5   | transactionId가 이미 존재하는 경우                                                                                       |
| -6   | DB오류. GAMEPOT에 문의해주세요.                                                                                          |
