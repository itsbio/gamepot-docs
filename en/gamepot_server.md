
## Server API<a name="ServerAPI"></a>


## GAMEPOT server > game server<a name="GAMEPOTserver>gameserver"></a>


```java
It is safe to apply the firewall to the webhook address for security.
In the absence of a firewall or normal request validation, 
items may be provided through abnormal requests.
Firewalls should preferably be created based on the whitelist, 
and the GAMEPOT IP permissions below are required.
49.236.143.202
49.236.143.198
106.10.53.19
106.10.52.84

In addition, if you want security to be safe from spoofing attacks, 
please complete the normal request validation by using the "etc" attribute.
```


### Purchase Webhook\(required\)<a name="PurchaseWebhookrequired"></a>


After the payment has been processed, the GAMEPOT server makes an HTTP request to the game server.



>GAMEPOT verifies receipts based on the payment information received from the client, preventing illegal payment attempts.


#### Request<a name="Request1"></a>


When GAMEPOT makes an HTTP request, the information shown below is forwarded and you can give items to users based upon that information.



>`{domain}` must be provided by the developer and should be added to Project settings > General > Webhook in your GAMEPOT dashboard.


```java
https://{domain}?
userId={uuid}&orderId={orderId}&projectId={projectId}&platform={platform}&productId={productId}&store={store}&payment={payment}&transactionId={transactionId}&gamepotOrderId={gamepotOrderId}&uniqueId={uniqueId}&tp={tp}
```

| Attribute      | Type    | Max Length | Description                                                                 |
| :------------- | :------ | :--------- | :-------------------------------------------------------------------------- |
| userId         | String  | 128        | User ID                                                                     |
| transactionId  | String  | 512        | Order number \(GPA-xxxx-xxxx-\)                                             |
| store          | String  | 64         | Store information \(Apple, Google, ONE\)                                    |
| projectId      | String  | 128        | Project ID                                                                  |
| productId      | String  | 256        | Product ID registered in Google Play Store, Apple App Store, and ONE Store. |
| platform       | String  | 128        | Platform information \(Android, iOS\)                                       |
| payment        | String  | 64         | Payment type \( Apple, Google, ONE, Danal, MyCard, Mol ... \)               |
| uniqueId       | String  | 512        | Unique id \(unique id entered when calling purchase api\)                   |
| gamepotOrderId | String  | 512        | GAMEPOT Order ID                                                            |
| serverId       | String  | -          | serverId \(serverId entered when calling purchase api\)                     |
| playerId       | String  | -          | playerId \(playerId entered when calling purchase api\)                     |
| tp             | Integer | -          | 1: Test payment<br />0: Regular payment                                            |
| etc            | String  | -          | etc \(etc entered when calling purchase api\)                               |

#### Response<a name="Response1"></a>


Return a response in the following format.

```javascript
{
    "status": 1,
    "message" : ""
}
```

| Attribute | Type   | Description                        |
| :-------- | :----- | :--------------------------------- |
| status    | Int    | Result \(0: Failed, 1: Succeeded\) |
| message   | String | Error message                      |

### Item Webhook\(required\)<a name="ItemWebhookrequired"></a>


After a coupon is used, the GAMEPOT server makes an HTTP request to the game server to provide an item.

#### Request<a name="Request2"></a>


When GAMEPOT makes an HTTP request, the information shown below is forwarded and you can give items to users based upon that information.



>`{domain}` must be provided by the developer and should be added to Project settings > General > Webhook in your GAMEPOT dashboard.


```text
https://{domain}?
userId={userId}&projectId={projectId}&platform={platform}&store={store}&userData={userData}&itemId=[{itemData}, {itemData}, ...]
```

| Attribute | Type   | Max Length | Description                                                                                        |
| :-------- | :----- | :--------- | :------------------------------------------------------------------------------------------------- |
| userId    | String | 128        | User ID (GAMEPOT Dashboard > Game > Present > If target value is all, all)                                                                                 |
| projectId | String | 128        | Project ID                                                                                 |
| platform  | String | 128        | Platform information \(Android, iOS\)                                                          |
| store     | String | 64         | Store information \(Apple, Google, ONE\)                                                             |
| title     | String | -          | The value in GAMEPOT Dashboard > Game > Present > Title                                                       |
| content   | String | -          | The value in GAMEPOT Dashboard > Game > Present > Description                                                       |
| target    | String | -          | GAMEPOT Dashboard > Game > Present > Target value - all: all/User ID: user                                                       |
|expireMs  | String | -        | GAMEPOT Dashboard > Game > Present > Expiry date value  Timestamp ( GMT+9)  | 
| userData  | String | -          | The value in the second parameter when the coupon API is called                                                      |
| itemId    | Array  | -          | itemData Array - itemData\(JSON\) {"item_id" : String, "store_item_id" : String, "count" : Number} |
|     |   |           | item_id: Go to GAMEPOT> Game > Unique ID. ID of the item created in the GAMEPOT. store_item_id : ID of the item to be provided. count: Number of items to be provided|


 ex)
 
>https://{domain}?itemId=\[{"item_id":"d0781c4e-df52-465b-ab93-0ee16fbf445d","store_item_id":"ttt","count":1}\]&platform=android&projectId=f1df9464-40a8-4a66-8421-196c7c661002&store=google&userId=2d485044-06c2-48c4-a6ed-4ab53dea88bb


#### Response<a name="Response2"></a>


Return a response in the following format.

```javascript
{
    "status": 1,
    "message" : ""
}
```

| Attribute | Type   | Description                        |
| :-------- | :----- | :--------------------------------- |
| status    | Int    | Result \(0: Failed, 1: Succeeded\) |
| message   | String | Error message                      |

## Game server > GAMEPOT server<a name="Gameserver>GAMEPOTserver"></a>


### Gamepot user ID verification\(optional\)<a name="TokenAuthenticationoptional"></a>


Using the information provided after login has been completed in your game, you can request the GAMEPOT server to verify the login.

Token authentication is processed in two steps: step 1 is GAMEPOT token authentication and step 2 is social token authentication.



 >For step 2, you should add a value in Project settings > Auth key of your GAMEPOT dashboard in advance.


Step 1 GAMEPOT Token Validation occurs when the sync token has been authenticated using a MemberID and the token obtained after login.

Step 2 of the social token authentication requires using a token from a social media account obtained after logging in to Google or Facebook.

If step 2 authentication fails, GAMEPOT blocks the user from logging in the game.



>The feature to block users after authentication fails works only when Project settings > Auth key is turned on in your GAMEPOT dashboard. You can check blocked users in Member > Block of the GAMEPOT dashboard.


**Do not synchronize step 1 authentication!**

This is the process for user log in. Synchronizing will create delays in the network communication thereby causing game play issues. Also, the network connection is physically separated, so the network connection is much more likely to be unstable.

Process the function asynchronously and implement it in a restrictive format.

#### Request<a name="Request3"></a>


For data integrity, the request should be made in the developer server, rather than to the client.

```text
POST
url : https://gamepot.apigw.ntruss.com/gpapps/v1/loginauth
Header : 'content-type: application/json'
data:
{
    "projectId": {GamePot SDK's projectId},
    "memberId": {GamePot SDK's memberid},
    "token": {GamePot SDK's Token}
}
```

| Attribute | Type   | Max Length | Description             |
| :-------- | :----- | :--------- | :---------------------- |
| projectId | String | 128        | GamePot SDK's projectId |
| memberId  | String | 128        | GamePot SDK's memberid  |
| token     | String | 2048       | GamePot SDK's Token     |

#### Response<a name="Response3"></a>


If step 1 authentication fails, the status will be set to a value other than 1.

In this case, restrict the user from entering the game.

```javascript
{
    "status": 1,
    "message" : ""
}
```

| Attribute | Type   | Description                                                         |
| :-------- | :----- | :------------------------------------------------------------------ |
| status    | Int    | Result \(1: Succeeded. Refer to Error code below for other cases.\) |
| message   | String | Error message                                                       |

#### Error code<a name="Errorcode1"></a>


| Code | Description                                                                                                                                                                         |
| :--- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0    | Required data is omitted from the body. Be sure that the projectId, memberId and token are all specified when making a request.                                                     |
| -1   | Token authentication failed. A fake token is used.                                                                                                                                  |
| -2   | MemberId authentication failed. The token’s MemberId does not match the MemberId in the body.                                                                                       |
| -3   | Token expired. There will be a time difference of more than 10 minutes from the time when the SDK login api was successful and the time when the authentication check is requested. |

### ThirdParty Purchase<a name="ThirdPartyPurchase"></a>




>It is not a common feature, so contact GAMEPOT before applying it.


#### Request<a name="Request"></a>

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

| Header    | Type   | Required | Description                             |
| :-------- | :----- | :------- | --------------------------------------- |
| x-api-key | String | O        | An authentication key issued by GamePot |

<br/>

| Attribute     | Type   | Max Length | Required | Description                      |
| :------------ | :----- | :--------- | :------- | :------------------------------- |
| projectId     | String | 128        | O        | GamePot SDK's projectId          |
| store         | String | 64         | O        | Store for payment                |
| productId     | String | 256        | O        | ID of the purchased items        |
| transactionId | String | 512        | O        | Unique ID of the payment         |
| memberId      | String | 128        | O        | GamePot SDK's memberid           |
| currency      | String | 64         | X        | Currency of the payment          |
| price         | Number | -          | X        | Amount of payment                |
| paymentId     | String | 64         | X        | Payment Method                   |
| uniqueId      | String | 512        | X        | In-game unique ID of the payment |

#### Response<a name="Response4"></a>


```javascript
{
    "status": 1,
    "message" : ""
}
```

| Attribute | Type   | Description                                                         |
| :-------- | :----- | :------------------------------------------------------------------ |
| status    | Int    | Result \(1: Succeeded. Refer to Error code below for other cases.\) |
| message   | String | Error message                                                       |

#### Error code<a name="Errorcode2"></a>


| Code | Description                                                                                                                              |
| :--- | :--------------------------------------------------------------------------------------------------------------------------------------- |
| -1   | Required data is omitted from the body. <br/> Be sure that projectId, transactionId, productId, store, and memberId are all specified. ¬ |
| -2   | The price value is not a number type.<br/> Specify a number type.                                                                        |
| -3   | No projectId.<br/> Check the projectId entered again.                                                                                    |
| -4   | The project does not support the api.<br/> Contact GAMEPOT.                                                                              |
| -5   | The transactionId already exists.                                                                                                        |
| -6   | DB error. Contact GAMEPOT.                                                                                                               |
