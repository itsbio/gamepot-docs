# GAMEPOT 고객문의 API 



### 고객문의 분류 API

고객문의 분류 리스트 확인

#### Request

 - Method : POST
 - URI : /v2/api/ticket/category

```text
POST
url : https://alpha-dashboard-api.gamepot.io/v2/api/ticket/category
Header : 'language: ko'
Header : 'X-API-KEY: 2c5752cdafc95da63de7d906335ec7c4e71b4f1f56a9a277'
Header : 'X-PROJECT-ID: 6936eef9-7e32-4a1b-9ace-7206c33a07a8'
```

| Header | Type   | Required          | Description                  |
| :-------- | :----- | :--------------------------: | ---------------------------- |
| language     | String |      |   고객문의 분류 설정상 언어 (국가코드 :ISO 639-1코드)   |
| X-API-KEY    | String | O | GamePot에서 발급하는 인증 키 |
| X-PROJECT-ID | String | O | 대시보드 프로젝트 아이디 |


#### Response

성공

```javascript
예제 :

[
  {
    "id": "1e156831-0111-4ec5-9195-9c3d56d2b3c1",
    "title": "회원",
    "agree_story_url": ""
  },
  {
    "id": "e87a0cad-39e2-495b-ba3d-d2cddb6b19a7",
    "title": "게임",
    "agree_story_url": ""
  },
  {
    "id": "493fb91f-1670-4d94-af2c-fb65e2a14f61",
    "title": "결제",
    "content": "- 결제 날짜 및 시간대 : (최대한 상세하게 기재 부탁드립니다.)\n- 통신사/번호 : (ex. SKT, KT, LGT / 010-0000-0000)\n- 결제 진행한 마켓 : (ex 구글, 앱스토어, 원스토어)\n- 구입 금액 : (여러 번 구매 시 날짜 및 시간대 별로 나누어 기재)\n- 구매 영수증번호 :\n- 요청사항 :",
    "agree_story_url": ""
  },
  {
    "id": "23ba4a6c-cd26-4003-914d-9f669c8a1169",
    "title": "이벤트",
    "agree_story_url": ""
  },
  {
    "id": "7e2cfd61-7715-4eb0-94b7-74fe0941f852",
    "title": "기타",
    "agree_story_url": ""
  }
]
```

| Attribute       | Type   | Description                                            |
| :-------------- | :----- | :----------------------------------------------------- |
| id              | String | 고객문의 분류 고유아이디                               |
| title           | String | 분류 제목                                              |
| content         | String | 분류 상세 내용                                         |
| agree_story_url | String | 대시보드 > 분류 > 이벤트 팝업 항목에 설정한 페이지 URL |


실패
```javascript
{
  "status": -1,
  "message": "X-API-KEY was wrong."
}
```



#### Error code

| Code | Description                                                       |
| :--- | :---------------------------------------------------------------- |
| -1  | X-API-KEY 오류 |
| -6 | 프로젝트 아이디 정보 오류 |
| -9 | 필수 파라미터 미 입력 |




### 고객문의 등록 API

고객문의 등록

#### Request

 - Method : POST
 - URI : /v2/api/ticket

```text
POST
url : https://alpha-dashboard-api.gamepot.io/v2/api/ticket 
Header : 'application/json'
Header : 'language: ko'
Header : 'X-PROJECT-ID: 6936eef9-7e32-4a1b-9ace-7206c33a07a8'
Header : 'X-API-KEY: 2c5752cdafc95da63de7d906335ec7c4e71b4f1f56a9a277'
DATA   : '{
"type": "3246bc09-52d5-4e73-a265-41b0a08f2b7b",
"subject": "title",
"body": "한국어",
"email": "XXXXXX@gmail.com",
"phone": "123-456-0789",
"serverName":"serverName",
"character": "character",
"agree_termsofuse": false,
"agree_type": false,
"file": ["https://kr.object.ncloudstorage.com/gamepot-cazu8gdl/cs/437800aa-b903-4398-b909-d7c94ac51bf4.mp4"]
}'
```



| Header       | Type   | Required | Description                                  |
| :----------- | :----- | :------: | -------------------------------------------- |
| language     | String |          | 고객문의를 한 언어 (국가코드 :ISO 639-1코드) |
| X-API-KEY    | String |    O     | GamePot에서 발급하는 인증 키                 |
| X-PROJECT-ID | String |    O     | 대시보드 프로젝트 아이디                     |

| Attribute        | Type    | Required | Description                                                  |
| :--------------- | :------ | :------: | :----------------------------------------------------------- |
| type             | String  |    O     | 고객문의 분류 고유아이디                                     |
| subject          | String  |    O     | 고객문의 제목                                                |
| body             | String  |    O     | 고객문의 본문 내용                                           |
| email            | String  |          | 고객문의 입력한 이메일 정보                                  |
| phone            | String  |          | 고객문의 입력한 연락처 정보                                  |
| serverName       | String  |          | 고객문의 서버/캐릭터 정보                                    |
| character        | String  |          | 고객문의 캐릭터 / 게임회원 ID 정보                           |
| agree_termsofuse | Boolean |          | 필수 약관 동의 (정보 수집에 동의 또는 고객문의 이용약관 동의 여부) |
| agree_type       | Boolean |          | 선택 약관 동의 ( 분류에 설정한 이벤트 약관 동의 여부)        |
| file             | String  |          | 업로드한 파일의 주소                                         |



#### 

#### Response

성공

```javascript
{
  "status": 1,
  "result": {
    "ticket": {
      "id": "VGlja2V0Ojk2MTY2ZWY0LWIxNjktNGNmYi05MWI1LWJiNzZiMjMwOTI2OA=="
    }
  }
}
```

| Attribute | Type | Description                                |
| :-------- | :--- | :----------------------------------------- |
| status    | Int  | 결과값 \(1: 성공, 실패는 Error code 참고\) |

실패

```javascript
{
  "status": -1,
  "message": "X-API-KEY was wrong."
}
```



#### Error code

| Code | Description               |
| :--- | :------------------------ |
| -1   | X-API-KEY 오류            |
| -6   | 프로젝트 아이디 정보 오류 |
| -9   | 필수 파라미터 미 입력     |

