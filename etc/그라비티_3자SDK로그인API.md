# 3자 SDK 로그인 API 

#### Request


 - Method : POST
 - URI : https://gamepot.apigw.ntruss.com/gpapps/v1/graphql

```text
PUT
url : https://gamepot.apigw.ntruss.com/gpapps/v1/graphql
Header : 'Content-Type: application/json'
body : 
{
"query":"mutation signInV3($projectId: String!, $storeId: String!, $provider:String!, $providerId: String!, $providerEmail: String!, $providerToken: String) {
                signInV3 (input: {projectId:$projectId, storeId: $storeId, provider: $provider, providerId: $providerId, providerEmail: $providerEmail, providerToken: $providerToken}) {
                    id
                    projectId
                    email
                    verify
                    agree
                    provider
                    providerId
                    nickname
                    token
                }
            }",
"variables":{
 "projectId" : "XXXXXX-XXXXXX-XXXXX-XXXXX",
 "storeId" : "android",
 "provider":"thirdpartysdk",
 "providerEmail":"",
 "providerToken":"",
 "providerId" : "XXXXXXXXXXXXX"
}
}
```

```text
예시)

curl --location --request POST 'https://gamepot.apigw.ntruss.com/gpapps/v1/graphql' \
--header 'Content-Type: application/json' \
--data-raw '{"query":"mutation signInV3($projectId: String!, $storeId: String!, $provider:String!, $providerId: String!, $providerEmail: String!, $providerToken: String) {
                    signInV3 (input: {projectId:$projectId, storeId: $storeId, provider: $provider, providerId: $providerId, providerEmail: $providerEmail, providerToken: $providerToken}) {                    
                        id                    
                        projectId                    
                        email                    
                        verify                    
                        agree                    
                        provider                    
                        providerId                    
                        nickname                    
                        token                
                    }            
            }","variables":{
                "projectId":"XXXXXX-XXXX-XXXX-XXXXX-XXXXXXX",
                "storeId":"pc",
                "provider":"thirdpartysdk",
                "providerEmail":"",
                "providerToken":"",
                "providerId":"XXXXXXXXXX"}}'



```
| Attribute    | Type   | Required | Description                  |
| :-------- | :----- | :------- | :--------------------------- |
| projectId  | String | O        |   GamePot SDK의 projectId   |
| storeId   | String | O        |   스토어 정보( google, one,galaxy,pc)   |
| provider   | String | O        |   thirdpartysdk 값으로 고정  |
| providerId   | String | O        |  3자 SDK를 통해 전달 받은 고유 사용자 아이디  |
| providerEmail / providerToken  | String | O        |  빈칸으로 유지   |




#### Response

성공

```javascript
{
    "data": {
        "signInV3": {
            "id": "XXXXXXXXXX",
            "projectId": "XXXXXX-XXXX-XXXX-XXXXX-XXXXXXX",
            "email": "",
            "verify": "N",
            "agree": "Y",
            "provider": "thirdpartysdk",
            "providerId": "XXXXXXXXXX",
            "nickname": "",
            "token": "게임팟 토큰"
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
                    "Variable \"$id\" of required type \"String!\" was not provided."
                ]
            },
            "locations": [
                {
                    "line": 2,
                    "column": 17
                }
            ],
            "path": [
                "signInV3"
            ]
        }
    ],
    "data": {
        "signInV3": null
    }
}
```


