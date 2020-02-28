---
search:
  keyword: ["gamepot"]
---

## Purchase Webhook

決済完了後に GAMEPOT サーバからゲームサーバにアイテム支給のために HTTP リクエストをします。

> GAMEPOT はクライアントから転送された決済情報を基にストア領収証の検証まで進めるため違法決済の試しを防ぎます。

### Request

HTTP リクエストの際の情報は以下のような内容で転送し、当該情報を基にユーザーにアイテムを支給してください。

> `{domain}` 項目はデベロッパー社で作業完了後知らせる必要があり、この値は**GAMEPOT ダッシュボード - プロジェクト設定 - 一般 - Webhook** 項目に追加する必要があります。

```java
https://{domain}?
userId={uuid}&orderId={orderId}&projectId={projectId}&platform={platform}&productId={productId}&store={store}&payment={payment}&transactionId={transactionId}&gamepotOrderId={gamepotOrderId}&uniqueId={uniqueId}
```

| Attribute      | Type   | Description                                                            |
| -------------- | ------ | ---------------------------------------------------------------------- |
| userId         | String | ユーザー UID                                                           |
| transactionId  | String | 注文番号(GPA-xxxx-xxxx-)                                               |
| store          | String | ストア情報(ios, google, one)                                           |
| projectId      | String | プロジェクト ID                                                        |
| productId      | String | グーグル/アップル/ワンストアに登録された商品 ID                        |
| platform       | String | オペレーティング Platform 情報 (android, ios)                          |
| payment        | String | 決済方法 ( apple, google, one, danal, mycard, mol ... )                |
| orderId        | String | **Deprecated** Unique id (purchase api 呼び出しの際に入れた unique id) |
| uniqueId       | String | Unique id (purchase api 呼び出しの際に入れた unique id)                |
| gamepotOrderId | String | GAMEPOT Order id                                                       |

### Response

レスポンスは以下のような形式にしてください。

```json
{
  "status": 1,
  "message": ""
}
```

| Attribute | Type   | Description                 |
| --------- | ------ | --------------------------- |
| status    | Int    | 結果値 ( 0: 失敗, 1: 成功 ) |
| message   | String | エラー内容                  |

## Item Webhook

クーポン/大量のアイテムの発送機能の使用時に GAMEPOT サーバーからゲームサーバーでアイテム支給のために HTTP 要求をします。

### Request

HTTP リクエストの際の情報は以下のような内容で転送し、当該情報を基にユーザーにアイテムを支給してください。

> `{domain}` 項目はデベロッパー社で作業完了後知らせる必要があり、この値は**GAMEPOT ダッシュボード - プロジェクト設定 - 一般 - Webhook** 項目に追加する必要があります。

> `GAMEPOTダッシュボード - ゲーム - アイテム`でアイテム発送時全体の送信機能があります。
> この機能を使用すると、`target`/`userId`が`all`に送信されるため、開発会社では、すべてのユーザーにアイテムを支給することができるよう処理する必要があります。

```web-idl
https://{domain}?
userId={userId}&projectId={projectId}&platform={platform}&store={store}&userData={userData}&itemId=[{itemData}, {itemData}, ...]
```

| Attribute | Type            | Description                                                                                                        |
| --------- | --------------- | ------------------------------------------------------------------------------------------------------------------ |
| userId    | String          | ユーザー ID                                                                                                        |
| projectId | String          | Project ID                                                                                                         |
| platform  | String          | オペレーティング Platform 情報 (Android, IOS, job)                                                                 |
| store     | String          | ストア情報(ios, google, one)                                                                                       |
| userData  | String          | coupon api 呼び出しの際に二番目のパラメータに入れた値                                                              |
| itemId    | Array<itemData> | itemData Array<br /><br />- itemData(JSON) <br /> {"item_id" : String, "store_item_id" : String, "count" : Number} |
| target    | String          | ユーザ/全 \(user, all\)                                                                                            |
| title     | String          | メールボックスに表示されるタイトル                                                                                 |
| content   | String          | メールボックスに表示される内容                                                                                     |

> ex)
>
> https://{domain}?itemId=[{"item_id":"d0781c4e-df52-465b-ab93-0ee16fbf445d","store_item_id":"ttt","count":1}]&platform=android&projectId=f1df9464-40a8-4a66-8421-196c7c661002&store=google&userId=2d485044-06c2-48c4-a6ed-4ab53dea88bb

### Response

レスポンスは以下のような形式にしてください。

```json
{
  "status": 1,
  "message": ""
}
```

| Attribute | Type   | Description                |
| --------- | ------ | -------------------------- |
| status    | Int    | 結果値( 0: 失敗, 1: 成功 ) |
| message   | String | エラー内容                 |

## Token Authentication

ゲームにログイン完了後に得た情報で GAMEPOT サーバにログイン検証をすることができます。

トックン検証は 2 段階で進められ、1 段階の GAMEPOT トックン(Token)検証後 2 段階のソーシャルトックンの検証が進められます。

> 2 段階の検証は **GAMEPOT ダッシュボード - プロジェクト設定 - Auth key**に値が入力されていなければなりません。

1 段階の GAMEPOT トックンの検証はログイン後に得た MemberID, Token で同期トックン検証を進め、

2 段階のソーシャルトックン検証はグーグルログインやフェイスブックログインを通じて獲得したソーシャルアカウントのトックンでソーシャル非同期トックン検証を進めます。

2 段階で検証に失敗した場合には GAMEPOT 利用停止機能が作動されてその後再ログインの際にログインできません。

> 検証失敗による利用停止は**GAMEPOT ダッシュボード - プロジェクト設定 - Auth key**項目でスイッチが ON になっている場合のみ作動し、利用停止対象者は **GAMEPOT ダッシュボード - 会員 - 利用停止**メニューで確認できます。

### Request

データインテグリティのためにクライアントではなくデベロッパー社のサーバで進めてください。

> {API URL} 項目は GAMEPOT ダッシュボードアドレスで `:8080`を除いたアドレスです。

```web-idl
POST
url : https://{API URL}/loginauth
Header : 'content-type: application/json'
data:
{
	"projectId": {GAMEPOT SDKのprojectId},
	"memberId": {GAMEPOT SDKのmemberId},
	"token": {GAMEPOT SDKのToken}
}
```

| Attribute | Type   | Description              |
| --------- | ------ | ------------------------ |
| projectId | String | GAMEPOT SDK の projectId |
| memberId  | String | GAMEPOT SDK の memberId  |
| token     | String | GAMEPOT SDK の Token     |

### Response

1 段階の検証で検証失敗した場合は Status が 1 ではない値が入力されます。

この場合はゲームへのアクセスを制限してください。

```json
{
  "status": 1,
  "message": ""
}
```

| Attribute | Type   | Description                                        |
| --------- | ------ | -------------------------------------------------- |
| status    | Int    | 結果値 (1: 成功, 失敗は以下の Error code をご参照) |
| message   | String | エラー内容                                         |

### Error code

| Code | Description                                                                                                              |
| ---- | ------------------------------------------------------------------------------------------------------------------------ |
| 0    | Body に欠落したデータがある場合<br />HTTP リクエストの際 projectId, memberId, token を全て入れたか確認してください。     |
| -1   | Token 検証の失敗<br />Token が捏造された場合                                                                             |
| -2   | MemberId 検証失敗<br />Token の MemberId 情報と Body の MemberId が一致しない場合                                        |
| -3   | Token の満了<br />SDK Login API が成功した時刻と当該 Authentication check をリクエストした時刻が 10 分以上差が生じた場合 |

## Push notification

ゲームサーバからユーザーにプッシュを送信しようとする場合に使用できるサーバプッシュです。

NAVER クラウドプラットフォームの Simple & Easy Notification Service を通じてユ―ザーに通知メッセージを発送するため、Simple & Easy Notification Service 商品に関する設定が先行されていなければなりません。

### Request

`{API URL}`は GAMEPOT ダッシュボードアドレスで `:8080`を除いたアドレスであり

`{API KEY}`は **ダッシュボード - プロジェクト設定 - NCloud - API 認証キー - Access Key**を入れてください。

```web-idl
POST
url : https://{API URL}/push
Header : 'content-type: application/json'
Header : 'x-api-key: {API KEY}'
data:
{
	"projectId": {GAMEPOT SDKのprojectId},
	"message": {ユーザーに送信するプッシュメッセージ},
	"title": {ユーザーに送信するプッシュのタイトル},
	"target": {プッシュを受け取るユーザーのmemberId 配列}
}
```

| Attribute | Type         | Description                                                                                                                                                 |
| --------- | ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| projectId | String       | GAMEPOT SDK の projectId                                                                                                                                    |
| message   | String       | ユーザーに送信するプッシュメッセージ                                                                                                                        |
| title     | String       | ユーザーに送信するプッシュのタイトル(基本値はアプリのタイトル)                                                                                              |
| target    | String Array | プッシュを受け取るユーザーの memberId 配列 **(最大 100 個)**<br />["e87b3a....","d28a30...."]<br />ユーザー全体に送信する際は空欄の配列[]を入れてください。 |

### Response

この場合はゲームへのアクセスを制限してください。

```json
{
  "status": 1,
  "message": "success"
}
```

| Attribute | Type   | Description                                      |
| --------- | ------ | ------------------------------------------------ |
| status    | Int    | 結果値 (1: 成功, 失敗は以下の Error code を参照) |
| message   | String | エラー内容                                       |

### Error code

| Code | Description                                                                                                                                                      |
| ---- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0    | Body またはヘッダーに欠落したデータがある場合<br />Request にあるデータを全て盛り込んだか確認してください。                                                      |
| -1   | Request の target 値のエラー<br />String Array に値を入れたか確認してください。 ["e87b3a....","d28a30...."]                                                      |
| -2   | ヘッダーで X-API-KEY 値のエラー<br />ダッシュボード - プロジェクト設定 - NCloud - API 認証キー - Access Key とヘッダーで `X-API-KEY`が一致しなければなりません。 |
| -3   | ダッシュボードに Access Key がない場合<br />ダッシュボード - プロジェクト設定 - NCloud - API 認証キー - Access Key を入れてください。                            |
| -4   | Request の `projectId`値のエラー<br />`projectId` 値が正しいか確認してください。                                                                                 |
| -5   | DB エラー<br /> GAMEPOT に問い合わせてください。                                                                                                                 |
