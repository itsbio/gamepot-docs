# 3자 SDK 로그인 API 

#### Request
ß

 - Method : POST
 - URI : https://gamepot.apigw.ntruss.com/gpapps/v1/graphql

```text
PUT
url : https://gamepot.apigw.ntruss.com/gpapps/v1/graphql
Header : 'Content-Type: application/json'
body : 
{
"query":"mutation CreateMemberByThirdPartySDK($projectId: String!, $storeId: String!, $id: String!) { createMemberByThirdPartySDK(input: { projectId: $projectId, storeId: $storeId, id: $id } ) { member { id } }}",
"variables":{
"projectId":"XXXXXXX-XXXX-XXXX-XXXXX-XXXXXXXX",
"storeId":"pc",
"id":"XXXXXXX-XXXX-XXXX-XXXXX-XXXXXXXXX"
}
}
```

```text
예시)

curl --location --request POST 'https://gamepot.apigw.ntruss.com/gpapps/v1/graphql' \
--header 'Content-Type: application/json' \
--data-raw '{"query":"mutation CreateMemberByThirdPartySDK($projectId: String!, $storeId: String!, $id: String!) { \n    createMemberByThirdPartySDK(input: {\n        projectId: $projectId, storeId: $storeId, id: $id\n        }\n    ) { member { id } }\n}","variables":{"projectId":"XXXXXXX-XXXX-XXXX-XXXXX-XXXXXXXX","storeId":"pc","id":"XXXXXXX-XXXX-XXXX-XXXXX-XXXXXXXXX"}}'



```
| Attribute    | Type   | Required | Description                  |
| :-------- | :----- | :------- | :--------------------------- |
| projectId  | String | O        |   GamePot SDK의 projectId   |
| storeId   | String | O        |   스토어 정보( google, one,galaxy,pc)   |
| id   | String | O        |   JS SDK를 통해 전달 받은 게임팟 사용자 아이디  |




#### Response

성공

```javascript
{
    "data": {
        "createMemberByThirdPartySDK": {
            "member": {
                "id": "TWVtYmVyOjYzNzk0M2E1LTdhNDEtNDM4Yi05NWJmLTNmMDNkZTQyNDZkZTE="
            }
        }
    }
}
```




실패시 error 관련 내용 제공
```javascript
{
    "errors": [
        {
            "message": "The request is invalid.",
            "code": 400,
            "state": {
                "": [
                    "projectId is not found"
                ]
            },
            "locations": [
                {
                    "line": 2,
                    "column": 5
                }
            ],
            "path": [
                "createMemberByThirdPartySDK"
            ]
        }
    ],
    "data": {
        "createMemberByThirdPartySDK": null
    }
}
```


