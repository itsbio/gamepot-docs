---
search:
  keyword: ['gamepot']
---

#### **We provide the <a href="https://guide.ncloud-docs.com/docs/en/home" target="_blank">[Manual]</a>and <a href="https://api.ncloud-docs.com/docs/en/home" target="_blank">[API Reference]</a>separately to offer more detailed information on how to use the NAVER CLOUD PLATFORM and help maximize the use of the API.**

<a href="https://api.ncloud-docs.com/docs/en/game-gamepot-index" target="_blank">Go to Gamepot API Reference >></a><br />
<a href="https://guide.ncloud-docs.com/docs/en/game-gamepotconsole" target="_blank">Go to Gamepot Manual >></a>

# Server API

## GAMEPOT server &gt; game server

### Purchase Webhook\(required\)

After the payment has been processed, the GAMEPOT server makes an HTTP request to the game server.

> GAMEPOT verifies receipts based on the payment information received from the client, preventing illegal payment attempts.

#### Request

When GAMEPOT makes an HTTP request, the information shown below is forwarded and you can give items to users based upon that information.

> `{domain}` must be provided by the developer and should be added to Project settings > General > Webhook in your GAMEPOT dashboard.

```java
https://{domain}?
userId={uuid}&orderId={orderId}&projectId={projectId}&platform={platform}&productId={productId}&store={store}&payment={payment}&transactionId={transactionId}&gamepotOrderId={gamepotOrderId}&uniqueId={uniqueId}&tp={tp}
```

| Attribute      | Type    | Max Length | Description                                                                 |
| :------------- | :------ | :--------- | :-------------------------------------------------------------------------- |
| userId         | String  | 128        | User ID                                                                     |
| transactionId  | String  | 512        | Order number \(GPA-xxxx-xxxx-\)                                             |
| store          | String  | 64         | Store information \(Apple, Google, One\)                                    |
| projectId      | String  | 128        | Project ID                                                                  |
| productId      | String  | 256        | Product ID registered in Google Play Store, Apple App Store, and ONE Store. |
| platform       | String  | 128        | Platform information \(Android, iOS\)                                       |
| payment        | String  | 64         | Payment type \( Apple, Google, One, Danal, MyCard, Mol ... \)               |
| uniqueId       | String  | 512        | Unique id \(unique id entered when calling purchase api\)                   |
| gamepotOrderId | String  | 512        | GAMEPOT Order ID                                                            |
| serverId       | String  | -          | serverId \(serverId entered when calling purchase api\)                     |
| playerId       | String  | -          | playerId \(playerId entered when calling purchase api\)                     |
| tp             | Integer | -          | 1: 테스트 결제<br />0: 일반 결제                                            |
| etc            | String  | -          | etc \(etc entered when calling purchase api\)                               |

#### Response

Return a response in the following format.

```javascript
{
    "status": 1,
    "message" : ""
}
```

| Attribute | Type   | Description                        |
| :-------- | :----- | :--------------------------------- |
| status    | Int    | Result \(0: Failed, 1: Succeeded\) |
| message   | String | Error message                      |

### Item Webhook\(required\)

After a coupon is used, the GAMEPOT server makes an HTTP request to the game server to provide an item.

#### Request

When GAMEPOT makes an HTTP request, the information shown below is forwarded and you can give items to users based upon that information.

> `{domain}` must be provided by the developer and should be added to Project settings > General > Webhook in your GAMEPOT dashboard.

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
| userData  | String | -          | coupon api 호출 시 두 번째 파라미터에 넣은 값                                                      |
| itemId    | Array  | -          | itemData Array - itemData\(JSON\) {"item_id" : String, "store_item_id" : String, "count" : Number} |

> ex\)
>
> [https://{domain}?itemId=\[{"item_id":"d0781c4e-df52-465b-ab93-0ee16fbf445d","store_item_id":"ttt","count":1}\]&platform=android&projectId=f1df9464-40a8-4a66-8421-196c7c661002&store=google&userId=2d485044-06c2-48c4-a6ed-4ab53dea88bb](https://{domain}?itemId=[{"item_id":"d0781c4e-df52-465b-ab93-0ee16fbf445d","store_item_id":"ttt","count":1}]&platform=android&projectId=f1df9464-40a8-4a66-8421-196c7c661002&store=google&userId=2d485044-06c2-48c4-a6ed-4ab53dea88bb)

#### Response

Return a response in the following format.

```javascript
{
    "status": 1,
    "message" : ""
}
```

| Attribute | Type   | Description                        |
| :-------- | :----- | :--------------------------------- |
| status    | Int    | Result \(0: Failed, 1: Succeeded\) |
| message   | String | Error message                      |

## Game server &gt; GAMEPOT server

### Token Authentication\(optional\)

Using the information provided after login has been completed in your game, you can request the GAMEPOT server to verify the login.

Token authentication is processed in two steps: step 1 is GAMEPOT token authentication and step 2 is social token authentication.

> For step 2, you should add a value in Project settings > Auth key of your GAMEPOT dashboard in advance.

Step 1 GAMEPOT Token Validation occurs when the sync token has been authenticated using a MemberID and the token obtained after login.

Step 2 of the social token authentication requires using a token from a social media account obtained after logging in to Google or Facebook.

If step 2 authentication fails, GAMEPOT blocks the user from logging in the game.

> The feature to block users after authentication fails works only when Project settings > Auth key is turned on in your GAMEPOT dashboard. You can check blocked users in Member > Block of the GAMEPOT dashboard.

**Do not synchronize step 1 authentication!**

This is the process for user log in. Synchronizing will create delays in the network communication thereby causing game play issues. Also, the network connection is physically separated, so the network connection is much more likely to be unstable.

Process the function asynchronously and implement it in a restrictive format.

#### Request

For data integrity, the request should be made in the developer server, rather than to the client.

```text
POST
url : https://gamepot.apigw.ntruss.com/gpapps/v1/loginauth
Header : 'content-type: application/json'
data:
{
    "projectId": {GamePot SDK's projectId},
    "memberId": {GamePot SDK's memberid},
    "token": {GamePot SDK's Token}
}
```

| Attribute | Type   | Max Length | Description             |
| :-------- | :----- | :--------- | :---------------------- |
| projectId | String | 128        | GamePot SDK's projectId |
| memberId  | String | 128        | GamePot SDK's memberid  |
| token     | String | 2048       | GamePot SDK's Token     |

#### Response

If step 1 authentication fails, the status will be set to a value other than 1.

In this case, restrict the user from entering the game.

```javascript
{
    "status": 1,
    "message" : ""
}
```

| Attribute | Type   | Description                                                         |
| :-------- | :----- | :------------------------------------------------------------------ |
| status    | Int    | Result \(1: Succeeded. Refer to Error code below for other cases.\) |
| message   | String | Error message                                                       |

#### Error code

| Code | Description                                                                                                                                                                         |
| :--- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0    | Required data is omitted from the body. Be sure that the projectId, memberId and token are all specified when making a request.                                                     |
| -1   | Token authentication failed. A fake token is used.                                                                                                                                  |
| -2   | MemberId authentication failed. The token’s MemberId does not match the MemberId in the body.                                                                                       |
| -3   | Token expired. There will be a time difference of more than 10 minutes from the time when the SDK login api was successful and the time when the authentication check is requested. |

### ThirdParty Purchase

> It is not a common feature, so contact GAMEPOT before applying it.

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

| Header    | Type   | Required | Description                             |
| :-------- | :----- | :------- | --------------------------------------- |
| x-api-key | String | O        | An authentication key issued by GamePot |

<br/>

| Attribute     | Type   | Max Length | Required | Description                      |
| :------------ | :----- | :--------- | :------- | :------------------------------- |
| projectId     | String | 128        | O        | GamePot SDK's projectId          |
| store         | String | 64         | O        | Store for payment                |
| productId     | String | 256        | O        | ID of the purchased items        |
| transactionId | String | 512        | O        | Unique ID of the payment         |
| memberId      | String | 128        | O        | GamePot SDK's memberid           |
| currency      | String | 64         | X        | Currency of the payment          |
| price         | Number | -          | X        | Amount of payment                |
| paymentId     | String | 64         | X        | Payment Method                   |
| uniqueId      | String | 512        | X        | In-game unique ID of the payment |

#### Response

```javascript
{
    "status": 1,
    "message" : ""
}
```

| Attribute | Type   | Description                                                         |
| :-------- | :----- | :------------------------------------------------------------------ |
| status    | Int    | Result \(1: Succeeded. Refer to Error code below for other cases.\) |
| message   | String | Error message                                                       |

#### Error code

| Code | Description                                                                                                                              |
| :--- | :--------------------------------------------------------------------------------------------------------------------------------------- |
| -1   | Required data is omitted from the body. <br/> Be sure that projectId, transactionId, productId, store, and memberId are all specified. ¬ |
| -2   | The price value is not a number type.<br/> Specify a number type.                                                                        |
| -3   | No projectId.<br/> Check the projectId entered again.                                                                                    |
| -4   | The project does not support the api.<br/> Contact GAMEPOT.                                                                              |
| -5   | The transactionId already exists.                                                                                                        |
| -6   | DB error. Contact GAMEPOT.                                                                                                               |
