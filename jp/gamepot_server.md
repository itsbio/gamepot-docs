## Server API<a name="ServerAPI"></a>

## GAMEPOT サーバ > ゲームサーバ<a name="GAMEPOTサーバ>ゲームサーバ"></a>



```java
セキュリティのためにWebhookアドレスにファイアウォールを適用すると安全です
ファイアウォール及び正常なリクエストの検証がない場合は、
異常リクエストによるアイテム支給などが行われることがあります。
ファイアウォールはホワイトリストに基づいて作成することをお勧めします。
その場合はGAMEPOT IPの許可が必要となります。
49.236.143.202
49.236.143.198
106.10.53.19
106.10.52.84

また、スプーフィング攻撃にも安全なセキュリティを希望する場合は、
「etc」アトリビュートによる正常なリクエストの検証を行ってください。
```

### Purchase Webhook（required）<a name="PurchaseWebhookrequired"></a>


決済が完了すると、GAMEPOT サーバからゲームサーバにアイテム支給のための HTTP リクエストを行います。

<Blockquote>
GAMEPOT は、ユーザーから伝達された決済情報をもとにストア領収証の検証まで行って不正決済を防いでいます 。
</Blockquote>


#### Request<a name="Request1"></a>


HTTP リクエストの際に以下のような内容の情報を伝えます。その情報をもとにユーザーにアイテムを支給してください。


>`{domain}`項目は開発会社で操作を完了してから知らせてください。この値は GAMEPOT ダッシュボード - プロジェクトの設定 - 一般 - Webhook 項目に追加する必要があります。


```java
https://{domain}?
userId={uuid}&orderId={orderId}&projectId={projectId}&platform={platform}&productId={productId}&store={store}&payment={payment}&transactionId={transactionId}&gamepotOrderId={gamepotOrderId}&uniqueId={uniqueId}&tp={tp}
```

|Attribute      |Type    |Max Length |Description                                               |
| :------------- | :------ | :--------- | :-------------------------------------------------------- |
|userId         |String  |128        |ユーザー ID|
|transactionId  |String  |512        |注文番号（GPA-xxxx-xxxx-）|
|store          |String  |64         |ストア情報（Apple、Google、ONE）|
|projectId      |String  |128        |プロジェクト ID|
|productId      |String  |256        |Google/Apple/ONE Store に登録された商品 ID|
|platform       |String  |128        |運用プラットフォーム情報（Android、iOS）|
|payment        |String  |64         |決済方法 （ Apple、Google、ONE、Danal、MyCard、mol...）|
|uniqueId       |String  |512        |Unique id （purchase api 呼び出しの際に入れた unique id）|
|gamepotOrderId |String  |512        |GAMEPOT Order id                                          |
|serverId       |String  |-          |serverId （purchase api 呼び出しの際に入れた serverId）|
|playerId       |String  |-          |playerId （purchase api 呼び出しの際に入れた playerId）|
|tp             |Integer |-          |1：テスト決済<br />0：一般決済|
|etc            |String  |-          |etc （purchase api 呼び出しの際に入れた etc）|

#### Response<a name="Response1"></a>


レスポンスは以下のような形式で行ってください。

```javascript
{
    "status": 1,
    "message" : ""
}
```

|Attribute |Type   |Description                  |
| :-------- | :----- | :--------------------------- |
|status    |Int    |結果値（ 0：失敗、1：成功 ）|
|message   |String |エラー内容|

### Item Webhook（required）<a name="ItemWebhookrequired"></a>


クーポンを使用すると、GAMEPOT サーバからゲームサーバにアイテム支給のための HTTP リクエストを行います。

#### Request<a name="Request2"></a>


HTTP リクエストの際に以下のような内容の情報を伝えます。その情報をもとにユーザーにアイテムを支給してください。


 >`{domain}`項目は開発会社で操作を完了してから知らせてください。この値は GAMEPOT ダッシュボード - プロジェクトの設定 - 一般 - Webhook 項目に追加する必要があります。


```text
https://{domain}?
userId={userId}&projectId={projectId}&platform={platform}&store={store}&userData={userData}&itemId=[{itemData}, {itemData}, ...]
```

|Attribute |Type   |Max Length |Description                                                                                        |
| :-------- | :----- | :--------- | :------------------------------------------------------------------------------------------------- |
|userId    |String |128        |ユーザーID（GAMEPOTダッシュボード > ゲーム > プレゼントする > 対象値が全体の場合、all）|
|projectId |String |128        |Project ID                                                                                 |
|platform  |String |128        |運用プラットフォーム情報（Android、iOS）|
|store     |String |64         |ストア情報（Apple、Google、ONE）|
|title     |String |-          |GAMEPOTダッシュボード > ゲーム > プレゼントする > 件名に入力した値|
|content   |String |-          |GAMEPOTダッシュボード > ゲーム > プレゼントする > 説明に入力した値|
|target    |String |-          |GAMEPOTダッシュボード > ゲーム > プレゼントする > 対象値 - 全体：all / ユーザーID：user |
|userData  |String |-          |Coupon API呼び出しの際に、二番目のパラメータに入力した値|
|itemId    |Array  |-          |itemData Array - itemData（JSON） {"item_id" : String, "store_item_id" : String, "count" : Number} |


 ex）

https://{domain}?itemId=\[{"item_id":"d0781c4e-df52-465b-ab93-0ee16fbf445d","store_item_id":"ttt","count":1}\]&platform=android&projectId=f1df9464-40a8-4a66-8421-196c7c661002&store=google&userId=2d485044-06c2-48c4-a6ed-4ab53dea88bb


#### Response<a name="Response2"></a>


レスポンスは以下のような形式で行ってください。

```javascript
{
    "status": 1,
    "message" : ""
}
```

|Attribute |Type   |Description                  |
| :-------- | :----- | :--------------------------- |
|status    |Int    |結果値（ 0：失敗、1：成功 ）|
|message   |String |エラー内容|

## ゲームサーバ > GAMEPOT サーバ<a name="ゲームサーバ>GAMEPOTサーバ"></a>


### Token Authentication（optional）<a name="TokenAuthenticationoptional"></a>


ゲームログイン完了後に取得した情報を用いて、GAMEPOT サーバでログイン検証ができます。

トークン検証は 2 段階で行われ、第 1 段階の GAMEPOT トークン検証の後、第 2 段階のソーシャルトークン検証が行われます。


>第 2 段階の検証では GAMEPOT ダッシュボード - プロジェクトの設定 - Auth key に値を入力する必要があります。


第 1 段階の GAMEPOT トークン検証では、ログイン後に取得した MemberID(ユーザー ID)、Token で同期トークン検証を行い、

第 2 段階のソーシャルトークン検証では、Google ログインや Facebook ログイン時に取得したソーシャルアカウントのトークンでソーシャル非同期トークン検証を行います。

第 2 段階で検証に失敗した場合は GAMEPOT の利用停止機能が作動し、その後再ログインはできません。


>検証失敗による利用停止は、GAMEPOT ダッシュボード - プロジェクトの設定 - Auth key 項目でスイッチが ON になっている場合にのみ作動し、利用停止対象者は GAMEPOT ダッシュボード - 会員 - 利用停止メニューで確認できます。


**第 1 段階の検証を同期処理しないでください!**

ユーザーがログインするプロセスですが、この機能を同期処理するとネットワーク通信による遅延が発生してゲーム利用の妨げになります。また、当該ネットワーク通信が物理的に分離されている状況なので、それによってネットワーク通信が不安定になる場合が多々あります。

この機能は非同期処理し、その後にゲーム利用を制限する形で機能を実装してください。

#### Request<a name="Request3"></a>


データ完全性のために、ゲームクライアントではなく開発会社のサーバで行ってください。

```text
POST
url : https://gamepot.apigw.ntruss.com/gpapps/v1/loginauth
Header : 'content-type: application/json'
data:
{
    「projectId」：{GamePot SDKのprojectId}、
    「memberId」：{GamePot SDKのmemberid(メンバーID)}、
    「token」：{GamePot SDKのToken}
}
```

|Attribute |Type   |Max Length |Description                          |
| :-------- | :----- | :--------- | :----------------------------------- |
|projectId |String |128        |GamePot SDK の projectId|
|memberId  |String |128        |GamePot SDK の memberid(メンバー ID)|
|token     |String |2048       |GamePot SDK の Token|

#### Response<a name="Response3"></a>


第 1 段階検証で検証に失敗した場合、status に 1 ではない値が入力されます。

この場合はゲーム入場を制限してください。

```javascript
{
    "status": 1,
    "message" : ""
}
```

|Attribute |Type   |Description                                     |
| :-------- | :----- | :---------------------------------------------- |
|status    |Int    |結果値（1：成功、失敗は以下の Error code 参照）|
|message   |String |エラー内容|

#### Error code<a name="Errorcode1"></a>

|Code |Description                                                                                                             |
| :--- | :---------------------------------------------------------------------------------------------------------------------- |
|0    |Body に漏れデータがある場合、HTTP リクエストの際に projectId、memberId、token をすべて入力したか確認してください。|
|-1   |Token 検証失敗 Token が捏造された場合|
|-2   |MemberId 検証失敗 Token の MemberId 情報と body の MemberId が一致しない場合|
|-3   |Token 満了 SDK login api が成功した時刻とその Authentication check をリクエストした時刻の間に 10 分以上の差が生じた場合|

### ThirdParty Purchase<a name="ThirdPartyPurchase"></a>



 >この機能は一般的には使用されない機能なので、適用前に GAMEPOT までお問い合わせください。


#### Request<a name="Request4"></a>


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

|Header    |Type   |Required |Description                |
| :-------- | :----- | :------- | -------------------------- |
|x-api-key |String |O        |GamePot で発行する認証キー|

<br/>

|Attribute     |Type   |Max Length |Required |Description                          |
| :------------ | :----- | :--------- | :------- | :----------------------------------- |
|projectId     |String |128        |O        |GamePot SDK の projectId|
|store         |String |64         |O        |決済ストア|
|productId     |String |256        |O        |決済アイテム ID|
|transactionId |String |512        |O        |決済固有 ID|
|memberId      |String |128        |O        |GamePot SDK の memberid(メンバー ID)|
|currency      |String |64         |X        |決済通貨|
|price         |Number |-          |X        |決済金額|
|paymentId     |String |64         |X        |決済方法|
|uniqueId      |String |512        |X        |ゲーム内決済の固有 ID|

#### Response<a name="Response4"></a>


```javascript
{
    "status": 1,
    "message" : ""
}
```

|Attribute |Type   |Description                                     |
| :-------- | :----- | :---------------------------------------------- |
|status    |Int    |結果値（1：成功、失敗は以下の Error code 参照）|
|message   |String |エラー内容|

#### Error code<a name="Errorcode2"></a>


|Code |Description                                                                                                                  |
| :--- | :--------------------------------------------------------------------------------------------------------------------------- |
|-1   |Body に漏れデータがある場合、<br/>projectId、transactionId、productId、store、memberId をすべて入力したか確認してください。¬ |
|-2   |price 値が number タイプではない場合、<br/>number タイプで入力してください。|
|-3   |projectId がない場合、<br/>入力した projectId をもう一度確認してください。|
|-4   |プロジェクトが当該 api に対応していない場合、<br/>GAMEPOT までお問い合わせください。|
|-5   |transactionId が既に存在している場合|
|-6   |DB エラー。GAMEPOT までお問い合わせください。|
