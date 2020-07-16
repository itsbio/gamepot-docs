---
search:
  keyword:
    - gamepot
---

# Open API

> ### 这是机器翻译的文档，可能在词汇，语法或语法上有错误。 我们很快会为您提供由专业翻译人员翻译的文档。
>
> #### 如有任何疑问，请[联系我们]（https://www.ncloud.com/support/question）。
>
> 我们将尽一切努力进一步改善我们的服务。

该功能可以通过指定的 API 调用 Gamepot 提供的某些功能。

> 您可以使用仪表板发出的允许的 API 密钥进行调用，还可以指定是否使用它以及到期日期。

## API Key

要调用 Open API，您必须首先在信息中心中创建一个 API 密钥。

可以在<b>仪表板>项目设置> API 密钥</b>中创建 API 密钥。

![gamepot_api_01](./images/gamepot_api_01.png)

① 单击添加按钮以生成 API 密钥。

![gamepot_api_02](./images/gamepot_api_02.png)

① 选择是否激活相应的 API 密钥。

② 设置 API 密钥的到期日期。

③ 输入用户可以识别的描述。

④ 用添加按钮注册 API 密钥。

![gamepot_api_03](./images/gamepot_api_03.png)

您可以通过单击生成的 API KEY 来修改或删除状态。

> 使用 Open API 时，将生成的 Key 值输入到标头的 x-api-key 值中。

## 使用 Open API

### Error code

请求 Open API 时发生的常见错误代码。

| Code | Description                  |
| :--- | :--------------------------- |
| -1   | 如果您使用了不在仪表板上的键 |
| -2   | 仪表板的键和标题的键不同     |
| -3   | 使用从仪表板上删除的键时     |
| -4   | 仪表板中使用了未使用的密钥   |
| -5   | 密钥已过期                   |
| -6   | 如果没有项目 ID              |

### 用户查找 API

通过用户 UID 查找用户。

#### Request

- Method : GET
- URI : /user/{userID}

```text
GET
url : https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/user/{userId}
Header : 'accept-language: ko'
Header : 'x-api-key: {从GamePot仪表板发出的API密钥}'
```

| Header    | Type   | Required | Description            |
| :-------- | :----- | :------- | :--------------------- |
| x-api-key | String | O        | GamePot 发行的验证密钥 |

| Attribute | Type   | Description                |
| :-------- | :----- | :------------------------- |
| projectId | String | GamePot SDK 中的 ProjectId |
| userId    | String | GamePot SDK 中的 UserId    |

#### Response

成功

```javascript
{
  "status": 1,
  "result": {
    "id": "xxxxxxxxxxxxxx",
    "deleted": false,
    "store_id": "google",
    "country": "KR",
    "remoteip": "xxx.xxx.xxx.xxx",
    "adid": "test_s6SksBK",
    "device": "android",
    "network": "WI-FI",
    "version": "testVersion",
    "model": "test-111",
    "token": "test:Qz9Fd81H6O",
    "push": true,
    "night": true,
    "ad": true,
    "memo": null,
    "device_id": null,
    "createdAt": "Tue Apr 07 2020 16:32:17 GMT+0900 (GMT+09:00)",
    "updatedAt": "Tue Apr 07 2020 16:32:19 GMT+0900 (GMT+09:00)",
    "loginedAt": "Tue Apr 07 2020 16:32:19 GMT+0900 (GMT+09:00)",
    "deletedAt": null
  }
}
```

| Attribute | Type    | Description                                      |
| :-------- | :------ | :----------------------------------------------- |
| status    | Int     | 结果值(1：有关成功和失败，请参见错误代码)        |
| id        | String  | 用户名                                           |
| deleted   | Boolean | 是否删除成员（true：删除，false：普通）          |
| store_id  | String  | 创建帐户时访问的商店（google ...）               |
| country   | String  | 用户国家/地区代码（基于 ISO 3166-1）             |
| remoteip  | String  | 用户 IP                                          |
| adid      | String  | 广告 ID                                          |
| device    | String  | 设备类型（android，ios)                          |
| network   | String  | 用户访问网络 (WI-FI...)                          |
| version   | String  | 客户端版本信息                                   |
| model     | String  | 用户设备型号名称                                 |
| token     | String  | 推送令牌                                         |
| push      | Boolean | 是否同意推送 \(true : 同意, false : 不同意\)     |
| night     | Boolean | 是否同意晚上推 \(true : 同意, false : 不同意\)   |
| ad        | Boolean | 是否推送广告同意 \(true : 同意, false : 不同意\) |
| memo      | String  | 会员须知                                         |
| device_id | String  | 会员设备 ID                                      |
| createdAt | String  | 创建成员的日期                                   |
| updatedAt | String  | 会员信息的修改日期                               |
| loginedAt | String  | 最后访问日期                                     |
| deletedAt | String  | 会员删除日期                                     |

失败

```javascript
{
  "status": -6,
  "message": "projectId was wrong."
}
```

| Attribute | Type   | Description                               |
| :-------- | :----- | :---------------------------------------- |
| status    | Int    | 结果值(1：有关成功和失败，请参见错误代码) |
| message   | String | 错误内容                                  |

### 用户暂停查询 API

查询用户是否被用户 UID 停止。

#### Request

- Method : GET
- URI : /user/{userID}/block

```text
GET
url : https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/user/{userId}/block
Header : 'accept-language: ko'
Header : 'x-api-key: {从GamePot仪表板发出的API密钥}'
```

| Header    | Type   | Required | Description            |
| :-------- | :----- | :------- | :--------------------- |
| x-api-key | String | O        | GamePot 发行的验证密钥 |

| Attribute | Type   | Description                |
| :-------- | :----- | :------------------------- |
| projectId | String | GamePot SDK 中的 ProjectId |
| userId    | String | GamePot SDK 中的 UserId    |

#### Response

成功

```javascript
{
  "status": 1,
  "result": {
    "id": "xxxxxxxxxxxxxx",
    "member_id": "xxxxxxxxxxxxxx",
    "deleted": false,
    "type": "manual",
    "status": 1,
    "message": null,
    "messageMulti": [
      {
        "lang": "ko",
        "value": "test-ko",
        "default": true
      }
    ],
    "startedAt": "Mon May 11 2020 12:02:00 GMT+0900 (GMT+09:00)",
    "endedAt": "Mon May 25 2020 22:00:00 GMT+0900 (GMT+09:00)",
    "createdAt": "Tue May 12 2020 14:06:40 GMT+0900 (GMT+09:00)",
    "updatedAt": "Tue May 12 2020 14:06:40 GMT+0900 (GMT+09:00)",
    "deletedAt": null,
    "category_id": ""
  }
}
```

| Attribute   | Type    | Description                                                                                    |
| :---------- | :------ | :--------------------------------------------------------------------------------------------- |
| status      | Int     | 结果值(1：有关成功和失败，请参见错误代码)                                                      |
| id          | String  | 用户暂停信息的 ID                                                                              |
| member_id   | String  | 用户身份                                                                                       |
| deleted     | Boolean | 是否删除用户暂停信息（true：删除，false：正常）                                                |
| type        | String  | 暂停使用的分类（手动：手动，自动购买：自动）                                                   |
| status      | Int     | 状态（1：启用，2：禁用）                                                                       |
| message     | String  | 暂停原因（目前未使用）                                                                         |
| lang        | String  | 停止讯息语言                                                                                   |
| value       | String  | 停权原因                                                                                       |
| default     | Boolean | 默认语言设置<br>如果 messageMulti 中不存在设备的语言值，则默认情况下会显示设置为 true 的消息。 |
| startedAt   | String  | 暂停开始日期                                                                                   |
| endedAt     | String  | 停权终止日期                                                                                   |
| createdAt   | Boolean | 暂停注册日期                                                                                   |
| updatedAt   | Boolean | 暂停使用日期                                                                                   |
| deletedAt   | Boolean | 暂停使用日期                                                                                   |
| category_id | String  | 中止使用的 ID                                                                                  |

失败

```javascript
{
  "status": -6,
  "message": "projectId was wrong."
}
```

| Attribute | Type   | Description                             |
| :-------- | :----- | :-------------------------------------- |
| status    | Int    | 结果值（1：成功或失败，请参见错误代码） |
| message   | String | 错误内容                                |

### 用户停止设置 API

用户被用户 UID 暂停。

#### Request

- Method : POST
- URI : /user/{userID}/block

```text
POST
url : https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/user/{userId}/block
Header : 'accept-language: ko'
Header : 'content-type: application/json'
Header : 'x-api-key: {由GamePot信息​​中心发布的API密钥}'
data: '{
        "messageMulti": [
                {
                    "lang": "ko",
                    "value": "test",
                    "default": true
                }
            ],
            "startedAt": "2020-05-11 12:02",
            "endedAt": "2020-05-25 22:00"
       }'
```

| Header    | Type   | Required | Description            |
| :-------- | :----- | :------- | :--------------------- |
| x-api-key | String | O        | GamePot 发行的验证密钥 |

| Attribute | Type    | Description                                                                                    |
| :-------- | :------ | :--------------------------------------------------------------------------------------------- |
| projectId | String  | GamePot SDK 中的 ProjectId                                                                     |
| userId    | String  | GamePot SDK 中的 userId                                                                        |
| lang      | String  | 停止讯息语言                                                                                   |
| value     | String  | 停权原因                                                                                       |
| default   | Boolean | 默认语言设置<br>如果 messageMulti 中不存在设备的语言值，则默认情况下会显示设置为 true 的消息。 |
| startedAt | String  | 暂停开始日期 `YYYY-MM-DD HH:mm`                                                                |
| endedAt   | String  | 停权终止日期 `YYYY-MM-DD HH:mm`                                                                |

#### Response

成功

```javascript
{
  "status": 1,
  "result": {
    "memberBlock": {
      "id": "xxxxxxxxxxxxx"
    }
  }
}
```

| Attribute | Type   | Description                               |
| :-------- | :----- | :---------------------------------------- |
| status    | Int    | 结果值(1：有关成功和失败，请参见错误代码) |
| id        | String | ID 已暂停                                 |

失败

```javascript
{
  "status": -5,
  "message": "ApiKey was expired."
}
```

| Attribute | Type   | Description                               |
| :-------- | :----- | :---------------------------------------- |
| status    | Int    | 结果值(1：有关成功和失败，请参见错误代码) |
| message   | String | 错误内容                                  |

#### Error code

| Code | Description                                                      |
| :--- | :--------------------------------------------------------------- |
| -11  | body 缺乏数据                                                    |
| -12  | messageMulti 值不是 JSON 数组                                    |
| -13  | 如果 startedAt 值的格式不正确，则只能使用格式`YYYY-MM-DD HH：mm` |
| -14  | 如果 endAt 值的格式不正确，则只能使用`YYYY-MM-DD HH：mm`格式。   |
| -15  | messageMulti 值的数据格式不正确                                  |
| -16  | 如果没有默认的 true 或 messageMulti 值数据的倍数                 |

### 每日访问器（DAU）查找 API

您可以搜索日常用户。

#### Request

- Method : GET
- URI : /user/statistics/dau

```text
GET
url : https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/user/statistics/dau
Header : 'accept-language: ko'
Header : 'x-api-key: {由GamePot信息​​中心发布的API密钥}'
```

| Header    | Type   | Required | Description            |
| :-------- | :----- | :------- | :--------------------- |
| x-api-key | String | O        | GamePot 发行的验证密钥 |

| Attribute | Type   | Description                     |
| :-------- | :----- | :------------------------------ |
| projectId | String | GamePot SDK 中的 ProjectId      |
| startDate | String | 查找开始日期 `YYYY-MM-DD`       |
| endDate   | String | 您想查看的最后日期 `YYYY-MM-DD` |

> 如果查询中不包含 startDate 和 endDate，则检索最近 30 天的数据。

#### Response

成功

```javascript
{
  "status": 1,
  "result": {
    "totalCount": 3,
    "edges": [
      {
        "node": {
          "date": "Fri Apr 10 2020 09:00:00 GMT+0900 (Korean Standard Time)",
          "count": 2
        }
      },

      ...

      {
        "node": {
          "date": "Tue Apr 14 2020 09:00:00 GMT+0900 (Korean Standard Time)",
          "count": 4
        }
      }
    ]
  }
}
```

| Attribute  | Type   | Description                               |
| :--------- | :----- | :---------------------------------------- |
| status     | Int    | 结果值(1：有关成功和失败，请参见错误代码) |
| totalCount | Int    | dau 搜索结果（数量）                      |
| date       | String | 计算日期和时间                            |
| count      | Int    | （日期）DAU                               |

失败

```javascript
{
  "status": -11,
  "message": "startDate format was wrong. (YYYY-MM-DD)"
}
```

| Attribute | Type   | Description                               |
| :-------- | :----- | :---------------------------------------- |
| status    | Int    | 结果值(1：有关成功和失败，请参见错误代码) |
| message   | String | 错误内容                                  |

#### Error code

| Code | Description                                   |
| :--- | :-------------------------------------------- |
| -11  | startDate 值的格式不正确。 `YYYY-MM-DD`仅可用 |
| -12  | endDate 值的格式不正确。 `YYYY-MM-DD`仅可用   |

### 新用户（NRU）查找 API

您可以搜索新用户。

#### Request

- Method : GET
- URI : /user/statistics/nru

```text
GET
url : https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/user/statistics/nru
Header : 'accept-language: ko'
Header : 'x-api-key: {由GamePot信息​​中心发布的API密钥}'
```

| Header    | Type   | Required | Description            |
| :-------- | :----- | :------- | :--------------------- |
| x-api-key | String | O        | GamePot 发行的验证密钥 |

| Attribute | Type   | Description                     |
| :-------- | :----- | :------------------------------ |
| projectId | String | GamePot SDK 中的 ProjectId      |
| startDate | String | 查找开始日期 `YYYY-MM-DD`       |
| endDate   | String | 您想查看的最后日期 `YYYY-MM-DD` |

> 如果查询中不包含 startDate 和 endDate，则检索最近 30 天的数据。

#### Response

成功

```javascript
{
  "status": 1,
  "result": {
    "totalCount": 3,
    "edges": [
      {
        "node": {
          "date": "2020-04-10",
          "count": 2
        }
      },

    ...

      {
        "node": {
          "date": "2020-04-14",
          "count": 1
        }
      }
    ]
  }
}
```

| Attribute  | Type   | Description                               |
| :--------- | :----- | :---------------------------------------- |
| status     | Int    | 结果值(1：有关成功和失败，请参见错误代码) |
| totalCount | int    | 视图（例）                                |
| date       | String | 点算日期                                  |
| count      | int    | (适用日期) NRU                            |

失败

```javascript
{
  "status": -11,
  "message": "startDate format was wrong. (YYYY-MM-DD)"
}
```

| Attribute | Type   | Description                               |
| :-------- | :----- | :---------------------------------------- |
| status    | Int    | 结果值(1：有关成功和失败，请参见错误代码) |
| message   | String | 错误内容                                  |

#### Error code

| Code | Description                                                 |
| :--- | :---------------------------------------------------------- |
| -11  | 如果 startDate 值的格式不正确，则只能使用`YYYY-MM-DD`格式。 |
| -12  | 如果 endDate 值的格式不正确，则只能使用`YYYY-MM-DD`格式。   |

### 并发访问者（CCU）查询 API

对于 3 个选定的日期，您可以按时间搜索并发用户。

#### Request

- Method : GET
- URI : /user/statistics/ccu

```text
GET
url : https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/user/statistics/ccu
Header : 'accept-language: ko'
Header : 'x-api-key: {由GamePot信息​​中心发布的API密钥}'
```

| Header    | Type   | Required | Description            |
| :-------- | :----- | :------- | :--------------------- |
| x-api-key | String | O        | GamePot 发行的验证密钥 |

| Attribute | Type   | Description                  |
| :-------- | :----- | :--------------------------- |
| projectId | String | GamePot SDK 中的 ProjectId   |
| oneDate   | String | 首次查询日期 `YYYY-MM-DD`    |
| twoDate   | String | 第二次查询日期`YYYY-MM-DD`   |
| threeDate | String | 第三次搜索的日期`YYYY-MM-DD` |

> 查询包括 oneDate，twoDate 和 threeDate，如果没有查询，则会在该日期之前 2 天（包括该天）进行搜索。

#### Response

成功

```javascript
{
  "status": 1,
  "result": {
    "totalCount": 1440,
    "edges": [
      {
        "node": {
          "createdAt": "00:00",
          "one": 0,
          "two": 0,
          "three": 0
        }
      },

        ...

      {
        "node": {
          "createdAt": "23:59",
          "one": 0,
          "two": 0,
          "three": null
        }
      }
    ]
  }
}

```

| Attribute  | Type   | Description                               |
| :--------- | :----- | :---------------------------------------- |
| status     | Int    | 结果值(1：有关成功和失败，请参见错误代码) |
| totalCount | Int    | ccu 搜索结果（数量）                      |
| createdAt  | String | 计算日期和时间                            |
| one        | Int    | （第一个日期）的并发用户数                |  |
| two        | Int    | （第二个日期）的并发用户数                |  |
| three      | Int    | （第三个日期）的并发用户数                |  |

失败

```javascript
{
  "status": -11,
  "message": "threeDate format was wrong. (YYYY-MM-DD)"
}
```

| Attribute | Type   | Description                               |
| :-------- | :----- | :---------------------------------------- |
| status    | Int    | 结果值(1：有关成功和失败，请参见错误代码) |
| message   | String | 错误内容                                  |

#### Error code

| Code | Description                                                 |
| :--- | :---------------------------------------------------------- |
| -11  | 如果 threeDate 值的格式不正确，则只能使用`YYYY-MM-DD`格式。 |
| -12  | 如果 twoDate 值的格式不正确，则只能使用`YYYY-MM-DD`格式。   |
| -13  | 如果 oneDate 值的格式不正确，则只能使用`YYYY-MM-DD`格式。   |

### 付款查询 API

按付款 ID 显示付款明细。

#### Request

- Method : GET
- URI : /purchase/{transactionID}

```text
GET
url : https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/purchase/{transactionID}
Header : 'accept-language: ko'
Header : 'x-api-key: {由GamePot信息​​中心发布的API密钥}'
```

| Header    | Type   | Required | Description            |
| :-------- | :----- | :------- | :--------------------- |
| x-api-key | String | O        | GamePot 发行的验证密钥 |

| Attribute     | Type   | Description                |
| :------------ | :----- | :------------------------- |
| projectId     | String | GamePot SDK 中的 ProjectId |
| transactionID | String | GamePot SDK 的付款 ID      |

#### Response

成功

```javascript
{
  "status": 1,
  "result": {
    "status": 1,
    "exchange_price": 5000,
    "project_id": "xxxxxxxxxxxxxx",
    "store_id": "google",
    "payment_id": "google",
    "signature": "xxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    "order_id": "u8934",
    "currency": "KRW",
    "userdata": "{\"unique_id\":\"u8934\",\"server_id\":\"\",\"player_id\":\"\",\"etc\":\"\"}",
    "price": 5000,
    "id": "xxxxxxxxxxxxxx",
    "unique_id": "u8934",
    "transaction_id": "xxxxxxxxxxxxxx",
    "createdAt": "Wed Mar 18 2020 17:55:29 GMT+0900 (GMT+09:00)",
    "updatedAt": "Wed Mar 18 2020 17:55:29 GMT+0900 (GMT+09:00)",
    "request": "https://xxxxxxxxxxxxxx",
    "response": "{\"status\":1}",
    "item_id": {
      "status": null,
      "type": "inapp",
      "name": "name_001",
      "prices": []
    },
    "user_id": {
      "id": "xxxxxxxxxxxxxx",
      "deleted": false,
      "store_id": "google",
      "country": "KR",
      "remoteip": "xxx.xxx.xxx.xxx",
      "adid": "xxxxxxxxxxxxxx",
      "device": "android",
      "network": "WIFI",
      "version": "10",
      "model": "Pixel_3",
      "token": "xxxxxxxxxxxxxx",
      "push": true,
      "night": false,
      "ad": true,
      "memo": null,
      "device_id": "xxxxxxxxxxxxxx",
      "createdAt": "Wed Mar 18 2020 17:54:41 GMT+0900 (GMT+09:00)",
      "updatedAt": "Wed Mar 18 2020 17:54:42 GMT+0900 (GMT+09:00)",
      "loginedAt": "Wed Mar 18 2020 17:54:41 GMT+0900 (GMT+09:00)",
      "deletedAt": null
    }
  }
}
```

| Attribute          | Type   | Description                                                               |
| :----------------- | :----- | :------------------------------------------------------------------------ |
| status             | Int    | 结果值(1：有关成功和失败，请参见错误代码)                                 |
| (result의) status  | Int    | 付款结果（1：成功）                                                       |
| exchange_price     | Int    | 付款金额（采用汇率）                                                      |
| project_id         | String | GamePot SDK 中的 ProjectId                                                |
| store_id           | String | 店铺编号 (google,one,apple,galaxy)                                        |
| payment_id         | String | 付款商店编号 (google,tpay...) ㅣ通常与 store_id                           | 相同。 |
| signature          | String | 签名                                                                      |
| order_id           | String | Order ID                                                                  |
| currency           | String | 货币                                                                      |
| userdata           | String | 用户信息                                                                  |
| price              | Int    | 付款金额                                                                  |
| id                 | String | 付款数据的唯一 ID                                                         |
| unique_id          | String | Unique ID                                                                 |
| transaction_id     | String | 店铺付款 ID                                                               |
| createdAt          | String | 创建                                                                      |
| updatedAt          | String | 续约                                                                      |
| request            | String | 付款要求值                                                                |
| response           | String | 付款回应值                                                                |
| (item_id의) status | String | 结果值（属于 item_id）                                                    |
| type               | String | 物品种类(inapp)                                                           |
| name               | String | 项目名称                                                                  |
| prices             | String | 商品价格                                                                  |
| user_id            |        | 有关成功响应值的 user_id 部分，请参考<b> <I> User Inquiry API </I> </b>。 |

失败

```javascript
{
  "status": -6,
  "message": "projectId was wrong."
}
```

| Attribute | Type   | Description                             |
| :-------- | :----- | :-------------------------------------- |
| status    | Int    | 结果值（1：成功或失败，请参见错误代码） |
| message   | String | 错误内容                                |

### 付款取消查询 API

按付款 ID 查看付款取消明细。

> 仅查看 Google 付款。

#### Request

- Method : GET
- URI : /purchase/voided/{transactionID}

```text
GET
url : https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/purchase/voided/{transactionID}
Header : 'accept-language: ko'
Header : 'x-api-key: {由GamePot信息​​中心发布的API密钥}'
```

| Header    | Type   | Required | Description            |
| :-------- | :----- | :------- | :--------------------- |
| x-api-key | String | O        | GamePot 发行的验证密钥 |

| Attribute     | Type   | Description                |
| :------------ | :----- | :------------------------- |
| projectId     | String | GamePot SDK 中的 ProjectId |
| transactionID | String | GamePot SDK 的付款 ID      |

#### Response

成功

```javascript
{
  "status": 1,
  "result": {
    "id": "xxxxxxxxxxxxxx",
    "member_id": "xxxxxxxxxxxxxx",
    "package_id": "xxx.xxx.xxxxxxx",
    "price": 3000,
    "deleted": false,
    "purchasedAt": "Fri Feb 21 2020 16:32:35 GMT+0900 (GMT+09:00)",
    "voidedAt": "Fri Feb 21 2020 16:33:58 GMT+0900 (GMT+09:00)",
    "createdAt": "Fri Feb 21 2020 17:25:10 GMT+0900 (GMT+09:00)",
    "updatedAt": "Fri Feb 21 2020 17:25:10 GMT+0900 (GMT+09:00)",
    "deletedAt": null,
    "currency": "KRW",
    "status": 0,
    "purchase_id": {
      "status": 1,
      "exchange_price": 3000,
      "project_id": "xxxxxxxxxxxxxxxxxx",
      "store_id": "google",
      "payment_id": "google",
      "signature": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
      "order_id": "xxxxxxxxxxxxxx",
      "currency": "KRW",
      "userdata": "{\"unique_id\":\"\",\"server_id\":\"\",\"player_id\":\"\",\"etc\":\"\"}",
      "price": 3000,
      "id": "xxxxxxxxxxxxxx",
      "unique_id": "",
      "transaction_id": "GPA.3307-2597-6064-86473",
      "createdAt": "Fri Feb 21 2020 16:32:39 GMT+0900 (GMT+09:00)",
      "updatedAt": "Fri Feb 21 2020 17:25:10 GMT+0900 (GMT+09:00)",
      "request": "https://xxxxxxxxxxxxxxxxxxxxxxxxxxxx",
      "response": "{\"status\":1}"
    }
  }
}
```

| Attribute   | Type    | Description                                                              |
| :---------- | :------ | :----------------------------------------------------------------------- |
| status      | Int     | 结果值(1：有关成功和失败，请参见错误代码)                                |
| id          | String  | 取消付款                                                                 |
| member_id   | String  | 用户 UID                                                                 |
| package_id  | String  | 包裹名字                                                                 |
| price       | int     | 付款金额                                                                 |
| deleted     | Boolean | 是否删除 \(true : 删除, false : 正常\)                                   |
| purchasedAt | String  | 支付日期                                                                 |
| voidedAt    | String  | 付款取消日期                                                             |
| createdAt   | String  | 创建                                                                     |
| updatedAt   | String  | 续约                                                                     |
| deletedAt   | String  | 删除日期                                                                 |
| currency    | String  | 货币                                                                     |
| status      | Int     | 州                                                                       |
| purchase_id |         | 请参阅<b> <I>付款查询 API </I> </b>以获取成功响应值的 Purchase_id 部分。 |

失败

```javascript
{
  "status": -6,
  "message": "projectId was wrong."
}
```

| Attribute | Type   | Description                             |
| :-------- | :----- | :-------------------------------------- |
| status    | Int    | 结果值（1：成功或失败，请参见错误代码） |
| message   | String | 错误内容                                |

### 付款销售统计查询 API

显示计费销售统计信息。

#### Request

- Method : GET
- URI : /purchase/statistics

```text
GET
url : https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/purchase/statistics?startDate={startDate}&endDate={endDate}&currency={currency}
Header : 'accept-language: ko'
Header : 'x-api-key: {由GamePot信息​​中心发布的API密钥}'
```

| Header    | Type   | Required | Description            |
| :-------- | :----- | :------- | :--------------------- |
| x-api-key | String | O        | GamePot 发行的验证密钥 |

| Attribute | Type   | Description                                                |
| :-------- | :----- | :--------------------------------------------------------- |
| projectId | String | GamePot SDK 中的 ProjectId                                 |
| startDate | String | 付款销售统计信息搜索开始日期`YYYY-MM-DD`                   |
| endDate   | String | 付款销售统计信息搜索结束日期`YYYY-MM-DD`                   |
| currency  | String | 付款销售统计货币搜索 (all...)<br> 我们遵循 ISO 4217 法规。 |

> 如果查询中不包含 startDate 和 endDate，则将检索最近 30 天的数据。

#### Response

成功

```javascript
"status": 1,
  "result": {
    "totalCount": 13,
    "currencyList": [
      "KRW",
      "USD"
    ],
    "edges": [
      {
        "node": {
          "date": "2020-05-01",
          "count": 0
        }
      },
      {
        "node": {
          "date": "2020-05-02",
          "count": 0
        }
      },

...

      {
        "node": {
          "date": "2020-05-13",
          "count": 4008857.31
        }
      }
    ]
  }
}
```

| Attribute    | Type   | Description                               |
| :----------- | :----- | :---------------------------------------- |
| status       | Int    | 结果值(1：有关成功和失败，请参见错误代码) |
| totalCount   | Int    | 搜索结果值的数量                          |
| currencyList | String | 货币列表<br>使用了 ISO 4217。             |
| date         | String | 统计日期                                  |
| count        | String | 销售统计金额                              |

失败

```javascript
{
  "status": -6,
  "message": "projectId was wrong."
}
```

| Attribute | Type   | Description                               |
| :-------- | :----- | :---------------------------------------- |
| status    | Int    | 结果值(1：有关成功和失败，请参见错误代码) |
| message   | String | 错误内容                                  |

#### Error code

| Code | Description                                                 |
| :--- | :---------------------------------------------------------- |
| -11  | 如果 startDate 值的格式不正确，则只能使用`YYYY-MM-DD`格式。 |
| -12  | 如果 endDate 值的格式不正确，则只能使用`YYYY-MM-DD`格式。   |

### 字符查询 API

检索游戏中玩家 ID。

#### Request

- Method : GET
- URI : /player/{playerID}

```text
GET
url : https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/player/{playerID}
Header : 'accept-language: ko'
Header : 'x-api-key: {由GamePot信息​​中心发布的API密钥}'
```

| Header    | Type   | Required | Description            |
| :-------- | :----- | :------- | :--------------------- |
| x-api-key | String | O        | GamePot 发行的验证密钥 |

| Attribute | Type   | Description                |
| :-------- | :----- | :------------------------- |
| projectId | String | GamePot SDK 中的 ProjectId |
| playerID  | String | GamePot SDK 的玩家 ID      |

#### Response

成功

```javascript
{
  "status": 1,
  "result": {
    "id": "xxxxxxxxxxxxxxx",
    "player_id": "테스트아이디",
    "server_id": "테스트서버",
    "name": "테스트이름",
    "level": "12",
    "userdata": "dododo",
    "ip": "xxx.xxx.xxx.xxx",
    "createdAt": "Fri Feb 21 2020 14:15:33 GMT+0900 (GMT+09:00)",
    "updatedAt": "Fri Feb 21 2020 14:15:33 GMT+0900 (GMT+09:00)",
    "user_id": "xxxxxxxxxxxxxxx"
  }
}
```

| Attribute | Type   | Description                               |
| :-------- | :----- | :---------------------------------------- |
| status    | Int    | 结果值(1：有关成功和失败，请参见错误代码) |
| id        | String | 用户名                                    |
| player_id | String | 玩家编号                                  |
| server_id | String | 服务器 ID                                 |
| name      | String | 玩家名称                                  |
| level     | String | 玩家等级                                  |
| userdata  | String | 注册用户数据                              |
| ip        | String | 播放器 IP                                 |
| createdAt | String | 播放器创建日期                            |
| updatedAt | String | 播放器更新日期                            |
| user_id   | String | Gamepot UID                               |

失败

```javascript
{
  "status": -1,
  "message": "ApiKey was wrong."
}
```

| Attribute | Type   | Description                             |
| :-------- | :----- | :-------------------------------------- |
| status    | Int    | 结果值（1：成功或失败，请参见错误代码） |
| message   | String | 错误内容                                |

### 优惠券使用情况查询 API

查看优惠券使用记录。

> 对于关键字优惠券，仅显示使用过的优惠券。

#### Request

- Method : GET
- URI : /coupon/{couponNumber}

```text
GET
url : https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/coupon/{couponNumber}?userData={userData}
Header : 'accept-language: ko'
Header : 'x-api-key: {由GamePot信息​​中心发布的API密钥}'
```

| Header    | Type   | Required | Description            |
| :-------- | :----- | :------- | :--------------------- |
| x-api-key | String | O        | GamePot 发行的验证密钥 |

| Attribute    | Type   | Description                |
| :----------- | :----- | :------------------------- |
| projectId    | String | GamePot SDK 中的 ProjectId |
| couponNumber | String | 仪表板发出的优惠券编号     |
| userData     | String | 用户资料                   |

#### Response

成功

```javascript
{
  "status": 1,
  "result": {
    "id": "xxxxxxxxxxxxxxxx",
    "status": false,
    "enable": 1,
    "number": "xxxxxxxxxxxxxxxx",
    "userdata": "",
    "usedAt": null,
    "createdAt": "Wed May 13 2020 12:12:04 GMT+0900 (Korean Standard Time)",
    "request": null,
    "response": null,
    "coupon_id": {
      "id": "xxxxxxxxxxxxxxxx",
      "enable": 1,
      "type": "normal",
      "keyword": null,
      "desc": "시즌2 업데이트 사전예약 보상",
      "used": 1,
      "count": 2010,
      "length": 7,
      "limit": null,
      "prefix": "",
      "suffix": "",
      "store_id": "",
      "startedAt": "Sun May 10 2020 16:35:00 GMT+0900 (Korean Standard Time)",
      "endedAt": "Sat May 23 2020 16:35:00 GMT+0900 (Korean Standard Time)",
      "items": [
        {
          "item_id": "xxxxxxxxxxxxxxxx",
          "store_item_id": "xxxxxxxxxxxxxxxx",
          "count": 10
        },
        {
          "item_id": "xxxxxxxxxxxxxxxx",
          "store_item_id": "xxxxxxxxxxxxxxxx",
          "count": 1
        }
      ]
    }
  }
}
```

| Attribute            | Type    | Description                                   |
| :------------------- | :------ | :-------------------------------------------- |
| status               | Int     | 结果值(1：有关成功和失败，请参见错误代码)     |
| id                   | String  | 优惠券使用编号                                |
| status               | Boolean | 是否使用优惠券（true：已使用，false：未使用） |
| enable               | Int     | 整数供货情况                                  |
| number               | String  | 优惠券编号                                    |
| userdata             | String  | 优惠券用户信息                                |
| usedAt               | String  | 优惠券日                                      |
| request              | String  | 优惠券申请                                    |
| response             | String  | 优惠券使用回应                                |
| (coupon_id의) id     | String  | 优惠券 ID                                     |
| (coupon_id의) enable | int     | 供货情况                                      |
| type                 | String  | 优惠券类型                                    |
| keyword              | String  | 关键字优惠券关键字                            |
| desc                 | String  | 优惠券名称                                    |
| used                 | int     | 优惠券状态                                    |
| count                | int     | 优惠券数量                                    |
| length               | int     | 票券长度                                      |
| limit                | String  | 项目数量                                      |
| prefix               | String  | 优惠券后缀                                    |
| suffix               | String  | 优惠券前缀                                    |
| store_id             | String  | 商店 ID (google,one,apple,galaxy)             |
| startedAt            | String  | 优惠券开始日期                                |
| endedAt              | String  | 优惠券结束日期                                |
| item_id              | String  | 商品编号                                      |
| store_item_id        | String  | 物料商店 ID                                   |
| count                | int     | 项目数量                                      |

失败

```javascript
{
  "status": -1,
  "message": "ApiKey was wrong."
}
```

| Attribute | Type   | Description                             |
| :-------- | :----- | :-------------------------------------- |
| status    | Int    | 结果值（1：成功或失败，请参见错误代码） |
| message   | String | 错误内容                                |

### 优惠券使用 API

可使用优惠券。

#### Request

- Method : PUT
- URI : /store/{storeID}/user/{userID}/coupon/{couponNumber}

```text
PUT
url : https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/store/{storeID}/user/{userID}/coupon/{couponNumber}
Header : 'accept-language: ko'
Header : 'x-api-key: {由GamePot信息​​中心发布的API密钥}'
```

| Header    | Type   | Required | Description            |
| :-------- | :----- | :------- | :--------------------- |
| x-api-key | String | O        | GamePot 发行的验证密钥 |

| Attribute    | Type   | Description                      |
| :----------- | :----- | :------------------------------- |
| projectId    | String | GamePot SDK 中的 ProjectId       |
| storeID      | String | 商店 ID(google,one,apple,galaxy) |
| userID       | String | GamePot SDK 的用户名             |
| couponNumber | String | 优惠券编号                       |

#### Response

成功

```javascript
{
  "status": 1,
  "message": "success"
}
```

| Attribute | Type   | Description                               |
| :-------- | :----- | :---------------------------------------- |
| status    | Int    | 结果值(1：有关成功和失败，请参见错误代码) |
| message   | String | 结果内容                                  |

失败

```javascript
{
  "status": -5,
  "message": "ApiKey was expired."
}
```

| Attribute | Type   | Description                             |
| :-------- | :----- | :-------------------------------------- |
| status    | Int    | 结果值（1：成功或失败，请参见错误代码） |
| message   | String | 错误内容                                |
| errorcode | String | 错误代码                                |

### 通知 API 已发布

您可以查看正在发布的公告。

#### Request

- Method : GET
- URI : /store/{storeID}/notice/posting

```text
GET
url : https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/store/{storeID}/notice/posting
Header : 'accept-language: ko'
Header : 'x-api-key: {由GamePot信息​​中心发布的API密钥}'
```

| Header    | Type   | Required | Description            |
| :-------- | :----- | :------- | :--------------------- |
| x-api-key | String | O        | GamePot 发行的验证密钥 |

| Attribute | Type   | Description                        |
| :-------- | :----- | :--------------------------------- |
| projectId | String | GamePot SDK 中的 ProjectId         |
| storeID   | String | 店铺编号 (google,one,apple,galaxy) |

#### Response

成功

```javascript
{
  "status": 1,
  "result": {
    "totalCount": 1,
    "baseUrl": "https://kr.object.ncloudstorage.com/gamepot-rms76mi9",
    "edges": [
      {
        "node": {
          "id": "Tm90aWNlOjU5ZDY3MTE3LTYyZWUtNGY0ZC04YTc0LTIyZmIzZWNjYmJiMQ==",
          "store_id": "",
          "enable": true,
          "url": null,
          "scheme": null,
          "startDate": "Fri May 01 2020 15:21:00 GMT+0900 (Korean Standard Time)",
          "endDate": "Sun May 31 2020 18:24:00 GMT+0900 (Korean Standard Time)",
          "image": [
            {
              "lang": "ko",
              "value": "/notices/06cd531c-ff20-4139-bfa3-317def49dcc8.png",
              "default": true
            }
          ]
        }
      }
    ]
  }
}
```

| Attribute  | Type    | Description                                                  |
| :--------- | :------ | :----------------------------------------------------------- |
| status     | Int     | 结果值(1：有关成功和失败，请参见错误代码)                    |
| totalCount | String  | 通知（图片）查询（案例）数                                   |
| baseUrl    | String  | 对象存储桶 URL                                               |
| id         | String  | （图片的）唯一 ID                                            |
| store_id   | String  | 支付商店（谷歌，一个，苹果，银河） (google,one,apple,galaxy) |
| enable     | Boolean | 公告激活                                                     |
| url        | String  | (点击操作) url                                               |
| scheme     | String  | （点击操作）方案                                             |
| startDate  | String  | 通知开始日期                                                 |
| endDate    | String  | 通知结束日期                                                 |
| lang       | String  | 语言                                                         |
| value      | String  | （不超过 baseUrl）资源地址                                   |
| default    | Boolean | 默认语言                                                     |

失败

```javascript
{
  "status": -1,
  "message": "ApiKey was wrong."
}
```

| Attribute | Type   | Description                             |
| :-------- | :----- | :-------------------------------------- |
| status    | Int    | 结果值（1：成功或失败，请参见错误代码） |
| message   | String | 错误内容                                |
