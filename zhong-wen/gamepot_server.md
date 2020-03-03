---
search:
  keyword:
    - gamepot
---

# Server API

## GAMEPOT Server&gt; Game Server

### Purchase\(required\)

支付完成后服务器会对游戏服务器请求发放物品。游戏服务会按照以下形式传达，依照此信息发放用户相关物品即可。

#### Request

```text
https://{domain}?
userId={uuid}&orderId={orderId}&projectId={projectId}&platform={platform}&productId={productId}&store={store}&payment={payment}&transactionId={transactionId}&gamepotOrderId={gamepotOrderId}&uniqueId={uniqueId}
```

| Attribute      | Type   | Description                                                                          |
| :------------- | :----- | :----------------------------------------------------------------------------------- |
| userId         | String | 用户 UID                                                                             |
| transactionId  | String | transaction id of Google/Apple/Onestore \(ex. Google is “GPA.0000-0000-0000-00000”\) |
| store          | String | 渠道信息\(apple, google, one\)                                                       |
| projectId      | String | ProjectID                                                                            |
| productId      | String | Google/Apple/Onestore 的商品 ID                                                      |
| platform       | String | 平台 Platform 信息 \(android, ios\)                                                  |
| payment        | String | 储值方式 \(apple, google, one, mycard, mol\)                                         |
| uniqueId       | String | Unique ID（称为 purchase API 时的 unique id）                                        |
| gamepotOrderId | String | GAMEPOT Order id                                                                     |

#### Response

```javascript
{
  "status": 1,
  "message": ""
}
```

| Attribute | Type   | Description                   |
| :-------- | :----- | :---------------------------- |
| status    | Int    | 结果值 \( 0: 失败, 1: 成功 \) |
| message   | String | 错误内容                      |

### Item\(required\)

使用优惠卷时会对游戏服务器请求发放物品 会依照以下形式来请求，游戏服务器就依照传达过来的内容发放给玩家相关物品即可。

#### Request

```text
https://{domain}?
userId={userId}&projectId={projectId}&platform={platform}&store={store}&userData={userData}&itemId=[{itemData}, {itemData}, ...]
```

| Attribute | Type   | Description                                                                                        |
| :-------- | :----- | :------------------------------------------------------------------------------------------------- |
| userId    | String | 用户 UID                                                                                           |
| projectId | String | ProjectID                                                                                          |
| platform  | String | 平台 Platform 信息 \(Android, IOS\)                                                                |
| store     | String | 渠道信息\(apple, google, one\)                                                                     |
| userData  | String | User data                                                                                          |
| itemID    | Array  | itemData Array - itemData\(JSON\) {"item_id" : String, "store_item_id" : String, "count" : Number} |

ex\) [https://{domain}?itemId=\[{"item_id":"d892ee43-d516-43c2-b16f-3ca5672e8166","store_item_id":"000","count":1},{"item_id":"989caae1-5f70-41d9-b797-2e27cc838cb0","store_item_id":"rrr","count":2}\]&platform=android&projectId=f1df9464-40a8-4a66-8421-196c7c661002&store=google&userData=abcdefg&userId=25dcea66-0719-4d18-8dcd-9b7f638f85e4](https://{domain}?itemId=[{"item_id":"d892ee43-d516-43c2-b16f-3ca5672e8166","store_item_id":"000","count":1},{"item_id":"989caae1-5f70-41d9-b797-2e27cc838cb0","store_item_id":"rrr","count":2}]&platform=android&projectId=f1df9464-40a8-4a66-8421-196c7c661002&store=google&userData=abcdefg&userId=25dcea66-0719-4d18-8dcd-9b7f638f85e4)

#### Response

```javascript
{
  "status": 1,
  "message": ""
}
```

| Attribute | Type   | Description                   |
| :-------- | :----- | :---------------------------- |
| status    | Int    | 结果值 \( 0: 失败, 1: 成功 \) |
| message   | String | 错误内容                      |

## Game Server &gt; GAMEPOT Server

### Authentication check\(optional\)

请求验证用户 ID

请求验证时，GamePot 服务器会实际的进行验证，按照验证结果会执行用户 Block。

**不同步！**

當用戶登錄時，如果此功能已同步，則由於網絡通信而導致延遲，因此將使用遊戲。 同樣，由於網絡通信在物理上是分開的，因此通常不希望得到最終的網絡通信。

請異步處理此功能，然後以限制遊戲使用的形式實現該功能。

#### Request

```text
POST
url : https://gamepot.apigw.ntruss.com/gpapps/v1/loginauth
Header : 'content-type: application/json'
data:
{
    "projectId": {GamePot SDK的projectId},
    "memberId": {GamePot SDK的memberId},
    "token": {GamePot SDK的Token}
}
```

| Attribute | Type   | Description              |
| :-------- | :----- | :----------------------- |
| projectId | String | GamePot SDK 的 projectId |
| memberId  | String | GamePot SDK 的 memberId  |
| token     | String | GamePot SDK 的 Token     |

#### Response

```javascript
{
  "status": 1,
  "message": ""
}
```

| Attribute | Type   | Description                                                                   |
| :-------- | :----- | :---------------------------------------------------------------------------- |
| status    | Int    | 结果值 \(1: 成功, 请参阅下面的错误代码以了解错误。\) 如果不是 1，请限制登录。 |
| message   | String | 错误内容                                                                      |

#### 错误代码

| Code | Description                                                    |
| :--- | :------------------------------------------------------------- |
| 0    | 缺少数据 确保包含 projectId，memberId 和 token。               |
| -1   | 令牌验证失败 令牌已被篡改。                                    |
| -2   | MemberId 验证失败 如果令牌的 MemberId 与正文的 MemberId 不匹配 |
| -3   | 过期令牌 SDK 登录 api 通话时间和认证检查请求时间差超过 10 分钟 |

### ThirdParty Purchase

> 此功能不常用，请在申请前联系 GAMEPOT。

#### Request

```text
POST
url : https://gamepot.apigw.ntruss.com/gpapps/v1/v1/thirdparty/purchase
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

| Header    | Type   | Required | Description            |
| :-------- | :----- | :------- | :--------------------- |
| x-api-key | String | O        | GamePot 颁发的授权密钥 |

<br/>

| Attribute     | Type   | Required | Description                |
| :------------ | :----- | :------- | :------------------------- |
| projectId     | String | O        | GamePot SDK 中的 ProjectId |
| store         | String | O        | 付款商店                   |
| productId     | String | O        | 付款项目编号               |
| transactionId | String | O        | 帐单唯一编号               |
| memberId      | String | O        | GamePot SDK 的 MemberId    |
| currency      | String | X        | 帐单币种                   |
| price         | Number | X        | 付款金额                   |
| paymentId     | String | X        | 付款方式                   |
| uniqueId      | String | X        | 游戏内付款唯一 ID          |

#### Response

```javascript
{
    "status": 1,
    "message" : ""
}
```

| Attribute | Type   | Description                           |
| :-------- | :----- | :------------------------------------ |
| status    | Int    | 结果值\(1：以下成功和失败的错误代码\) |
| message   | String | 错误内容                              |

#### Error code

| Code | Description                                                                                     |
| :--- | :---------------------------------------------------------------------------------------------- |
| -1   | 如果正文中缺少数据，请确保已输入<br/> projectId，transactionId，productId，store 和 memberId。  |
| -2   | 如果价格值不是数字类型，则将其输入为<br/>数字。                                                 |
| -3   | 如果您没有 projectId <br/>，请仔细检查您输入的 projectId。                                      |
| -4   | 如果您的项目不支持此 API，请与 GAMEPOT 联系。                                                   |
| -5   | transactionId 已经存在                                                                          |
| -6   | DB 错误。 请与 GAMEPOT 联系。                                                                   |
