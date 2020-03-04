---
search:
  keyword: ["gamepot"]
---

## Purchase Webhook

After the payment is completed, the GAMEPOT server makes an HTTP request to the game server to provide an item.

> GAMEPOT checks receipts based on the payment information received from the client, preventing illegal payment attempts.

### Request

The following information is passed when GAMEPOT makes an HTTP request, and you can give items to users based on the information.

> `{domain}` should be provided by the developer, and should be added to **Project settings > General > Webhook** in your GAMEPOT dashboard.

```java
https://{domain}?
userId={uuid}&orderId={orderId}&projectId={projectId}&platform={platform}&productid={productId}&store={store}&payment={payment}&transactionId={transactionId}
```

| Attribute     | Type   | Description                                                    |
| ------------- | ------ | -------------------------------------------------------------- |
| userId        | String | User UID                                                       |
| transactionId | String | Transaction number (GPA-xxxx-xxxx-)                            |
| store         | String | Store information (ios, google, one)                           |
| projectId     | String | Project ID                                                     |
| productId     | String | Product ID registered in Google Play, App Store and ONE store. |
| platform      | String | Platform information (Android, iOS)                            |
| payment       | String | Payment type (apple, google, one, mycard, mol)                 |
| orderId       | String | Order number (automatically generated)                         |
| domain        | String | Domain of the server that provides items to the game server.   |

### Response

Return a response in the following format.

```json
{
  "status": 1,
  "message": ""
}
```

| Attribute | Type   | Description                      |
| --------- | ------ | -------------------------------- |
| status    | Int    | Result (0: Failed, 1: Succeeded) |
| message   | String | Error message                    |

## Item Webhook

After a coupon is used, the GAMEPOT server makes an HTTP request to the game server to provide an item.

### Request

The following information is passed when GAMEPOT makes an HTTP request, and you can give items to users based on the information.

> `{domain}` should be provided by the developer, and should be added to **Project settings > General > Webhook** in your GAMEPOT dashboard.

```web-idl
https://{domain}?
userId={userId}&projectId={projectId}&platform={platform}&store={store}&userData={userData}&itemId=[{itemData}, {itemData}, ...]
```

| Attribute | Type            | Description                                                                                                        |
| --------- | --------------- | ------------------------------------------------------------------------------------------------------------------ |
| userId    | String          | User ID                                                                                                            |
| projectId | String          | Project ID                                                                                                         |
| platform  | String          | Platform information (Android, iOS)                                                                                |
| store     | String          | Store information (ios, google, one)                                                                               |
| userData  | String          | The value in the second parameter when the coupon api is called.                                                   |
| itemId    | Array<itemData> | itemData Array<br /><br />- itemData(JSON) <br /> {"item_id" : String, "store_item_id" : String, "count" : Number} |

> ex)
>
> https://{domain}?itemId=[{"item_id":"d0781c4e-df52-465b-ab93-0ee16fbf445d","store_item_id":"ttt","count":1}]&platform=android&projectId=f1df9464-40a8-4a66-8421-196c7c661002&store=google&userId=2d485044-06c2-48c4-a6ed-4ab53dea88bb

### Response

Return a response in the following format.

```json
{
  "status": 1,
  "message": ""
}
```

| Attribute | Type   | Description                      |
| --------- | ------ | -------------------------------- |
| status    | Int    | Result (0: Failed, 1: Succeeded) |
| message   | String | Error message                    |

## Token authentication

Using the information you get after login is completed in your game, you can request the GAMEPOT server to verify the login.

Token authentication is processed in two steps: step 1 is GAMEPOT token authentication, and step 2 is social token authentication.

> For the step 2, you should add a value in **Project settings > Auth key** of your GAMEPOT dashboard in advance.

The step 1 is synchronous token authentication that is performed with a memberID and token obtained after login is completed,

while the step 2 is asynchronous social token authentication that is performed with a token of a social media account obtained after Google or Facebook login is completed.

If the step 2 authentication fails, GAMEPOT blocks the user from logging in the game.

> The feature to block users after authentication fails works only when **Project settings > Auth key** is turned on in your GAMEPOT dashboard. You can check blocked users in **Member > Block** of the GAMEPOT dashboard.

### Request

For data integrity, the request should be made in the developer server, rather than the client.

> {API URL} is the address of your GAMEPOT dashboard, without `:8080`.

```web-idl
POST
url : https://{API URL}/loginauth
Header : 'content-type: application/json'
data:
{
	"projectId": {GamePot SDK's projectId},
	"memberId": {GamePot SDK's memberId},
	"token": {GamePot SDK's Token}
}
```

| Attribute | Type   | Description             |
| --------- | ------ | ----------------------- |
| projectId | String | GamePot SDK's projectId |
| memberId  | String | GamePot SDK's memberId  |
| token     | String | GamePot SDK's Token     |

### Response

If the step 1 authentication fails, the status is set to a value other than 1.

In this case, restrict the user from entering the game.

```json
{
  "status": 1,
  "message": ""
}
```

| Attribute | Type   | Description                                                       |
| --------- | ------ | ----------------------------------------------------------------- |
| status    | Int    | Result (1: Succeeded. Refer to Error code below for other cases.) |
| message   | String | Error message                                                     |

### Error code

| Code | Description                                                                                                                                                        |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 0    | Required data is omitted from the body.<br />Make sure that projectId, memberId, and token are all specified when making a request.                                |
| -1   | Token authentication failed.<br />A fake token is used.                                                                                                            |
| -2   | MemberId authentication failed.<br />The token’s memberId does not match the memberId in the body.                                                                 |
| -3   | Token expired.<br />The time when the SDK login api was successful is different from the time when the authentication check is requested, by more than 10 minutes. |

## Push notification

Push notification is used by the game server to send push notifications to users.

Since this feature uses NAVER CLOUD PLATFORM’s Simple & Easy Notification Service to send push messages, you should configure settings for Simple & Easy Notification Service.

### Request

`{API URL}` is the address of your GAMEPOT dashboard, without `:8080`,

while `{API KEY}` is the value set in **Project settings > Ncloud > API auth key > Access Key** of your GAMEPOT dashboard.

```web-idl
POST
url : https://{API URL}/push
Header : 'content-type: application/json'
Header : 'x-api-key: {API KEY}'
data:
{
	"projectId": {GamePot SDK의 projectId},
	"message": {Push message to be sent to users},
	"title": {Title of push message to be sent to users},
	"target": {Array of memberIds of users who receive push messages}
}
```

| Attribute | Type         | Description                                                                                                                                                                                    |
| --------- | ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| projectId | String       | GamePot SDK’s projectId                                                                                                                                                                        |
| message   | String       | Push message to be sent to users                                                                                                                                                               |
| title     | String       | Title of the push message to be sent to users (The default value is the app’s title)                                                                                                           |
| target    | String Array | Array of memberIds of users who receive push notifications **(up to 100 memberIds)**<br />["e87b3a....","d28a30...."]<br />Set this to an empty array ([]) to send push messages to all users. |

### Response

In this case, restrict the user from entering the game.

```json
{
  "status": 1,
  "message": "success"
}
```

| Attribute | Type   | Description                                                       |
| --------- | ------ | ----------------------------------------------------------------- |
| status    | Int    | Result (1: Succeeded. Refer to Error code below for other cases.) |
| message   | String | Error message                                                     |

### Error code

| Code | Description                                                                                                                                                                          |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 0    | Required data is omitted in the body or header.<br />Make sure that the requested data is all included.                                                                              |
| -1   | Invalid target in the request.<br />Make sure that you specify the target value in String Array. ["e87b3a....","d28a30...."]                                                         |
| -2   | Invalid `X-API-KEY value` in the header.<br />The X-API-KEY value in the header must match the value in **Project settings > Ncloud > API auth key > Access Key** in your dashboard. |
| -3   | No Access Key specified in your dashboard.<br />Set **Project settings > Ncloud > API auth key > Access Key** in your dashboard.                                                     |
| -4   | Invalid `projectId value` in the request.<br />Check if the `projectId value` is valid.                                                                                              |
| -5   | DB error.<br />Contact GAMEPOT.                                                                                                                                                      |

### ThirdParty Purchase

> This feature is not commonly used. Please contact GAMEPOT before applying.

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

| Header    | Type   | Required | Description                         |
| :-------- | :----- | :------- | :---------------------------------- |
| x-api-key | String | O        | Authorization key issued by GamePot |

<br/>

| Attribute     | Type   | Required | Description               |
| :------------ | :----- | :------- | :------------------------ |
| projectId     | String | O        | ProjectId in GamePot SDK  |
| store         | String | O        | Payment store             |
| productId     | String | O        | Payment item ID           |
| transactionId | String | O        | Billing Unique ID         |
| memberId      | String | O        | MemberId from GamePot SDK |
| currency      | String | X        | Billing currency          |
| price         | Number | X        | Amount of payment         |
| paymentId     | String | X        | method of payment         |
| uniqueId      | String | X        | In-game payment unique ID |

#### Response

```javascript
{
    "status": 1,
    "message" : ""
}
```

| Attribute | Type   | Description                                                   |
| :-------- | :----- | :------------------------------------------------------------ |
| status    | Int    | Result value \(1: Error code below for success and failure \) |
| message   | String | Error description                                             |

#### Error code

| Code | Description                                                                                                                          |
| :--- | :----------------------------------------------------------------------------------------------------------------------------------- |
| -1   | If there is missing data in the Body, make sure you have entered the <br/> projectId, transactionId, productId, store and memberId.  |
| -2   | If the price value is not of type number, put it as type number.                                                                     |
| -3   | If you don't have a projectId <br/> double check the projectId you entered.                                                          |
| -4   | If your project doesn't support this api <br/> contact GAMEPOT.                                                                      |
| -5   | transactionId already exists                                                                                                         |
| -6   | DB error. Please contact GAMEPOT.                                                                                                    |
