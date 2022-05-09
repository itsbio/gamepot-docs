---
search:
  keyword:
    - gamepot
---

#### **为提供 NAVER CLOUD PLATFORM 产品的详细使用方法和 API 的多种使用方式，分别提供<a href="https://guide.ncloud-docs.com/docs/zh/home" target="_blank">[说明书]</a>和<a href="https://api.ncloud-docs.com/docs/zh/home" target="_blank">[API 参考指南]</a>以供参考。**

<a href="https://api.ncloud-docs.com/docs/zh/game-gamepot" target="_blank">进入 Gamepot API 参考指南 >></a><br />
<a href="https://guide.ncloud-docs.com/docs/zh/game-gamepot-overview" target="_blank">进入 Gamepot 说明书 >></a>

# Javascript SDK

## 1. 开始

### 开发环境配置

在浏览器中使用 GAMEPOT 时所需系统环境如下。

\[系统环境\]

- 最低配置：`Chrome 4`、`IE 8`、`Firefox 3.5`、`Safari 4`、`Opera 10.50`等

#### 添加 JAVA 脚本

Reference URL : https://lx4fc.csb.app

The basic setup method for using the JavaScript SDK is as follows.
1. Download [gamepot-sdk-javascript-lastest.min.js](https://cdn.gamepot.io/release/gamepot-sdk-javascript-lastest.min.js) please give it to me.
2. Add the downloaded file gamepot-sdk-javascript-lastest.min.js between the head and the head.
     ```javascript
     <head><script src="gamepot-sdk-javascript-latest.min.js"></script></head>
     ```

The GamePot Javascript SDK is provided as an npm package and is also available through yarn .
```javascript
# using npm
npm install gamepot

# using yarn
yarn add gamepot
```


在`<header>`块或`<body>`块中添加已下载的 Javascript SDK 文件。

> 可通过`GP`全局变量使用功能\
> 加载 GAMEPOT 脚本后，请注意不要用相同的变量名再次声明。

```html
<script src="/js/GamePot-2.1.0b.js"></script>
```

## 2. 初始化

使用`window.onload = function() {...}`或 jQuery 时，在`$(ducement).ready(function() {...})`代码块内初始化，以便网页加载完成时可以运行。

```html
<html>
  <head>
    <title>Gamepot Javscript</title>
  </head>
  <body>
    <!-- YOUR WEB HTML CODES -->
    <script>
      window.onload = function () {
        // Your project ID can be found on your GAMEPOT Dashboard.
        var project_id = 'xxxxxxx-xxxx-xxxx-xxxx-xxxxxx';
        var gamepotConfig = {
          // common
          api_url: "https://gpapps.gamepot.ntruss.com",
          api_key: "XXXXXXXXXXXXX",
          // If you are using Google Sign-In, enter your Google API Client ID as shown below.
          google_signin_client_id:"XXXXXXXXXX-XXXXXXXXXXX.apps.googleusercontent.com",
          // If you are using Facebook login, enter your Facebook App ID as shown below.
          facebook_app_id: "XXXXXXXXXX",
          // If you are using Apple Login, enter the Services ID of the Apple Console and the domain address you are trying to log in to as shown below.(Set as empty value when not in use)
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
| :---------------------- | :----------------------------------------------------------------------------------------------------------------------- |
| project_id              | GAMEPOT Dashboard Project ID|
| api_url                 | The URL associated with the Gamepot dashboard (by default, https://gpapps.gamepot.ntruss.com, but for managed product customers, the address is different, so you need to contact Gamepot)|
| api_key | Authentication key issued by GamePot ( Dashboard > Project Settings > API Key) |
| google_signin_client_id | Web Application ID in Google Console |
| facebook_app_id         | facebook app id |
| apple_client_id         | Services ID created in Apple console |
| apple_redirect_uri      | The domain address you are trying to log in to.|


## 3. 登录、退出登录、注销会员

可以综合使用 Google、Facebook、邮箱等各种登录 SDK。

### Google\(API CONSOLE\)控制台设置

按照在[Google API Console](https://console.developers.google.com)中创建项目 > 创建用户认证信息 > OAuth 客户端 ID > Web 应用程序类型的顺序创建后使用客户端 ID 值。

> 示例）533847112608-qv8149tijkoh0vljrpeashk0udf39eoe.apps.googleusercontent.com

![gamepot_js_01](images/gamepot_js_01.png)

### Facebook 控制台设置

在[Facebook Developers](https://developers.facebook.com/apps)中创建应用后使用应用 ID

> 示例）149235210820417

### 登录

登录 UI 由开发公司实现，点击登录按钮时进行关联。

#### 社交平台登录

```javascript
// 定义登录类型
// GP.ChannelType.GOOGLE: Google
// GP.ChannelType.FACEBOOK: Facebook
// GP.ChannelType.EMAIL: 邮箱

// 点击Facebook登录按钮时调用
GP.login(GP.ChannelType.FACEBOOK, {
  onSuccess: function (userInfo) {
    console.log(
      '登录成功.memberid: ' + userInfo.memberid + ',userid: ' + userInfo.userid
    );
  },
  onCancel: function () {
    console.log('取消登录');
  },
  onFailure: function (gamepotError) {
    console.log('登录失败: ' + gamepotError.toString());
  },
});
```

#### 邮箱登录

```javascript
// <input>标签等中由用户输入
var email_id = $('#input-email-id').val();
var email_password = $('#input-email-password').val();

$('#email-result-status').html('');

GP.login(GP.ChannelType.EMAIL, email_id, email_password, {
  onSuccess: function (gamepotUserInfo) {
    console.log('邮箱登录成功', gamepotUserInfo);
    $('#email-result-status').html(
      '登录成功.memberid: ' +
        gameUserInfo.memberid +
        ',userid: ' +
        gameUserInfo.userid
    );
  },
  onCancel: function () {
    console.log('取消邮箱登录');
  },
  onFailure: function (gamepotError) {
    console.log('邮箱登录失败: ' + gamepotError.toString());

    var msg = '';
    switch (gamepotError.getCode()) {
      case GP.Error.EMAIL_AUTH_WRONG_EMAIL_FORMAT:
        msg = '邮箱格式不正确。';
        break;
      case GP.Error.EMAIL_AUTH_WRONG_PASSWORD_EMPTY:
        msg = '请输入密码。';
        break;
      case GP.Error.EMAIL_AUTH_WRONG_PASSWORD_LENGTH:
        msg = '密码可输入最少8个字符、最多32个字符。';
        break;
      case GP.Error.EMAIL_AUTH_WRONG_PASSWORD:
        msg = '密码不一致。';
        break;
      case GP.Error.EMAIL_AUTH_WRONG_PASSWORD_BLOCKED:
        msg = '超出密码错误次数上限，无法登录。';
        break;
      case GP.Error.EMAIL_AUTH_NOT_FOUND:
        msg = '连接账户不存在。';
        break;
      default:
        msg = gamepotError.getMessage();
        break;
    }

    $('#email-result-status').html(msg); // 结果显示示例。
  },
});
```

#### 邮箱注册

```javascript
// <input>标签等中由用户输入
var new_email_id = $('#input-email-new-id').val();
var new_email_password = $('#input-email-new-password').val();

$('#email-result-status2').html('');

GP.Channel.emailRegister(new_email_id, new_email_password, {
  onSuccess: function (gamepotUserInfo) {
    console.log('邮箱注册成功', gamepotUserInfo);
  },
  onCancel: function () {
    console.log('取消邮箱注册');
  },
  onFailure: function (gamepotError) {
    console.log('邮箱注册失败: ' + gamepotError.toString());

    var msg = '';
    switch (gamepotError.getCode()) {
      case GP.Error.EMAIL_AUTH_WRONG_EMAIL_FORMAT:
        msg = '邮箱格式不正确。';
        break;
      case GP.Error.EMAIL_AUTH_WRONG_PASSWORD_EMPTY:
        msg = '请输入密码。';
        break;
      case GP.Error.EMAIL_AUTH_WRONG_PASSWORD_LENGTH:
        msg = '密码可输入最少8个字符、最多32个字符。';
        break;
      case GP.Error.EMAIL_AUTH_WRONG_PASSWORD:
        msg = '密码不一致。';
        break;
      case GP.Error.EMAIL_AUTH_WRONG_PASSWORD_BLOCKED:
        msg = '超出密码错误次数上限，无法登录。';
        break;
      case GP.Error.EMAIL_AUTH_NOT_FOUND:
        msg = '连接账户不存在。';
        break;
      case GP.Error.EMAIL_AUTH_ALREADY_IN_USE:
        msg = '该账户已存在。';
        break;
      default:
        msg = gamepotError.getMessage();
        break;
    }
    $('#email-result-status2').html(msg);
  },
});
```

#### 会员固有 ID

```javascript
GP.getMemberId();
```

### 自动登录

通过传递用户最后登录信息的 API，可以实现自动登录。

```javascript
// 传递用户最后登录信息的API
var lastLoginType = GP.getLastLoginType();
if (lastLoginType !== GP.ChannelType.NONE) {
  console.log('自动登录.lastLoginType: ' + lastLoginType);
  GP.login(lastLoginType, {
    onSuccess: function (gameUserInfo) {
      console.log(
        // user.id == gamepot member_id
        // user.token == token
        // user.email == email
        '自动登录 - 成功.' + user.id + ',' + user.token + ',' + user.email
      );
    },

    onCancel: function () {
      console.log('自动登录 - 取消');
    },

    onFailure: function (gamepotError) {
      console.log('自动登录 - 失败: ' + gamepotError.toString());
    },

    onNeedUpdate: function (status) {
      console.log('自动登录 - 需要更新: ' + status);
    },

    onMainternance: function (status) {
      console.log('自动登录 - 检查中: ' + status);
    },
  });
} else {
  // 第一次运行游戏或退出登录的状态。请向用户显示可以登录的登录界面。
}
```

### 退出登录

退出当前登录的会员账户。

```javascript
GP.logout({
  onSuccess() {
    console.log('成功退出登录。');
  },
  onFailure(gamepotError) {
    console.log(
      '退出登录失败。并非已登录状态或会话已结束的情况: ' +
        gamepotError.toString()
    );
  },
});
```

### 修改邮箱密码

修改当前已登录邮箱账户的密码。

```javascript
GP.changeEmailPassword('my_old_password', 'my_new_password', {
  onSuccess: function () {
    // 密码修改成功。请显示关联结果相关语句。（例如：已解除账户关联。）
  },
  onFailure: function (error) {
    // 邮箱密码修改失败，请通过error.getMessage()显示错误消息。
  },
});
```

### 注销会员

注销当前登录的会员账户。

```javascript
GP.deleteMember({
  onSuccess: function () {
    console.log('会员注销成功，请转到初始页面。 ');
  },
  onFailure: function (error) {
    // 会员注销失败，请通过error.getMessage()显示错误消息。
    console.log(error.getMessage());
  },
});
```

### 验证

登录成功后，登录信息从开发公司服务器传递至 GAMEPOT 服务器后，开始进行登录验证。

详细说明请参考`Server to server api`菜单中的`Authentication check`项目。

## 4. 账户关联

可以将多个社交账户\(Google、Facebook 等\)与同一个游戏账户关联或解除关联的功能。\(至少关联一个社交账户。\)

> 关联页面 UI 由开发公司实现。

### 社交账户关联

可用 Google、Facebook 等 ID 关联账户。

```javascript
// 关联Google账户
// GP.ChannelType.GOOGLE
// 关联Facebook账户
// GP.ChannelType.FACEBOOK
// 关联到邮箱账户
// GP.ChannelType.EMAIL

GP.createLinking(GP.ChannelType.GOOGLE, {
  onSuccess: function (userInfo) {
    // 关联成功，请显示关联结果相关语句。（例如：账户关联成功。）
  },

  onCancel: function () {
    // 用户取消时
  },

  onFailure: function (error) {
    // 关联失败，请通过error.getMessage()显示错误消息。
  },
});
```

### 关联邮箱账户

可以为已关联社交账户的账户追加关联邮箱 ID。

```javascript
GP.createEmailLinking('some@example.com', 'some_my_password', {
  onSuccess: function (userInfo) {
    // 关联成功，请显示关联结果相关语句。（例如：账户关联成功。）
  },

  onFailure: function (error) {
    // 关联失败，请通过error.getMessage()显示错误消息。
  },
});
```

### 已关联列表

可以通过该 API 确认账户是否已关联。

```javascript
// 定义类型
// GP.ChannelType.GOOGLE
// GP.ChannelType.FACEBOOK
// GP.ChannelType.EMAIL
// 返回各类型的关联结果。
var isLinked = GP.isLinked(GP.ChannelType.GOOGLE);

// 对已关联的所有类型，以json object格式返回。
// 与GOOGLE和FACEBOOK关联时，将按照以下方式返回。
// [{“provider”:”google”},{“provider”:”facebook”}]
var linking = GP.getLinkedList();
```

### 解除关联

解除当前关联账户。

```javascript
GP.deleteLinking(GP.ChannelType.GOOGLE, {
  onSuccess: function () {
    // 成功解除关联，请显示关联结果相关语句。（例如：已解除账户关联。）
  },
  onFailure: function (error) {
    // 解除关联失败，请通过error.getMessage()显示错误消息。
  },
});
```
