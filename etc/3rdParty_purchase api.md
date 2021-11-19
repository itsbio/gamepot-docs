# 3rdParty_Purchase API 

3자 SDK를 통해 발생한 결제 이력을 게임팟 대시보드이 이력을 남기기 위한 기능 

#### Request

 - Method : POST
 - URI : https://gamepot.apigw.ntruss.com/gpapps/v2/thirdparty/purchase

```text
PUT
url : https://gamepot.apigw.ntruss.com/gpapps/v2/thirdparty/purchase
Header : 'Content-Type: application/json'
Header : 'x-api-key: U4niFBmP7mkrNpofkp4qjd37nGJvchiLMPyc69kdwZ9bf9wHqiwu7nNaNi'
data:
{
     "projectId": "c3a931d5-66bf-41af-88bd-9f1aee20e18c",
     "store": "pc",
     "productId": "purchase_001",
     "transactionId": "t-123412812-sadl-2384-75847",
     "memberId":"89a907ed-0e1d-42fb-ae4d-75e95581220d",
     "currency": "KRW",
     "price":1000,
     "paymentId": "prepaid",
     "uniqueId": ""

}
```
| Attribute    | Type   | Required | Description                  |
| :-------- | :----- | :------- | :--------------------------- |
| projectId  | String | O        |   GamePot SDK의 projectId   |
| store  | String | O        |   결제 스토어   |
| productId  | String | O        |   결제 아이템 아이디   |
| transactionId  | String | O        |   결제 고유 아이디   |
| memberId  | String | O        |   GamePot SDK의 memberId   |
| currency  | String | X        |   결제 통화   |
| price  | String | X        |   결제 금액   |
| paymentId  | String | X        |   결제 수단   |
| uniqueId  | String | X        |   게임내 결제 고유 아이디   |



#### Response

성공

```javascript
{
  "status": 1,
  "message" : ""
}
```

| Attribute       | Type    | Description                                     |
| :---------------| :------ | :---------------------------------------------- |
| status          | Int     | 결과값 \(1: 성공, 실패는 Error code 참고\)            |
| message        | String  | 오류 내용    |


실패
```javascript
{
  "status": -5,
  "message": "The order id already exist"
}
```

| Attribute | Type   | Description                                     |
| :-------- | :----- | :---------------------------------------------- |
| status    | Int    | 결과값 \(1: 성공, 실패시 Error code 참고\)            |
| message   | String | 오류 내용                                         |



#### Error code

| Code | Description                                                       |
| :--- | :---------------------------------------------------------------- |
| -1  | Body에 누락된 데이터가 있는 경우 projectId, transactionId, productId, store, memberId을 모두 었는지 확인하세요.                    |
| -2  | price 값이 number타입이 아닌 경우 number타입으로 넣으세요.        |
| -3  | projectId가 없는 경우 입력한 projectId를 다시 확인하세요.         |
| -4  | 프로젝트가 해당 api를 지원하지 않는 경우 GAMEPOT에 문의해주세요.         |
| -5  | transactionId가 이미 존재하는 경우         |
| -6  | DB오류. GAMEPOT에 문의해주세요.        |
| -99  | x-api-key 권한 오류         |




