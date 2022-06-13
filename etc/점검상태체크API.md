# 점검상태 조회 API 

대시보드 내 점검설정 확인

#### Request


 - Method : POST
 - URI : https://gamepot.apigw.ntruss.com/gpapps/v1/graphql

```text
PUT
url : https://gamepot.apigw.ntruss.com/gpapps/v1/graphql
Header : 'language: ko'
Header : 'Accept: application/json'
Header : 'Content-Type: application/json'
Header : 'Authorization: Bearer {token}' // {token} 부분은 로그인 이후 획득한 토큰으로 교체
body : 
{   
    "query": "query maintenanceAppV2($projectId: String!, $storeId: String!) {
    maintenanceAppV2(projectId: $projectId, storeId: $storeId) {
        store {
                google
                one
                galaxy
                pc
            }
            message {
                default
                lang
                value
            }
            url
            startedAt
            endedAt
        }
    }",
    "variables":
    {
        "projectId": "{게임팟 프로젝트 아이디}",
        "storeId": "pc"
    }
```

```text
예시)

curl --location --request POST 'https://gamepot.apigw.ntruss.com/gpapps/v1/graphql' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'language: ko' \
--header 'Authorization: Bearer eyJhbXXXXXXXXXXXXXXXXXXXXXXXX' \
--data-raw '{"query":"query maintenanceAppV2($projectId: String!, $storeId: String!) {\n    maintenanceAppV2(projectId: $projectId, storeId: $storeId) {\n        store {\n                google\n                one\n                galaxy\n                pc\n            }\n            message {\n                default\n                lang\n                value\n            }\n            url\n            startedAt\n            endedAt\n        }\n    }",
"variables":{"projectId":"XXXXXX-XXXXX-XXXX-XXXXX","storeId":"pc"}}'



```
| Attribute    | Type   | Required | Description                  |
| :-------- | :----- | :------- | :--------------------------- |
| projectId  | String | O        |   GamePot SDK의 projectId   |
| storeId   | String | O        |   스토어 정보( google, one,galaxy,pc)   |

| Header    | Type   | Required | Description                  |
| :-------- | :----- | :------- | :--------------------------- |
| Authorization: Bearer| String | O        |   로그인 이후 획득한 토큰    |



#### Response

성공

```javascript
{
    "data": {
        "maintenanceAppV2": {
            "store": {
                "google": "0",
                "one": "0",
                "galaxy": "0",
                "pc": "1"
            },
            "message": [
                {
                    "default": true,
                    "lang": "ko",
                    "value": "점검중"
                },
                {
                    "default": false,
                    "lang": "en",
                    "value": "maintenance "
                }
            ],
            "url": "https://www.naver.com",
            "startedAt": "1653894480",
            "endedAt": "1656313680"
        }
    }
}
```

| Attribute       | Type    | Description                                     |
| :---------------| :------ | :---------------------------------------------- |
| store          | String    | 스토어 체크 값 ( 1 : On / o : Off)            |
| message        | String  | 점검 문구 설정 정보    |
| url        | String  | URL 설정 정보  |


조회 결과 없음
```javascript
{
    "data": {
        "maintenanceAppV2": null
    }
}
```


