---
search:
  keyword: ['gamepot']
---

#### **为提供 NAVER CLOUD PLATFORM 产品的详细使用方法和 API 的多种使用方式，分别提供<a href="https://guide.ncloud-docs.com/docs/zh/home" target="_blank">[说明书]</a>和<a href="https://api.ncloud-docs.com/docs/zh/home" target="_blank">[API 参考指南]</a>以供参考。**

<a href="https://api.ncloud-docs.com/docs/zh/game-gamepot" target="_blank">进入 Gamepot API 参考指南 >></a><br />
<a href="https://guide.ncloud-docs.com/docs/zh/game-gamepotconsole" target="_blank">进入 Gamepot 说明书 >></a>

# 服务器 API

## GAMEPOT 服务器 > 游戏服务器

### Purchase Webhook\(required\)

付款完成后，GAMEPOT 服务器向游戏服务器发送 HTTP 请求以发放道具。

> GAMEPOT 根据从客户端收到的付款信息进行商店发票验证，阻止非法付款尝试。

#### 请求

发送 HTTP 请求时传递的信息内容如下，在此信息的基础上向用户发放道具即可。

开发公司完成操作后须告知> `{domain}`项目，该值需要添加到 GAMEPOT 仪表盘 - 项目设置 - 一般 - Webhook 项目中。

```java
https://{domain}?
userId={uuid}&orderId={orderId}&projectId={projectId}&platform={platform}&productId={productId}&store={store}&payment={payment}&transactionId={transactionId}&gamepotOrderId={gamepotOrderId}&uniqueId={uniqueId}&tp={tp}
```

| 属性           | 类型    | 最大长度 | 描述                                                |
| :------------- | :------ | :------- | :-------------------------------------------------- |
| userId         | 字符串  | 128      | 用户 ID                                             |
| transactionId  | 字符串  | 512      | 订单号\(GPA-xxxx-xxxx-\)                            |
| store          | 字符串  | 64       | 商店信息\(apple、google、one\)                      |
| projectId      | 字符串  | 128      | 项目 ID                                             |
| productId      | 字符串  | 256      | Google/Apple/One Store 中添加的产品 ID              |
| platform       | 字符串  | 128      | 操作平台信息\(android、ios\)                        |
| payment        | 字符串  | 64       | 支付方式\(apple、google、one、danal、mycard、mol…\) |
| uniqueId       | 字符串  | 512      | Unique id \(调用 purchase api 时放入的 unique id\)  |
| gamepotOrderId | 字符串  | 512      | GAMEPOT Order id                                    |
| serverId       | 字符串  | -        | serverId \(调用 purchase api 时放入的 serverId\)    |
| playerId       | 字符串  | -        | playerId \(调用 purchase api 时放入的 playerId\)    |
| tp             | Integer | -        | 1: 테스트 결제<br />0: 일반 결제                    |
| etc            | 字符串  | -        | 其他\(调用 purchase api 时放入的其他\)              |

#### 响应

响应形式如下。

```javascript
{
    "status": 1,
    "message" : ""
}
```

| 属性    | 类型   | 描述                       |
| :------ | :----- | :------------------------- |
| status  | Int    | 结果值\(0：失败，1：成功\) |
| message | 字符串 | 错误内容                   |

### Item Webhook\(required\)

使用优惠券后 GAMEPOT 服务器向游戏服务器发送 HTTP 请求以发放道具。

#### 请求

发送 HTTP 请求时传递的信息内容如下，在此信息的基础上向用户发放道具即可。

开发公司完成操作后须告知> `{domain}`项目，该值需要添加到 GAMEPOT 仪表盘 - 项目设置 - 一般 - Webhook 项目中。

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
|     |   |           | item_id : 게임팟 > 게임 > 게임팟에서 생성한 아이템 항목의 고유아이디 / store_item_id : 아이템을 지급하고자 하는 아이템 아이디 / count : 지급할 아이템 수 |

> 例如\)
>
> https://{domain}?itemId=\[{"item_id":"d0781c4e-df52-465b-ab93-0ee16fbf445d","store_item_id":"ttt","count":1}\]&platform=android&projectId=f1df9464-40a8-4a66-8421-196c7c661002&store=google&userId=2d485044-06c2-48c4-a6ed-4ab53dea88bb

#### 响应

响应形式如下。

```javascript
{
    "status": 1,
    "message" : ""
}
```

| 属性    | 类型   | 描述                       |
| :------ | :----- | :------------------------- |
| status  | Int    | 结果值\(0：失败，1：成功\) |
| message | 字符串 | 错误内容                   |

## 游戏服务器 > GAMEPOT 服务器

### Token Authentication\(optional\)

可以使用在游戏中完成登录后获得的信息在 GAMEPOT 服务器上进行登录验证。

令牌验证分两步进行，完成第一步的 GAMEPOT 令牌验证后进行第二步的社交令牌验证。

> 第二步验证须在 GAMEPOT 仪表盘 - 项目设置 - Auth key 中输入值后进行。

第一步的 GAMEPOT 令牌验证使用登录后获得的 MemberID（用户 ID）、令牌进行同步令牌验证，

第二步的社交令牌验证须使用通过 Google 登录或 Facebook 登录获得的社交账户令牌进行社交异步令牌验证。

第二步验证失败时，GAMEPOT 停用功能启用，之后再登录时将无法登录。

> 验证失败造成的停用仅在 GAMEPOT 仪表盘 - 项目设置 - Auth key 项目的开关已开启时启用，停用对象可在 GAMEPOT 仪表盘 - 会员 - 停用菜单中查看。

**请勿同步处理第一步验证！**

这是用户登录的过程，如果将该功能同步处理，会发生网络通信引起的延迟，成为使用游戏的障碍。而且，相应网络通信已被物理分离，经常会导致网络通信不畅。

请对该功能进行异步处理，以后以限制游戏使用的形式实现功能。

#### 请求

为了确保数据完整性，请在开发公司的服务器而非客户端进行。

```text
POST
url : https://gamepot.apigw.ntruss.com/gpapps/v1/loginauth
Header : 'content-type: application/json'
data:
{
    "projectId": {GamePot SDK的projectId},
    "memberId": {GamePot SDK的memberid（用户ID）},
    "token": {GamePot SDK的令牌}
}
```

| 属性      | 类型   | 最大长度 | 描述                               |
| :-------- | :----- | :------- | :--------------------------------- |
| projectId | 字符串 | 128      | GamePot SDK 的 projectId           |
| memberId  | 字符串 | 128      | GamePot SDK 的 memberid（用户 ID） |
| token     | 字符串 | 2048     | GamePot SDK 的令牌                 |

#### 响应

第一步验证失败时，status 会输入 1 以外的值。

此时请限制进入游戏。

```javascript
{
    "status": 1,
    "message" : ""
}
```

| 属性    | 类型   | 描述                                      |
| :------ | :----- | :---------------------------------------- |
| status  | Int    | 结果值\(1：成功，失败请参考以下错误代码\) |
| message | 字符串 | 错误内容                                  |

#### 错误代码

| 代码 | 描述                                                                                        |
| :--- | :------------------------------------------------------------------------------------------ |
| 0    | 正文中存在遗漏数据的情况，请确认发送 HTTP 请求时 projectId、memberId、令牌是否已全部放入。  |
| -1   | 令牌验证失败，令牌被伪造的情况                                                              |
| -2   | MemberId 验证失败，令牌的 MemberId 信息与正文的 MemberId 不一致的情况                       |
| -3   | 令牌到期，SDK 登录 API 成功的时间与请求相应 Authentication 检查的时间相差 10 分钟以上的情况 |

### ThirdParty Purchase

> 该功能一般不使用，因此应用前请咨询 GAMEPOT。

#### 请求

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

| 头部      | 类型   | 必填 | 描述                   |
| :-------- | :----- | :--- | ---------------------- |
| x-api-key | 字符串 | O    | GamePot 发放的认证密钥 |

<br/>

| 属性          | 类型   | 最大长度 | 必填 | 描述                               |
| :------------ | :----- | :------- | :--- | :--------------------------------- |
| projectId     | 字符串 | 128      | O    | GamePot SDK 的 projectId           |
| store         | 字符串 | 64       | O    | 支付商店                           |
| productId     | 字符串 | 256      | O    | 付款道具 ID                        |
| transactionId | 字符串 | 512      | O    | 付款固有 ID                        |
| memberId      | 字符串 | 128      | O    | GamePot SDK 的 memberid（用户 ID） |
| currency      | 字符串 | 64       | X    | 付款货币                           |
| price         | 数字   | -        | X    | 支付金额                           |
| paymentId     | 字符串 | 64       | X    | 支付方式                           |
| uniqueId      | 字符串 | 512      | X    | 游戏内付款固有 ID                  |

#### 响应

```javascript
{
    "status": 1,
    "message" : ""
}
```

| 属性    | 类型   | 描述                                      |
| :------ | :----- | :---------------------------------------- |
| status  | Int    | 结果值\(1：成功，失败请参考以下错误代码\) |
| message | 字符串 | 错误内容                                  |

#### 错误代码

| 代码 | 描述                                                                                                       |
| :--- | :--------------------------------------------------------------------------------------------------------- |
| -1   | 正文中存在遗漏数据的情况<br/>请确认 projectId、transactionId、productId、store、memberId 是否已全部放入。¬ |
| -2   | price 值并非数字类型的情况<br/>请放入数字类型。                                                            |
| -3   | 没有 projectId 的情况<br/>请重新确认输入的 projectId。                                                     |
| -4   | 项目不支持相应 api 的情况<br/>请咨询 GAMEPOT。                                                             |
| -5   | transactionId 已经存在的情况                                                                               |
| -6   | DB 错误，请咨询 GAMEPOT。                                                                                  |
