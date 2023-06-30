下面将介绍为发放道具、登录验证，设置服务器向服务器发送请求的方法。

## 请求发放付费道具 <a name="결제아이템지급요청"></a>

可以设置为通过Webhook发送HTTP请求来发放付费或使用优惠券的道具。

为发放道具，设置通过Webhook发送HTTP请求的方法如下。

1. 使用管理员账户登录仪表盘。
2. 依次点击 **项目设置 > 一般** 菜单。
3. 请参考以下指南，在 **Webhook** 区域的 **付费道具（服务）** 或 **优惠券道具（服务）** 输入栏输入HTTP/HTTPS URL。
   * 支付后发放道具的情况，请参考[支付后的请求及响应](#결제후요청및응답)。
   * 使用优惠券发放道具，请参考[使用优惠券后的请求及响应](#쿠폰사용후요청및응답)。
   * 发放道具给测试用户时，请在显示 **（测试用户）** 标识的输入栏输入请求。
4. 点击 **[修改]** 按钮。

### 支付后的请求及响应 <a name="결제후요청및응답"></a>

请参考以下表和代码设置HTTP请求及响应。

* **请求**
  
  ```java
  https://{domain}?
  userId={uuid}&orderId={orderId}&projectId={projectId}&platform={platform}&productId={productId}&store={store}&payment={payment}&transactionId={transactionId}&gamepotOrderId={gamepotOrderId}&uniqueId={uniqueId}&tp={tp}
  ```
  
  | 属性| 类型| 最大长度| 说明
  |----------|----------|----------|----------
  | `userId`| `String`| 128| 用户ID
  | `transactionId`| `String`| 512| 订购编号(GPA-xxxx-xxxx-)
  | `store`| `String`| 64| 商店信息（`apple`、`google`、`one`）
  | `projectId`| `String`| 128| 项目ID
  | `productId`| `String`| 256| Google/Apple/One Store中注册的产品ID
  | `platform`| `String`| 128| 运营Platform信息（`android`、`ios`）
  | `payment`| `String`| 64| 支付方式
  | `uniqueId`| `String`| 512| Unique id（调用purchase api 时输入的 `uniqueId` ）
  | `gamepotOrderId`| `String`| 512| GAMEPOT Order ID
  | `serverId`| `String`| -| serverId（调用purchase api时输入的`serverId` ）
  | `playerId`| `String`| -| playerId（调用purchase api时输入的`playerId` ）
  | `tp`| `Integer`| -| 1：测试付款<br/>0：常规付款
  | `etc`| `String`| -| etcd（调用purchase api时输入的`etc`）



<br/>

* **响应**
  ```Java
  {
      "status": 1,
      "message" : ""
  }
  ```
  
  | 属性| 类型| 说明
  |----------|----------|----------
  | `status`| `Integer`| 结果值<br/>`0`：失败，`1`：成功
  | `message`| `String`| 错误内容



### 赠送礼物与使用优惠券后的请求及响应<a name="쿠폰사용후요청및응답"></a>

请参考以下表和代码设置HTTP请求及响应。

* **请求**
  
  ```text
  https://{domain}?
  userId={userId}&projectId={projectId}&platform={platform}&store={store}&userData={userData}&itemId=[{itemData}, {itemData}, ...]
  ```
  
  | 属性| 类型| 最大长度| 说明
  |----------|----------|----------|----------
  | `userId`| `String`| 128| 用户ID（仪表盘中的 **游戏 > 赠送礼物 > 对象** 值为全部时`all`）
  | `projectId`| `String`| 128| 项目ID
  | `platform`| `String`| 128| 运营Platform信息（`android`、`ios`）
  | `store`| `String`| 64| 商店信息（`apple`、`google`、`one`）
  | `title`| `String`| -| 在 **仪表盘 > 游戏 > 赠送礼物 > 标题** 中输入的值
  | `content`| `String`| -| 在 **仪表盘 > 游戏 > 赠送礼物 > 说明** 中输入的值
  | `target`| `String`| -| GAMEPOT仪表盘 > 游戏 > 赠送礼物 > 对象值 - 全部：all / 用户ID：user
  | `expireMs`| `String`| -| 在 **仪表盘 > 游戏 > 赠送礼物 > 有效期** 中输入的Timestamp(GMT+9)
  | `userData`| `String`| -| 调取客户端SDK优惠券API时输入的第二个参数值或在 **仪表盘 > 游戏 > 赠送礼物 > UserData** 中输入的值
  | `itemId`| `Array`| -| itemData Array - `itemData(JSON) {"item_id" : String, "store_item_id" : String, "count" : Number}`<br/><br/>`item_id`：在仪表盘 **游戏 > 道具**中创建的道具项目的固有ID<br/>`store_item_id`：要发放的道具ID<br/>`count`：要发放的道具数量


* **响应**
  
  ```Java
  {
      "status": 1,
      "message" : ""
  }
  ```
  
  | 属性| 类型| 说明
  |----------|----------|----------
  | `status`| `Integer`| 结果值<br/>`0`：失败，`1`：成功
  | `message`| `String`| 错误内容



## 登录验证请求（可选）<a name="로그인검증요청"></a>

可以使用会员完成登录时获得的信息向GAMEPOT服务器请求登录验证。

登录验证将按第一步验证GAMEPOT Token、第二步验证社交媒体账户的顺序进行。如果第二步的验证流程失败，会启动停止使用GAMEPOT功能，相应账户将停止使用。

::: (Warning) (注意)

请不要同步处理第一步的GAMEPOT Token验证功能。如果同步处理第一步的Token验证功能，网络通信不流畅的可能性很高，而且会员可能因此不能正常使用游戏。因此，请将第一步的Token验证处理为非同步后，确保在后续流程停止使用功能生效。

:::

1. 使用管理员账户登录仪表盘。
2. 依次点击 **项目设置 > 一般** 菜单后，在 **Auth Key** 区域输入从各个开发控制台获取的ID和密钥值。
   * 如果不使用第二步骤的验证流程以及使用停止功能时，请忽略该流程。
3. 请参考以下请求、响应及错误代码进行请求登录验证。

### 请求、响应及错误代码<a name="요청응답및오류코드"></a>

请参考以下表和代码设置登录验证请求、响应及错误代码。

* **请求**
  
  ```text
  POST
  url : https://gamepot.apigw.ntruss.com/gpapps/v1/loginauth
  Header : 'content-type: application/json'
  data:
  {
      "projectId"：{GamePot SDK的projectId}，
      "memberId"：{GamePot SDK的memberid（用户ID）}，
      "token"：{GamePot SDK的Token},
      "remoteip": {로그인한 계정의 아이피 정보},
      "platform": ""
  }
  ```
  
  | 属性| 类型| 最大长度| 说明
  |----------|----------|----------|----------
  | `projectId`| `String`| 128| GAMEPOT SDK的项目ID
  | `memberId`| `String`| 128| GAMEPOT SDK的用户ID
  | `token`| `String`| 2048| GAMEPOT SDK的Token
  | `remoteip`| `String`| -| 로그인한 계정의 아이피 정보 ( ex) XXX.XXX.XXX.XXX )
  | `platform`| `String`| -| pc 플랫폼 사용하는 경우에만 pc로 설정


<br/>

* **响应**
  
  ```java
  {
      "status": 1,
      "message" : ""
  }
  ```
  
  | 属性| 类型| 说明
  |----------|----------|----------
  | `status`| `Integer`| 结果值<br/>`1`：成功<br/>失败请参考以下错误代码
  | `message`| `String`| 错误内容



<br/>

* **错误代码**
  
  | 代码| 说明
  |----------|----------
  | `0`| body存在遗漏数据时<br/>发送HTTP请求时，确认是否完成输入`projectId`、`memberId`、`token`
  | `-1`| Token验证失败<br/>Token被伪造时
  | `-2`| MemberId验证失败<br/>Token的用户ID信息与正文的用户ID不一致时
  | `-3`| Token到期<br/> SDK login api的成功登录时间与请求相应Authentication check的时间之间相差60分钟以上时



## 外部支付 <a name="외부결제"></a>

为关联外部支付，可设置服务器之间的请求。

使用相应功能前，请务必向NAVER Cloud Platform咨询详细的使用方法。

* [咨询](https://www.ncloud.com/support/question){target="_blank"}

### 请求、响应及错误代码<a name="요청응답및오류코드2"></a>

* **请求**
  
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
  
  | 报头| 类型| 是否必填| 说明
  |----------|----------|----------|----------
  | `x-api-key`| `String`| 必填| GAMEPOT发放的认证密钥

  | 属性| 类型| 最大长度| 说明
  |----------|----------|----------|----------
  | `projectId`| `String`| 128| GAMEPOT SDK的项目ID
  | `store`| `String`| 64| 支付商店
  | `productId`| `String`| 256| 支付的道具ID
  | `transactionId`| `String`| 512| 支付固有ID
  | `memberId`| `String`| 128| GAMEPOT SDK的用户ID
  | `currency`| `String`| 64| 付款货币
  | `price`| `Number`| -| 支付金额
  | `paymentId`| `String`| 64| 支付方式
  | `uniqueId`| `String`| 512| 游戏内支付固有ID



<br/>

* **响应**
  
  ```java
  {
      "status": 1,
      "message" : ""
  }
  ```
  
  属性 | 类型 |	概述 
  --- | --- | --- 
  `status` |	`Integer` |	 结果值<br/>`1`：成功<br/>失败请参考以下错误代码 
  `message`	| `String` | 出错内容<br/>

* **错误代码** 

代码	| 概述 
--- |  --- 
`-1`	|  body存在遗漏数据时<br/>发送HTTP请求时，确认是否完成输入 `projectId`、`transactionId`、`productId`、`store`、`memberId` 
`-2` | `price` 的值不是 `number` 类型时  
`-3` |  没有 `projectId` 时 
`-4` |  项目不支持该API时<br/>咨询GAMEPOT 
`-5` | 已存在 `transactionId` 时 
`-6` | DB错误。<br/>咨询GAMEPOT
