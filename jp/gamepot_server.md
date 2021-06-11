---
search:
  keyword: ['gamepot']
---

#### **NAVER クラウドプラットフォーム商品の使用方法をより詳細に提供し、様々な API の活用をサポートするために<a href="https://guide.ncloud-docs.com/docs/ja/home" target="_blank">[説明書]</a>と<a href="https://api.ncloud-docs.com/docs/ja/home" target="_blank">[API リファレンス]</a>を分けて提供しています。**

<a href="https://api.ncloud-docs.com/docs/ja/game-gamepot" target="_blank">GAMEPOT API リファレンスへ >></a><br />
<a href="https://guide.ncloud-docs.com/docs/ja/game-gamepotconsole" target="_blank">GAMEPOT 説明書へ >></a>

# Server API

## GAMEPOT サーバ &gt; ゲームサーバ

### Purchase Webhook\(required\)

決済が完了すると、GAMEPOT サーバからゲームサーバにアイテム支給のための HTTP リクエストを行います。

> GAMEPOT は、ユーザーから伝達された決済情報をもとにストア領収証の検証まで行って不正決済を防いでいます。

#### Request

HTTP リクエストの際に以下のような内容の情報を伝えます。その情報をもとにユーザーにアイテムを支給してください。

> `{domain}`項目は開発会社で操作を完了してから知らせてください。この値は GAMEPOT ダッシュボード - プロジェクトの設定 - 一般 - Webhook 項目に追加する必要があります。

```java
https://{domain}?
userId={uuid}&orderId={orderId}&projectId={projectId}&platform={platform}&productId={productId}&store={store}&payment={payment}&transactionId={transactionId}&gamepotOrderId={gamepotOrderId}&uniqueId={uniqueId}&tp={tp}
```

| Attribute      | Type    | Max Length | Description                                               |
| :------------- | :------ | :--------- | :-------------------------------------------------------- |
| userId         | String  | 128        | ユーザー ID                                               |
| transactionId  | String  | 512        | 注文番号\(GPA-xxxx-xxxx-\)                                |
| store          | String  | 64         | ストア情報\(apple、google、one\)                          |
| projectId      | String  | 128        | プロジェクト ID                                           |
| productId      | String  | 256        | Google/Apple/ONE Store に登録された商品 ID                |
| platform       | String  | 128        | 運用プラットフォーム情報\(android、ios\)                  |
| payment        | String  | 64         | 決済方法 \( apple、google、one、danal、mycard、mol...\)   |
| uniqueId       | String  | 512        | Unique id \(purchase api 呼び出しの際に入れた unique id\) |
| gamepotOrderId | String  | 512        | GAMEPOT Order id                                          |
| serverId       | String  | -          | serverId \(purchase api 呼び出しの際に入れた serverId\)   |
| playerId       | String  | -          | playerId \(purchase api 呼び出しの際に入れた playerId\)   |
| tp             | Integer | -          | 1: 테스트 결제<br />0: 일반 결제                          |
| etc            | String  | -          | etc \(purchase api 呼び出しの際に入れた etc\)             |

#### Response

レスポンスは以下のような形式で行ってください。

```javascript
{
    "status": 1,
    "message" : ""
}
```

| Attribute | Type   | Description                  |
| :-------- | :----- | :--------------------------- |
| status    | Int    | 結果値\( 0：失敗、1：成功 \) |
| message   | String | エラー内容                   |

### Item Webhook\(required\)

クーポンを使用すると、GAMEPOT サーバからゲームサーバにアイテム支給のための HTTP リクエストを行います。

#### Request

HTTP リクエストの際に以下のような内容の情報を伝えます。その情報をもとにユーザーにアイテムを支給してください。

> `{domain}`項目は開発会社で操作を完了してから知らせてください。この値は GAMEPOT ダッシュボード - プロジェクトの設定 - 一般 - Webhook 項目に追加する必要があります。

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
> ex\)
>
> https://{domain}?itemId=\[{"item_id":"d0781c4e-df52-465b-ab93-0ee16fbf445d","store_item_id":"ttt","count":1}\]&platform=android&projectId=f1df9464-40a8-4a66-8421-196c7c661002&store=google&userId=2d485044-06c2-48c4-a6ed-4ab53dea88bb

#### Response

レスポンスは以下のような形式で行ってください。

```javascript
{
    "status": 1,
    "message" : ""
}
```

| Attribute | Type   | Description                  |
| :-------- | :----- | :--------------------------- |
| status    | Int    | 結果値\( 0：失敗、1：成功 \) |
| message   | String | エラー内容                   |

## ゲームサーバ &gt; GAMEPOT サーバ

### Token Authentication\(optional\)

ゲームログイン完了後に取得した情報を用いて、GAMEPOT サーバでログイン検証ができます。

トークン検証は 2 段階で行われ、第 1 段階の GAMEPOT トークン検証の後、第 2 段階のソーシャルトークン検証が行われます。

> 第 2 段階の検証では GAMEPOT ダッシュボード - プロジェクトの設定 - Auth key に値を入力する必要があります。

第 1 段階の GAMEPOT トークン検証では、ログイン後に取得した MemberID(ユーザー ID)、Token で同期トークン検証を行い、

第 2 段階のソーシャルトークン検証では、Google ログインや Facebook ログイン時に取得したソーシャルアカウントのトークンでソーシャル非同期トークン検証を行います。

第 2 段階で検証に失敗した場合は GAMEPOT の利用停止機能が作動し、その後再ログインはできません。

> 検証失敗による利用停止は、GAMEPOT ダッシュボード - プロジェクトの設定 - Auth key 項目でスイッチが ON になっている場合にのみ作動し、利用停止対象者は GAMEPOT ダッシュボード - 会員 - 利用停止メニューで確認できます。

**第 1 段階の検証を同期処理しないでください!**

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

| Attribute | Type   | Max Length | Description                          |
| :-------- | :----- | :--------- | :----------------------------------- |
| projectId | String | 128        | GamePot SDK の projectId             |
| memberId  | String | 128        | GamePot SDK の memberid(メンバー ID) |
| token     | String | 2048       | GamePot SDK の Token                 |

#### Response

第 1 段階検証で検証に失敗した場合、status に 1 ではない値が入力されます。

この場合はゲーム入場を制限してください。

```javascript
{
    "status": 1,
    "message" : ""
}
```

| Attribute | Type   | Description                                     |
| :-------- | :----- | :---------------------------------------------- |
| status    | Int    | 結果値\(1：成功、失敗は以下の Error code 参照\) |
| message   | String | エラー内容                                      |

#### Error code

| Code | Description                                                                                                             |
| :--- | :---------------------------------------------------------------------------------------------------------------------- |
| 0    | Body に漏れデータがある場合、HTTP リクエストの際に projectId、memberId、token をすべて入力したか確認してください。      |
| -1   | Token 検証失敗 Token が捏造された場合                                                                                   |
| -2   | MemberId 検証失敗 Token の MemberId 情報と body の MemberId が一致しない場合                                            |
| -3   | Token 満了 SDK login api が成功した時刻とその Authentication check をリクエストした時刻の間に 10 分以上の差が生じた場合 |

### ThirdParty Purchase

> この機能は一般的には使用されない機能なので、適用前に GAMEPOT までお問い合わせください。

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

| Header    | Type   | Required | Description                |
| :-------- | :----- | :------- | -------------------------- |
| x-api-key | String | O        | GamePot で発行する認証キー |

<br/>

| Attribute     | Type   | Max Length | Required | Description                          |
| :------------ | :----- | :--------- | :------- | :----------------------------------- |
| projectId     | String | 128        | O        | GamePot SDK の projectId             |
| store         | String | 64         | O        | 決済ストア                           |
| productId     | String | 256        | O        | 決済アイテム ID                      |
| transactionId | String | 512        | O        | 決済固有 ID                          |
| memberId      | String | 128        | O        | GamePot SDK の memberid(メンバー ID) |
| currency      | String | 64         | X        | 決済通貨                             |
| price         | Number | -          | X        | 決済金額                             |
| paymentId     | String | 64         | X        | 決済方法                             |
| uniqueId      | String | 512        | X        | ゲーム内決済の固有 ID                |

#### Response

```javascript
{
    "status": 1,
    "message" : ""
}
```

| Attribute | Type   | Description                                     |
| :-------- | :----- | :---------------------------------------------- |
| status    | Int    | 結果値\(1：成功、失敗は以下の Error code 参照\) |
| message   | String | エラー内容                                      |

#### Error code

| Code | Description                                                                                                                  |
| :--- | :--------------------------------------------------------------------------------------------------------------------------- |
| -1   | Body に漏れデータがある場合、<br/>projectId、transactionId、productId、store、memberId をすべて入力したか確認してください。¬ |
| -2   | price 値が number タイプではない場合、<br/>number タイプで入力してください。                                                 |
| -3   | projectId がない場合、<br/>入力した projectId をもう一度確認してください。                                                   |
| -4   | プロジェクトが当該 api に対応していない場合、<br/>GAMEPOT までお問い合わせください。                                         |
| -5   | transactionId が既に存在している場合                                                                                         |
| -6   | DB エラー。GAMEPOT までお問い合わせください。                                                                                |
