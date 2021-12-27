### 이메일 계정 비밀번호 초기화 API

이메일 계정 비밀번호 초기화

#### Request

 - Method : POST
 - URI : /forgetpassword/local

```text
POST
url : https://itoxi-api.gamepot.io/v1/forgetpassword/local
Header : 'accept-language: ko'
Header : 'Content-Type: application/x-www-form-urlencoded'
data-urlencode 'projectId=XXXXXXX' \
data-urlencode 'id=XXXXXXXXXXXXX' \
data-urlencode 'verifyKey=wn+Kxh4SLzy8lEf7RM+iYEQdSrqCiADlOj418P1Plk4xUxs5ppoOe4vShvGqWGw9fAQjmgc4dzmntXFdwzpO/g==' \
data-urlencode 'newPassword=abcd1'
```


| data | Type   | Description                             |
| :-------- | :----- | :---------------------------------------|
| projectId | String | 프로젝트 아이디     |
| id        | String | 이메일 계정        |
| verifyKey | String | 본인인증 CI        |
| newPassword  | String | 신규 패스워드    |






#### Response

성공

```javascript
{
    "status": 1,
    "message": "비밀번호가 정상적으로 변경되었습니다."
}
```

| Attribute       | Type    | Description                                     |
| :---------------| :------ | :---------------------------------------------- |
| status          | Int     | 결과값 \(1: 성공, 실패는 Error code 참고\)            |

실패
```javascript
{
    "status": -6,
    "message": "사용할 수 없는 비밀번호 입니다."
}
```

| Attribute | Type   | Description                                     |
| :-------- | :----- | :---------------------------------------------- |
| status    | Int    | 결과값 \(1: 성공, 실패는 Error code 참고\)        |
| message   | String | 오류 내용                                         |

#### Error code

| Code | Description                                                       |
| :--- | :---------------------------------------------------------------- |
| -1   | 파라미터 누락                                |
| -4   | 본인인증 CI 값 오류                           |
| -6   | 사용할 수 없는 비밀번호 / 회원정보 확인 불가        |