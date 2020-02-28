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

使用优惠券/散装物品发送功能时，会发出 HTTP 请求以将物品从 GAMEPOT 服务器发送到游戏服务器。

#### Request

当 HTTP 请求时，信息将按以下方式交付，并根据该信息将商品支付给用户。

> 开发人员完成任务后，应通知`{domain}`条目，该值应添加到 GAMEPOT 仪表板-项目设置-常规-Webhook。

> `GAMEPOT仪表板-游戏-物品`现在具有发送物品时的全部发送功能。
> 如果您使用此功能，则将`target` / `userId`发送给`all`，因此开发人员应将该项目处理给所有用户。

```text
https://{domain}?
userId={userId}&projectId={projectId}&platform={platform}&store={store}&userData={userData}&itemId=[{itemData}, {itemData}, ...]
```

| Attribute | Type   | Description                                                                                                        |
| :-------- | :----- | :----------------------------------------------------------------------------------------------------------------- |
| userId    | String | 用户 UID                                                                                                           |
| projectId | String | ProjectID                                                                                                          |
| platform  | String | 平台 Platform 信息 \(Android, IOS, job\)                                                                           |
| store     | String | 渠道信息\(apple, google, one\)                                                                                     |
| userData  | String | User data                                                                                                          |
| itemID    | Array  | itemData Array<br /><br />- itemData(JSON) <br /> {"item_id" : String, "store_item_id" : String, "count" : Number} |
| target    | String | 用户/全部 \(user, all\)                                                                                            |
| title     | String | 要显示在邮箱中的标题                                                                                               |
| content   | String | 要显示在邮箱中的内容                                                                                               |

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
