---
search:
  keyword:
    - gamepot
---

#### **为提供 NAVER CLOUD PLATFORM 产品的详细使用方法和 API 的多种使用方式，分别提供<a href="https://guide.ncloud-docs.com/docs/zh/home" target="_blank">[说明书]</a>和<a href="https://api.ncloud-docs.com/docs/zh/home" target="_blank">[API 参考指南]</a>以供参考。**

<a href="https://api.ncloud-docs.com/docs/zh/game-gamepot" target="_blank">进入 Gamepot API 参考指南 >></a><br />
<a href="https://guide.ncloud-docs.com/docs/zh/game-gamepot-overview" target="_blank">进入 Gamepot 说明书 >></a>

# Open API

该功能可以利用规定的 API 调用 GAMEPOT 提供的几种功能。

> 须使用仪表盘发放的被允许的 API 密钥才能调用，可以指定是否使用及到期日。

## API 密钥发放

如想调用 Open API，必须先在仪表盘中创建 API 密钥。

API 密钥可在<b>仪表盘 > 项目设置 > API 密钥 </b>中创建。

![gamepot_api_01](./images/gamepot_api_01.png)

① 请点击添加按钮，创建 API 密钥。

![gamepot_api_02](./images/gamepot_api_02.png)

① 选择是否激活相应 API 密钥。

② 设置 API 密钥到期日。

③ 输入用户可以看懂的描述。

④ 利用添加按钮添加 API 密钥。

![gamepot_api_03](./images/gamepot_api_03.png)

点击已创建的 API 密钥，即可修改或删除状态。

> 使用 Open API 时，已创建的密钥值将进入头部的 x-api-key 值中。

## 使用 Open API

### 错误代码

发送 Open API 请求时发生的通用错误代码。

| 代码 | 描述                               |
| :--- | :--------------------------------- |
| -1   | 使用了仪表盘中没有的密钥时         |
| -2   | 仪表盘密钥和头部的密钥不同时       |
| -3   | 使用了仪表盘中已删除的密钥时       |
| -4   | 使用了仪表盘中作未使用处理的密钥时 |
| -5   | 密钥到期时                         |
| -6   | 没有项目 ID 时                     |


## 概述<a name="개요"></a>

该功能可以利用规定的API调用GAMEPOT提供的用户/优惠券/结算等功能。须使用仪表盘发放的已被授权的API Key才能调用，可以指定是否使用及到期日。

## 通用设置<a name="공통설정"></a>

### GAMEPOT API URL<a name="GAMEPOTAPIURL"></a>

```http
韩国区域 :
https://dashboard-api.gamepot.ntruss.com/v1/api

日本区域 
https://jp-dashboard-api.gamepot.ntruss.com/v1/api

新加坡区域
https://sg-dashboard-api.gamepot.ntruss.com/v1/api
```

### 请求报头<a name="요청헤더"></a>

| 报头名称| 说明|
|:----------|:----------|
| x-api-key| GamePot发放的认证密钥|

### 确认API KEY<a name="APIKEY확인하기"></a>

- 可以在GAMEPOT仪表盘 > 项目设置 > API Key页面创建或确认API Key。<br>



# 查询用户

使用用户UID查询用户。

## 请求<a name="请求"></a>


```http
GET https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/user/{userId}
```

| 项目| 类型| 是否为必填项| 描述| 备注|
| :---| :---| :---:| :---| :---|
| projectId| String| O| GamePot SDK的projectId|  |
| userId| String| O| GamePot SDK的userId|  |

### 请求头<a name="请求头"></a>


| 报头名称| 是否为必填项| 描述|
| :---| :---:| :---|
| x-api-key| O| GamePot发放的认证密钥|
| accept-language| X| 使用语言|


## 响应<a name="响应"></a>


| 字段名称| 类型| 描述|
| :---| :---| :---|
| status| Int| 结果值\（1：成功\）|
| id| String| 用户ID|
| deleted| Boolean| 是否删除会员 \（true：删除，false：正常\）|
| store_id| String| 创建账户时访问的商店(google...)|
| country| String| 用户国家代码（ISO 3166-1标准）|
| remoteip| String| 用户IP|
| adid| String| 广告ID|
| device| String| 设备种类(android,ios)|
| network| String| 用户访问网络(WI-FI...)|
| version| String| 客户的版本信息|
| model| String| 用户设备型号名称|
| token| String| 推送令牌|
| push| Boolean| 是否同意推送 \（true：同意，false：不同意\）|
| night| Boolean| 是否同意夜间推送 \（true：同意，false：不同意\）|
| ad| Boolean| 是否同意广告推送 \（true：同意，false：不同意\）|
| memo| String| 会员备忘录|
| device_id| String| 会员设备ID|
| createdAt| String| 会员创建日期|
| updatedAt| String| 会员信息修改日期|
| loginedAt| String| 最后访问日期|
| deletedAt| String| 会员删除日期|

## 示例<a name="示例"></a>


### 请求示例<a name="请求示例"></a>


```http
curl --request GET \
--url https://dashboard-api.gamepot.ntruss.com/v1/api/project/12a0f2ff-xxxx-xxxx-xxxx-9c13ef02f5fs/user/h43ea8e8-xxxx-xxxx-xxxx-531a46d25eef \
--header 'accept-language:ko' \
--header 'x-api-key:86dcgffae0641745432as02a8801ce5a5475f764fxxxxxxxxx'
```

### 响应示例<a name="响应示例"></a>


```http
{
  "status": 1,
  "result":{
    "id":"XXXXXXXX",
    "deleted":false,
    "store_id":"one",
    "country":"KR",
    "remoteip":"xxx.xxx.xxx.xxxx",
    "nickname":null,
    "adid":"XXXXXX-XXXX-XXXX-XXXX-XXXXXX",
    "device":"android",
    "network":"WIFI",
    "version":"11",
    "model":"SM-G977N",
    "token":"XXXXXXXX",
    "push":true,
    "push_date":{
        "on":"2023-04-21T11:22:55+09:00",
        "off":null
    },
    "night":true,
    "night_date":{
        "on":"2023-04-21T11:22:55+09:00",
        "off":"2023-04-20T11:22:58+09:00"
    },
    "ad":true,
    "memo":null,
    "device_id":"XXXXX-XXXXX-XXXXX",
    "agree":{
        "termsofuse":"Y",
        "termsofuseAt":"2023-04-21T11:22:55+09:00",
        "privacypolicy":"Y",
        "privacypolicyAt":"2023-04-21T11:22:55+09:00"
    },
    "verify":{
        "key":null,
        "updatedAt":null
    },
    "adult":null,
    "gdpr":{
        "status":4,
        "email_verified":null,
        "checked_story_category_ids":[
        "gdpr_term",
        "gdpr_privacy",
        "gdpr_push_normal",
        "gdpr_push_night"
        ]
    },
    "createdAt":"2023-04-21T11:22:55+09:00",
    "updatedAt":"2023-04-21T11:22:55+09:00",
    "loginedAt":"2023-04-21T11:22:55+09:00",
    "deletedAt":null
 }
}
```

## 错误代码<a name="错误代码"></a>



发送Gamepot Open API请求时发生的通用错误代码。

| 参数| 描述|
| :---| :---|
| status| 错误代码\（1：成功，失败时请参考Error code\）|
| message| 错误详细描述|

| 错误代码| 描述|
| :---:| :---|
| -1| 使用了仪表盘上没有的密钥时|
| -2| 仪表盘密钥和报头的密钥不同时|
| -3| 使用了仪表盘已删除的密钥时|
| -4| 使用了仪表盘中作为未使用处理的密钥时|
| -5| 密钥到期时|
| -6| 没有项目ID时|
```
{
  "status":-6,
  "message":"projectId was wrong."
}
```

# 查询用户停用

使用用户UID查询用户是否已停用。

## 请求<a name="请求"></a>


```http
GET https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/user/{userId}/block
```

| 项目| 类型| 是否为必填项| 描述| 备注|
| :---| :---| :---:| :---| :---|
| projectId| String| O| GamePot SDK的projectId|  |
| userId| String| O| GamePot SDK的userId|  |

### 请求头<a name="请求头"></a>


| 报头名称| 是否为必填项| 描述|
| :---| :---:| :---|
| x-api-key| O| GamePot发放的认证密钥|
| accept-language| X| 使用语言|


## 响应<a name="响应"></a>


| 字段名称| 类型| 描述|
| :---| :---| :---|
| status| Int| 结果值\（1：成功）|
| id| String| 用户停用信息相关ID|
| member_id| String| 用户ID|
| deleted| Boolean| 用户停用信息删除与否 \（true：删除，false：正常\）|
| type| String| 使用停用分类 \（manual：手动，autopurchase：自动\）|
| status| Int| 状态\（1：启用，2：禁用\）|
| message| String| 用户停用原因（目前未使用）|
| lang| String| 停用消息语言|
| value| String| 停用原因消息|
| default| Boolean| 设置默认语言<br>设备语言值未在messageMulti时，会默认显示设置为true的消息。|
| startedAt| String| 停用开始日期|
| endedAt| String| 停用结束日期|
| createdAt| Boolean| 停用注册日期|
| updatedAt| Boolean| 停用修改日期|
| deletedAt| Boolean| 停用删除日期|
| category_id| String| 停用分类ID|

## 示例<a name="示例"></a>


### 请求示例<a name="请求示例"></a>


```http
curl --request GET \
--url https://dashboard-api.gamepot.ntruss.com/v1/api/project/12a0f2ff-xxxx-xxxx-xxxx-9c13ef02f5fs/user/h43ea8e8-xxxx-xxxx-xxxx-531a46d25eef/block \
--header 'accept-language:ko' \
--header 'x-api-key:86dcgffae0641745432as02a8801ce5a5475f764fxxxxxxxxx'
```

### 响应示例<a name="响应示例"></a>


```http
{
  "status":1,
  "result":{
    "id":"xxxxxxxxxxxxxx",
    "member_id":"xxxxxxxxxxxxxx",
    "deleted":false,
    "type":"manual",
    "status":1,
    "message":null,
    "messageMulti":[
      {
        "lang":"ko",
        "value":"测试-ko",
        "default":true
      }
    ],
    "startedAt":"Mon May 11 2020 12:02:00 GMT+0900 (GMT+09:00)",
    "endedAt":"Mon May 25 2020 22:00:00 GMT+0900 (GMT+09:00)",
    "createdAt":"Tue May 12 2020 14:06:40 GMT+0900 (GMT+09:00)",
    "updatedAt":"Tue May 12 2020 14:06:40 GMT+0900 (GMT+09:00)",
    "deletedAt":null,
    "category_id":""
  }
}
```

## 错误代码<a name="错误代码"></a>


发送Gamepot Open API请求时发生的通用错误代码。

| 参数| 描述|
| :---| :---|
| status| 错误代码\（1：成功，失败时请参考Error code\）|
| message| 错误详细描述|

| 错误代码| 描述|
| :---:| :---|
| -1| 使用了仪表盘上没有的密钥时|
| -2| 仪表盘密钥和报头的密钥不同时|
| -3| 使用了仪表盘已删除的密钥时|
| -4| 使用了仪表盘中作为未使用处理的密钥时|
| -5| 密钥到期时|
| -6| 没有项目ID时|
```
{
  "status":-6,
  "message":"projectId was wrong."
}
```

# 设置用户停用

使用用户UID进行用户停用处理。

## 请求<a name="请求"></a>


```http
POST https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/user/{userId}/block
```

| 项目| 类型| 是否为必填项| 描述| 备注|
| :---| :---| :---:| :---| :---|
| projectId| String| O| GamePot SDK的projectId|   |
| userId| String| O| GamePot SDK的userId|   |

### 请求头<a name="请求头"></a>


| 报头名称| 是否为必填项| 描述|
| :---| :---:| :---|
| x-api-key| O| GamePot发放的认证密钥|
| accept-language| X| 使用语言|


### 请求体<a name="请求体"></a>


| 项目| 类型| 是否为必填项| 描述| 备注|
| :---| :---| :---:| :---| :---|
| lang| String| O| 停用消息语言|  |
| value| String| O| 停用原因消息|  |
| default| Boolean| O| 设置默认语言<br>设备语言值未在messageMulti时，会默认显示设置为true的消息。| true, false|       
| startedAt| String| O| 停用开始日期| `YYYY-MM-DD HH:mm`|
| endedAt| String| O| 停用结束日期| `YYYY-MM-DD HH:mm`|

## 响应<a name="响应"></a>


| 字段名称| 类型| 描述|
| :---| :---| :---|
| status| Int| 结果值\（1：成功\）|
| id| String| 已停用的ID|

## 示例<a name="示例"></a>


### 请求示例<a name="请求示例"></a>


```http
curl --request POST \
--url https://dashboard-api.gamepot.ntruss.com/v1/api/project/12a0f2ff-xxxx-xxxx-xxxx-9c13ef02f5fs/user/h43ea8e8-xxxx-xxxx-xxxx-531a46d25eef/block \
--header 'accept-language:ko' \
--header 'content-type:application/json' \
--header 'x-api-key:86dcgffae0641745432as02a8801ce5a5475f764fxxxxxxxxx'
  --data '{
	"messageMulti":[
		{
			"lang":"ko",
			"value":"测试-ko",
			"default":true
		}
	],
	"startedAt":"2020-05-11 12:02",
	"endedAt":"2020-05-25 22:00"
}'
```

### 响应示例<a name="响应示例"></a>


```http
{
  "status":1,
  "result":{
    "memberBlock":{
      "id":"xxxxxxxxxxxxx"
    }
  }
}
```

## 错误代码<a name="错误代码"></a>



发送Gamepot Open API请求时发生的通用错误代码。

| 参数| 描述|
| :---| :---|
| status| 错误代码\（1：成功，失败时请参考Error code\）|
| message| 错误详细描述|

| 错误代码| 描述|
| :---:| :---|
| -1| 使用了仪表盘上没有的密钥时|
| -2| 仪表盘密钥和报头的密钥不同时|
| -3| 使用了仪表盘已删除的密钥时|
| -4| 使用了仪表盘中作为未使用处理的密钥时|
| -5| 密钥到期时|
| -6| 没有项目ID时|
```
{
  "status":-6,
  "message":"projectId was wrong."
}
```

发送用户停用设置的API请求时发生的错误代码。

| 错误代码| 描述|
| :---:| :---|
| -11| body缺少数据|
| -12| messageMulti值不是JSON Array时|
| -13| startedAt值的格式有误时，仅可使用`YYYY-MM-DD HH:mm`形式|
| -14| endedAt值的格式有误时，仅可使用`YYYY-MM-DD HH:mm`形式|
| -15| messageMulti值的data格式有误时，|
| -16| messageMulti值的data中没有default true或存在多个时|
| -100| 该用户已设置为停用用户时|


# 查询每日访问者(DAU)

可以查询每日访问者。

## 请求<a name="请求"></a>


```http
GET https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/user/statistics/dau?startDate={startDate}&endDate={endDate}
```

| 项目| 类型| 是否为必填项| 描述| 备注|
| :---| :---| :---:| :---| :---|
| projectId| String| O| GamePot SDK的projectId|              |
| startDate| String| X| 要查询的起始日期| `YYYY-MM-DD`|
| endDate| String| X| 查询的最终日期| `YYYY-MM-DD`|
:::(Info) (参考)
 如果不输入startDate、endDate，则会查询最近30天内的数据。
:::

### 请求头<a name="请求头"></a>


| 报头名称| 是否为必填项| 描述|
| :---| :---:| :---|
| x-api-key| O| GamePot发放的认证密钥|
| accept-language| X| 使用语言|

## 响应<a name="响应"></a>


| 字段名称| 类型| 描述|
| :---| :---| :---|
| status| Int| 结果值\（1：成功\）|
| totalCount| Int| dau查询结果（个）数|
| date| String| 统计时间|
| count| Int| （相应日期）DAU|


## 示例<a name="示例"></a>

### 请求示例<a name="请求示例"></a>


```http
curl --request GET \
--url https://dashboard-api.gamepot.ntruss.com/v1/api/project/12a0f2ff-xxxx-xxxx-xxxx-9c13ef02f5fs/user/statistics/dau?startDate=2020-03-01&endDate=2020-06-01
--header 'accept-language:ko' \
--header 'x-api-key:86dcgffae0641745432as02a8801ce5a5475f764fxxxxxxxxx'
```

### 响应示例<a name="响应示例"></a>


```http
{
  "status":1,
  "result":{
    "totalCount":3,
    "edges":[
      {
        "node":{
          "date":"Fri Apr 10 2020 09:00:00 GMT+0900 (Korean Standard Time)",
          "count":2
        }
      },

      ...

      {
        "node":{
          "date":"Tue Apr 14 2020 09:00:00 GMT+0900 (Korean Standard Time)",
          "count":4
        }
      }
    ]
  }
}
```

## 错误代码<a name="错误代码"></a>



发送Gamepot Open API请求时发生的通用错误代码。

| 参数| 描述|
| :---| :---|
| status| 错误代码\（1：成功，失败时请参考Error code\）|
| message| 错误详细描述|

| 错误代码| 描述|
| :---:| :---|
| -1| 使用了仪表盘上没有的密钥时|
| -2| 仪表盘密钥和报头的密钥不同时|
| -3| 使用了仪表盘已删除的密钥时|
| -4| 使用了仪表盘中作为未使用处理的密钥时|
| -5| 密钥到期时|
| -6| 没有项目ID时|
```
{
  "status":-6,
  "message":"projectId was wrong."
}
```

发送查询每日访问者(DAU)的API请求时发生的错误代码。

| 错误代码| 描述|
| :---:| :---|
| -11| startDate值的格式有误时，仅可使用`YYYY-MM-DD`形式|
| -12| endDate值的格式有误时，仅可使用`YYYY-MM-DD`形式|


# 查询新用户(NRU)

可以查询新用户。

## 请求<a name="请求"></a>


```http
GET https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/user/statistics/nru?startDate={startDate}&endDate={endDate}
```

| 项目| 类型| 是否为必填项| 描述| 备注|
| :---| :---| :---:| :---| :---|
| projectId| String| O| GamePot SDK的projectId|  |
| startDate| String| X| 要查询的起始日期| `YYYY-MM-DD`|
| endDate| String| X| 查询的最终日期| `YYYY-MM-DD`|
:::(Info) (参考)
 如果不输入startDate、endDate，则会查询最近30天内的数据。
:::

### 请求头<a name="请求头"></a>


| 报头名称| 是否为必填项| 描述|
| :---| :---:| :---|
| x-api-key| O| GamePot发放的认证密钥|
| accept-language| X| 使用语言|


## 响应<a name="响应"></a>


| 字段名称| 类型| 描述|
| :---| :---| :---|
| status| Int| 结果值\（1：成功）|
| totalCount| int| 查询（个）数|  
| date| String| 统计日期|     
| count| int| （相应日期）NRU|     


## 示例<a name="示例"></a>


### 请求示例<a name="请求示例"></a>


```http
curl --request GET \
--url https://dashboard-api.gamepot.ntruss.com/v1/api/project/12a0f2ff-xxxx-xxxx-xxxx-9c13ef02f5fs/user/statistics/nru?startDate=2020-03-01&endDate=2020-06-01
--header 'accept-language:ko' \
--header 'x-api-key:86dcgffae0641745432as02a8801ce5a5475f764fxxxxxxxxx'
```

### 响应示例<a name="响应示例"></a>


```http
{
  "status":1,
  "result":{
    "totalCount":3,
    "edges":[
      {
        "node":{
          "date":"2020-04-10",
          "count":2
        }
      },

    ...

      {
        "node":{
          "date":"2020-04-14",
          "count":1
        }
      }
    ]
  }
}
```

## 错误代码<a name="错误代码"></a>



发送Gamepot Open API请求时发生的通用错误代码。

| 参数| 描述|
| :---| :---|
| status| 错误代码\（1：成功，失败时请参考Error code\）|
| message| 错误详细描述|

| 错误代码| 描述|
| :---:| :---|
| -1| 使用了仪表盘上没有的密钥时|
| -2| 仪表盘密钥和报头的密钥不同时|
| -3| 使用了仪表盘已删除的密钥时|
| -4| 使用了仪表盘中作为未使用处理的密钥时|
| -5| 密钥到期时|
| -6| 没有项目ID时|
```
{
  "status":-6,
  "message":"projectId was wrong."
}
```

发送查询新用户(NRU)的API请求时发生的错误代码。

| 错误代码| 描述|
| :---:| :---|
| -11| startDate值的格式有误时，仅可使用`YYYY-MM-DD`形式|
| -12| endDate值的格式有误时，仅可使用`YYYY-MM-DD`形式|


# 查询同时访问者(CCU)

可以查询所选3个日期的各时间段同时访问者。

## 请求<a name="请求"></a>


```http
GET https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/user/statistics/ccu?oneDate={oneDate}&twoDate={twoDate}&threeDate={threeDate}
```

| 项目| 类型| 是否为必填项| 描述| 备注|
| :---| :---| :---:| :---| :---|
| projectId| String| O| GamePot SDK的projectId|  |
| oneDate| String| X| 第一个要查询的日期| `YYYY-MM-DD`|
| twoDate| String| X| 第二个要查询的日期| `YYYY-MM-DD`|
| threeDate| String| X| 第三个要查询的日期| `YYYY-MM-DD`|
:::(Info) (参考)
提供oneDate、twoDate、threeDate的查询条件，未提供时可查询当天及前2日的访问者。
:::

### 请求头<a name="请求头"></a>


| 报头名称| 是否为必填项| 描述|
| :---| :---:| :---|
| x-api-key| O| GamePot发放的认证密钥|
| accept-language| X| 使用语言|

## 响应<a name="响应"></a>


| 字段名称| 类型| 描述|
| :---| :---| :---|
| status| Int| 结果值\（1：成功\）|  
| totalCount| Int| ccu查询结果（个）数|
| createdAt| String| 统计时间|
| one| Int| （第一个日期的）相应时间同时访问者数|
| two| Int| （第二个日期的）相应时间同时访问者数|
| three| Int| （第三个日期的）相应时间同时访问者数|

## 示例<a name="示例"></a>


### 请求示例<a name="请求示例"></a>


```http
curl --request GET \
--url https://dashboard-api.gamepot.ntruss.com/v1/api/project/12a0f2ff-xxxx-xxxx-xxxx-9c13ef02f5fs/user/statistics/ccu?oneDate=2020-03-01&twoDate=2020-04-01&threeDate=2020-05-09
--header 'accept-language:ko' \
--header 'x-api-key:86dcgffae0641745432as02a8801ce5a5475f764fxxxxxxxxx'
```

### 响应示例<a name="响应示例"></a>

```http
{
  "status":1,
  "result":{
    "totalCount":1440,
    "edges":[
      {
        "node":{
          "createdAt":"00:00",
          "one":0,
          "two":0,
          "three":0
        }
      },

        ...

      {
        "node":{
          "createdAt":"23:59",
          "one":0,
          "two":0,
          "three":null
        }
      }
    ]
  }
}
```

## 错误代码<a name="错误代码"></a>


发送Gamepot Open API请求时发生的通用错误代码。

| 参数| 描述|
| :---| :---|
| status| 错误代码\（1：成功，失败时请参考Error code\）|
| message| 错误详细描述|

| 错误代码| 描述|
| :---:| :---|
| -1| 使用了仪表盘上没有的密钥时|
| -2| 仪表盘密钥和报头的密钥不同时|
| -3| 使用了仪表盘已删除的密钥时|
| -4| 使用了仪表盘中作为未使用处理的密钥时|
| -5| 密钥到期时|
| -6| 没有项目ID时|
```
{
  "status":-6,
  "message":"projectId was wrong."
}
```

发送查询同时访问者(CCU)API请求时发生的错误代码。

| 错误代码| 描述|
| :---:| :---|
| -11| threeDate值的格式有误时，仅可使用`YYYY-MM-DD`形式|
| -12| twoDate值的格式有误时，仅可使用`YYYY-MM-DD`形式|
| -13| oneDate值的格式有误时，仅可使用`YYYY-MM-DD`形式|


# 查询支付

以支付ID查询支付明细。

## 请求<a name="请求"></a>


```http
GET https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/purchase/{transactionID}
```

| 项目| 类型| 是否为必填项| 描述| 备注|
| :---| :---| :---:| :---| :---|
| projectId| String| O| GamePot SDK的projectId|   |
| transactionID| String| O| GamePot SDK的支付ID|   |

### 请求头<a name="请求头"></a>


| 报头名称| 是否为必填项| 描述|
| :---| :---:| :---|
| x-api-key| O| GamePot发放的认证密钥|
| accept-language| X| 使用语言|

## 响应<a name="响应"></a>


| 字段名称| 类型| 描述|
| :---| :---| :---|
| status| Int| 结果值\（1：成功\）|
| （result的）status| Int| 支付结果值\（1：成功）|
| exchange_price| Int| 支付金额（适用汇率）|
| project_id| String| GamePot SDK的projectId|
| store_id| String| 商店ID(google,one,apple,galaxy)|
| payment_id| String| 支付商店ID(google,tpay...)ㅣ一般与store_id相同|
| signature| String| 签名|
| order_id| String| Order ID|
| currency| String| 货币|
| userdata| String| 用户信息|
| price| Int| 支付金额|
| id| String| 支付数据的unique ID|
| unique_id| String| Unique ID|
| transaction_id| String| 商店支付ID|
| createdAt| String| 创建日期|
| updatedAt| String| 更新日期|
| request| String| 支付请求值|
| response| String| 支付响应值|
| （item_id的）status| String| （item_id的）结果值|
| type| String| 道具类型(inapp)|
| name| String| 道具名称|
| prices| String| 道具价格|
| user_id|        | 响应成功值中user_id部分<b><I>请参阅用户查询API</I></b>。|

## 示例<a name="示例"></a>


### 请求示例<a name="请求示例"></a>


```http
curl --request GET \
  --url https://dashboard-api.gamepot.ntruss.com/v1/api/project/12a0f2ff-xxxx-xxxx-xxxx-9c13ef02f5fs/purchase/GPA.xxxx-xxxx-xxxx-xxxxxx \
  --header 'accept-language:ko' \
  --header 'x-api-key:86dcgffae0641745432as02a8801ce5a5475f764fxxxxxxxxx'
```

### 响应示例<a name="响应示例"></a>


```http
{
  "status":1,
  "result":{
    "status":1,
    "exchange_price":5000,
    "project_id":"xxxxxxxxxxxxxx",
    "store_id":"google",
    "payment_id":"google",
    "signature":"xxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    "order_id":"u8934",
    "currency":"KRW",
    "userdata":"{\"unique_id\":\"u8934\",\"server_id\":\"\",\"player_id\":\"\",\"etc\":\"\"}",
    "price":5000,
    "id":"xxxxxxxxxxxxxx",
    "unique_id":"u8934",
    "transaction_id":"xxxxxxxxxxxxxx",
    "createdAt":"Wed Mar 18 2020 17:55:29 GMT+0900 (GMT+09:00)",
    "updatedAt":"Wed Mar 18 2020 17:55:29 GMT+0900 (GMT+09:00)",
    "request":"https://xxxxxxxxxxxxxx",
    "response":"{\"status\":1}",
    "item_id":{
      "status":null,
      "type":"inapp",
      "name":"name_001",
      "prices":[]
    },
    "user_id":{
      "id":"xxxxxxxxxxxxxx",
      "deleted":false,
      "store_id":"google",
      "country":"KR",
      "remoteip":"xxx.xxx.xxx.xxx",
      "adid":"xxxxxxxxxxxxxx",
      "device":"android",
      "network":"WIFI",
      "version":"10",
      "model":"Pixel_3",
      "token":"xxxxxxxxxxxxxx",
      "push":true,
      "night":false,
      "ad":true,
      "memo":null,
      "device_id":"xxxxxxxxxxxxxx",
      "createdAt":"Wed Mar 18 2020 17:54:41 GMT+0900 (GMT+09:00)",
      "updatedAt":"Wed Mar 18 2020 17:54:42 GMT+0900 (GMT+09:00)",
      "loginedAt":"Wed Mar 18 2020 17:54:41 GMT+0900 (GMT+09:00)",
      "deletedAt":null
    }
  }
}
```

## 错误代码<a name="错误代码"></a>



发送Gamepot Open API请求时发生的通用错误代码。

| 参数| 描述|
| :---| :---|
| status| 错误代码\（1：成功，失败时请参考Error code\）|
| message| 错误详细描述|

| 错误代码| 描述|
| :---:| :---|
| -1| 使用了仪表盘上没有的密钥时|
| -2| 仪表盘密钥和报头的密钥不同时|
| -3| 使用了仪表盘已删除的密钥时|
| -4| 使用了仪表盘中作为未使用处理的密钥时|
| -5| 密钥到期时|
| -6| 没有项目ID时|
```
{
  "status":-6,
  "message":"projectId was wrong."
}
```


# 查询取消支付

以支付ID查询取消支付明细。
:::(Info) (参考)
只能查询谷歌支付。
:::

## 请求<a name="请求"></a>

```http
GET https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/purchase/voided/{transactionID}
```

| 项目| 类型| 是否为必填项| 描述| 备注|
| :---| :---| :---:| :---| :---|
| projectId| String| O| GamePot SDK的projectId|   |
| transactionID| String| O| GamePot SDK的支付ID|   |

### 请求头<a name="请求头"></a>


| 报头名称| 是否为必填项| 描述|
| :---| :---:| :---|
| x-api-key| O| GamePot发放的认证密钥|
| accept-language| X| 使用语言|

## 响应<a name="响应"></a>


| 字段名称| 类型| 描述|
| :---| :---| :---|
| status| Int| 结果值\（1：成功\）|
| id| String| 取消支付ID|
| member_id| String| 用户UID|
| package_id| String| 包名称|
| price| int| 支付金额|
| deleted| Boolean| 是否删除 \（true：删除，false：正常\）|
| purchasedAt| String| 支付日期|
| voidedAt| String| 取消支付日期|
| createdAt| String| 创建日期|
| updatedAt| String| 更新日期|
| deletedAt| String| 删除日期|
| currency| String| 货币|
| status| Int| 状态|
| purchase_id|         | 响应成功值中purchase_id部分<b><I>请参阅支付查询API</I></b>。|

## 示例<a name="示例"></a>


### 请求示例<a name="请求示例"></a>


```http

curl --request GET \
  --url https://dashboard-api.gamepot.ntruss.com/v1/api/project/12a0f2ff-xxxx-xxxx-xxxx-9c13ef02f5fs/purchase/voided/GPA.3381-xxxx-xxxx-12398 \
  --header 'accept-language:ko' \
  --header 'x-api-key:86dcgffae0641745432as02a8801ce5a5475f764fxxxxxxxxx'
```

### 响应示例<a name="响应示例"></a>


```http
{
  "status":1,
  "result":{
    "id":"xxxxxxxxxxxxxx",
    "member_id":"xxxxxxxxxxxxxx",
    "package_id":"xxx.xxx.xxxxxxx",
    "price":3000,
    "deleted":false,
    "purchasedAt":"Fri Feb 21 2020 16:32:35 GMT+0900 (GMT+09:00)",
    "voidedAt":"Fri Feb 21 2020 16:33:58 GMT+0900 (GMT+09:00)",
    "createdAt":"Fri Feb 21 2020 17:25:10 GMT+0900 (GMT+09:00)",
    "updatedAt":"Fri Feb 21 2020 17:25:10 GMT+0900 (GMT+09:00)",
    "deletedAt":null,
    "currency":"KRW",
    "status":0,
    "purchase_id":{
      "status":1,
      "exchange_price":3000,
      "project_id":"xxxxxxxxxxxxxxxxxx",
      "store_id":"google",
      "payment_id":"google",
      "signature":"xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
      "order_id":"xxxxxxxxxxxxxx",
      "currency":"KRW",
      "userdata":"{\"unique_id\":\"\",\"server_id\":\"\",\"player_id\":\"\",\"etc\":\"\"}",
      "price":3000,
      "id":"xxxxxxxxxxxxxx",
      "unique_id":"",
      "transaction_id":"GPA.3307-2597-6064-86473",
      "createdAt":"Fri Feb 21 2020 16:32:39 GMT+0900 (GMT+09:00)",
      "updatedAt":"Fri Feb 21 2020 17:25:10 GMT+0900 (GMT+09:00)",
      "request":"https://xxxxxxxxxxxxxxxxxxxxxxxxxxxx",
      "response":"{\"status\":1}"
    }
  }
}
```

## 错误代码<a name="错误代码"></a>



发送Gamepot Open API请求时发生的通用错误代码。

| 参数| 描述|
| :---| :---|
| status| 错误代码\（1：成功，失败时请参考Error code\）|
| message| 错误详细描述|

| 错误代码| 描述|
| :---:| :---|
| -1| 使用了仪表盘上没有的密钥时|
| -2| 仪表盘密钥和报头的密钥不同时|
| -3| 使用了仪表盘已删除的密钥时|
| -4| 使用了仪表盘中作为未使用处理的密钥时|
| -5| 密钥到期时|
| -6| 没有项目ID时|
```
{
  "status":-6,
  "message":"projectId was wrong."
}
```

# 查询支付销售统计

查询支付销售统计。

## 请求<a name="请求"></a>


```http
GET https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/purchase/statistics?startDate={startDate}&endDate={endDate}&currency={currency}
```

| 项目| 类型| 是否为必填项| 描述| 备注|
| :---| :---| :---:| :---| :---|
| projectId| String| O| GamePot SDK的projectId|   |
| startDate| String| X| 支付销售统计搜索起始日期| `YYYY-MM-DD`|
| endDate| String| X| 支付销售统计搜索截止日期| `YYYY-MM-DD`|
| currency| String| X| 支付销售统计货币搜索(all...)| 遵循ISO 4217标准。|
:::(Info) (参考)
如果不输入startDate、endDate，则会查询最近30天内的数据。
:::

### 请求头<a name="请求头"></a>


| 报头名称| 是否为必填项| 描述|
| :---| :---:| :---|
| x-api-key| O| GamePot发放的认证密钥|
| accept-language| X| 使用语言|

## 响应<a name="响应"></a>


| 字段名称| 类型| 描述|
| :---| :---| :---|
| status| Int| 结果值\（1：成功\）|
| totalCount| Int| 搜索结果值数|
| currencyList| String| 货币列表<br>遵循ISO 4217标准。|
| date| String| 统计日期|
| count| String| 销量统计金额|

## 示例<a name="示例"></a>


### 请求示例<a name="请求示例"></a>


```http

curl --request GET \
  --url https://dashboard-api.gamepot.ntruss.com/v1/api/project/12a0f2ff-xxxx-xxxx-xxxx-9c13ef02f5fs/purchase/statistics?startDate=2020-05-01&endDate=2020-06-01&currency=all \
  --header 'accept-language:ko' \
  --header 'x-api-key:86dcgffae0641745432as02a8801ce5a5475f764fxxxxxxxxx'
```

### 响应示例<a name="响应示例"></a>


```http
"status":1,
  "result":{
    "totalCount":13,
    "currencyList":[
      "KRW",
      "USD"
    ],
    "edges":[
      {
        "node":{
          "date":"2020-05-01",
          "count":0
        }
      },
      {
        "node":{
          "date":"2020-05-02",
          "count":0
        }
      },

...

      {
        "node":{
          "date":"2020-05-13",
          "count":4008857.31
        }
      }
    ]
  }
}
```

## 错误代码<a name="错误代码"></a>



发送Gamepot Open API请求时发生的通用错误代码。

| 参数| 描述|
| :---| :---|
| status| 错误代码\（1：成功，失败时请参考Error code\）|
| message| 错误详细描述|

| 错误代码| 描述|
| :---:| :---|
| -1| 使用了仪表盘上没有的密钥时|
| -2| 仪表盘密钥和报头的密钥不同时|
| -3| 使用了仪表盘已删除的密钥时|
| -4| 使用了仪表盘中作为未使用处理的密钥时|
| -5| 密钥到期时|
| -6| 没有项目ID时|
```
{
  "status":-6,
  "message":"projectId was wrong."
}
```

发送支付销售统计查询API请求时发生的错误代码。

| 错误代码| 描述|
| :---:| :---|
| -11| startDate值的格式有误时，仅可使用`YYYY-MM-DD`形式|
| -12| endDate值的格式有误时，仅可使用`YYYY-MM-DD`形式|


# 查询角色

查询游戏内玩家ID。

## 请求<a name="请求"></a>


```http
GET https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/player/{playerID}
```

| 项目| 类型| 是否为必填项| 描述| 备注|
| :---| :---| :---:| :---| :---|
| projectId| String| O| GamePot SDK的projectId|   |
| playerID| String| O| GamePot SDK的玩家ID|   |

### 请求头<a name="请求头"></a>

| 报头名称| 是否为必填项| 描述|
| :---| :---:| :---|
| x-api-key| O| GamePot发放的认证密钥|
| accept-language| X| 使用语言|

## 响应<a name="响应"></a>


| 字段名称| 类型| 描述|
| :---| :---| :---|
| status| Int| 结果值\（1：成功\）|
| id| String| 用户ID|
| player_id| String| 玩家ID|
| server_id| String| 服务器ID|
| name| String| 玩家名|
| level| String| 玩家等级|
| userdata| String| 注册的Userdata|
| ip| String| 玩家IP|
| createdAt| String| 玩家创建日期|
| updatedAt| String| 玩家更新日期|
| user_id| String| GAMEPOT UID|

## 示例<a name="示例"></a>


### 请求示例<a name="请求示例"></a>


```http

curl --request GET \
  --url https://dashboard-api.gamepot.ntruss.com/v1/api/project/12a0f2ff-xxxx-xxxx-xxxx-9c13ef02f5fs/player/dodo  \
  --header 'accept-language:ko' \
  --header 'x-api-key:86dcgffae0641745432as02a8801ce5a5475f764fxxxxxxxxx'
```

### 响应示例<a name="响应示例"></a>


```http
{
  "status":1,
  "result":{
    "id":"xxxxxxxxxxxxxxx",
    "player_id":"测试ID",
    "server_id":"测试服务器",
    "name":"测试名称",
    "level":"12",
    "userdata":"dododo",
    "ip":"xxx.xxx.xxx.xxx",
    "createdAt":"Fri Feb 21 2020 14:15:33 GMT+0900 (GMT+09:00)",
    "updatedAt":"Fri Feb 21 2020 14:15:33 GMT+0900 (GMT+09:00)",
    "user_id":"xxxxxxxxxxxxxxx"
  }
}
```

## 错误代码<a name="错误代码"></a>



发送Gamepot Open API请求时发生的通用错误代码。

| 参数| 描述|
| :---| :---|
| status| 错误代码\（1：成功，失败时请参考Error code\）|
| message| 错误详细描述|

| 错误代码| 描述|
| :---:| :---|
| -1| 使用了仪表盘上没有的密钥时|
| -2| 仪表盘密钥和报头的密钥不同时|
| -3| 使用了仪表盘已删除的密钥时|
| -4| 使用了仪表盘中作为未使用处理的密钥时|
| -5| 密钥到期时|
| -6| 没有项目ID时|
```
{
  "status":-6,
  "message":"projectId was wrong."
}
```


# 查询一般优惠券的使用

查询一般优惠券使用明细。
无法查询关键词优惠券使用明细。

## 请求<a name="请求"></a>


```http
GET https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/coupon/{couponNumber}
```

| 项目| 类型| 是否为必填项| 描述| 备注|
| :---| :---| :---:| :---| :---|
| projectId| String| O| GamePot SDK的projectId|   |
| couponNumber| String| O| 仪表盘发放的优惠券编号|   |

### 请求头<a name="请求头"></a>


| 报头名称| 是否为必填项| 描述|
| :---| :---:| :---|
| x-api-key| O| GamePot发放的认证密钥|
| accept-language| X| 使用语言|

## 响应<a name="响应"></a>


| 字段名称| 类型| 描述|
| :---| :---| :---|
| status| Int| 结果值\（1：成功\）|
| id| String| 优惠券使用明细ID|
| status| Boolean| 是否使用优惠券\（true：使用，false：未使用\）|
| enable| Int| 是否可用|
| number| String| 优惠券编号|
| userdata| String| 优惠券使用用户查询|
| usedAt| String| 优惠券使用日期|
| request| String| 优惠券使用请求|
| response| String| 优惠券使用响应|
| （coupon_id的）id| String| 优惠券ID|
| （coupon_id的）enable| int| 是否可用|
| type| String| 优惠券类型|
| keyword| String| 关键词优惠券关键词|
| desc| String| 优惠券名称|
| used| int| 优惠券状态|
| count| int| 优惠券数量|
| length| int| 优惠券长度|
| limit| String| 道具数量|
| prefix| String| 优惠券后缀|
| suffix| String| 优惠券前缀|
| store_id| String| 商店ID(google,one,apple,galaxy)|
| startedAt| String| 优惠券使用开始日期|
| endedAt| String| 优惠券使用结束日期|
| item_id| String| 道具ID|
| store_item_id| String| 道具商店ID|
| count| int| 道具数量|

## 示例<a name="示例"></a>


### 请求示例<a name="请求示例"></a>


```http

curl --request GET \
  --url https://dashboard-api.gamepot.ntruss.com/v1/api/project/12a0f2ff-xxxx-xxxx-xxxx-9c13ef02f5fs/coupon/xxxxxx  \
  --header 'accept-language:ko' \
  --header 'x-api-key:86dcgffae0641745432as02a8801ce5a5475f764fxxxxxxxxx'
```

### 响应示例<a name="响应示例"></a>


```http
{
  "status":1,
  "result":{
    "id":"xxxxxxxxxxxxxxxx",
    "status":false,
    "enable":1,
    "number":"xxxxxxxxxxxxxxxx",
    "userdata":"",
    "usedAt":null,
    "createdAt":"Wed May 13 2020 12:12:04 GMT+0900 (Korean Standard Time)",
    "request":null,
    "response":null,
    "coupon_id":{
      "id":"xxxxxxxxxxxxxxxx",
      "enable":1,
      "type":"normal",
      "keyword":null,
      "desc":"第2季更新提前预约奖励",
      "used":1,
      "count":2010,
      "length":7,
      "limit":null,
      "prefix":"",
      "suffix":"",
      "store_id":"",
      "startedAt":"Sun May 10 2020 16:35:00 GMT+0900 (Korean Standard Time)",
      "endedAt":"Sat May 23 2020 16:35:00 GMT+0900 (Korean Standard Time)",
      "items":[
        {
          "item_id":"xxxxxxxxxxxxxxxx",
          "store_item_id":"xxxxxxxxxxxxxxxx",
          "count":10
        },
        {
          "item_id":"xxxxxxxxxxxxxxxx",
          "store_item_id":"xxxxxxxxxxxxxxxx",
          "count":1
        }
      ]
    }
  }
}
```

## 错误代码<a name="错误代码"></a>


发送Gamepot Open API请求时发生的通用错误代码。

| 参数| 描述|
| :---| :---|
| status| 错误代码\（1：成功，失败时请参考Error code\）|
| message| 错误详细描述|

| 错误代码| 描述|
| :---:| :---|
| -1| 使用了仪表盘上没有的密钥时|
| -2| 仪表盘密钥和报头的密钥不同时|
| -3| 使用了仪表盘已删除的密钥时|
| -4| 使用了仪表盘中作为未使用处理的密钥时|
| -5| 密钥到期时|
| -6| 没有项目ID时|
```
{
  "status":-6,
  "message":"projectId was wrong."
}
```

# 使用优惠券

可以使用一般优惠券和关键词优惠券。

## 请求<a name="请求"></a>


```http
PUT https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/store/{storeID}/user/{userID}/coupon/{couponNumber}?userData={userData}
```

| 项目| 类型| 是否为必填项| 描述| 备注|
| :---| :---| :---:| :---| :---|
| projectId| String| O| GamePot SDK的projectId|   |
| storeID| String| O| 商店ID(google,one,apple,galaxy)|   |
| userID| String| O| GamePot SDK的用户UID|   |
| couponNumber| String| O| 仪表盘发放的优惠券编号|   |
  | userData  | String | X |  웹훅 API  파라미터 중 userData 항목에 넣을 추가 정보              |   |

### 请求头<a name="请求头"></a>


| 报头名称| 是否为必填项| 描述|
| :---| :---:| :---|
| x-api-key| O| GamePot发放的认证密钥|
| accept-language| X| 使用语言|

## 响应<a name="响应"></a>


| 字段名称| 类型| 描述|
| :---| :---| :---|
| status| Int| 结果值\（1：成功\）|
| message| String| 结果内容|     

## 示例<a name="示例"></a>


### 请求示例<a name="请求示例"></a>


```http
  curl --request PUT \
  --url https://dashboard-api.gamepot.ntruss.com/v1/api/project/12a0f2ff-xxxx-xxxx-xxxx-9c13ef02f5fs/store/google/user/h43ea8e8-xxxx-xxxx-xxxx-531a46d25eef/coupon/xxxxxx \
  --header 'accept-language: ko' \
  --header 'x-api-key: 86dcgffae064174543xxxx02a8801ce5a547xxxxxxxxxxxxxx'

```

### 响应示例<a name="响应示例"></a>


```http
{
  "status":1,
  "message":"success"
}
```

## 错误代码<a name="错误代码"></a>



发送Gamepot Open API请求时发生的通用错误代码。

| 参数| 描述|
| :---| :---|
| status| 错误代码\（1：成功，失败时请参考Error code\）|
| message| 错误详细描述|

| 错误代码| 描述|
| :---:| :---|
| -1| 使用了仪表盘上没有的密钥时|
| -2| 仪表盘密钥和报头的密钥不同时|
| -3| 使用了仪表盘已删除的密钥时|
| -4| 使用了仪表盘中作为未使用处理的密钥时|
| -5| 密钥到期时|
| -6| 没有项目ID时|
```
{
  "status":-6,
  "message":"projectId was wrong."
}
```

# 查询展示中的公告事项

可以查看展示中的公告事项。

## 请求<a name="请求"></a>


```http
GET https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/store/{storeID}/notice/posting
```

| 项目| 类型| 是否为必填项| 描述| 备注|
| :---| :---| :---:| :---| :---|
| projectId| String| O| GamePot SDK的projectId|   |
| storeID| String| O| 商店ID(google,one,apple,galaxy)|   |


### 请求头<a name="请求头"></a>


| 报头名称| 是否为必填项| 描述|
| :---| :---:| :---|
| x-api-key| O| GamePot发放的认证密钥|
| accept-language| X| 使用语言|

## 响应<a name="响应"></a>


| 字段名称| 类型| 描述|
| :---| :---| :---|
| status| Int| 结果值\（1：成功\）|
| totalCount| String| 公告事项（镜像）查询（个）数|     
| baseUrl| String| Object Storage Bucket URL|     
| id| String| （相应镜像的）唯一ID|     
| store_id| String| 支付商店(google,one,apple,galaxy)|     
| enable| Boolean| 是否启用公告事项|     
| url| String| （单击操作）url|     
| scheme| String| （单击操作）scheme|     
| startDate| String| 公告开始日期|     
| endDate| String| 公告结束日期|     
| lang| String| 语言|     
| value| String| （baseUrl以下）资源地址|     
| default| Boolean| 是否为默认语言|   

## 示例<a name="示例"></a>

### 请求示例<a name="请求示例"></a>


```http
curl --request GET \
  --url https://dashboard-api.gamepot.ntruss.com/v1/api/project/12a0f2ff-xxxx-xxxx-xxxx-9c13ef02f5fs/store/google/notice/posting \
  --header 'accept-language: ko' \
  --header 'x-api-key: 86dcgffae064174543xxxx02a8801ce5a5xxxxxxxxxxxxx'

```

### 响应示例<a name="响应示例"></a>

```http
{
  "status":1,
  "result":{
    "totalCount":1,
    "baseUrl":"https://kr.object.ncloudstorage.com/gamepot-xxxxxxx",
    "edges":[
      {
        "node":{
          "id":"xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
          "store_id":"",
          "enable":true,
          "url":null,
          "scheme":null,
          "startDate":"Fri May 01 2020 15:21:00 GMT+0900 (Korean Standard Time)",
          "endDate":"Sun May 31 2020 18:24:00 GMT+0900 (Korean Standard Time)",
          "image":[
            {
              "lang":"ko",
              "value":"/notices/xxxxxxxxxxxxxxxxxxxxxxxx.png",
              "default":true
            }
          ]
        }
      }
    ]
  }
}
```

## 错误代码<a name="错误代码"></a>



发送Gamepot Open API请求时发生的通用错误代码。

| 参数| 描述|
| :---| :---|
| status| 错误代码\（1：成功，失败时请参考Error code\）|
| message| 错误详细描述|

| 错误代码| 描述|
| :---:| :---|
| -1| 使用了仪表盘上没有的密钥时|
| -2| 仪表盘密钥和报头的密钥不同时|
| -3| 使用了仪表盘已删除的密钥时|
| -4| 使用了仪表盘中作为未使用处理的密钥时|
| -5| 密钥到期时|
| -6| 没有项目ID时|
```
{
  "status":-6,
  "message":"projectId was wrong."
}
```

# 排名板

## 排名板API

## 排名板用户分数登录API

#### Request

- Method : POST
- URI : https://gamepot.apigw.ntruss.com/gpapps/v2/leaderboardlogs

```text
POST
url : https://gamepot.apigw.ntruss.com/gpapps/v2/leaderboardlogs
Header : 'content-type: application/json'
Header 'x-api-key: 86dcgffae0xxxxxxxxxxxxxx'
Header : 'x-project-id: ec8231b2-6b20-4ad1-xxxx-xxxxxxxxx'
data:
{
     "leaderboardId" : "leaderboardId",
    "userId" : "70045665-f64a-45c0-xxxx-xxxxxxxxx",
    "score": 10,
    "subscore": 0,
    "metadata": "{\"key\":\"value\"}"
}
```

| Header| Type| Required| Description|
|:----------|:----------|:----------|----------|
| X-API-KEY| String| O| GamePot发放的认证密钥|
| X-PROJECT-ID| String| O| 仪表盘项目ID|

| Attribute| Type| Required| Description|
|:----------|:----------|:----------|:----------|
| leaderboardId| String| O| 在仪表盘中生成的排名板固有ID|
| userId| String| O| 用户ID|
| score| Integer| X| 分数|
| subscore| Integer| X| 分项分数（非必需）|
| metadata| String| X| 附加信息|

#### Response

成功

```javascript
{
   "leaderboardlog": {
        "project_id": "ec8231b2-6b20-4ad1-xxxx-xxxxxxxxx",
        "id": "TGVhZGVyYm9hcmRMb2c6NjNkMzRhYTgxxxxxxxxx",
        "user_id": "70045665-f64a-45c0-xxxx-xxxxxxxxx",
        "score": 10,
        "subscore": 0,
        "metadata": "{\"key\":\"value\"}",
        "expiredAt": "2023-01-30T20:00:00-08:00"
    }
}
```

| Attribute| Type| Description|
|:----------|:----------|:----------|
| status| Int| 结果值（-1 失败）|
| message| String| 错误消息|
| leaderboardlog.project_id| String| 项目ID|
| leaderboardlog.id| String| 输入ID|
| leaderboardlog.user_id| String| 用户ID|
| leaderboardlog.score| Int| 分数|
| leaderboardlog.subscore| Int| 分项分数|
| leaderboardlog.metadata| Int| 用户自定义数据|
| leaderboardlog.expiredAt| String| 到期日|

失败

```javascript
{
    "status": -1,
    "message": "登录失败"
}
```

| Attribute| Type| Description|
|:----------|:----------|:----------|
| code| Int| 结果值（1：成功，失败时请参考Error code）|
| error| String| 错误内容|

## 导入排名板用户分数API

#### Request

- Method : GET
- URI : https://gamepot.apigw.ntruss.com/gpapps/v2/leaderboardlogs

```text
GET
url : https://gamepot.apigw.ntruss.com/gpapps/v2/leaderboardlogs
Header : 'content-type: application/json'
Header 'x-api-key: 86dcgffae0xxxxxxxxxxxxxx'
Header : 'x-project-id: ec8231b2-6b20-4ad1-xxxx-xxxxxxxxx'
data:
{
     "leaderboardId" : "leaderboardId",
    "offset": 0,
    "per_page": 20
}
```

| Header| Type| Required| Description|
|:----------|:----------|:----------|----------|
| X-API-KEY| String| O| GamePot发放的认证密钥|
| X-PROJECT-ID| String| O| 仪表盘项目ID|

| Attribute| Type| Required| Description|
|:----------|:----------|:----------|:----------|
| leaderboardId| String| O| 在仪表盘中生成的排名板固有ID|
| offset| Integer| -| OFFSET|
| per_page| Integer| -| LIMIT|

#### Response

成功

```javascript
[
    {
        "rank": 1,
        "leaderboard_id": "leaderboardId",
        "user_id": "9c510599-f77a-4e3e-xxxxxx-xxxxxxx",
         "project_id": "ec8231b2-6b20-4ad1-9c59-xxxxxxxxxxx",
        "score": 1100,
        "subscore": 0,
        "metadata": "{\"key\":\"value\"}",
        "expiredAt": "2023-01-30T20:00:00-08:00",
        "updatedAt": "2023-01-26T19:46:07-08:00"
    },
    {
        "rank": 2,
        "leaderboard_id": "leaderboardId",
        "user_id": "63ae4ac9-a0f4-4fba-xxxx-xxxxxxxx",
        "project_id": "ec8231b2-6b20-4ad1-9c59-xxxxxxxxxxx",
        "score": 1000,
        "subscore": 0,
        "metadata": "{\"key\":\"value\"}",
        "expiredAt": "2023-01-30T20:00:00-08:00",
        "updatedAt": "2023-01-26T19:45:58-08:00"
    },
]
  
```

| Attribute| Type| Description|
|:----------|:----------|:----------|
| status| Int| 结果值（-1 失败）|
| message| String| 错误消息|
| rank| Int| 排名|
| project_id| String| 项目ID|
| leaderboardId| String| 在仪表盘中生成的排名板固有ID|
| user_id| String| 用户ID|
| score| Int| 分数|
| subscore| Int| 分项分数|
| metadata| Int| 用户自定义数据|
| updatedAt| String| 更新日期|
| expiredAt| String| 到期日|

失败

```javascript
{
    "status": -1,
    "message": "查询失败"
}
```

| Attribute| Type| Description|
|:----------|:----------|:----------|
| status| Int| 结果值（失败时请参考Error code）|
| message| String| 错误内容|

## 使用特定搜索词获取分数API

#### Request

- Method : GET
- URI : https://gamepot.apigw.ntruss.com/gpapps/v2/leaderboardlogs

如何通过ID搜索

```javascript
GET
url : https://gamepot.apigw.ntruss.com/gpapps/v2/leaderboardlogs
Header : 'content-type: application/json'
Header 'x-api-key: 86dcgffae0xxxxxxxxxxxxxx'
Header : 'x-project-id: ec8231b2-6b20-4ad1-xxxx-xxxxxxxxx'
data:
{
     "leaderboardId" : "leaderboardId",
     "search" : "user_id",
     "query" : "f1deb103-cae1-47dd-b0aa-xxxxxxxxxx",
    "offset": 0,
    "per_page": 20
}
```

通过SCORE范围的搜索方法

```javascript
GET
url : https://gamepot.apigw.ntruss.com/gpapps/v2/leaderboardlogs
Header : 'content-type: application/json'
Header 'x-api-key: 86dcgffae0xxxxxxxxxxxxxx'
Header : 'x-project-id: ec8231b2-6b20-4ad1-xxxx-xxxxxxxxx'
data:
{
     "leaderboardId" : "leaderboardId",
     "search" : "score",
     "query" : "99-120",
    "offset": 0,
    "per_page": 20
}
```

| Header| Type| Required| Description|
|:----------|:----------|:----------|----------|
| X-API-KEY| String| O| GamePot发放的认证密钥|
| X-PROJECT-ID| String| O| 仪表盘项目ID|

| Attribute| Type| Required| Description|
|:----------|:----------|:----------|:----------|
| leaderboardId| String| O| 在仪表盘中生成的排名板固有ID|
| offset| Integer| -| OFFSET|
| per_page| Integer| -| LIMIT|

#### Response

成功

```javascript
[
    {
        "rank": 5,
        "leaderboard_id": "leaderboardId",
        "user_id": "f1deb103-cae1-47dd-b0aa-xxxxxx",
        "project_id": "ec8231b2-6b20-4ad1-9c59-xxxxxxxxx",
        "score": 99,
        "subscore": 100,
        "metadata": "{\"key\":\"value\"}",
        "expiredAt": "2023-01-30T20:00:00-08:00",
        "updatedAt": "2023-01-26T16:23:39-08:00"
    }
]
  
```

失败

```javascript
{
    "status": -1,
    "message": "错误消息"
}
```

| Attribute| Type| Description|
|:----------|:----------|:----------|
| status| Int| 结果值（失败时请参考Error code）|
| message| String| 错误内容|

## 获取排名板信息和用户数的API

#### Request

- Method : GET
- URI : https://gamepot.apigw.ntruss.com/gpapps/v2/leaderboards?/{leaderboardId}?offset=0\&per_page=10

```text
GET
url : https://gamepot.apigw.ntruss.com/gpapps/v2/leaderboard
Header 'x-api-key: 86dcgffae0xxxxxxxxxxxxxx'
Header : 'x-project-id: ec8231b2-6b20-4ad1-xxxx-xxxxxxxxx'
```

| Header| Type| Required| Description|
|:----------|:----------|:----------|----------|
| X-API-KEY| String| O| GamePot发放的认证密钥|
| X-PROJECT-ID| String| O| 仪表盘项目ID|

| Attribute| Type| Required| Description|
|:----------|:----------|:----------|:----------|
| leaderboardId| String| O| 在仪表盘中生成的排名板固有ID|
| offset| Integer| X| OFFSET|
| per_page| Integer| X| LIMIT|

#### Response

成功

```javascript
[
    {
        "status": true,
        "ranking": "best",
        "tie_breaking": "first",
        "id": "TGVhZGVyYm9hcmQ6YXNkYWRhZHNhZHNh",
        "name": "test",
        "description": "TEST",
        "descending": true,
        "resetDay": 0,
        "resetTime": "00:00",
        "resetDate": 1,
        "startedAt": "2023-01-25T12:09:47-08:00",
        "timezone": "America/Kralendijk",
        "project_id": "ec8231b2-6b20-4ad1-9c59-8e183087a742",
        "period_type": "monthly",
        "icon_url": "sdadasds",
        "user_count": 28,
    }
]
  
```

| Attribute| Type| Required| Description|
|:----------|:----------|:----------|:----------|
| id| String| O| 排名板固有ID|
| projectId| String| O| 项目ID|
| status| Boolean| O| 状态|
| is_check_user| Boolean| -| 是否检查用户ID|
| name| String| -| 排名板名称|
| description| String| -| 说明|
| icon_url| String| -| 图标URL|
| descending| Boolean| -| 排序|
| startedAt| String| -| 开始日期|
| expiredAt| String| -| 结束日期（season的情况）|
| timezone| String| -| 时区|
| period_type| String| -| 周期(daily、weekly、monthly、season)|
| resetDay| Integer| -| 初始化日期 1：星期日、2.星期一、3.星期二、4.星期三、5.星期四、6.星期五、7.星期六（periodType为weekly时）|
| resetTime| String| -| 初始化时间|
| resetDate| Integer| -| 初始化日期1~31（periodType为monthly时）|
| ranking| String| O| 排名更新标准(latest、accumulated、best)|
| tie_breaking| String| O| 同分者处理标准(first、last)|

失败

```javascript
{
    "status": -1,
    "message": "错误消息"
}
```

| Attribute| Type| Description|
|:----------|:----------|:----------|
| status| Int| 结果值（失败时请参考Error code）|
| message| String| 错误内容|

## 用排名板查询用户分数的API

#### Request

- Method : GET
- URI : https://gamepot.apigw.ntruss.com/gpapps/v2/leaderboard/{leaderboardID}/user{userid}

```text
GET
url : https://gamepot.apigw.ntruss.com/gpapps/v2/leaderboard
Header 'x-api-key: 86dcgffae0xxxxxxxxxxxxxx'
Header : 'x-project-id: ec8231b2-6b20-4ad1-xxxx-xxxxxxxxx'

```

| Header| Type| Required| Description|
|:----------|:----------|:----------|----------|
| X-API-KEY| String| O| GamePot发放的认证密钥|
| X-PROJECT-ID| String| O| 仪表盘项目ID|

| Attribute| Type| Required| Description|
|:----------|:----------|:----------|:----------|
| leaderboardID| String| O| 在仪表盘中生成的排名板固有ID|
| userid| String| O| 用户ID|

#### Response

成功

```javascript
{
	"rank": 1,
	"leaderboard_id": "leaderboardID",
	"user_id": "8f372bf4-XXXX-XXXX-XXXX-XXXXXXXX",
	"project_id": "ec8231b2-6b20-4ad1-XXXX-XXXXXXXX",
	"score": 1,
	"prev_score": null,
	"subscore": 10,
	"metadata": "",
	"user_count": 2,
	"expiredAt": "2023-01-30T17:00:00+09:00",
	"updatedAt": "2023-01-30T11:55:37+09:00"
}
  
```

| Attribute| Type| Description|
|:----------|:----------|:----------|
| status| Int| 结果值（-1 失败）|
| message| String| 错误消息|
| rank| Int| 排名|
| project_id| String| 项目ID|
| leaderboardId| String| 在仪表盘中生成的排名板固有ID|
| user_id| String| 用户ID|
| score| Int| 分数|
| subscore| Int| 分项分数|
| metadata| Int| 用户自定义数据|
| updatedAt| String| 更新日期|
| expiredAt| String| 到期日|

失败

```javascript
{
    "status": -1,
    "message": "错误消息"
}
```

| Attribute| Type| Description|
|:----------|:----------|:----------|
| status| Int| 结果值（失败时请参考Error code）|
| message| String| 错误内容|

## 删除登录排行板用户API

#### Request

- Method : DELETE
- URI : https://gamepot.apigw.ntruss.com/gpapps/v2/leaderboardlogs

```text
DELETE
url : https://gamepot.apigw.ntruss.com/gpapps/v2/leaderboardlogs
Header : 'content-type: application/json'
Header 'x-api-key: 86dcgffae0xxxxxxxxxxxxxx'
Header : 'x-project-id: ec8231b2-6b20-4ad1-xxxx-xxxxxxxxx'
data:
{
     "leaderboardId" : "leaderboardId",
     "userId" : "560963c3-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
}
```

| Header| Type| Required| Description|
|:----------|:----------|:----------|----------|
| X-API-KEY| String| O| GamePot发放的认证密钥|
| X-PROJECT-ID| String| O| 仪表盘项目ID|

| Attribute| Type| Required| Description|
|:----------|:----------|:----------|:----------|
| leaderboardId| String| -| 排名板ID|
| userId| String| -| 排名板用户ID|

#### Response

成功

```javascript
[
    {
        "leaderboard_id": "leaderboardId",
        "user_id": "f1deb103-cae1-47dd-b0aa-xxxxxx",
        "project_id": "ec8231b2-6b20-4ad1-9c59-xxxxxxxxx",
        "score": 99,
        "subscore": 100,
        "metadata": "{\"key\":\"value\"}",
        "expiredAt": "2023-01-30T20:00:00-08:00",
        "updatedAt": "2023-01-26T16:23:39-08:00"
    }
]
  
```

| Attribute| Type| Description|
|:----------|:----------|:----------|
| status| Int| 结果值（-1 失败）|
| message| String| 错误消息|
| project_id| String| 项目ID|
| leaderboardId| String| 在仪表盘中生成的排名板固有ID|
| user_id| String| 用户ID|
| score| Int| 分数|
| subscore| Int| 分项分数|
| metadata| Int| 用户自定义数据|
| updatedAt| String| 更新日期|
| expiredAt| String| 到期日|

失败

```javascript
{
    "status": -1,
    "message": "错误消息"
}
```

| Attribute| Type| Description|
|:----------|:----------|:----------|
| status| Int| 结果值（失败时请参考Error code）|
| message| String| 错误内容|

## 排名板登录API

#### Request

- Method : POST
- URI : https://gamepot.apigw.ntruss.com/gpapps/v2/leaderboards

```text
POST
url : https://gamepot.apigw.ntruss.com/gpapps/v2/leaderboards
Header : 'content-type: application/json'
Header 'x-api-key: 86dcgffae0xxxxxxxxxxxxxx'
Header : 'x-project-id: ec8231b2-6b20-4ad1-xxxx-xxxxxxxxx'
data:
{
    "id" : "leaderboardId",
    "status": true,
    "name": "name",
    "description": "description",
    "iconUrl" : "icon_url",
    "descending": true,
    "startedAt" : "2023-01-22 13:00:00",
    "timezone" : "Asia/Seoul",
    "periodType" : "weekly",
    "resetDay": 1,
    "resetDate": 1,
    "resetTime" : "00:01:01",
    "ranking" : "latest", 
    "tie_breaking" : "first"
}
```

| Header| Type| Required| Description|
|:----------|:----------|:----------|----------|
| X-API-KEY| String| O| GamePot发放的认证密钥|
| X-PROJECT-ID| String| O| 仪表盘项目ID|

| Attribute| Type| Required| Description|
|:----------|:----------|:----------|:----------|
| id| String| O| 排名板固有ID|
| projectId| String| O| 项目ID|
| status| Boolean| O| 状态|
| is_check_user| Boolean| -| 是否检查用户ID|
| name| String| -| 排名板名称|
| description| String| -| 说明|
| iconUrl| String| -| 图标URL|
| descending| Boolean| -| 排序|
| startedAt| String| -| 开始日期|
| expiredAt| String| -| 结束日期（season的情况）|
| timezone| String| -| 时区|
| period_type| String| -| 周期(daily、weekly、monthly、season)|
| resetDay| Integer| -| 初始化日期 1：星期日、2.星期一、3.星期二、4.星期三、5.星期四、6.星期五、7.星期六（periodType为weekly时）|
| resetTime| String| -| 初始化时间|
| resetDate| Integer| -| 初始化日期1~31（periodType为monthly时）|
| ranking| String| O| 排名更新标准(latest、accumulated、best)|
| tie_breaking| String| O| 同分者处理标准(first、last)|

#### Response

成功

```javascript
{
   "leaderboard": {
        "status": true,
        "is_check_user": true,
        "ranking": "latest",
        "tie_breaking": "first",
        "id": "TGVhZGVyYm9hcmQ6ZHNzZGFkMTIyMjIyMTJhZA==",
        "name": "name",
        "description": "description",
        "descending": true,
        "resetDay": 1,
        "resetTime": "00:01:01",
        "resetDate": 1,
        "startedAt": "2023-01-22T13:00:00-08:00",
        "expiredAt": "2023-11-22T13:00:00-08:00",
        "timezone": "Asia/Seoul",
        "project_id": "ec8231b2-6b20-4ad1-9c59-8e183087a742",
        "period_type": "weekly",
        "icon_url": "icon_url",
        "user_count": null,
        "updatedAt": "2023-02-01T15:52:24-08:00",
        "createdAt": "2023-02-01T15:52:24-08:00"
    }
}
```

| Attribute| Type| Required| Description|
|:----------|:----------|:----------|:----------|
| id| String| O| 排名板固有ID|
| projectId| String| O| 项目ID|
| status| Boolean| O| 状态|
| is_check_user| Boolean| -| 是否检查用户ID|
| name| String| -| 排名板名称|
| description| String| -| 说明|
| icon_url| String| -| 图标URL|
| descending| Boolean| -| 排序|
| startedAt| String| -| 开始日期|
| expiredAt| String| -| 结束日期（season的情况）|
| timezone| String| -| 时区|
| period_type| String| -| 周期(daily、weekly、monthly、season)|
| resetDay| Integer| -| 初始化日期 1：星期日、2.星期一、3.星期二、4.星期三、5.星期四、6.星期五、7.星期六（periodType为weekly时）|
| resetTime| String| -| 初始化时间|
| resetDate| Integer| -| 初始化日期1~31（periodType为monthly时）|
| ranking| String| O| 排名更新标准(latest、accumulated、best)|
| tie_breaking| String| O| 同分者处理标准(first、last)|

失败

```javascript
 "status": -1,
"message": "错误消息"
```

| Attribute| Type| Description|
|:----------|:----------|:----------|
| code| Int| 结果值（1：成功，失败时请参考Error code）|
| error| String| 错误内容|

## 排名板修改API

#### Request

- Method : PUT
- URI : https://gamepot.apigw.ntruss.com/gpapps/v2/leaderboards/{leaderboardId}

```text
PUT
url : https://gamepot.apigw.ntruss.com/gpapps/v2/leaderboards/{leaderboardId}
Header : 'content-type: application/json'
Header 'x-api-key: 86dcgffae0xxxxxxxxxxxxxx'
Header : 'x-project-id: ec8231b2-6b20-4ad1-xxxx-xxxxxxxxx'
data:
{
    "status": true,
    "name": "name",
    "description": "description",
    "iconUrl" : "icon_url",
    "descending": true,
    "startedAt" : "2023-01-22 13:00:00",
    "timezone" : "Asia/Seoul",
    "periodType" : "weekly",
    "resetDay": 1,
    "resetDate": 1,
    "resetTime" : "00:01:01",
    "ranking" : "latest", 
    "tie_breaking" : "first"
}
```

| Header| Type| Required| Description|
|:----------|:----------|:----------|----------|
| X-API-KEY| String| O| GamePot发放的认证密钥|
| X-PROJECT-ID| String| O| 仪表盘项目ID|

| Attribute| Type| Required| Description|
|:----------|:----------|:----------|:----------|
| leaderboardId| String| O| 排名板固有ID|
| status| Boolean| O| 状态|
| is_check_user| Boolean| -| 是否检查用户ID|
| name| String| -| 排名板名称|
| description| String| -| 说明|
| icon_url| String| -| 图标URL|
| descending| Boolean| -| 排序|
| startedAt| String| -| 开始日期|
| expiredAt| String| -| 结束日期（season的情况）|
| timezone| String| -| 时区|
| period_type| String| -| 周期(daily、weekly、monthly、season)|
| resetDay| Integer| -| 初始化日期 1：星期日、2.星期一、3.星期二、4.星期三、5.星期四、6.星期五、7.星期六（periodType为weekly时）|
| resetTime| String| -| 初始化时间|
| resetDate| Integer| -| 初始化日期1~31（periodType为monthly时）|
| ranking| String| O| 排名更新标准(latest、accumulated、best)|
| tie_breaking| String| O| 同分者处理标准(first、last)|

#### Response

成功

```javascript
{
   "leaderboard": {
        "status": true,
        "is_check_user": true,
        "ranking": "latest",
        "tie_breaking": "first",
        "id": "TGVhZGVyYm9hcmQ6ZHNzZGFkMTIyMjIyMTJhZA==",
        "name": "name",
        "description": "description",
        "descending": true,
        "resetDay": 1,
        "resetTime": "00:01:01",
        "resetDate": 1,
        "startedAt": "2023-01-22T13:00:00-08:00",
        "expiredAt": "2023-11-22T13:00:00-08:00",
        "timezone": "Asia/Seoul",
        "project_id": "ec8231b2-6b20-4ad1-9c59-8e183087a742",
        "period_type": "weekly",
        "icon_url": "icon_url",
        "user_count": null,
        "updatedAt": "2023-02-01T15:52:24-08:00",
        "createdAt": "2023-02-01T15:52:24-08:00"
    }
}
```

| Attribute| Type| Required| Description|
|:----------|:----------|:----------|:----------|
| id| String| O| 排名板固有ID|
| projectId| String| O| 项目ID|
| status| Boolean| O| 状态|
| is_check_user| Boolean| -| 是否检查用户ID|
| name| String| -| 排名板名称|
| description| String| -| 说明|
| icon_url| String| -| 图标URL|
| descending| Boolean| -| 排序|
| startedAt| String| -| 开始日期|
| expiredAt| String| -| 结束日期（season的情况）|
| timezone| String| -| 时区|
| period_type| String| -| 周期(daily、weekly、monthly、season)|
| resetDay| Integer| -| 初始化日期 1：星期日、2.星期一、3.星期二、4.星期三、5.星期四、6.星期五、7.星期六（periodType为weekly时）|
| resetTime| String| -| 初始化时间|
| resetDate| Integer| -| 初始化日期1~31（periodType为monthly时）|
| ranking| String| O| 排名更新标准(latest、accumulated、best)|
| tie_breaking| String| O| 同分者处理标准(first、last)|

失败

```javascript
 "status": -1,
"message": "错误消息"
```

| Attribute| Type| Description|
|:----------|:----------|:----------|
| code| Int| 结果值（1：成功，失败时请参考Error code）|
| error| String| 错误内容|

## 排名板删除API

#### Request

- Method : DELETE
- URI : https://gamepot.apigw.ntruss.com/gpapps/v2/leaderboards/{leaderboardId}

```text
DELETE
url : https://gamepot.apigw.ntruss.com/gpapps/v2/leaderboards/leaderboardId
Header 'x-api-key: 86dcgffae0xxxxxxxxxxxxxx'
Header : 'x-project-id: ec8231b2-6b20-4ad1-xxxx-xxxxxxxxx'

```

| Header| Type| Required| Description|
|:----------|:----------|:----------|----------|
| X-API-KEY| String| O| GamePot发放的认证密钥|
| X-PROJECT-ID| String| O| 仪表盘项目ID|

| Attribute| Type| Required| Description|
|:----------|:----------|:----------|:----------|
| leaderboardId| String| O| 排名板固有ID|

#### Response

成功

```javascript
{
   "leaderboard": {
        "status": true,
        "is_check_user": true,
        "ranking": "latest",
        "tie_breaking": "first",
        "id": "TGVhZGVyYm9hcmQ6ZHNzZGFkMTIyMjIyMTJhZA==",
        "name": "name",
        "description": "description",
        "descending": true,
        "resetDay": 1,
        "resetTime": "00:01:01",
        "resetDate": 1,
        "startedAt": "2023-01-22T13:00:00-08:00",
        "expiredAt": "2023-11-22T13:00:00-08:00",
        "timezone": "Asia/Seoul",
        "project_id": "ec8231b2-6b20-4ad1-9c59-8e183087a742",
        "period_type": "weekly",
        "icon_url": "icon_url",
        "user_count": null,
        "updatedAt": "2023-02-01T15:52:24-08:00",
        "createdAt": "2023-02-01T15:52:24-08:00"
    }
}
```

成功

| Attribute| Type| Required| Description|
|:----------|:----------|:----------|:----------|
| id| String| O| 排名板固有ID|
| projectId| String| O| 项目ID|
| status| Boolean| O| 状态|
| is_check_user| Boolean| -| 是否检查用户ID|
| name| String| -| 排名板名称|
| description| String| -| 说明|
| icon_url| String| -| 图标URL|
| descending| Boolean| -| 排序|
| startedAt| String| -| 开始日期|
| expiredAt| String| -| 结束日期（season的情况）|
| timezone| String| -| 时区|
| period_type| String| -| 周期(daily、weekly、monthly、season)|
| resetDay| Integer| -| 初始化日期 1：星期日、2.星期一、3.星期二、4.星期三、5.星期四、6.星期五、7.星期六（periodType为weekly时）|
| resetTime| String| -| 初始化时间|
| resetDate| Integer| -| 初始化日期1~31（periodType为monthly时）|
| ranking| String| O| 排名更新标准(latest、accumulated、best)|
| tie_breaking| String| O| 同分者处理标准(first、last)|

失败

```javascript
 "status": -1,
"message": "错误消息"
```

| Attribute| Type| Description|
|:----------|:----------|:----------|
| code| Int| 结果值（1：成功，失败时请参考Error code）|
| error| String| 错误内容|

# 好友管理

## 好友管理

### 请求加为好友

向其他用户发送好友申请。收件人将收到该请求的通知。

#### Request

- Method : POST
- URI : https://gamepot.apigw.ntruss.com/gpapps/v2/friendship/request

```javascript
POST
url : https://gamepot.apigw.ntruss.com/gpapps/v2/friendship/request
Header : 'content-type: application/json'
Header 'x-api-key: 86dcgffae0xxxxxxxxxxxxxx'
Header : 'x-project-id: ec8231b2-6b20-4ad1-xxxx-xxxxxxxxx'
data:
{
    "userId": "80803902-8b83-4860-b8a6-xxxxxxxx",
    "friendId": "a1c4aaa2-02f6-40bd-afb4-xxxxxxx",
    "message": "做朋友吧!!"
}
```

| Header| Type| Required| Description|
|:----------|:----------|:----------|----------|
| X-API-KEY| String| O| GamePot发放的认证密钥|
| X-PROJECT-ID| String| O| 仪表盘项目ID|

| Attribute| Type| Required| Description|
|:----------|:----------|:----------|:----------|
| userId| String| O| 用户ID|
| friendId| String| O| 添加好友ID|
| message| String| X| 消息|

### Response

成功

```javascript
{
   "friendship": {
        "project_id": "ec8231b2-6b20-4ad1-9c59-xxxxx",
        "id": "5fe78d95-6186-4128-b52a-28759cxxxxxx",
        "status": "requested",
        "user_id" : "xxxxxxxxxx",
        "user": {
            "id": "xxxxxxxxxx",
            "nickname": "xxxxxxxxxx"
        },
        "friend_id" : "xxxxxxxx",
        "friend": {
            "id": "xxxxxxxxxx",
            "nickname": "xxxxxxxxxx"
        },
        "friend_id": "a1c4aaa2-02f6-40bd-afb4-b1d6caacf0de",
        "requested_at": "2023-01-31T16:13:26-08:00"
    }
}
```

| Attribute| Type| Description|
|:----------|:----------|:----------|
| friendship.project_id| String| 项目ID|
| friendship.id| String| 输入ID|
| friendship.user_id| String| 用户ID|
| friendship.status| String| 状态|
| friendship.user_id| String| ID|
| friendship.user| Object| 我的信息|
| friendship.friend_id| String| 好友ID|
| friendship.friend| Object| 好友信息|
| friendship.requested_at| String| 请求日期|

失败

```javascript
{
    "status": -1,
    "message": "错误消息"
}
```

| Attribute| Type| Description|
|:----------|:----------|:----------|
| code| Int| 结果值（1：成功，失败时请参考Error code）|
| error| String| 错误内容|

### 同意好友申请

同意对方发送的好友申请。同意后两用户成为好友关系。

#### Request

- Method : POST
- URI : https://gamepot.apigw.ntruss.com/gpapps/v2/friendship/accept

```javascript
POST
url : https://gamepot.apigw.ntruss.com/gpapps/v2/friendship/accept
Header : 'content-type: application/json'
Header 'x-api-key: 86dcgffae0xxxxxxxxxxxxxx'
Header : 'x-project-id: ec8231b2-6b20-4ad1-xxxx-xxxxxxxxx'
data:
{
    "userId": "a1c4aaa2-02f6-40bd-afb4-xxxxxxxxx",
    "friendId": "80803902-8b83-4860-b8a6-xxxxxxx"
}
```

| Header| Type| Required| Description|
|:----------|:----------|:----------|----------|
| X-API-KEY| String| O| GamePot发放的认证密钥|
| X-PROJECT-ID| String| O| 仪表盘项目ID|

| Attribute| Type| Required| Description|
|:----------|:----------|:----------|:----------|
| userId| String| O| 用户ID|
| friendId| String| O| 添加好友ID|

### Response

成功

```javascript
{
   "friendship": {
        "project_id": "ec8231b2-6b20-4ad1-9c59-xxxxxx",
        "id": "5fe78d95-6186-4128-b52a-xxxxxxxxx",
        "status": "accepted",
        "user_id" : "xxxxxxxxxx",
        "user": {
            "id": "xxxxxxxxxx",
            "nickname": "xxxxxxxxxx"
        },
        "friend_id" : "xxxxxxxx",
        "friend": {
            "id": "xxxxxxxxxx",
            "nickname": "xxxxxxxxxx"
        },
        "friend_id": "80803902-8b83-4860-b8a6-xxxxxxxxx",
        "created_at": "2023-01-31T16:13:26-08:00",
        "updated_at": "2023-01-31T16:13:26-08:00",
        "requested_at": "2023-01-31T16:13:26-08:00"
    }
}
```

| Attribute| Type| Description|
|:----------|:----------|:----------|
| friendship.project_id| String| 项目ID|
| friendship.id| String| 输入ID|
| friendship.user_id| String| 用户ID|
| friendship.status| String| 状态|
| friendship.user_id| String| ID|
| friendship.friend_id| String| 好友ID|
| friendship.user| Object| 我的信息|
| friendship.friend| Object| 好友信息|
| friendship.requested_at| String| 请求日期|

失败

```javascript
{
    "status": -1,
    "message": "错误消息"
}
```

| Attribute| Type| Description|
|:----------|:----------|:----------|
| code| Int| 结果值（1：成功，失败时请参考Error code）|
| error| String| 错误内容|

### 拒绝好友

拒绝对方发来的好友申请。

#### Request

- Method : POST
- URI : https://gamepot.apigw.ntruss.com/gpapps/v2/friendship/reject

```javascript
POST
url : https://gamepot.apigw.ntruss.com/gpapps/v2/friendship/reject
Header : 'content-type: application/json'
Header 'x-api-key: 86dcgffae0xxxxxxxxxxxxxx'
Header : 'x-project-id: ec8231b2-6b20-4ad1-xxxx-xxxxxxxxx'
data:
{
     "userId": "a1c4aaa2-02f6-40bd-afb4-xxxxxxx",
    "friendId": "80803902-8b83-4860-b8a6-xxxxxx"
}
```

| Header| Type| Required| Description|
|:----------|:----------|:----------|----------|
| X-API-KEY| String| O| GamePot发放的认证密钥|
| X-PROJECT-ID| String| O| 仪表盘项目ID|

| Attribute| Type| Required| Description|
|:----------|:----------|:----------|:----------|
| userId| String| O| 用户ID|
| friendId| String| O| 添加好友ID|

### Response

成功

```javascript
{
   "friendship": {
        "project_id": "ec8231b2-6b20-4ad1-9c59-xxxxxx",
        "id": "5fe78d95-6186-4128-b52a-xxxxxxxxx",
        "status": "rejected",
        "user_id" : "xxxxxxxxxx",
        "user": {
            "id": "xxxxxxxxxx",
            "nickname": "xxxxxxxxxx"
        },
        "friend_id" : "xxxxxxxx",
        "friend": {
            "id": "xxxxxxxxxx",
            "nickname": "xxxxxxxxxx"
        },
        "friend_id": "80803902-8b83-4860-b8a6-xxxxxxxxx",
        "created_at": "2023-01-31T16:13:26-08:00",
        "updated_at": "2023-01-31T16:13:26-08:00",
        "requested_at": "2023-01-31T16:13:26-08:00"
    }
}
```

| Attribute| Type| Description|
|:----------|:----------|:----------|
| friendship.project_id| String| 项目ID|
| friendship.id| String| 输入ID|
| friendship.user_id| String| ID|
| friendship.friend_id| String| 好友ID|
| friendship.status| String| 状态|
| friendship.user| Object| 我的信息|
| friendship.friend| Object| 好友信息|
| friendship.requested_at| String| 请求日期|

失败

```javascript
{
    "status": -1,
    "message": "错误消息"
}
```

| Attribute| Type| Description|
|:----------|:----------|:----------|
| code| Int| 结果值（1：成功，失败时参考错误代码）|
| error| String| 错误内容|

### 解除好友

此功能可以取消与其他用户的好友关系。解除好友功能是将相应用户在当事人的好友列表中移除。若当事人想再次与取消的好友成为好友关系，需要重新发送好友申请。

#### Request

- Method : POST
- URI : https://gamepot.apigw.ntruss.com/gpapps/v2/friendship

```javascript
DELETE
url : https://gamepot.apigw.ntruss.com/gpapps/v2/friendship
Header : 'content-type: application/json'
Header 'x-api-key: 86dcgffae0xxxxxxxxxxxxxx'
Header : 'x-project-id: ec8231b2-6b20-4ad1-xxxx-xxxxxxxxx'
data:
{
     "userId": "80803902-8b83-4860-b8a6-xxxxxx",
    "friendId": "a1c4aaa2-02f6-40bd-afb4-xxxxxxx",
}
```

| Header| Type| Required| Description|
|:----------|:----------|:----------|----------|
| X-API-KEY| String| O| GamePot发放的认证密钥|
| X-PROJECT-ID| String| O| 仪表盘项目ID|

| Attribute| Type| Required| Description|
|:----------|:----------|:----------|:----------|
| userId| String| O| 用户ID|
| friendId| String| O| 添加好友ID|

### Response

成功

```javascript
{
   "friendship": {
        "project_id": "ec8231b2-6b20-4ad1-9c59-xxxxxx",
        "id": "5fe78d95-6186-4128-b52a-xxxxxxxxx",
        "status": "deleted",
        "user_id" : "xxxxxxxxxx",
        "user": {
            "id": "xxxxxxxxxx",
            "nickname": "xxxxxxxxxx"
        },
        "friend_id" : "xxxxxxxx",
        "friend": {
            "id": "xxxxxxxxxx",
            "nickname": "xxxxxxxxxx"
        },
        "created_at": "2023-01-31T16:13:26-08:00",
        "updated_at": "2023-01-31T16:13:26-08:00",
        "requested_at": "2023-01-31T16:13:26-08:00"
    }
}
```

| Attribute| Type| Description|
|:----------|:----------|:----------|
| friendship.project_id| String| 项目ID|
| friendship.id| String| 输入ID|
| friendship.status| String| 状态|
| friendship.user_id| String| ID|
| friendship.friend_id| String| 好友ID|
| friendship.user| Object| 我的信息|
| friendship.friend| Object| 好友信息|
| friendship.requested_at| String| 请求日期|

失败

```javascript
{
    "status": -1,
    "message": "错误消息"
}
```

| Attribute| Type| Description|
|:----------|:----------|:----------|
| code| Int| 结果值（1：成功，失败时请参考Error code）|
| error| String| 错误内容|

### 好友列表

显示当前好友列表。

#### Request

- Method : GET
- URI : https://gamepot.apigw.ntruss.com/gpapps/v2/friendships?filter={"status":"accepted","user_id":"2d51cc68-a0d9-xxxxx-xxxx-xxxxxxxxxxxx"}

```javascript
POST
url : https://gamepot.apigw.ntruss.com/gpapps/v2/friendship?filter={"status":"accepted","user_id":"2d51cc68-a0d9-xxxxx-xxxx-xxxxxxxxxxxx"}
Header 'x-api-key: 86dcgffae0xxxxxxxxxxxxxx'
Header : 'x-project-id: ec8231b2-6b20-4ad1-xxxx-xxxxxxxxx'
```

| Header| Type| Required| Description|
|:----------|:----------|:----------|----------|
| X-API-KEY| String| O| GamePot发放的认证密钥|
| X-PROJECT-ID| String| O| 仪表盘项目ID|

| Attribute| Type| Required| Description|
|:----------|:----------|:----------|:----------|
| filter| String| O| 可通过过滤器搜索所有字段。|
| user_id| String| O| 用户ID|

** 过滤器可通过代码进行多种应用。  
Status 可以根据代码搜索好友列表。

"accepted"：已接受邀请成为好友的列表  
"rejected"：拒绝邀请的列表  
"requested"：请求交友的列表  
"pending"：已同意交友请求的列表

### Response

成功

```javascript
[
    {
        "project_id": "ec8231b2-6b20-4ad1-9c59-8e183087a742",
        "id":"xxxxxxxxxxxxxxxxxxxx",
        "status": "accepted",
        "user_id" : "xxxxxxxxxx",
        "user": {
            "id": "xxxxxxxxxx",
            "nickname": "xxxxxxxxxx"
        },
        "friend_id" : "xxxxxxxx",
        "friend": {
            "id": "xxxxxxxxxx",
            "nickname": "xxxxxxxxxx"
        },
        "created_at": "2023-01-31T16:28:00-08:00",
        "updated_at": "2023-01-31T16:28:03-08:00",
        "requested_at": "2023-01-31T16:28:00-08:00"
    },
    {
        "project_id": "ec8231b2-6b20-4ad1-9c59-8e183087a742",
        "id":"xxxxxxxxxxxxxxxxxxxx",
        "status": "accepted",
        "user_id" : "xxxxxxxxxx",
        "user": {
            "id": "xxxxxxxxxx",
            "nickname": "xxxxxxxxxx"
        },
        "friend_id" : "xxxxxxxx",
        "friend": {
            "id": "xxxxxxxxxx",
            "nickname": "xxxxxxxxxx"
        },
        "created_at": "2023-01-31T16:28:00-08:00",
        "updated_at": "2023-01-31T16:28:03-08:00",
        "requested_at": "2023-01-31T16:28:00-08:00"
    }
]
```

| Attribute| Type| Description|
|:----------|:----------|:----------|
| project_id| String| 项目ID|
| id| String| 固有ID|
| status| String| 状态|
| user_id| String| ID|
| friend_id| String| 好友ID|
| user| Object| 我的信息|
| friend| Object| 好友信息|
| created_at| String| 创建日期|
| updated_at| String| 更新日期|
| requested_at| String| 请求日期|

失败

```javascript
{
    "status": -1,
    "message": "错误消息"
}
```

| Attribute| Type| Description|
|:----------|:----------|:----------|
| code| Int| 结果值（1：成功，失败时请参考Error code）|
| error| String| 错误内容|


# 提前预约参与

## 提前预约参与API

此API用于成功参与提前预约后的注册过程

### Request

- Method：POST
- URI：https://gamepot.apigw.ntruss.com/gpapps/v2/phone/join

```text
POST
url : https://gamepot.apigw.ntruss.com/gpapps/v2/phone/join
Header : 'content-type: application/json'
data:
{
    "projectId":"ab2775b4-cf09-4794-XXXX-XXXXXXXXXXXX",
    "categoryId":"b062a3f3-0a37-44d1-XXXX-XXXXXXXXXXXX",
    "code":"61XX",
       "from":"02XXXXXXXX",
    "to":"010XXXXXXX",
    "store":"google",
        "tag":""
}
```

| Attribute | Type | Required | Description |
| --- | --- | --- | --- |
| projectId | String | -   | GAMEPOT SDK的projectId |
| categoryId | String | -   | GAMEPOT提前预约页面的categoryId |
| code | String | -   | 收到的验证码 |
| from | String | -   | 获得审批的主叫号码 |
| to  | String | -   | 接收SMS验证码的联系方式 |
| store | String | -   | 商店（Google、ONE、Apple） |
| tag | String | -   | 其他信息（进入路径等信息） |

### Response

成功

```javascript
{
    "code": 200,
    "error": "验证成功。"
}
```

| Attribute | Type | Description |
| --- | --- | --- |
| code | Int | 结果值 \（200：成功，404：失败\） |
| error | String | 错误消息 |

失败

```javascript
{
    "code": 404,
    "error": "此号码已注册。"
}
```

| Attribute | Type | Description |
| --- | --- | --- |
| code | Int | 结果值 \（1：成功，失败情况下请参考错误代码\） |
| error | String | 错误内容 |


# 提前预约验证码发送

## 提前预约验证码发送API

此API用来为提前预约者生成验证码并发送短信。

### Request

- Method：POST
- URI：https://gamepot.apigw.ntruss.com/gpapps/v2/phone/request

```text
POST
url : https://gamepot.apigw.ntruss.com/gpapps/v2/phone/request
Header : 'content-type: application/json'
data:
{
    "projectId":"ab2775b4-cf09-4794-XXXX-XXXXXXXXXXXX",
    "categoryId":"b062a3f3-0a37-44d1-XXXX-XXXXXXXXXXXX",
    "from":"XXXXXXX",
    "to":"010XXXXXXX",
    "store":"google"
}
```

| Attribute | Type | Required | Description |
| --- | --- | --- | --- |
| projectId | String | -   | GAMEPOT SDK的projectId |
| categoryId | String | -   | GAMEPOT提前预约页面的categoryId |
| from | String | -   | 获得审批的主叫号码 |
| to  | String | -   | 接收SMS验证码的联系方式 |
| store | String | -   | 商店（Google、ONE、Apple） |

### Response

成功

```javascript
{
    "code": 200,
    "error": "验证成功。"
}
```

| Attribute | Type | Description |
| --- | --- | --- |
| code | Int | 结果值 \（200：成功，404：失败\） |
| error | String | 错误消息 |

失败

```javascript
{
    "code": 404,
    "error": "此号码已注册。"
}
```

| Attribute | Type | Description |
| --- | --- | --- |
| code | Int | 结果值 \（1：成功，失败情况下请参考错误代码\） |
| error | String | 错误内容 |


# 提前预约验证码确认

## 提前预约验证码确认API

此API用来确认发送给提前预约者的验证码与输入的验证码是否一致

### Request

- Method：POST
- URI：https://gamepot.apigw.ntruss.com/gpapps/v2/phone/verify

```text
POST
url : https://gamepot.apigw.ntruss.com/gpapps/v2/phone/verify
Header : 'content-type: application/json'
data:
{
    "projectId":"ab2775b4-cf09-4794-XXXX-XXXXXXXXXXXX",
    "categoryId":"b062a3f3-0a37-44d1-XXXX-XXXXXXXXXXXX",
    "code":"61XX",
    "to":"010XXXXXXX",
    "store":"google"
}
```

| Attribute | Type | Required | Description |
| --- | --- | --- | --- |
| projectId | String | -   | GAMEPOT SDK的projectId |
| categoryId | String | -   | GAMEPOT提前预约页面的categoryId |
| code | String | -   | 收到的验证码 |
| to  | String | -   | 接收SMS验证码的联系方式 |
| store | String | -   | 商店（Google、ONE、Apple） |

### Response

成功

```javascript
{
    "code": 200,
    "error": "验证成功。"
}
```

| Attribute | Type | Description |
| --- | --- | --- |
| code | Int | 结果值 \（200：成功，404：失败\） |
| error | String | 错误消息 |

失败

```javascript
{
    "code": 404,
    "error": "此号码已注册。"
}
```

| Attribute | Type | Description |
| --- | --- | --- |
| code | Int | 结果值 \（1：成功，失败情况下请参考错误代码\） |
| error | String | 错误内容 |


# 查询本人认证结果

可查询本人认证结果值。

## 请求<a name="요청"></a>

```http
GET https://plugin.gamepot.io/v1/certifications/{orderID}
```

### 请求报头<a name="요청헤더"></a>

| 报头名称| 是否为必填| 说明|
|:----------|:----------:|:----------|
| X-API-KEY| O| GamePot发放的认证密钥参数|
| X-PROJECT-ID| O| 项目ID

## 响应<a name="응답"></a>

| 字段名称| 类型| 说明|
|:----------|:----------|:----------|
| project_id| String| 项目ID|
| plugin_id| String| 插件ID|
| user_id| String| 用户ID|
| name| String| 名称|
| gender| Int| 性别|
| birth| Int| 出生年月日|
| phone| String| 手机号码|
| tid| String| TID|
| ci| String| CI|
| di| String| DI|
| order_id| String| 订单号|
| userdata| String| 用户数据|
| createdAt| Date| 输入日期|

## 示例<a name="예시"></a>

### 请求示例<a name="요청예시"></a>

```http
  curl --location --request GET 'https://plugin.gamepot.io/v1/certifications/[ORDER-ID]' \
--header 'X-API-KEY: [X-API-KEY]' \
--header 'X-PROJECT-ID: [PROJECT-ID]' \
--data-raw ''

```

### 响应示例<a name="응답예시"></a>

```http
{
    "_id": "61f23bca9xxxxxxx",
    "project_id": "ab2775b4-xxxx-xxxx-xxxx-xxxxxxxxx",
    "plugin_id": "61dxxxxxxxx",
    "user_id": "djd827hd-xxxx-xxxx-xxxx-xxxxxxxx",
    "name": "洪吉童",
    "gender": "1",
    "birth": "1979xxxx",
    "phone": "010xxxxxxxx",
    "tid": "20220xxxxxxxxxxxxxxx",
    "ci": "PPfDvGpApYltvl5cN+xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    "di": "MC0GCCqGSIb3Dxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    "order_id": "ODe1c6e1xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    "userdata": "",
    "createdAt": "2022-01-27T06:29:30.000Z"
}
```

## 错误代码<a name="오류코드"></a>

如果不存在OrderID，则返回如下内容。

```
{
  "status": -1,
  "message": "orderId is not found"
}
```

<!--

# 查询客户咨询分类

## 查询客户咨询分类



可确认客户咨询问题的分类列表。

#### Request

- Method : POST
- URI : /v2/api/ticket/category

```text
POST
url : https://dashboard-api.gamepot.ntruss.com/v2/api/ticket/category
Header : 'language: ko'
Header : 'X-API-KEY: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
Header : 'X-PROJECT-ID: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'
```

| Header       | Type   | Required | Description                                         |
| :----------- | :----- | :------- | --------------------------------------------------- |
| language     | String |          | 客户咨询分类中设置的语言（国家代码：ISO 639-1代码） |
| X-API-KEY    | String | O        | GAMEPOT发放的认证密钥                               |
| X-PROJECT-ID | String | O        | 仪表盘项目ID                                        |

#### Response

成功

```javascript
示例：[
  {
    id: '1e156831-0111-4ec5-9195-9c3d56d2b3c1',
    title: '会员',
    agree_story_url: '',
  },
  {
    id: 'e87a0cad-39e2-495b-ba3d-d2cddb6b19a7',
    title: '游戏',
    agree_story_url: '',
  },
  {
    id: '493fb91f-1670-4d94-af2c-fb65e2a14f61',
    title: '支付',
    content:
      '- 支付日期与时间段：（请尽可能详细填写。）\n- 电信运营商/编号：（例如，SKT、KT、LGT / 010-0000-0000）\n- 进行支付的商店：（例如，Google、App Store、ONE Store）\n- 购买金额：（购买多次时，按日期和时间段分开填写）\n- 购买发票号码：\n- 请求事项：',
    agree_story_url: '',
  },
  {
    id: '23ba4a6c-cd26-4003-914d-9f669c8a1169',
    title: '事件',
    agree_story_url: '',
  },
  {
    id: '7e2cfd61-7715-4eb0-94b7-74fe0941f852',
    title: '其他',
    agree_story_url: '',
  },
];
```

| Attribute       | Type   | Description                                   |
| :-------------- | :----- | :-------------------------------------------- |
| id              | String | 客户咨询分类唯一ID                            |
| title           | String | 分类标题                                      |
| content         | String | 分类详细内容                                  |
| agree_story_url | String | 在仪表盘 > 分类 > 事件弹窗项目中设置的页面URL |

失败

```javascript
{
  "status": -1,
  "message": "X-API-KEY was wrong."
}
```

#### Error code

| Code | Description    |
| :--- | :------------- |
| -1   | X-API-KEY错误  |
| -6   | 项目ID信息错误 |
| -9   | 未输入必须参数 |



# 添加客户咨询

## 添加客户咨询



此API用于添加客户咨询的问题。

#### Request

- Method : POST
- URI : /v2/api/ticket

```text
POST
url : https://dashboard-api.gamepot.ntruss.com/v2/api/ticket
Header : 'application/json'
Header : 'language: ko'
Header : 'X-PROJECT-ID: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'
Header : 'X-API-KEY: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
DATA : '{
"type": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
"subject": "title",
"body": "韩语",
"email": "email address",
"phone": "11234",
"serverName":"serverName",
"character": "character",
"agree_termsofuse": false,
"agree_type": false,
"file": ["uploded url address", ...]
}'
```

| Header       | Type   | Required | Description                                   |
| :----------- | :----- | :------- | --------------------------------------------- |
| language     | String |          | 客户咨询时所用语言（国家代码：ISO 639-1代码） |
| X-API-KEY    | String | O        | GAMEPOT发放的认证密钥                         |
| X-PROJECT-ID | String | O        | 仪表盘项目ID                                  |

| Attribute        | Type    | Required | Description                                                |
| :--------------- | :------ | :------- | :--------------------------------------------------------- |
| type             | String  | O        | 客户咨询分类唯一ID                                         |
| subject          | String  | O        | 客户咨询标题                                               |
| body             | String  | O        | 客户咨询正文内容                                           |
| email            | String  |          | 客户咨询输入的邮件信息                                     |
| phone            | String  |          | 客户咨询输入的联系方式信息                                 |
| serverName       | String  |          | 客户咨询的服务器/角色信息                                  |
| character        | String  |          | 客户咨询的角色/游戏会员ID信息                              |
| agree_termsofuse | Boolean |          | 是否同意必要条款（是否同意平台收集信息或客户咨询使用条款） |
| agree_type       | Boolean |          | 是否同意可选条款（是否同意分类中设置的事件条款）           |
| file             | String  |          | 上传文件的地址                                             |

####

#### Response

成功

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

| Attribute | Type | Description                           |
| :-------- | :--- | :------------------------------------ |
| status    | Int  | 结果值\(1：成功，失败请参考错误代码\) |

失败

```javascript
{
  "status": -1,
  "message": "X-API-KEY was wrong."
}
```

#### Error code

| Code | Description    |
| :--- | :------------- |
| -1   | X-API-KEY错误  |
| -6   | 项目ID信息错误 |
| -9   | 未输入必须参数 |


-->









<!--

### 用户查询 API

使用用户 UID 查询用户。

#### 请求

- Method : GET
- URI : /user/{userID}

```text
GET
url : https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/user/{userId}
Header : 'accept-language: ko'
Header : 'x-api-key: {从GamePot仪表盘中获取的API密钥}'
```

| 头部      | 类型   | 必填 | 描述                   |
| :-------- | :----- | :--- | :--------------------- |
| x-api-key | 字符串 | O    | GamePot 发放的认证密钥 |

| 属性      | 类型   | 描述                     |
| :-------- | :----- | :----------------------- |
| projectId | 字符串 | GamePot SDK 的 projectId |
| userId    | 字符串 | GamePot SDK 的 userId    |

#### 响应

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

| 属性      | 类型   | 描述                                            |
| :-------- | :----- | :---------------------------------------------- |
| status    | Int    | 结果值\(1：成功，失败请参考错误代码\)           |
| id        | 字符串 | 用户 ID                                         |
| deleted   | 布尔型 | 是否删除会员\(true：删除，false：正常\)         |
| store_id  | 字符串 | 创建账户时访问的商店（google…）                 |
| country   | 字符串 | 用户国家代码（ISO 3166-1 标准）                 |
| remoteip  | 字符串 | 用户 IP                                         |
| adid      | 字符串 | 广告 ID                                         |
| device    | 字符串 | 设备种类（Android、ios）                        |
| network   | 字符串 | 用户访问网络（WI-FI…）                          |
| version   | 字符串 | 客户端的版本信息                                |
| model     | 字符串 | 用户设备型号名称                                |
| token     | 字符串 | 推送令牌                                        |
| push      | 布尔型 | 是否同意推送\(true：同意，false：不同意\)       |
| night     | 布尔型 | 是否同意夜间推送\(true：同意，false：不同意\)   |
| ad        | 布尔型 | 是否同意广告性推送\(true：同意，false：不同意\) |
| memo      | 字符串 | 会员备忘录                                      |
| device_id | 字符串 | 会员设备 ID                                     |
| createdAt | 字符串 | 会员创建日期                                    |
| updatedAt | 字符串 | 会员信息修改日期                                |
| loginedAt | 字符串 | 最后访问日期                                    |
| deletedAt | 字符串 | 会员删除日期                                    |

失败

```javascript
{
  "status": -6,
  "message": "projectId was wrong."
}
```

| 属性    | 类型   | 描述                                  |
| :------ | :----- | :------------------------------------ |
| status  | Int    | 结果值\(1：成功，失败请参考错误代码\) |
| message | 字符串 | 错误内容                              |

### 用户停用查询 API

使用用户 UID 查询用户是否已停用。

#### 请求

- Method : GET
- URI : /user/{userID}/block

```text
GET
url : https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/user/{userId}/block
Header : 'accept-language: ko'
Header : 'x-api-key: {从GamePot仪表盘中获取的API密钥}'
```

| 头部      | 类型   | 必填 | 描述                   |
| :-------- | :----- | :--- | :--------------------- |
| x-api-key | 字符串 | O    | GamePot 发放的认证密钥 |

| 属性      | 类型   | 描述                     |
| :-------- | :----- | :----------------------- |
| projectId | 字符串 | GamePot SDK 的 projectId |
| userId    | 字符串 | GamePot SDK 的 userId    |

#### 响应

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
        "value": "测试-ko",
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

| 属性        | 类型   | 描述                                                                            |
| :---------- | :----- | :------------------------------------------------------------------------------ |
| status      | Int    | 结果值\(1：成功，失败请参考错误代码\)                                           |
| id          | 字符串 | 用户停用信息相关 ID                                                             |
| member_id   | 字符串 | 用户 ID                                                                         |
| deleted     | 布尔型 | 是否删除用户停用信息\(true：删除，false：正常\)                                 |
| type        | 字符串 | 停用分类\(manual：手动，autopurchase：自动\)                                    |
| status      | Int    | 状态 \(1：激活，2：禁用\)                                                       |
| message     | 字符串 | 用户停用原因（目前未使用）                                                      |
| lang        | 字符串 | 停用消息语言                                                                    |
| value       | 字符串 | 停用原因消息                                                                    |
| default     | 布尔型 | 默认语言设置<br>messageMulti 中没有设备的语言值时，默认显示设置为 true 的消息。 |
| startedAt   | 字符串 | 停用开始日期                                                                    |
| endedAt     | 字符串 | 停用结束日期                                                                    |
| createdAt   | 布尔型 | 停用添加日期                                                                    |
| updatedAt   | 布尔型 | 停用修改日期                                                                    |
| deletedAt   | 布尔型 | 停用删除日期                                                                    |
| category_id | 字符串 | 停用分类 ID                                                                     |

失败

```javascript
{
  "status": -6,
  "message": "projectId was wrong."
}
```

| 属性    | 类型   | 描述                                     |
| :------ | :----- | :--------------------------------------- |
| status  | Int    | 结果值 \(1：成功，失败时请参考错误代码\) |
| message | 字符串 | 错误内容                                 |

### 用户停用设置 API

使用用户 UID 进行用户停用处理。

#### 请求

- Method : POST
- URI : /user/{userID}/block

```text
POST
url : https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/user/{userId}/block
Header : 'accept-language: ko'
Header : 'content-type: application/json'
Header : 'x-api-key: {从GamePot仪表盘中获取的API密钥}'
data: '{
        "messageMulti": [
                {
                    "lang": "ko",
                    "value": "测试",
                    "default": true
                }
            ],
            "startedAt": "2020-05-11 12:02",
            "endedAt": "2020-05-25 22:00"
       }'
```

| 头部      | 类型   | 必填 | 描述                   |
| :-------- | :----- | :--- | :--------------------- |
| x-api-key | 字符串 | O    | GamePot 发放的认证密钥 |

| 属性      | 类型   | 描述                                                                            |
| :-------- | :----- | :------------------------------------------------------------------------------ |
| projectId | 字符串 | GamePot SDK 的 projectId                                                        |
| userId    | 字符串 | GamePot SDK 的 userId                                                           |
| lang      | 字符串 | 停用消息语言                                                                    |
| value     | 字符串 | 停用原因消息                                                                    |
| default   | 布尔型 | 默认语言设置<br>messageMulti 中没有设备的语言值时，默认显示设置为 true 的消息。 |
| startedAt | 字符串 | 停用开始日期`YYYY-MM-DD HH:mm`                                                  |
| endedAt   | 字符串 | 停用结束日期 `YYYY-MM-DD HH:mm`                                                 |

#### 响应

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

| 属性   | 类型   | 描述                                  |
| :----- | :----- | :------------------------------------ |
| status | Int    | 结果值\(1：成功，失败请参考错误代码\) |
| id     | 字符串 | 已停用的 ID                           |

失败

```javascript
{
  "status": -5,
  "message": "ApiKey was expired."
}
```

| 属性    | 类型   | 描述                                  |
| :------ | :----- | :------------------------------------ |
| status  | Int    | 结果值\(1：成功，失败请参考错误代码\) |
| message | 字符串 | 错误内容                              |

#### 错误代码

| 代码 | 描述                                                     |
| :--- | :------------------------------------------------------- |
| -11  | 正文中缺少数据                                           |
| -12  | messageMulti 值不是 JSON Array 时                        |
| -13  | startedAt 值的格式有误时。仅可使用`YYYY-MM-DD HH:mm`形式 |
| -14  | endedAt 值的格式有误时。仅可使用`YYYY-MM-DD HH:mm`形式   |
| -15  | messageMulti 值的数据格式有误时                          |
| -16  | messageMulti 值的数据中没有 default true 或存在多个时    |

### 每日访问者（DAU）查询 API

可以查询每日访问者。

#### 请求

- Method : GET
- URI : /user/statistics/dau

```text
GET
url : https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/user/statistics/dau
Header : 'accept-language: ko'
Header : 'x-api-key: {从GamePot仪表盘中获取的API密钥}'
```

| 头部      | 类型   | 必填 | 描述                   |
| :-------- | :----- | :--- | :--------------------- |
| x-api-key | 字符串 | O    | GamePot 发放的认证密钥 |

| 属性      | 类型   | 描述                     |
| :-------- | :----- | :----------------------- |
| projectId | 字符串 | GamePot SDK 的 projectId |
| startDate | 字符串 | 开始查询日期`YYYY-MM-DD` |
| endDate   | 字符串 | 最终查询日期`YYYY-MM-DD` |

> 未输入 startDate、endDate 等查询条件时，将查询最近 30 天的数据。

#### 响应

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

| 属性       | 类型   | 描述                                  |
| :--------- | :----- | :------------------------------------ |
| status     | Int    | 结果值\(1：成功，失败请参考错误代码\) |
| totalCount | Int    | dau 查询结果（个）数                  |
| date       | 字符串 | 统计时间                              |
| count      | Int    | （相应日期）DAU                       |

失败

```javascript
{
  "status": -11,
  "message": "startDate format was wrong.(YYYY-MM-DD)"
}
```

| 属性    | 类型   | 描述                                  |
| :------ | :----- | :------------------------------------ |
| status  | Int    | 结果值\(1：成功，失败请参考错误代码\) |
| message | 字符串 | 错误内容                              |

#### 错误代码

| 代码 | 描述                                               |
| :--- | :------------------------------------------------- |
| -11  | startDate 值的格式有误时。仅可使用`YYYY-MM-DD`形式 |
| -12  | endDate 值的格式有误时。仅可使用`YYYY-MM-DD`形式   |

### 新用户（NRU）查询 API

可以查询新用户。

#### 请求

- Method : GET
- URI : /user/statistics/nru

```text
GET
url : https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/user/statistics/nru
Header : 'accept-language: ko'
Header : 'x-api-key: {从GamePot仪表盘中获取的API密钥}'
```

| 头部      | 类型   | 必填 | 描述                   |
| :-------- | :----- | :--- | :--------------------- |
| x-api-key | 字符串 | O    | GamePot 发放的认证密钥 |

| 属性      | 类型   | 描述                     |
| :-------- | :----- | :----------------------- |
| projectId | 字符串 | GamePot SDK 的 projectId |
| startDate | 字符串 | 开始查询日期`YYYY-MM-DD` |
| endDate   | 字符串 | 最终查询日期`YYYY-MM-DD` |

> 未输入 startDate、endDate 等查询条件时，将查询最近 30 天的数据。

#### 响应

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

| 属性       | 类型   | 描述                                  |
| :--------- | :----- | :------------------------------------ |
| status     | Int    | 结果值\(1：成功，失败请参考错误代码\) |
| totalCount | int    | 查询（个）数                          |
| date       | 字符串 | 统计日期                              |
| count      | int    | （相应日期）NRU                       |

失败

```javascript
{
  "status": -11,
  "message": "startDate format was wrong.(YYYY-MM-DD)"
}
```

| 属性    | 类型   | 描述                                  |
| :------ | :----- | :------------------------------------ |
| status  | Int    | 结果值\(1：成功，失败请参考错误代码\) |
| message | 字符串 | 错误内容                              |

#### 错误代码

| 代码 | 描述                                               |
| :--- | :------------------------------------------------- |
| -11  | startDate 值的格式有误时。仅可使用`YYYY-MM-DD`形式 |
| -12  | endDate 值的格式有误时。仅可使用`YYYY-MM-DD`形式   |

### 同时访问者（CCU）查询 API

在所选的三个日期里，可按时间段查询同时访问者。

#### 请求

- Method : GET
- URI : /user/statistics/ccu

```text
GET
url : https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/user/statistics/ccu
Header : 'accept-language: ko'
Header : 'x-api-key: {从GamePot仪表盘中获取的API密钥}'
```

| 头部      | 类型   | 必填 | 描述                   |
| :-------- | :----- | :--- | :--------------------- |
| x-api-key | 字符串 | O    | GamePot 发放的认证密钥 |

| 属性      | 类型   | 描述                       |
| :-------- | :----- | :------------------------- |
| projectId | 字符串 | GamePot SDK 的 projectId   |
| oneDate   | 字符串 | 第一个查询日期`YYYY-MM-DD` |
| twoDate   | 字符串 | 第二个查询日期`YYYY-MM-DD` |
| threeDate | 字符串 | 第三个查询日期`YYYY-MM-DD` |

> 提供 oneDate、twoDate、threeDate 的查询条件，未提供时可查询当天及前 2 日的访问者。

#### 响应

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

| 属性       | 类型   | 描述                                  |
| :--------- | :----- | :------------------------------------ |
| status     | Int    | 结果值\(1：成功，失败请参考错误代码\) |
| totalCount | Int    | ccu 查询结果（个）数                  |
| createdAt  | 字符串 | 统计时间                              |
| one        | Int    | （第一个日期的）相应时间同时访问者数  |
| two        | Int    | （第二个日期的）相应时间同时访问者数  |
| three      | Int    | （第三个日期的）相应时间同时访问者数  |

失败

```javascript
{
  "status": -11,
  "message": "threeDate format was wrong.(YYYY-MM-DD)"
}
```

| 属性    | 类型   | 描述                                  |
| :------ | :----- | :------------------------------------ |
| status  | Int    | 结果值\(1：成功，失败请参考错误代码\) |
| message | 字符串 | 错误内容                              |

#### 错误代码

| 代码 | 描述                                               |
| :--- | :------------------------------------------------- |
| -11  | threeDate 值的格式有误时。仅可使用`YYYY-MM-DD`形式 |
| -12  | twoDate 值的格式有误时。仅可使用`YYYY-MM-DD`形式   |
| -13  | oneDate 值的格式有误时。仅可使用`YYYY-MM-DD`形式   |

### 支付查询 API

以支付 ID 查询支付明细。

#### 请求

- Method : GET
- URI : /purchase/{transactionID}

```text
GET
url : https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/purchase/{transactionID}
Header : 'accept-language: ko'
Header : 'x-api-key: {从GamePot仪表盘中获取的API密钥}'
```

| 头部      | 类型   | 必填 | 描述                   |
| :-------- | :----- | :--- | :--------------------- |
| x-api-key | 字符串 | O    | GamePot 发放的认证密钥 |

| 属性          | 类型   | 描述                     |
| :------------ | :----- | :----------------------- |
| projectId     | 字符串 | GamePot SDK 的 projectId |
| transactionID | 字符串 | GamePot SDK 的支付 ID    |

#### 响应

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

| 属性                 | 类型   | 描述                                                        |
| :------------------- | :----- | :---------------------------------------------------------- |
| status               | Int    | 结果值\(1：成功，失败请参考错误代码\)                       |
| （result 的）status  | Int    | 支付结果值\(1：成功）                                       |
| exchange_price       | Int    | 支付金额（适用汇率）                                        |
| project_id           | 字符串 | GamePot SDK 的 projectId                                    |
| store_id             | 字符串 | 商店 ID（google、one、apple、galaxy）                       |
| payment_id           | 字符串 | 支付商店 ID（google、tpay…）ㅣ一般与 store_id 相同          |
| signature            | 字符串 | 签名                                                        |
| order_id             | 字符串 | Order ID                                                    |
| currency             | 字符串 | 货币                                                        |
| userdata             | 字符串 | 用户信息                                                    |
| price                | Int    | 支付金额                                                    |
| id                   | 字符串 | 支付数据的 unique ID                                        |
| unique_id            | 字符串 | Unique ID                                                   |
| transaction_id       | 字符串 | 商店支付 ID                                                 |
| createdAt            | 字符串 | 创建日期                                                    |
| updatedAt            | 字符串 | 更新日期                                                    |
| request              | 字符串 | 支付请求值                                                  |
| response             | 字符串 | 支付响应值                                                  |
| （item_id 的）status | 字符串 | （item_id 的）结果值                                        |
| type                 | 字符串 | 道具类型（应用内）                                          |
| name                 | 字符串 | 道具名称                                                    |
| prices               | 字符串 | 道具价格                                                    |
| user_id              |        | 响应成功值中 user_id 部分请参考<b><I>用户查询 API</I></b>。 |

失败

```javascript
{
  "status": -6,
  "message": "projectId was wrong."
}
```

| 属性    | 类型   | 描述                                     |
| :------ | :----- | :--------------------------------------- |
| status  | Int    | 结果值 \(1：成功，失败时请参考错误代码\) |
| message | 字符串 | 错误内容                                 |

### 支付取消查询 API

以支付 ID 查询取消支付明细。

> 仅限查询 Google 支付。

#### 请求

- Method : GET
- URI : /purchase/voided/{transactionID}

```text
GET
url : https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/purchase/voided/{transactionID}
Header : 'accept-language: ko'
Header : 'x-api-key: {从GamePot仪表盘中获取的API密钥}'
```

| 头部      | 类型   | 必填 | 描述                   |
| :-------- | :----- | :--- | :--------------------- |
| x-api-key | 字符串 | O    | GamePot 发放的认证密钥 |

| 属性          | 类型   | 描述                     |
| :------------ | :----- | :----------------------- |
| projectId     | 字符串 | GamePot SDK 的 projectId |
| transactionID | 字符串 | GamePot SDK 的支付 ID    |

#### 响应

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

| 属性        | 类型   | 描述                                                            |
| :---------- | :----- | :-------------------------------------------------------------- |
| status      | Int    | 结果值\(1：成功，失败请参考错误代码\)                           |
| id          | 字符串 | 取消支付 ID                                                     |
| member_id   | 字符串 | 用户 UID                                                        |
| package_id  | 字符串 | 包名                                                            |
| price       | int    | 支付金额                                                        |
| deleted     | 布尔型 | 是否删除\(true：删除，false：正常\)                             |
| purchasedAt | 字符串 | 支付日期                                                        |
| voidedAt    | 字符串 | 取消支付日期                                                    |
| createdAt   | 字符串 | 创建日期                                                        |
| updatedAt   | 字符串 | 更新日期                                                        |
| deletedAt   | 字符串 | 删除日期                                                        |
| currency    | 字符串 | 货币                                                            |
| status      | Int    | 状态                                                            |
| purchase_id |        | 响应成功值中 purchase_id 部分请参考<b><I>支付查询 API</I></b>。 |

失败

```javascript
{
  "status": -6,
  "message": "projectId was wrong."
}
```

| 属性    | 类型   | 描述                                     |
| :------ | :----- | :--------------------------------------- |
| status  | Int    | 结果值 \(1：成功，失败时请参考错误代码\) |
| message | 字符串 | 错误内容                                 |

### 支付销售统计查询 API

查询支付销售统计。

#### 请求

- Method : GET
- URI : /purchase/statistics

```text
GET
url : https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/purchase/statistics?startDate={startDate}&endDate={endDate}&currency={currency}
Header : 'accept-language: ko'
Header : 'x-api-key: {从GamePot仪表盘中获取的API密钥}'
```

| 头部      | 类型   | 必填 | 描述                   |
| :-------- | :----- | :--- | :--------------------- |
| x-api-key | 字符串 | O    | GamePot 发放的认证密钥 |

| 属性      | 类型   | 描述                                                  |
| :-------- | :----- | :---------------------------------------------------- |
| projectId | 字符串 | GamePot SDK 的 projectId                              |
| startDate | 字符串 | 支付销售统计搜索开始日期`YYYY-MM-DD`                  |
| endDate   | 字符串 | 支付销售统计搜索结束日期`YYYY-MM-DD`                  |
| currency  | 字符串 | 支付销售统计货币搜索（全部…）<br>遵循 ISO 4217 标准。 |

> 未输入 startDate、endDate 等查询条件时，将查询最近 30 天的数据。

#### 响应

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

| 属性         | 类型   | 描述                                  |
| :----------- | :----- | :------------------------------------ |
| status       | Int    | 结果值\(1：成功，失败请参考错误代码\) |
| totalCount   | Int    | 搜索结果值数                          |
| currencyList | 字符串 | 货币列表<br>遵循 ISO 4217 标准。      |
| date         | 字符串 | 统计日期                              |
| count        | 字符串 | 销量统计金额                          |

失败

```javascript
{
  "status": -6,
  "message": "projectId was wrong."
}
```

| 属性    | 类型   | 描述                                  |
| :------ | :----- | :------------------------------------ |
| status  | Int    | 结果值\(1：成功，失败请参考错误代码\) |
| message | 字符串 | 错误内容                              |

#### 错误代码

| 代码 | 描述                                               |
| :--- | :------------------------------------------------- |
| -11  | startDate 值的格式有误时。仅可使用`YYYY-MM-DD`形式 |
| -12  | endDate 值的格式有误时。仅可使用`YYYY-MM-DD`形式   |

### 角色查询 API

查询游戏内玩家 ID。

#### 请求

- Method : GET
- URI : /player/{playerID}

```text
GET
url : https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/player/{playerID}
Header : 'accept-language: ko'
Header : 'x-api-key: {从GamePot仪表盘中获取的API密钥}'
```

| 头部      | 类型   | 必填 | 描述                   |
| :-------- | :----- | :--- | :--------------------- |
| x-api-key | 字符串 | O    | GamePot 发放的认证密钥 |

| 属性      | 类型   | 描述                     |
| :-------- | :----- | :----------------------- |
| projectId | 字符串 | GamePot SDK 的 projectId |
| playerID  | 字符串 | GamePot SDK 的玩家 ID    |

#### 响应

成功

```javascript
{
  "status": 1,
  "result": {
    "id": "xxxxxxxxxxxxxxx",
    "player_id": "测试ID",
    "server_id": "测试服务器",
    "name": "测试名称",
    "level": "12",
    "userdata": "dododo",
    "ip": "xxx.xxx.xxx.xxx",
    "createdAt": "Fri Feb 21 2020 14:15:33 GMT+0900 (GMT+09:00)",
    "updatedAt": "Fri Feb 21 2020 14:15:33 GMT+0900 (GMT+09:00)",
    "user_id": "xxxxxxxxxxxxxxx"
  }
}
```

| 属性      | 类型   | 描述                                  |
| :-------- | :----- | :------------------------------------ |
| status    | Int    | 结果值\(1：成功，失败请参考错误代码\) |
| id        | 字符串 | 用户 ID  / 请忽略它。                             |
| player_id | 字符串 | 玩家 ID                               |
| server_id | 字符串 | 服务器 ID                             |
| name      | 字符串 | 玩家名                                |
| level     | 字符串 | 玩家等级                              |
| userdata  | 字符串 | 添加的 Userdata                       |
| ip        | 字符串 | 玩家 IP                               |
| createdAt | 字符串 | 玩家创建日期                          |
| updatedAt | 字符串 | 玩家更新日期                          |
| user_id   | 字符串 | GAMEPOT UID                           |

失败

```javascript
{
  "status": -1,
  "message": "ApiKey was wrong."
}
```

| 属性    | 类型   | 描述                                     |
| :------ | :----- | :--------------------------------------- |
| status  | Int    | 结果值 \(1：成功，失败时请参考错误代码\) |
| message | 字符串 | 错误内容                                 |

### 优惠券使用查询 API

查询优惠券使用明细。

> 关键词优惠券仅可查询已使用的优惠券。

#### 请求

- Method : GET
- URI : /coupon/{couponNumber}

```text
GET
url : https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/coupon/{couponNumber}?userData={userData}
Header : 'accept-language: ko'
Header : 'x-api-key: {从GamePot仪表盘中获取的API密钥}'
```

| 头部      | 类型   | 必填 | 描述                   |
| :-------- | :----- | :--- | :--------------------- |
| x-api-key | 字符串 | O    | GamePot 发放的认证密钥 |

| 属性         | 类型   | 描述                     |
| :----------- | :----- | :----------------------- |
| projectId    | 字符串 | GamePot SDK 的 projectId |
| couponNumber | 字符串 | 仪表盘发放的优惠券编号   |
| userData     | 字符串 | 用户数据                 |

#### 响应

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
      "desc": "第2季更新提前预约奖励",
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

| 属性                   | 类型   | 描述                                        |
| :--------------------- | :----- | :------------------------------------------ |
| status                 | Int    | 结果值\(1：成功，失败请参考错误代码\)       |
| id                     | 字符串 | 优惠券使用明细 ID                           |
| status                 | 布尔型 | 优惠券是否使用\(true：使用，false：未使用\) |
| enable                 | Int    | 是否可用                                    |
| number                 | 字符串 | 优惠券编号                                  |
| userdata               | 字符串 | 优惠券使用用户查询                          |
| usedAt                 | 字符串 | 优惠券使用日期                              |
| request                | 字符串 | 优惠券使用请求                              |
| response               | 字符串 | 优惠券使用响应                              |
| （coupon_id 的）id     | 字符串 | 优惠券 ID                                   |
| （coupon_id 的）enable | int    | 是否可用                                    |
| type                   | 字符串 | 优惠券类型                                  |
| keyword                | 字符串 | 关键词优惠券关键词                          |
| desc                   | 字符串 | 优惠券名称                                  |
| used                   | int    | 优惠券状态                                  |
| count                  | int    | 优惠券数量                                  |
| length                 | int    | 优惠券长度                                  |
| limit                  | 字符串 | 道具数量                                    |
| prefix                 | 字符串 | 优惠券后缀                                  |
| suffix                 | 字符串 | 优惠券前缀                                  |
| store_id               | 字符串 | 商店 ID（google、one、apple、galaxy）       |
| startedAt              | 字符串 | 优惠券使用开始日期                          |
| endedAt                | 字符串 | 优惠券使用结束日期                          |
| item_id                | 字符串 | 道具 ID                                     |
| store_item_id          | 字符串 | 道具商店 ID                                 |
| count                  | int    | 道具数量                                    |

失败

```javascript
{
  "status": -1,
  "message": "ApiKey was wrong."
}
```

| 属性    | 类型   | 描述                                     |
| :------ | :----- | :--------------------------------------- |
| status  | Int    | 结果值 \(1：成功，失败时请参考错误代码\) |
| message | 字符串 | 错误内容                                 |

### 优惠券使用 API

可以使用优惠券。

#### 请求

- Method : PUT
- URI : /store/{storeID}/user/{userID}/coupon/{couponNumber}

```text
PUT
url : https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/store/{storeID}/user/{userID}/coupon/{couponNumber}
Header : 'accept-language: ko'
Header : 'x-api-key: {从GamePot仪表盘中获取的API密钥}'
```

| 头部      | 类型   | 必填 | 描述                   |
| :-------- | :----- | :--- | :--------------------- |
| x-api-key | 字符串 | O    | GamePot 发放的认证密钥 |

| 属性         | 类型   | 描述                                  |
| :----------- | :----- | :------------------------------------ |
| projectId    | 字符串 | GamePot SDK 的 projectId              |
| storeID      | 字符串 | 商店 ID（google、one、apple、galaxy） |
| userID       | 字符串 | GamePot SDK 的用户 UID                |
| couponNumber | 字符串 | 优惠券编号                            |

#### 响应

成功

```javascript
{
  "status": 1,
  "message": "success"
}
```

| 属性    | 类型   | 描述                                  |
| :------ | :----- | :------------------------------------ |
| status  | Int    | 结果值\(1：成功，失败请参考错误代码\) |
| message | 字符串 | 结果内容                              |

失败

```javascript
{
  "status": -5,
  "message": "ApiKey was expired."
}
```

| 属性      | 类型   | 描述                                     |
| :-------- | :----- | :--------------------------------------- |
| status    | Int    | 结果值 \(1：成功，失败时请参考错误代码\) |
| message   | 字符串 | 错误内容                                 |
| errorcode | 字符串 | 错误代码                                 |

### 发布中的公告事项 API

可以查看发布中的公告事项。

#### 请求

- Method : GET
- URI : /store/{storeID}/notice/posting

```text
GET
url : https://dashboard-api.gamepot.ntruss.com/v1/api/project/{projectId}/store/{storeID}/notice/posting
Header : 'accept-language: ko'
Header : 'x-api-key: {从GamePot仪表盘中获取的API密钥}'
```

| 头部      | 类型   | 必填 | 描述                   |
| :-------- | :----- | :--- | :--------------------- |
| x-api-key | 字符串 | O    | GamePot 发放的认证密钥 |

| 属性      | 类型   | 描述                                  |
| :-------- | :----- | :------------------------------------ |
| projectId | 字符串 | GamePot SDK 的 projectId              |
| storeID   | 字符串 | 商店 ID（google、one、apple、galaxy） |

#### 响应

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

| 属性       | 类型   | 描述                                   |
| :--------- | :----- | :------------------------------------- |
| status     | Int    | 结果值\(1：成功，失败请参考错误代码\)  |
| totalCount | 字符串 | 公告事项（图像）查询（个）数           |
| baseUrl    | 字符串 | Object Storage Bucket URL              |
| id         | 字符串 | （相应图像的）唯一 ID                  |
| store_id   | 字符串 | 支付商店（google、one、apple、galaxy） |
| enable     | 布尔型 | 是否激活公告事项                       |
| url        | 字符串 | （单击操作）url                        |
| scheme     | 字符串 | （单击操作）scheme                     |
| startDate  | 字符串 | 公告开始日期                           |
| endDate    | 字符串 | 公告结束日期                           |
| lang       | 字符串 | 语言                                   |
| value      | 字符串 | （baseUrl 以下）资源地址               |
| default    | 布尔型 | 是否为默认语言                         |

失败

```javascript
{
  "status": -1,
  "message": "ApiKey was wrong."
}
```

| 属性    | 类型   | 描述                                     |
| :------ | :----- | :--------------------------------------- |
| status  | Int    | 结果值 \(1：成功，失败时请参考错误代码\) |
| message | 字符串 | 错误内容                                 |

-->