---
search:
  keyword: ["gamepot"]
---

# Server API

> ### 这是机器翻译的文档，可能在词汇，语法或语法上有错误。 我们很快会为您提供由专业翻译人员翻译的文档。
>
> #### 如有任何疑问，请[联系我们]（https://www.ncloud.com/support/question）。
>
> 我们将尽一切努力进一步改善我们的服务。

## GAMEPOT Server&gt; Game Server

### Purchase Webhook(required)

付款完成后，会发出 HTTP 请求以将商品从 GAMEPOT 服务器支付到游戏服务器。

> GAMEPOT 通过根据从客户收到的付款信息验证商店收据来防止非法付款尝试。

#### Request

请求 HTTP 时，信息将按以下方式发送，您可以根据该信息向用户付款。

> 开发人员必须在完成工作后通知{domain}项目，并将此值添加到 GAMEPOT 仪表板项目 project-general-webhook 项目中。

```java
https://{domain}?
userId={uuid}&orderId={orderId}&projectId={projectId}&platform={platform}&productId={productId}&store={store}&payment={payment}&transactionId={transactionId}&gamepotOrderId={gamepotOrderId}&uniqueId={uniqueId}
```

| Attribute      | Type   | Max Length | Description                                             |
| :------------- | :----- | :--------- | :------------------------------------------------------ |
| userId         | String | 128        | 用户 ID                                                 |
| transactionId  | String | 512        | 订单号(GPA-xxxx-xxxx-)                                  |
| store          | String | 64         | 储存信息(apple, google, one)                            |
| projectId      | String | 128        | 项目编号                                                |
| productId      | String | 256        | 在 Google / Apple / One Store 中注册的产品 ID           |
| platform       | String | 128        | 操作平台信息 (android, ios)                             |
| payment        | String | 64         | 付款方式 ( apple, google, one, danal, mycard, mol ... ) |
| uniqueId       | String | 512        | Unique id (调用购买 API 时输入的唯一 ID)                |
| gamepotOrderId | String | 512        | GAMEPOT Order id                                        |
| serverId       | String | -          | serverId (调用购买 api 时输入的 serverId)               |
| playerId       | String | -          | playerId (调用购买 api 时输入的 playerId)               |
| etc            | String | -          | etc (调用购买 api 时添加了等)                           |

#### Response

请在下面的表格中回复。

```javascript
{
    "status": 1,
    "message" : ""
}
```

| Attribute | Type   | Description              |
| :-------- | :----- | :----------------------- |
| status    | Int    | 结果（0：失败，1：成功） |
| message   | String | 错误内容                 |

### Item Webhook(required)

使用优惠券后，会发出 HTTP 请求以将商品从 GAMEPOT 服务器支付到游戏服务器。

#### 请求

请求 HTTP 时，信息将按以下方式发送，您可以根据该信息向用户付款。

> 开发人员必须在完成工作后通知{domain}项目，并将此值添加到 GAMEPOT 仪表板项目 project-general-webhook 项目中。

```text
https://{domain}?
userId={userId}&projectId={projectId}&platform={platform}&store={store}&userData={userData}&itemId=[{itemData}, {itemData}, ...]
```

| Attribute | Type   | Max Length | Description                                                                                      |
| :-------- | :----- | :--------- | :----------------------------------------------------------------------------------------------- |
| userId    | String | 128        | 用户 ID                                                                                          |
| projectId | String | 128        | Project ID                                                                                       |
| platform  | String | 128        | 操作平台信息 (Android, IOS)                                                                      |
| store     | String | 64         | 储存信息(apple, google, one)                                                                     |
| title     | String | -          | Gamepot 仪表板>游戏>演示>标题中的值                                                              |
| content   | String | -          | Gamepot 仪表板>游戏>礼物>在描述中输入的值                                                        |
| userData  | String | -          | 调用优惠券 api 时在第二个参数中输入的值                                                          |
| itemId    | Array  | -          | itemData Array - itemData(JSON) {"item_id" : String, "store_item_id" : String, "count" : Number} |

> ex)
>
> [https://{domain}?itemId=\[{"item_id":"d0781c4e-df52-465b-ab93-0ee16fbf445d","store_item_id":"ttt","count":1}\]&platform=android&projectId=f1df9464-40a8-4a66-8421-196c7c661002&store=google&userId=2d485044-06c2-48c4-a6ed-4ab53dea88bb](https://{domain}?itemId=[{"item_id":"d0781c4e-df52-465b-ab93-0ee16fbf445d","store_item_id":"ttt","count":1}]&platform=android&projectId=f1df9464-40a8-4a66-8421-196c7c661002&store=google&userId=2d485044-06c2-48c4-a6ed-4ab53dea88bb)

#### Response

请在下面的表格中回复。

```javascript
{
    "status": 1,
    "message" : ""
}
```

| Attribute | Type   | Description              |
| :-------- | :----- | :----------------------- |
| status    | Int    | 结果（0：失败，1：成功） |
| message   | String | 错误内容                 |

## 游戏服务器> GAMEPOT 服务器

### 令牌认证（可选）

您可以使用在游戏中完成登录后获得的信息来验证对 GAMEPOT 服务器的登录。

令牌验证将分两个阶段进行，在第一次 GAMEPOT 令牌验证之后，将继续进行第二个社交令牌验证。

> 对于两步验证，必须在 GAMEPOT Dashboard-Project Settings-Auth 键中输入一个值。

步骤 1 GAMEPOT 令牌验证是通过验证一个具有 MemberID（用户 ID）和登录后获得的令牌的同步令牌来执行的。

第二阶段社交令牌验证是使用通过 Google 登录或 Facebook 登录获得的社交帐户令牌的社交异步令牌验证。

如果在步骤 2 中验证失败，则会激活 GAMEPOT 使用停止功能，并且无法进行后续登录。

> 由于验证失败而导致的暂停仅在 GAMEPOT 仪表板项目设置-Auth 关键项中的开关为 ON 时有效，并且可以在 GAMEPOT 仪表板成员-暂停菜单中检查暂停的目标。

**请勿同步单步验证！**

当用户登录并且此功能是同步的时，由于网络通信而导致延迟，这使游戏无用。 另外，由于网络通信在物理上是分开的，因此通常不期望网络通信。

异步处理功能后，请以限制游戏使用的方式实施该功能。

#### 请求

为了确保数据完整性，请继续使用开发者的服务器而不是客户端。

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

| Attribute | Type   | Max Length | Description                   |
| :-------- | :----- | :--------- | :---------------------------- |
| projectId | String | 128        | GamePot SDK projectId         |
| memberId  | String | 128        | GamePot SDK memberid(用户 ID) |
| token     | String | 2048       | GamePot SDK Token             |

#### Response

如果在一步验证中验证失败，则输入非 1 的值。

在这种情况下，请限制游戏的进入。

```javascript
{
    "status": 1,
    "message" : ""
}
```

| Attribute | Type   | Description                                       |
| :-------- | :----- | :------------------------------------------------ |
| status    | Int    | 结果值（1：关于成功和失败，请参见下面的错误代码） |
| message   | String | 错误内容                                          |

#### Error code

| Code | Description                                                                          |
| :--- | :----------------------------------------------------------------------------------- |
| 0    | 如果正文中缺少数据，请确保在请求 HTTP 时包括所有 projectId，memberId 和令牌。        |
| -1   | 令牌验证失败令牌被篡改                                                               |
| -2   | 如果令牌的 MemberId 信息与正文的 MemberId                                            | 不匹配，则 MemberId 验证失败。 |
| -3   | 当令牌到期 SDK 登录 api 成功执行时，以及请求相应身份验证检查的时间，相差超过 10 分钟 |

### ThirdParty Purchase

> 通常不使用此功能，因此请在申请前联系 GAMEPOT。

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

| Header    | Type   | Required | Description            |
| :-------- | :----- | :------- | ---------------------- |
| x-api-key | String | O        | GamePot 发行的验证密钥 |

<br/>

| Attribute     | Type   | Max Length | Required | Description                |
| :------------ | :----- | :--------- | :------- | :------------------------- |
| projectId     | String | 128        | O        | GamePot SDK 中的 ProjectId |
| store         | String | 64         | O        | 付款商店                   |
| productId     | String | 256        | O        | 付款项目编号               |
| transactionId | String | 512        | O        | 付款编号                   |
| memberId      | String | 128        | O        | GamePot SDK 的会员 ID)     |
| currency      | String | 64         | X        | 付款货币                   |
| price         | Number | -          | X        | 付款金额                   |
| paymentId     | String | 64         | X        | 付款方式                   |
| uniqueId      | String | 512        | X        | 游戏内付款 ID              |

#### Response

```javascript
{
    "status": 1,
    "message" : ""
}
```

| Attribute | Type   | Description                                       |
| :-------- | :----- | :------------------------------------------------ |
| status    | Int    | 结果值（1：关于成功和失败，请参见下面的错误代码） |
| message   | String | 错误内容                                          |

#### Error code

| Code | Description                                                                                  |
| :--- | :------------------------------------------------------------------------------------------- |
| -1   | 如果正文中缺少数据，请确保包含<br/> projectId，transactionId，productId，store 和 memberId。 |
| -2   | 如果价格值不是数字类型，则将其放在<br/>数字类型中。                                          |
| -3   | 如果没有 projectId，请再次检查输入的 projectId。                                             |
| -4   | 如果项目不支持 api，请与<br/> GAMEPOT 联系。                                                 |
| -5   | transactionId 已经存在                                                                       |
| -6   | DB 错误。 请与 GAMEPOT 联系。                                                                |
