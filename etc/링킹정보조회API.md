# 링킹 정보 조회 API 

로그인한 사용자 아이디의 링킹 정보 획득

#### Request

 - Method : GET
 - URI : {domain}/v1/api/project/{projectid}/linkings

```text
예시)

GET
url : https://itoxi-api.gamepot.io/v1/api/project/8cb9cf0d-ea73-4c4f-b1ef-66785ee6013f/linkings
Header : 'Authorization: Bearer: {로그인 성공 후 토큰}'

```
| Attribute    | Type   | Required | Description                  |
| :-------- | :----- | :------- | :--------------------------- |
| projectId  | String | O        |   GamePot SDK의 projectId   |

| Header    | Type   | Required | Description                  |
| :-------- | :----- | :------- | :--------------------------- |
| Authorization: Bearer| String | O        |   로그인 이후 획득한 토큰    |



#### Response

성공

```javascript
{
    "status": 1,
    "result": {
        "edges": [
            {
                "node": {
                    "id": "TGlua2luZzpjZWM4NWE3ZS1iOWEzLTQyYmMtOTFkOS01OGJiMzBiYTcyYzc=",
                    "username": "XXXXXXX",
                    "provider": "email"
                }
            }
        ]
    }
}
```

| Attribute       | Type    | Description                                     |
| :---------------| :------ | :---------------------------------------------- |
| status          | Int     | 결과값 \(1: 성공, 실패는 Error code 참고\)            |
| username        | String  | 소셜 아이디 정보 ( 이메일 로그인의 경우 암호화된 값을 전달)    |
| provider        | String  | 링킹 타입 정보 ( google , facebook, email ....)   |


실패
```javascript
{
    "status": -1,
    "message": "token is required."
}
```

| Attribute | Type   | Description                                     |
| :-------- | :----- | :---------------------------------------------- |
| status    | Int    | 결과값 \(1: 성공, 실패시 Error code 참고\)            |
| message   | String | 오류 내용                                         |



#### Error code

| Code | Description                                                       |
| :--- | :---------------------------------------------------------------- |
| -1  | 토큰 장보 누락                   |
| -9  | 잘못된 토큰 정보        |





