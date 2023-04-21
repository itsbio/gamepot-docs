### 회원 탈퇴 API

회원 탈퇴

#### Request

 - Method : DELETE
 - URI : /v1/api/project/{projectId}/user/{UserId}

```text
POST
url : https://gamepot.apigw.ntruss.com/gpapps/v1/v1/api/project/{projectId}/user/{UserId}
Header : 'accept-language: ko'
Header : 'Authorization: Bearer {token}' // {token} 부분은 로그인 이후 획득한 토큰으로 교체
```

| Header    | Type   | Required | Description                  |
| :-------- | :----- | :------- | :--------------------------- |
| Authorization: Bearer| String | O        |   로그인 이후 획득한 토큰    |

| Attribute | Type   | Description                             |
| :-------- | :----- | :---------------------------------------|
| projectId | String | GamePot SDK의 projectId                  |
| UserId | String | 탈퇴를 진행할 사용자 ID                  |

#### Response

성공

```javascript
{
  "status":1,
  "result":
  {
    "member":
      {
       "id":"TWVtYmVyOmVkZWNkODY4LTJmMmYtNGRhMi1hYjc5LWMwYzYxZTZiY2RlZQ=="
      },
    "withdrewAt":1614913841
  }
}
```

| Attribute       | Type    | Description                                     |
| :---------------| :------ | :---------------------------------------------- |
| status          | Int     | 결과값 \(1: 성공, 실패는 Error code 참고\)            |
| withdrewAt      | String  | 회원 탈퇴 완료 시각  ( 프로젝트 설정에 따라 null 될 수 있음)   |

실패
```javascript
{
  "status":-100,
  "message":"이미 탈퇴가 진행중입니다.",
  "errorcode":400
}
```

| Attribute | Type   | Description                                     |
| :-------- | :----- | :---------------------------------------------- |
| status    | Int    | 결과값 \(1: 성공, 실패는 Error code 참고\)        |
| message   | String | 오류 내용                                         |
| errorcode | String | 에러 코드    (해당 정보가 없을 수도 있습니다.)            |

#### Error code

| Code | Description                                                       |
| :--- | :---------------------------------------------------------------- |
| -100 | 회원 탈퇴 실패                                                   |
| -1   | 토큰 정보가 없을때                               |
| -9   | 잘못된 토큰 또는 잘못된 요청         |