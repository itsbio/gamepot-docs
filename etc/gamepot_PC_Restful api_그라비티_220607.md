# GAMEPOT ( PC ) Restful API 

### 이메일 회원가입 

이메일 회원가입 기능 사용시 게임팟에 사용 문의 필요

네이버 클라우드 Cloud Outbound Mailer 서비스 신청이 되어 있어야 하며 인증 이메일 발송을 위한 셋팅이 필요


#### Request

 - Method : POST
 - URI : /v1/signup/local

```text
POST 
url :'https://gravity-api.gamepot.io/v1/signup/local' 
--header 'language: ko' 
--header 'Content-Type: application/x-www-form-urlencoded' 
--data-urlencode 'projectId=XXXX' 
--data-urlencode 'storeId=pc' \
--data-urlencode 'username=XXXX@itsb.io' 
--data-urlencode 'password=XXXX!@#' 
--data-urlencode 'nickname=XXXX1231'
--data-urlencode 'returnURL=XXXXXX'
```
| Header    | Type   | Required | Description                  |
| :-------- | :----- | :------- | :--------------------------- |

| data      | Type   | Description                  |
| :-------- | :----- | :--------------------------- |
| projectId | String | GamePot SDK의 projectId      |
| storeId   | String | 스토어 정보                     |
| username  | String | 이메일 정보   |
| password  | String | 비밀번호   |
| nickname  | String | 닉네임   |
| returnURL | String | 이메일 인증 이후 처리를 하기 위한 URL / get 형식으로 관련 정보 전달 (ex. http://dwww.gamepot.io/callback/signup?email=jyj1127jph2@gmail.com&message=인증을 완료 했습니다. 로그인을 진행하세요.&status=1 )   |



#### Response

성공

```javascript
{
    "status": 1,
    "message": "이메일을 발송 했습니다. 인증을 진행하세요.",
    "id": "2a210dfb-2ec8-471a-XXXXXXXX",
    "projectId": "XXXXXXXXXXXXX",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhZ3JlZSI6eyJ0ZXJtc29mdXNlIjoiTiIsInByaXZhY3lwb2xpY3kiOiJOIn0sImdkcHIiOnsic3RhdHVzIjowLCJjaGVja2VkX3N0b3J5X2NhdGVnb3J5X2lkcyI6W119LCJsb2NhbCI6eyJzdGF0dXMiOjB9LCJwdXNoIjp0cnVlLCJuaWdodCI6ZmFsc2UsImFkIjp0cnVlLCJkZWxldGVkIjpmYWxzZSwibWFuYWdlciI6ZmFsc2UsInNhbmRib3giOmZhbHNlLCJfaWQiOiI2MWE1ZDYyNDcxZGFmZGRlMGE2YTJmMzIiLCJ1c2VybmFtZSI6IiIsInBhc3N3b3JkIjoiJDJiJDA0JFZXVVBoZ0JIaXRZM01heGVTZFJkRE85RjNlZ3B3V2FTNXJBejBSRS5HZmdEb1BxdFZTNEZDIiwicHJvamVjdF9pZCI6ImJmNTU2YzM5LTg5YjAtNDIxZi05YjliLTBjNTcyMTMyNmZkOSIsInN0b3JlX2lkIjoicGMiLCJpZCI6IjJhMjEwZGZiLTJlYzgtNDcxYS04MzZkLThhOWU2M2JmZmQzMSIsInJlbW90ZWlwIjoiMTE2LjEyNC41MC4xMzAiLCJsb2dpbmVkQXQiOiIyMDIxLTExLTMwVDA3OjQzOjMyLjU2MloiLCJjb3VudHJ5IjoiS1IiLCJjcmVhdGVkQXQiOiIyMDIxLTExLTMwVDA3OjQzOjMyLjU2NVoiLCJ1cGRhdGVkQXQiOiIyMDIxLTExLTMwVDA3OjQzOjMyLjU2NVoiLCJfX3YiOjAsImlhdCI6MTYzODI1ODIxMiwiZXhwIjoxNjQ2MDM0MjEyfQ.0Ar6vhmTIhgDfBA5sE21DoO4C2zfEjVmuXNIWGE9fd4"
}
```

| Attribute       | Type    | Description                                     |
| :---------------| :------ | :---------------------------------------------- |
| status          | Int     | 결과값 \(1: 성공, 실패는 Error code 참고\)            |
| message         | String  | 메시지     |
| id              | String  | 게임팟 사용자 아이디     |
| token           | Boolean | 로그인 이후 획득한 토큰 |
| projectId       | String | GamePot SDK의 projectId      |



실패
```javascript
{
    "error": {
        "status": -4,
        "message": "사용 중인 이메일 입니다."
    }
}
```

| Attribute | Type   | Description                                     |
| :-------- | :----- | :---------------------------------------------- |
| status    | Int    | 결과값 \(1: 성공, 실패시 Error code 참고\)            |
| message   | String | 오류 내용                                         |



#### Error code

| Code | Description                                                       |
| :--- | :---------------------------------------------------------------- |
| -1  | 데이터가 부족한 경우      |
| -3  | 프로젝트 아이디 정보 필요      |
| -4  | 사용 중인 이메일 입니다.      |
| -5  | 사용할 수 없는 닉네임인 경우.      |
| -6  | 이메일 발송 실패한 경우.      |
| -7  | 요청 데이터에 닉네임이 없는 경우      |
| -8  | 이미 사용 중인 닉네임 입니다.     |
| -9  | 서버 오류    |
| -11  | 올바르지 않은 이메일 입니다.                    |
| -12  | 사용할 수 없는 비밀번호 입니다.         |





### 이메일 회원가입 - 인증 이메일 재 발송

이메일 회원가입 - 인증 이메일 재 발송

#### Request

 - Method : POST
 - URI : /v1/resend/mail/local

```text
POST 
url : 'https://gravity-api.gamepot.io/v1/resend/mail/local' \
--header 'language: ko' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'projectId=XXXX' \
--data-urlencode 'username=XXXX' \
--data-urlencode 'returnURL=http://dwww.gamepot.io/callback/signup'
```
| Header    | Type   | Required | Description                  |
| :-------- | :----- | :------- | :--------------------------- |

| data      | Type   | Description                  |
| :-------- | :----- | :--------------------------- |
| projectId | String | GamePot SDK의 projectId      |
| username  | String | 이메일 정보   |
| returnURL | String | 이메일 인증 이후 처리를 하기 위한 URL / get 형식으로 관련 정보 전달 (ex. http://dwww.gamepot.io/callback/signup?email=jyj1127jph2@gmail.com&message=인증을 완료 했습니다. 로그인을 진행하세요.&status=1 )   |



#### Response

성공

```javascript
{
    "status": 1,
    "message": "이메일을 발송 했습니다. 인증을 진행하세요."
}
```

| Attribute       | Type    | Description                                     |
| :---------------| :------ | :---------------------------------------------- |
| status          | Int     | 결과값 \(1: 성공, 실패는 Error code 참고\)            |
| message         | String  | 메시지     |



실패
```javascript
{
    "error": {
        "status": -4,
        "message": "이미 인증을 완료하였습니다."
    }
}
```

| Attribute | Type   | Description                                     |
| :-------- | :----- | :---------------------------------------------- |
| status    | Int    | 결과값 \(1: 성공, 실패시 Error code 참고\)            |
| message   | String | 오류 내용                                         |



#### Error code

| Code | Description                                                       |
| :--- | :---------------------------------------------------------------- |
| -1  | 데이터가 부족합니다.      |
| -2  | 프로젝트 아이디 없는 경우.      |
| -3  | 존재하지 않는 회원인 경우.      |
| -4  | 이미 인증을 완료하였습니다.      |
| -5  | 이메일 발송 실패      |
| -6  | 계정 연동 정보가 없는 경우      |





### 이메일 로그인

이메일 로그인

#### Request

 - Method : POST
 - URI : /v1/login/local

```text
POST 
url : 'https://gravity-api.gamepot.io/v1/login/local' 
--header 'language: ko' 
--header 'Content-Type: application/x-www-form-urlencoded' 
--data-urlencode 'projectId=XXXXXXX' \
--data-urlencode 'storeId=pc' 
--data-urlencode 'username=XXXXXX' 
--data-urlencode 'password=XXXXX'
```
| Header    | Type   | Required | Description                  |
| :-------- | :----- | :------- | :--------------------------- |

| data      | Type   | Description                  |
| :-------- | :----- | :--------------------------- |
| projectId | String | GamePot SDK의 projectId      |
| storeId   | String | 스토어정보      |
| username  | String | 이메일 정보   |
| password | String | 비밀번호   |



#### Response

성공

```javascript
{
    "id": "09d04b1c-69b7-48af-XXXXXXXXXX",
    "projectId": "XXXXXXXX",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhZ3JlZSI6eyJ0ZXJtc29mdXNlIjoiTiIsInByaXZhY3lwb2xpY3kiOiJOIn0sImdkcHIiOnsic3RhdHVzIjowLCJjaGVja2VkX3N0b3J5X2NhdGVnb3J5X2lkcyI6W119LCJsb2NhbCI6eyJzdGF0dXMiOjIsImVtYWlsX2NlcnRfZXhwaXJlZF9hdCI6bnVsbCwiZW1haWxfY2VydF9rZXkiOm51bGx9LCJwdXNoIjp0cnVlLCJuaWdodCI6ZmFsc2UsImFkIjp0cnVlLCJkZWxldGVkIjpmYWxzZSwibWFuYWdlciI6ZmFsc2UsInNhbmRib3giOmZhbHNlLCJfaWQiOiI2MWE1ZDcxNzI1YWQ1NTQwMzIxMzA5NTEiLCJ1c2VybmFtZSI6IiIsInBhc3N3b3JkIjoiJDJiJDA0JGJOY2xjVEZrQndrLndkWWNCTndNY09mNEhoTGdxdWNOMW5TWFF6cG10ZC5veEdyenFEM0dLIiwicHJvamVjdF9pZCI6ImJmNTU2YzM5LTg5YjAtNDIxZi05YjliLTBjNTcyMTMyNmZkOSIsInN0b3JlX2lkIjoicGMiLCJpZCI6IjA5ZDA0YjFjLTY5YjctNDhhZi1iYmQzLWI5MzRiZTI3NmZkNSIsInJlbW90ZWlwIjoiMTE2LjEyNC41MC4xMzAiLCJsb2dpbmVkQXQiOiIyMDIxLTExLTMwVDA3OjQ3OjM1LjUyN1oiLCJjb3VudHJ5IjoiS1IiLCJjcmVhdGVkQXQiOiIyMDIxLTExLTMwVDA3OjQ3OjM1LjQ5NFoiLCJ1cGRhdGVkQXQiOiIyMDIxLTExLTMwVDA3OjQ3OjQ2LjI3N1oiLCJfX3YiOjAsIm5pY2tuYW1lIjoiMnMyczNzMnMiLCJpYXQiOjE2MzgyNjA5NzgsImV4cCI6MTY0NjAzNjk3OH0.ywuWjI24F5lvWeUkiIbjo9hOOclp57i-uExCJcBb_z4",
    "email": "XXXXXXXX",
    "verify": "N",
    "agree": "N",
    "providerId": "XXXXXXXXX",
    "provider": "email",
    "nickname": "2s2s3s2s"
}
```

| Attribute       | Type    | Description                                     |
| :---------------| :------ | :---------------------------------------------- |
| id              | String     | 게임팟 사용자 아이디           |
| projectId       | String | GamePot SDK의 projectId                  |
| token          | String | GamePot SDK의 projectId                  |
| email          | String | 로그인시 사용한 이메일 주소 정보                  |
| providerId     | String | 로그인시 사용한 이메일 주소 정보                 |
| provider     | String | 로그인 타입 정보                  |
| nickname     | String | 닉네임                  |




실패
```javascript
{
    "error": {
        "status": -4,
        "message": "존재하지 않는 회원입니다."
    }
}
```

| Attribute | Type   | Description                                     |
| :-------- | :----- | :---------------------------------------------- |
| status    | Int    | 결과값 \(1: 성공, 실패시 Error code 참고\)            |
| message   | String | 오류 내용                                         |



#### Error code

| Code | Description                                                       |
| :--- | :---------------------------------------------------------------- |
| -1  | 데이터가 부족합니다. / 프로젝트 아이디가 없는 경우      |
| -2  | 멤버 아이디가 없는 경우 / 점검 설정 사항일때      |
| -3  | 이메일 인증 미완료.      |
| -4  | 계정 연동 정보 없는 경우    |
| -5  | 비밀번호가 틀린 경우.      |
| -9  | 서버 오류    |
| -11  | 올바르지 않은 이메일 입니다.                    |
| -12  | 사용할 수 없는 비밀번호 입니다.         |


### 닉네임 설정 API

사용자 닉네임 설정

#### Request

 - Method : PUT
 - URI : /v1/api/project/{projectId}/store/pc/user

```text
PUT
url : https://gravity-api.gamepot.io/v1/api/project/{projectId}/store/pc/user
Header : 'accept-language: ko'
Header : 'Content-Type: application/json'
Header : 'Authorization: Bearer {token}' // {token} 부분은 로그인 이후 획득한 토큰으로 교체
body : { "nickname":"{닉네임}" }
```
| Header    | Type   | Required | Description                  |
| :-------- | :----- | :------- | :--------------------------- |
| Authorization: Bearer| String | O        |   로그인 이후 획득한 토큰    |

| Attribute | Type   | Description                             |
| :-------- | :----- | :---------------------------------------|
| projectId | String | GamePot SDK의 projectId                  |

| body    | Type   | Required | Description                  |
| :-------- | :----- | :------- | :--------------------------- |
| nickname  | String | O        |   닉네임   |


#### Response

성공

```javascript
{
  "status":1,
    "result":
    {
      "member":
      {
        "id":"TWVtYmVyOjBjNTJlYjAyLWVlOTEtNDhjZi05MjcwLTQzZGQwODNkODhhMg==",
        "push":true,
        "night":false,
        "ad":true,
        "nickname":"닉네임12"
      }
  }
}
```

| Attribute       | Type    | Description                                     |
| :---------------| :------ | :---------------------------------------------- |
| status          | Int     | 결과값 \(1: 성공, 실패는 Error code 참고\)            |
| push            | Boolean | -  광고성 이벤트 푸시 설정 상태 ( PC 프로젝트는 무시)      |
| night           | Boolean | -  광고성 이벤트 야간 푸시 설정 상태 ( PC 프로젝트는 무시 ) |
| ad              | Boolean | -  광고성 푸시 설정  상태( PC 프로젝트는 무시 )           |
| nickname        | String  | 설정한 닉네임    |


실패
```javascript
{
  "status":-100,
  "message":"닉네임은 2자리이상 8자 이하로 입력해 주세요.",
  "errorcode":400
}
```

| Attribute | Type   | Description                                     |
| :-------- | :----- | :---------------------------------------------- |
| status    | Int    | 결과값 \(1: 성공, 실패시 Error code 참고\)            |
| message   | String | 오류 내용                                         |



#### Error code

| Code | Description                                                       |
| :--- | :---------------------------------------------------------------- |
| -1  | 토큰 정보 누락                    |
| -9  | 잘못된 토큰 또는 잘못된 요청         |
| -100  | 닉네임변경 실패 (message :닉네임은 2자리이상 8자 이하로 입력해 주세요. / 이미 사용 중인 닉네임 입니다. )      |



### 회원 탈퇴 API

회원 탈퇴

#### Request

 - Method : DELETE
 - URI : /v1/api/project/{projectId}/user/{UserId}

```text
POST
url : https://gravity-api.gamepot.io/v1/api/project/{projectId}/user/{UserId}
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
    "withdrewAt":null
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
    "message":"Membership information not found.",
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


** 회원탈퇴 후 동일한 사용자 아이디로 로그인 시도시 아래와 같은 오류 결과 처리가 진행됩니다.
status 값이 -409 일때 탈퇴 철회관련 로직을 진행해주세요.
```javascript
{
    "error": {
        "status": -409,
        "message": "{\"projectId\":\"75d18134-9e49-4be2-b614-7cc5ad2901dc\",\"id\":\"7aece54e-07e6-4690-8479-565b07b15d25\",\"message\":\"탈퇴가 진행중입니다. 탈퇴를 철회하고자 하는 경우 철회 버튼을 누르세요.\",\"withdrewAt\":1615193029,\"token\":\"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhZ3JlZSI6eyJ0ZXJtc29mdXNlIjoiTiIsInByaXZhY3lwb2xpY3kiOiJOIn0sInZlcmlmeSI6eyJrZXkiOiJ3bitLeGg0U0x6eThsRWY3Uk0raVlFUWRTcnFDaUFEbE9qNDE4UDFQbGs0eFV4czVwcG9PZTR2U2h2R3FXR3c5ZkFRam1nYzRkem1udFhGZHd6cE8vZz09IiwidXBkYXRlZEF0IjoiMjAyMC0wOS0yMlQwNToxMzo1My43MjFaIn0sImdkcHIiOnsic3RhdHVzIjowLCJjaGVja2VkX3N0b3J5X2NhdGVnb3J5X2lkcyI6W10sImNoZWNrZWRfY2F0ZWdvcnlfaWRzIjpbXX0sImxvY2FsIjp7InN0YXR1cyI6MiwiZW1haWxfY2VydF9leHBpcmVkX2F0IjpudWxsLCJlbWFpbF9jZXJ0X2tleSI6bnVsbH0sInB1c2giOnRydWUsIm5pZ2h0IjpmYWxzZSwiYWQiOnRydWUsImRlbGV0ZWQiOmZhbHNlLCJtYW5hZ2VyIjpmYWxzZSwic2FuZGJveCI6ZmFsc2UsIl9pZCI6IjVmNjk4NzlhY2NhNGYzMDVhMWZiNmM3ZCIsInVzZXJuYW1lIjoiIiwicGFzc3dvcmQiOiIkMmIkMDQka0RZOUhpand4UGQ1cUhWQ2JrQ0pYZXhTOElwY3NObXJLSWZYSDFnWG53V0V0Y1FOT0t2RHkiLCJwcm9qZWN0X2lkIjoiNzVkMTgxMzQtOWU0OS00YmUyLWI2MTQtN2NjNWFkMjkwMWRjIiwic3RvcmVfaWQiOiJwYyIsImlkIjoiN2FlY2U1NGUtMDdlNi00NjkwLTg0NzktNTY1YjA3YjE1ZDI1IiwicmVtb3RlaXAiOiIyMjAuNzYuNTIuMTYzIiwibG9naW5lZEF0IjoiMjAyMS0wMy0wOFQwNzo0MzowNi41MTlaIiwiY291bnRyeSI6IktSIiwiY3JlYXRlZEF0IjoiMjAyMC0wOS0yMlQwNToxMTo1NC42MTdaIiwidXBkYXRlZEF0IjoiMjAyMS0wMy0wOFQwNzo0Mzo0OS4wNDVaIiwiX192IjoxLCJuaWNrbmFtZSI6ImFiY2RlIiwid2l0aGRyZXdBdCI6IjIwMjEtMDMtMDhUMDg6NDM6NDkuMDQ1WiIsImlhdCI6MTYxNTE4OTQzNSwiZXhwIjoxNjIyOTY1NDM1fQ.SOEuWDp7CYWy4tC2moY5R1__4HtlsX-zpflqs4PV_4o\"}"
    }
}
```
| Attribute | Type   | Description                                     |
| :-------- | :----- | :---------------------------------------------- |
| projectId  | String | 프로젝트 아이디         |
| withdrewAt | String | 회원탈퇴 시간          |
| token      | String | 로그인 후 생성된 토큰    |
| message    | String | 오류 관련 메시지    |






### 탈퇴 철회 API

회원 탈퇴 철회

#### Request

 - Method : PUT
 - URI : /v1/api/project/{projectId}/user/{UserId}/withdraw

```text
POST
url : https://gravity-api.gamepot.io/v1/api/project/{projectId}/user/{UserId}/withdraw
Header : 'accept-language: ko'
Header : 'Authorization: Bearer {token}' // {token} 부분은 로그인 이후 획득한 토큰으로 교체
```

| Header    | Type   | Required | Description                  |
| :-------- | :----- | :------- | :--------------------------- |
| Authorization: Bearer| String | O        |   로그인 이후 획득한 토큰    |

| Attribute | Type   | Description                             |
| :-------- | :----- | :---------------------------------------|
| projectId | String | GamePot SDK의 projectId                  |
| UserId | String | 탈퇴 철회할 사용자 ID                  |

#### Response

성공

```javascript
{
  "status":1,
    "result":
    {
      "member":
      {
        "id":"TWVtYmVyOjBjNTJlYjAyLWVlOTEtNDhjZi05MjcwLTQzZGQwODNkODhhMg=="
      }
  }
}
```

| Attribute       | Type    | Description                                     |
| :---------------| :------ | :---------------------------------------------- |
| status          | Int     | 결과값 \(1: 성공, 실패는 Error code 참고\)            |


실패
```javascript
{
  "status":-100,
  "message":"회원 정보를 찾을 수 없습니다.",
  "errorcode":406
}
```

| Attribute | Type   | Description                                     |
| :-------- | :----- | :---------------------------------------------- |
| status    | Int    | 결과값 \(1: 성공, 실패는 Error code 참고\)           |
| message   | String | 오류 내용                                         |
| errorcode | String | 에러 코드    (해당 정보가 없을 수도 있습니다.)            |

#### Error code

| Code | Description                                                       |
| :--- | :---------------------------------------------------------------- |
| -100 | 회원 탈퇴 철회 실패                                                  |
| -1   | 토큰 정보가 없을때                               |
| -9   | 잘못된 토큰 또는 잘못된 요청         |





### 점검 API

점검 상태 확인

#### Request

 - Method : GET
 - URI : /v1/api/project/{projectId}/store/pc/maintenance

```text
POST
url : https://gravity-api.gamepot.io/v1/api/project/{projectId}/store/pc/maintenance
Header : 'accept-language: ko'
Header : 'Authorization: Bearer {token}' // {token} 부분은 로그인 이후 획득한 토큰으로 교체
```

| Header    | Type   | Required | Description                  |
| :-------- | :----- | :------- | :--------------------------- |
| Authorization: Bearer| String | O        |   로그인 이후 획득한 토큰    |

| Attribute | Type   | Description                             |
| :-------- | :----- | :---------------------------------------|
| projectId | String | GamePot SDK의 projectId                  |

#### Response

성공

```javascript
점검이 아닌 경우
{
  "status":1,
  "result":null
}

점검 설정이 된 경우
{
  "status":1,
  "result":
  {
    "message":"점검중",
    "url":"https://rob.gnjoy.com/Community/BoardDetail/301",
    "startedAt":"1614578880",
    "endedAt":"1615874880"
  }
}

```

| Attribute       | Type    | Description                                     |
| :---------------| :------ | :---------------------------------------------- |
| status          | Int     | 결과값 \(1: 성공, 실패는 Error code 참고\)            |
| message       | String | 점검 메시지 문구                  |
| url           | String | 자세히 URL에 설정된 주소           |
| startedAt     | String | 점검 시작 시간                   |
| endedAt       | String | 점검 종료 시간                    |

실패
```javascript
{
    "status": -1,
    "message": "token is required."
}
```

| Attribute | Type   | Description                                     |
| :-------- | :----- | :---------------------------------------------- |
| status    | Int    | 결과값 \(1: 성공, 실패는 Error code 참고\)        |
| message   | String | 오류 내용                                         |

#### Error code

| Code | Description                                                       |
| :--- | :---------------------------------------------------------------- |
| -1   | 토큰 정보가 없을때                               |
| -9   | 잘못된 토큰 또는 잘못된 요청         |



### 사용자 토큰 확인 API

사용자 토큰 확인 API

#### Request

 - Method : POST
 - URI : /v1/api/project/{projectid}/auth/token

```text
POST
url : https://gravity-api.gamepot.io/v1/api/project/{projectid}/auth/token
Header : 'accept-language: ko'
Header : 'Content-Type: application/json'
body : 
{
	"memberId":"7aece54e-07e6-XXXX-XXXX-XXXXXXX",
	"token":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhZ3JlZSI6eyJ0ZXJtc29mdXNlIjoiTiIsInByaXZhY3lwb2xpY3kiOiJOIn0sInZlcmlmeSI6eyJrZXkiOiJ3bitLeGg0U0x6eThsRWY3Uk0raVlFUWRTcnFDaUFEbE9qNDE4UDFQbGs0eFV4czVwcG9PZTR2U2h2R3FXR3c5ZkFRam1nYzRkem1udFhGZHd6cE8vZz09IiwidXBkYXRlZEF0IjoiMjAyMC0wOS0yMlQwNToxMzo1My43MjFaIn0sImdkcHIiOnsic3RhdHVzIjowLCJjaGVja2VkX3N0b3J5X2NhdGVnb3J5X2lkcyI6W10sImNoZWNrZWRfY2F0ZWdvcnlfaWRzIjpbXX0sImxvY2FsIjp7InN0YXR1cyI6MiwiZW1haWxfY2VydF9leHBpcmVkX2F0IjpudWxsLCJlbWFpbF9jZXJ0X2tleSI6bnVsbH0sInB1c2giOnRydWUsIm5pZ2h0IjpmYWxzZSwiYWQiOnRydWUsImRlbGV0ZWQiOmZhbHNlLCJtYW5hZ2VyIjpmYWxzZSwic2FuZGJveCI6ZmFsc2UsIl9pZCI6IjVmNjk4NzlhY2NhNGYzMDVhMWZiNmM3ZCIsInVzZXJuYW1lIjoiIiwicGFzc3dvcmQiOiIkMmIkMDQka0RZOUhpand4UGQ1cUhWQ2JrQ0pYZXhTOElwY3NObXJLSWZYSDFnWG53V0V0Y1FOT0t2RHkiLCJwcm9qZWN0X2lkIjoiNzVkMTgxMzQtOWU0OS00YmUyLWI2MTQtN2NjNWFkMjkwMWRjIiwic3RvcmVfaWQiOiJwYyIsImlkIjoiN2FlY2U1NGUtMDdlNi00NjkwLTg0NzktNTY1YjA3YjE1ZDI1IiwicmVtb3RlaXAiOiIyMjAuNzYuNTIuMTYzIiwibG9naW5lZEF0IjoiMjAyMC0wOS0yMlQwODoyOToyOS4wMDNaIiwiY291bnRyeSI6IktSIiwiY3JlYXRlZEF0IjoiMjAyMC0wOS0yMlQwNToxMTo1NC42MTdaIiwidXBkYXRlZEF0IjoiMjAyMC0wOS0yMlQwODoyOToyOS4wMDNaIiwiX192IjoxLCJpYXQiOjE2MTUxODY5MzcsImV4cCI6MTYyMjk2MjkzN30.NBsaTwDJ94mMYPscQayRXFuVA2RVezegqj75midpYBM"
}


```

| Attribute | Type   | Description                             |
| :-------- | :----- | :---------------------------------------|
| projectId | String | GamePot SDK의 projectId                  |

| body | Type   | Description                             |
| :-------- | :----- | :---------------------------------------|
| memberId | String | 사용자 아이디                  |
| token | String | 로그인 이후 획득한 토큰                  |





#### Response

성공

```javascript
{
    "status": 1,
    "decoded": {
        "agree": {
            "termsofuse": "N",
            "privacypolicy": "N"
        },
        "verify": {
            "key": "wn+Kxh4SLzy8lEf7RM+iYEQdSrqCiADlXXXXXXXXX",
            "updatedAt": "2020-09-22T05:13:53.721Z"
        },
        "gdpr": {
            "status": 0,
            "checked_story_category_ids": [],
            "checked_category_ids": []
        },
        "local": {
            "status": 2,
            "email_cert_expired_at": null,
            "email_cert_key": null
        },
        "push": true,
        "night": false,
        "ad": true,
        "deleted": false,
        "manager": false,
        "sandbox": false,
        "username": "",
        "password": "$2b$04$kDY9HijwxPd5qHVCbkCJXexS8IpcsNmrKIfXH1gXnwWEtcQNOKvDy",
        "project_id": "{GamePot SDK의 projectId }",
        "store_id": "pc",
        "id": "7aece54e-07e6-4690-XXXXX-XXXX5",
        "remoteip": "2XX.XX.XX.163",
        "loginedAt": "20XX-09-22T08:29:29.003Z",
        "country": "KR",
        "createdAt": "20xX-09-22T05:11:54.617Z",
        "updatedAt": "20XX-09-22T08:29:29.003Z",
        "iat": 1615186937,
        "exp": 1622962937
    }
}
```

| Attribute       | Type    | Description                                     |
| :---------------| :------ | :---------------------------------------------- |
| status          | Int     | 결과값 \(1: 성공, 실패는 Error code 참고\)            |
| agree           | String | 약관동의    (termsofuse/privacypolicy 값은 동일한 값 - Y : 동의 / N : 미동의)   |
| verify          | String | 본인인증     (해당 항목이 있는 경우 본인인증을 진행한 케이스)      |
| id              | String | 사용자 아이디           |
| project_id      | String | 프로젝트 아이디           |

실패
```javascript
{
    "status": -2,
    "message": "Token authentication failed."
}
```

| Attribute | Type   | Description                                     |
| :-------- | :----- | :---------------------------------------------- |
| status    | Int    | 결과값 \(1: 성공, 실패는 Error code 참고\)        |
| message   | String | 오류 내용                                         |

#### Error code

| Code | Description                                                       |
| :--- | :---------------------------------------------------------------- |
| -1   | 토큰 정보가 올바르지 않을 때                              |
| -2   | 토큰 정보가 올바르지 않을 때                              |





### 약관 동의 상태 변경 API

사용자 약관 동의 상태 변경

#### Request

 - Method : PUT
 - URI : /v1/api/project/{projectid}/user/terms

```text
POST
url : https://gravity-api.gamepot.io/v1/api/project/{projectid}/user/terms
Header : 'language: ko'
Header : 'Content-Type: application/json'
body : 
{
    "memberId":"7aece54e-07e6-4690-8479-565b07b15d25",
    "agree":"N"
}


```

| Attribute | Type   | Description                             |
| :-------- | :----- | :---------------------------------------|
| projectId | String | GamePot SDK의 projectId                  |

| body | Type   | Description                             |
| :-------- | :----- | :---------------------------------------|
| memberId | String | 사용자 아이디                  |
| agree | String | 약관 동의 여부 ( Y : 약관동의 / N : 약괸 미동의)     |





#### Response

성공

```javascript
{
    "status": 1,
    "message": "success"
}
```

| Attribute       | Type    | Description                                     |
| :---------------| :------ | :---------------------------------------------- |
| status          | Int     | 결과값 \(1: 성공, 실패는 Error code 참고\)            |

실패
```javascript
{
    "error": 
    {
        "status": -1,
        "message": "데이터가 부족합니다. request body is '{\"memberId\":\"XXX-XXXX-XXXX\",\"agree\":\"\"}'"
    }
}
```

| Attribute | Type   | Description                                     |
| :-------- | :----- | :---------------------------------------------- |
| status    | Int    | 결과값 \(1: 성공, 실패는 Error code 참고\)        |
| message   | String | 오류 내용                                         |

#### Error code

| Code | Description                                                       |
| :--- | :---------------------------------------------------------------- |
| -1   | agree 설정 값이 없을 때                              |
| -2   | agree 설정 값이 Y / N 이 아닐 때                      |
| -3   | 회원 정보 오류                             |












#### Response

성공

```javascript
{
    "status": 1,
    "message": "success"
}
```

| Attribute       | Type    | Description                                     |
| :---------------| :------ | :---------------------------------------------- |
| status          | Int     | 결과값 \(1: 성공, 그외 실패\)            |





### 공지사항 정보 획득 API

대시보드 공지사항 정보 획득

#### Request

 - Method : GET
 - URI : /v1/api/project/{projectid}/store/pc/notice/posting

```text
POST
url : https://gravity-api.gamepot.io/v1/api/project/{projectid}/store/pc/notice
Header : 'accept-language: ko'
```

| Attribute | Type   | Description                             |
| :-------- | :----- | :---------------------------------------|
| projectId | String | GamePot SDK의 projectId                  |



#### Response

성공

```javascript
게시중인 공지사항이 없을 때 
{
  "status":1,
  "result":[]
}

게시중인 공지사항이 있을때
{
  "status":1,
  "result":
  [
    {
      "image":"다운로드 경로/notices/8b862325-4c90-4fb8-94af-681eb40d417d.png",
      "url":"링크 주소",
      "scheme":""
    },
    {
      "image":"다운로드 경로/notices/5e3f2a68-c6f9-44e1-9071-4fc2ba7148a9.png",
      "url":"",
      "scheme":"https://www.daum.net/"
    }
  ]
}


```

| Attribute       | Type    | Description                                     |
| :---------------| :------ | :---------------------------------------------- |
| status          | Int     | 결과값 \(1: 성공, 실패는 Error code 참고\)            |
| image           | String  | 공지사항 이미지 주소                           |
| url             | String  | 공지사항내 클릭 액션 타입 URL 선택 + 입력된 정보            |
| scheme          | String  | 공지사항내 클릭 액션 타입 SCHEME 선택 + 입력된 정보      |





### 이메일 계정 비밀번호 초기화 API

이메일 계정 비밀번호 초기화

#### Request

 - Method : POST
 - URI : /forgetpassword/local

```text
POST
url : https://gravity-api.gamepot.io/forgetpassword/local
Header : 'accept-language: ko'
Header : 'Content-Type: application/x-www-form-urlencoded'
data-urlencode 'projectId=75d18134-9e49-4be2-b614-7cc5ad2901dc' \
data-urlencode 'id=jyj1127j@gmail.com' \
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
| -2   | 프로젝트 아이디 없는 경우                       |
| -3   | 존재하지 않는 회원인 경우                       |
| -4   | 본인인증 키가 올바르지 않은 경우                           |
| -6   | 사용할 수 없는 비밀번호 / 회원정보 확인 불가        |


### 계정 조회 API

계정 조회


#### Request

 - Method : POST
 - URI : /v1/forgetid/local

```text
POST
url : https://gravity-api.gamepot.io//v1/forgetid/local
Header : 'accept-language: ko'
Header : 'Content-Type: application/x-www-form-urlencoded'
--data-urlencode 'projectId=75d18134-9e49-4be2-b614-7cc5ad2901dc' \
--data-urlencode 'verifyKey=wn+Kxh4SLzy8lEf7RM+iYEQdSrqCiADlOj418P1Plk4xUxs5ppoOe4vShvGqWGw9fAQjmgc4dzmntXFdwzpO/g=='
```


| data | Type   | Description                             |
| :-------- | :----- | :---------------------------------------|
| projectId | String | 프로젝트 아이디     |
| verifyKey | String | 본인인증 CI        |






#### Response

성공

```javascript
{
    "status": 1,
    "verifyKey": "wn+Kxh4SLzy8lEf7RM+iYEQdSrqCiADlOj418P1Plk4xUxs5ppoOe4vShvGqWGw9fAQjmgc4dzmntXFdwzpO/g==",
    "data": "[{\"providerId\":\"109477521151116762117\",\"provider\":\"google\",\"createdAt\":1604628245},{\"providerId\":\"jyj1127j@naver.com\",\"provider\":\"email\",\"createdAt\":1600751514}]"
}
```

| Attribute       | Type    | Description                                     |
| :---------------| :------ | :---------------------------------------------- |
| status          | Int     | 결과값 \(1: 성공, 실패는 Error code 참고\)            |
| providerId      | String  | 계정연동 아이디          |
| provider        | String  | 계정연동 타입 ( google / facebook / email )            |
| createdAt       | String  | 본인인증 완료한 일            |



실패
```javascript
{
    "error": {
        "status": -2,
        "message": "본인인증을 하지 않은 회원입니다."
    }
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
| -2   | 본인인증을 하지 않은 회원                        |
| -4   | 존재하지 않는 회원인 경우                        |
| -5   | 연동된 이메일이 없는 경우                        |


### 이메일 계정 비밀번호 변경 API

이메일 계정 비밀번호 변경

#### Request

 - Method : POST
 - URI : /v1/changepassword/local

```text
POST
url : https://gravity-api.gamepot.io/v1/changepassword/local
Header : 'language: ko'
Header : 'Content-Type: application/x-www-form-urlencoded'
Header : 'token: {token}'
data-urlencode 'projectId={GamePot SDK의 projectId }' \
data-urlencode 'id=74f178cf-1409-4b6b-9845-ae75db5dd0fc' \
data-urlencode 'newPassword=Gamepot123!@' \
data-urlencode 'currentPassword=Gamepot123!@'
```

| Header    | Type   | Required | Description                  |
| :-------- | :----- | :------- | :--------------------------- |
| token     | String | O        |   로그인 이후 획득한 토큰    |


| data | Type   | Description                             |
| :-------- | :----- | :---------------------------------------|
| projectId | String | 프로젝트 아이디     |
| id        | String | 이메일 계정        |
| newPassword      | String | 신규 패스워드    |
| currentPassword  | String | 기존 패스워드    |






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
| -1   | 파라미터 누락                             |
| -2   | 토큰 디코딩 실패                     |
| -3   | 토큰 인증 실패                     |
| -4   | 존재하지 않는 회원인 경우.                     |
| -5   | 현재 비밀번호가 일치하지 않은 경우                     |
| -6   | 올바르지 않은 비밀번호인 경우                     |
| -7   | 계정 연동 정보가 없는 경우                     |
| -8   | 이메일 인증을 완료하지 않은 상태                     |




----------------------------
