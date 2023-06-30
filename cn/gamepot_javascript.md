---
search:
  keyword:
    - gamepot
---

#### **为提供 NAVER CLOUD PLATFORM 产品的详细使用方法和 API 的多种使用方式，分别提供<a href="https://guide.ncloud-docs.com/docs/zh/home" target="_blank">[说明书]</a>和<a href="https://api.ncloud-docs.com/docs/zh/home" target="_blank">[API 参考指南]</a>以供参考。**

<a href="https://api.ncloud-docs.com/docs/zh/game-gamepot" target="_blank">进入 Gamepot API 参考指南 >></a><br />
<a href="https://guide.ncloud-docs.com/docs/zh/game-gamepot-overview" target="_blank">进入 Gamepot 说明书 >></a>

# Javascript SDK

说明如何使用GAMEPOT Javascript SDK在网页上关联GAMEPOT。 通过安装SDK并配置环境，可关联游戏和仪表盘。

使用Javascript的GAMEPOT SDK时，所需的配置要求如下。

* 最低配置：Chrome 4、IE 8、Firefox 3.5、Safari 4、Opera 10.50等


## SDK安装及环境配置 <a name="SDK설치및환경구성"></a>

使用JavaScript SDK时所需的基本设置方法如下。 


1. 请下载[gamepot-sdk-javascript-lastest.min.js](https://gamepot.gcdn.ntruss.com/gamepot-sdk-javascript-lastest.min.js){target=&quot;_blank&quot;}。 
2. 请在head和head之间添加gamepot-sdk-javascript-lastest. min.js。 
    ```javascript
    <head><script src="gamepot-sdk-javascript-lastest.min.js"></script></head>
    
    // 也可直接使用CDN链接。 （推荐）    
     <head><script src="https://gamepot.gcdn.ntruss.com/gamepot-sdk-javascript-lastest.min.js"></script></head>
    ```

GAMEPOT Javascript SDK作为NPM包提供，也可以通过YARN使用。
```javascript
# using npm
npm install gamepot

# using yarn
yarn add gamepot
```

社交登录控制台内设置指南： [下载](https://xyuditqzezxs1008973.cdn.ntruss.com/patch/JavascriptSDK%E1%84%85%E1%85%A9%E1%84%80%E1%85%B3%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%87%E1%85%A1%E1%86%BC%E1%84%89%E1%85%B5%E1%86%A8%E1%84%89%E1%85%A1%E1%84%8B%E1%85%AD%E1%86%BC%E1%84%89%E1%85%B5%E1%84%8F%E1%85%A9%E1%86%AB%E1%84%89%E1%85%A9%E1%86%AF%E1%84%89%E1%85%A6%E1%86%BA%E1%84%90%E1%85%B5%E1%86%BC%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3.pdf)

可用登录：Google/Facebook/Apple登录

进行Apple登录时，需要填写GAMEPOT仪表盘 > 项目设置 > 一般 > Apple ID登录项目。
必须在GAMEPOT仪表盘 > 项目设置 > 一般 > WEB- 允许域中填写登录域的地址信息。


## 重置  <a name="초기화"></a>

使用`window.onload = function() {...}`或jQuery时，在`$(ducement).ready(function() {...})`代码块内初始化，以便网页加载完成时可以运行。

```html
<html>
  <head>
    <title>Gamepot Javscript</title>
  </head>
  <body>
    <!-- YOUR WEB HTML CODES -->
    <script>
      window.onload = function () {
        // 可在GAMEPOT仪表盘中确认项目ID。
        var project_id = 'xxxxxxx-xxxx-xxxx-xxxx-xxxxxx';
        var gamepotConfig = {
          // 通用
          api_url: "https://gpapps.gamepot.ntruss.com",
          api_key: "XXXXXXXXXXXXX",
          // 使用Google登录时，如下输入Google API客户端ID。
          google_signin_client_id:"XXXXXXXXXX-XXXXXXXXXXX.apps.googleusercontent.com",
          // 使用Facebook登录时，如下输入Facebook应用ID。
          facebook_app_id: "XXXXXXXXXX",
          // 使用Apple登录时，如下输入Apple Console的Services ID和尝试登录的域名地址（未使用时设置为空值）。
          apple_client_id: "XXXXXXXXXX",
          apple_redirect_uri: "https://XXXXXXXXXX"

        };
        GP.initialize(project_id, gamepotConfig);
      };
    </script>
    <!-- YOUR WEB HTML CODES -->
  </body>
</html>
```


| Attribute | Description                                                                                                              |
| :----------- | :------------------------------------------------------------ |
| project_id              | GAMEPOT仪表盘项目ID |
| api_url                 | 与GAMEPOT仪表盘相关的URL（默认为https://gpapps.gamepot.ntruss.com或托管产品客户时，因相关地址不同，需咨询GAMEPOT） |
| api_key | GAMEPOT发放的验证密钥（仪表盘 > 项目设置 > API Key） |
| google_signin_client_id | Google控制台内的网络应用程序ID |
| facebook_app_id         | Facebook应用程序ID |
| apple_client_id         | Apple控制台生成的Services ID |
| apple_redirect_uri      | 尝试登录的域名地址 |


### 处理错误

所有的错误处理方法都相同，如果存在function (user, error){ }等错误会显示消息，如果没有错误则返回成功。

```javascript
GP.login(GP.ChannelType.EMAIL, function (user, error) { 
        if(error) { // 登录失败 
            alert(error); // 失败消息 
            return;
        } 
        alert(user);
});
```

## 登录，退出  <a name="로그인로그아웃"></a>

Google、Facebook和AppleID登录SDK可以整合使用。 


### 登录

登录UI由开发公司实现，点击登录按钮时进行关联。


#### 社交平台登录

```javascript
// 定义登录类型
// GP.ChannelType.GOOGLE：Google
// GP.ChannelType.FACEBOOK：Facebook
// GP.ChannelType.APPLE：AppleID
// GP.ChannelType.KAKAO：KakaoTalk

// 点击Facebook登录按钮时调用
GP.login(GP.ChannelType.FACEBOOK, function (user, error) {
  if (error) {
    alert(error); // 错误消息
    return;
  }
    // 登录成功
    alert(user);
});
```

USER Data Class 
| ID         | type   | desc               |
| :--------- | :----- | :----------------- |
| id | string | 会员ID      |
| token    | string | 登录令牌（JWT）  |
| nickname | string | 昵称 |
| provider | string | 社交平台登录种类 |
| providerId | string | 社交平台登录ID |
| verify | string | 是否认证 |
| agree | string | 是否同意条款 |


### 退出登录

退出当前登录的会员账户。

```javascript
GP.logout(function (result, error) {
});
```


### 通过社交账户检查是否是会员
登录后，确保在GAMEPOT的成员中，社交账户与该社交账户相连。 
```javascript
GP.linkingByUser(channeltype, function( user, error) {
    if(error) {
        alert(`${error.code}-${error.message}`); // 错误消息
        return false;
    }
    if(user == null)
        警报（“账户不存在”）
   else if(user.member_id.id)
        alert(user.member_id.id);       // 返回ID
});
```

USER Data Class 
| ID         | type   | desc               |
| :--------- | :----- | :----------------- |
| member_id.id    | string | GAMEPOT会员ID  |
| username | string | 社交ID |

## 4. 插件
除了GAMEPOT基本功能外，还支持多种外部模块库的联动功能等。
可支持模块 
- 本人认证(Danal)
- 海外PG(exola)
- 国内PG(Danal)
- 区块链(正在准备)


### 本人身份认证

手机实名认证服务是指以用户名义使用手机通过认证程序确认用户的身份的功能。 （仅限韩国）

```javascript
 GP.Identity('[本人身份认证代码]',{},function(resp) {
  if(resp.success) {
    alert(resp.orderId); 
  } else {
    alert(resp.error);
  }
});
```


### 第三方支付

当使用外部PG如Exora或Danal时，显示结算窗口的功能。

```javascript
function Payment(key) {
    GP.Payment(key,
      {
        userId: "[USERID]",
        productId : "[ITEMID]",
        name: "[ITEMNAME]",
        buyer_name: "[买方名称]",
        buyer_email: "[买方EMAIL]",
    },function(resp) {
        if(resp.success) {
          alert(resp.orderId);
        } else {
          alert(resp.error);
        }
      })
  }
```

| Attribute | Description                                                                                                              |
| :---------------------- | :------------------------------------------------------------------------------------ |
| userId              | GAMEPOT会员ID |
| productId                 |  产品代码 |
| name | 道具名称 |
| buyer_name | 买方名称(option) |
| buyer_email         | 买方邮箱(option) |
| playerId  | 玩家ID(option) |
| serverId         | 服务器 ID(option) |
| userdata      | 用户数据(option) |
