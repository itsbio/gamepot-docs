---
search:
  keyword: ['gamepot']
---


#### **NAVERクラウドプラットフォーム商品の使用方法をより詳細に提供し、様々なAPIの活用をサポートするために<a href="http://docs.ncloud.com/ko/" target="_blank">[説明書]</a>と<a href="https://apidocs.ncloud.com/ko/" target="_blank">[APIリファレンス]</a>を分けて提供しています。**

<a href="https://apidocs.ncloud.com/ko/game/gamepot/" target="_blank">GAMEPOT APIリファレンスへ >></a><br />
<a href="https://docs.ncloud.com/ko/game/gamepot_console.html" target="_blank">GAMEPOT説明書へ >></a>


# Server API

## GAMEPOTサーバ &gt; ゲームサーバ

### Purchase Webhook\(required\)

決済が完了すると、GAMEPOTサーバからゲームサーバにアイテム支給のためのHTTPリクエストを行います。

> GAMEPOTは、ユーザーから伝達された決済情報をもとにストア領収証の検証まで行って不正決済を防いでいます。

#### Request

HTTPリクエストの際に以下のような内容の情報を伝えます。その情報をもとにユーザーにアイテムを支給してください。

> `{domain}`項目は開発会社で操作を完了してから知らせてください。この値はGAMEPOTダッシュボード - プロジェクトの設定 - 一般 - Webhook項目に追加する必要があります。

```java
https://{domain}?
userId={uuid}&orderId={orderId}&projectId={projectId}&platform={platform}&productId={productId}&store={store}&payment={payment}&transactionId={transactionId}&gamepotOrderId={gamepotOrderId}&uniqueId={uniqueId}
```

| Attribute| Type| Max Length| Description|
| :------------- | :----- | :--------- | :--------------------------------------------------------|
| userId| String| 128| ユーザーID|
| transactionId| String| 512| 注文番号\(GPA-xxxx-xxxx-\)|
| store| String| 64| ストア情報\(apple、google、one\)|
| projectId| String| 128| プロジェクトID|
| productId| String| 256| Google/Apple/ONE Storeに登録された商品ID|
| platform| String| 128| 運用プラットフォーム情報\(android、ios\)|
| payment| String| 64| 決済方法 \( apple、google、one、danal、mycard、mol...\) |
| uniqueId| String| 512| Unique id \(purchase api呼び出しの際に入れたunique id\)|
| gamepotOrderId| String| 512| GAMEPOT Order id|
| serverId| String| -| serverId \(purchase api呼び出しの際に入れたserverId\)|
| playerId| String| -| playerId \(purchase api呼び出しの際に入れたplayerId\)|
| etc| String| -| etc \(purchase api呼び出しの際に入れたetc\)|

#### Response

レスポンスは以下のような形式で行ってください。

```javascript
{
    "status": 1,
    "message" : ""
}
```

| Attribute| Type| Description|
| :-------- | :----- | :---------------------------- |
| status| Int| 結果値\( 0：失敗、1：成功 \)|
| message| String| エラー内容|

### Item Webhook\(required\)

クーポンを使用すると、GAMEPOTサーバからゲームサーバにアイテム支給のためのHTTPリクエストを行います。

#### Request

HTTPリクエストの際に以下のような内容の情報を伝えます。その情報をもとにユーザーにアイテムを支給してください。

> `{domain}`項目は開発会社で操作を完了してから知らせてください。この値はGAMEPOTダッシュボード - プロジェクトの設定 - 一般 - Webhook項目に追加する必要があります。

```text
https://{domain}?
userId={userId}&projectId={projectId}&platform={platform}&store={store}&userData={userData}&itemId=[{itemData}, {itemData}, ...]
```

| Attribute| Type| Max Length| Description|
| :-------- | :----- | :--------- | :------------------------------------------------------------------------------------------------- |
| userId| String| 128| ユーザーID|
| projectId| String| 128| Project ID|
| platform| String| 128| 運用プラットフォーム情報 \(Android、IOS\)|
| store| String| 64| ストア情報\(apple、google、one\)|
| title| String| -| GAMEPOTダッシュボード > ゲーム > プレゼントする > 件名に入力した値|
| content| String| -| GAMEPOTダッシュボード > ゲーム > プレゼントする > 説明に入力した値|
| userData| String| -| coupon api呼び出しの際に、二番目のパラメータに入力した値|
| itemId| Array| -| itemData Array - itemData\(JSON\) {"item_id" : String, "store_item_id" : String, "count" : Number}|

> ex\)
>
> [https://{domain}?itemId=\[{"item_id":"d0781c4e-df52-465b-ab93-0ee16fbf445d","store_item_id":"ttt","count":1}\]&platform=android&projectId=f1df9464-40a8-4a66-8421-196c7c661002&store=google&userId=2d485044-06c2-48c4-a6ed-4ab53dea88bb](https://{domain}?itemId=[{"item_id":"d0781c4e-df52-465b-ab93-0ee16fbf445d","store_item_id":"ttt","count":1}]&platform=android&projectId=f1df9464-40a8-4a66-8421-196c7c661002&store=google&userId=2d485044-06c2-48c4-a6ed-4ab53dea88bb)

#### Response

レスポンスは以下のような形式で行ってください。

```javascript
{
    "status": 1,
    "message" : ""
}
```

| Attribute| Type| Description|
| :-------- | :----- | :---------------------------- |
| status| Int| 結果値\( 0：失敗、1：成功 \)|
| message| String| エラー内容|

## ゲームサーバ &gt; GAMEPOTサーバ

### Token Authentication\(optional\)

ゲームログイン完了後に取得した情報を用いて、GAMEPOTサーバでログイン検証ができます。

トークン検証は2段階で行われ、第1段階のGAMEPOTトークン検証の後、第2段階のソーシャルトークン検証が行われます。

> 第2段階の検証ではGAMEPOTダッシュボード - プロジェクトの設定 - Auth keyに値を入力する必要があります。

第1段階のGAMEPOTトークン検証では、ログイン後に取得したMemberID(ユーザーID)、Tokenで同期トークン検証を行い、

第2段階のソーシャルトークン検証では、GoogleログインやFacebookログイン時に取得したソーシャルアカウントのトークンでソーシャル非同期トークン検証を行います。

第2段階で検証に失敗した場合はGAMEPOTの利用停止機能が作動し、その後再ログインはできません。

> 検証失敗による利用停止は、GAMEPOTダッシュボード - プロジェクトの設定 - Auth key項目でスイッチがONになっている場合にのみ作動し、利用停止対象者はGAMEPOTダッシュボード - 会員 - 利用停止メニューで確認できます。

**第1段階の検証を同期処理しないでください!**

ユーザーがログインするプロセスですが、この機能を同期処理するとネットワーク通信による遅延が発生してゲーム利用の妨げになります。また、当該ネットワーク通信が物理的に分離されている状況なので、それによってネットワーク通信が不安定になる場合が多々あります。

この機能は非同期処理し、その後にゲーム利用を制限する形で機能を実装してください。

#### Request

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

| Attribute| Type| Max Length| Description|
| :-------- | :----- | :--------- | :---------------------- |
| projectId| String| 128| GamePot SDKのprojectId|
| memberId| String| 128| GamePot SDKのmemberid(メンバーID)|
| token| String| 2048| GamePot SDKのToken|

#### Response

第1段階検証で検証に失敗した場合、statusに1ではない値が入力されます。

この場合はゲーム入場を制限してください。

```javascript
{
    "status": 1,
    "message" : ""
}
```

| Attribute| Type| Description|
| :-------- | :----- | :---------------------------------------------- |
| status| Int| 結果値\(1：成功、失敗は以下のError code参照\)|
| message| String| エラー内容|

#### Error code

| Code| Description|
| :--- | :-------------------------------------------------------------------------------------------------------------- |
| 0| Bodyに漏れデータがある場合、HTTPリクエストの際にprojectId、memberId、tokenをすべて入力したか確認してください。|
| -1| Token検証失敗Tokenが捏造された場合|
| -2| MemberId検証失敗TokenのMemberId情報とbodyのMemberIdが一致しない場合|
| -3| Token満了SDK login apiが成功した時刻とそのAuthentication checkをリクエストした時刻の間に10分以上の差が生じた場合|

### ThirdParty Purchase

> この機能は一般的には使用されない機能なので、適用前にGAMEPOTまでお問い合わせください。

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

| Header| Type| Required| Description|
| :-------- | :----- | :------- | ---------------------------- |
| x-api-key| String| O| GamePotで発行する認証キー|

<br/>

| Attribute| Type| Max Length| Required| Description|
| :------------ | :----- | :--------- | :------- | :---------------------- |
| projectId| String| 128| O| GamePot SDKのprojectId|
| store| String| 64| O| 決済ストア|
| productId| String| 256| O| 決済アイテムID|
| transactionId| String| 512| O| 決済固有ID|
| memberId| String| 128| O| GamePot SDKのmemberid(メンバーID)|
| currency| String| 64| X| 決済通貨|
| price| Number| -| X| 決済金額|
| paymentId| String| 64| X| 決済方法|
| uniqueId| String| 512| X| ゲーム内決済の固有ID|

#### Response

```javascript
{
    "status": 1,
    "message" : ""
}
```

| Attribute| Type| Description|
| :-------- | :----- | :---------------------------------------------- |
| status| Int| 結果値\(1：成功、失敗は以下のError code参照\)|
| message| String| エラー内容|

#### Error code

| Code| Description|
| :--- | :----------------------------------------------------------------------------------------------------------------------- |
| -1| Bodyに漏れデータがある場合、<br/>projectId、transactionId、productId、store、memberIdをすべて入力したか確認してください。¬ |
| -2| price値がnumberタイプではない場合、<br/>numberタイプで入力してください。|
| -3| projectIdがない場合、<br/>入力したprojectIdをもう一度確認してください。|
| -4| プロジェクトが当該apiに対応していない場合、<br/>GAMEPOTまでお問い合わせください。|
| -5| transactionIdが既に存在している場合|
| -6| DBエラー。GAMEPOTまでお問い合わせください。|
