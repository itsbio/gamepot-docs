---
search:
  keyword:
    - gamepot
---

#### **We provide the <a href="https://guide.ncloud-docs.com/docs/en/home" target="_blank">[Manual]</a>and <a href="https://api.ncloud-docs.com/docs/en/home" target="_blank">[API Reference]</a>separately to offer more detailed information on how to use the NAVER CLOUD PLATFORM and help maximize the use of the API.**

<a href="https://api.ncloud-docs.com/docs/en/game-gamepot" target="_blank">Go to Gamepot API Reference >></a><br />
<a href="https://guide.ncloud-docs.com/docs/en/game-gamepot-overview" target="_blank">Go to Gamepot Manual >></a>

# Javascript SDK

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


> ### This is a machine-translated document that may have errors in vocabulary, syntax, or grammar. We will soon provide you with the document translated by a professional translator.
>
> #### If you have any questions, please [contact us](https://www.ncloud.com/support/question).
>
> We will make every effort to further enhance our services.

## 1. Getting Started

### Development Environment Configuration

The system environment for using GAMEPOT in a browser is as follows.

\[ system environment \]

-Minimum: `Chrome 4`, `IE 8`, `Firefox 3.5`, `Safari 4`, `Opera 10.50`, etc.

#### Add JavaScript

Add the downloaded Javascript SDK file within the `<header>` block or `<body>` block.

> You can use the function through the `GP` global variable\
> Be careful not to re-declare the same variable name after loading the gamepot script.

```html
<script src="/js/GamePot-2.1.0b.js"></script>
```

## 2. Initialization

In the `$(ducement).ready(function() {...})` block when using `window.onload = function() {...}` or jQuery so that it can be executed when the webpage is finished loading. Initialize from.

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


## 3. Login, logout, withdrawal from membership

You can integrate and use various login SDKs such as Google, Facebook, and email.

### Google\(API CONSOLE\) Console Settings

Create a project in [Google API Console](https://console.developers.google.com)> Create user authentication information> OAuth client ID> Create as web application type and use the client ID value.

> Example) 533847112608-qv8149tijkoh0vljrpeashk0udf39eoe.apps.googleusercontent.com

![gamepot_js_01](images/gamepot_js_01.png)

### Facebook console settings

Use the app ID after creating the app in [Facebook Developers](https://developers.facebook.com/apps)

> Example) 149235210820417

### login

The login UI is implemented by the developer and works when clicking the login button.

#### Social Platform Login

```javascript
// Login type definition
// GP.ChannelType.GOOGLE: Google
// GP.ChannelType.FACEBOOK: Facebook
// GP.ChannelType.EMAIL: Email

// Called when the Facebook login button is pressed
GP.login(GP.ChannelType.FACEBOOK, {
  onSuccess: function (userInfo) {
    console.log(
      // user.id == gamepot member_id
      // user.token == token
      // user.email == email

      'Login success.' +
        user.id + ',' + user.token + ',' + user.email
    );
  },
  onCancel: function () {
    console.log('Cancel Login');
  },
  onFailure: function (gamepotError) {
    console.log('Login failed: ' + gamepotError.toString());
  },
});
```

#### Email Login

```javascript
// Input from user in <input> tag, etc.
var email_id = $('#input-email-id').val();
var email_password = $('#input-email-password').val();

$('#email-result-status').html('');

GP.login(GP.ChannelType.EMAIL, email_id, email_password, {
  onSuccess: function (gamepotUserInfo) {
    console.log('Email login successful', gamepotUserInfo);
    $('#email-result-status').html(
      'Login success. memberid: ' +
        gameUserInfo.memberid +
        ', userid: ' +
        gameUserInfo.userid
    );
  },
  onCancel: function () {
    console.log('Cancel Email Login');
  },
  onFailure: function (gamepotError) {
    console.log('Email login failed: ' + gamepotError.toString());

    var msg = '';
    switch (gamepotError.getCode()) {
      case GP.Error.EMAIL_AUTH_WRONG_EMAIL_FORMAT:
        msg = 'The email format is incorrect.';
        break;
      case GP.Error.EMAIL_AUTH_WRONG_PASSWORD_EMPTY:
        msg = 'Please enter your password.';
        break;
      case GP.Error.EMAIL_AUTH_WRONG_PASSWORD_LENGTH:
        msg =
          'You can enter a minimum of 8 characters and a maximum of 32 characters.';
        break;
      case GP.Error.EMAIL_AUTH_WRONG_PASSWORD:
        msg = 'Passwords do not match.';
        break;
      case GP.Error.EMAIL_AUTH_WRONG_PASSWORD_BLOCKED:
        msg =
          'You were unable to log in because you exceeded the number of password errors.';
        break;
      case GP.Error.EMAIL_AUTH_NOT_FOUND:
        msg = 'The linked account does not exist.';
        break;
      default:
        msg = gamepotError.getMessage();
        break;
    }

    $('#email-result-status').html(msg); // Example of displaying results.
  },
});
```

#### Email Signup

```javascript
// Input from user in <input> tag, etc.
var new_email_id = $('#input-email-new-id').val();
var new_email_password = $('#input-email-new-password').val();

$('#email-result-status2').html('');

GP.Channel.emailRegister(new_email_id, new_email_password, {
  onSuccess: function (gamepotUserInfo) {
    console.log('Email sign-up successful', gamepotUserInfo);
  },
  onCancel: function () {
    console.log('Cancel email subscription');
  },
  onFailure: function (gamepotError) {
    console.log('Failed to sign up for email: ' + gamepotError.toString());

    var msg = '';
    switch (gamepotError.getCode()) {
      case GP.Error.EMAIL_AUTH_WRONG_EMAIL_FORMAT:
        msg = 'The email format is incorrect.';
        break;
      case GP.Error.EMAIL_AUTH_WRONG_PASSWORD_EMPTY:
        msg = 'Please enter your password.';
        break;
      case GP.Error.EMAIL_AUTH_WRONG_PASSWORD_LENGTH:
        msg =
          'You can enter a minimum of 8 characters and a maximum of 32 characters.';
        break;
      case GP.Error.EMAIL_AUTH_WRONG_PASSWORD:
        msg = 'Passwords do not match.';
        break;
      case GP.Error.EMAIL_AUTH_WRONG_PASSWORD_BLOCKED:
        msg =
          'You were unable to log in because you exceeded the number of password errors.';
        break;
      case GP.Error.EMAIL_AUTH_NOT_FOUND:
        msg = 'The linked account does not exist.';
        break;
      case GP.Error.EMAIL_AUTH_ALREADY_IN_USE:
        msg = 'This account is already in use.';
        break;
      default:
        msg = gamepotError.getMessage();
        break;
    }
    $('#email-result-status2').html(msg);
  },
});
```

#### Member Unique ID

```javascript
GP.getMemberId();
```

### Auto-Login

Automatic login can be implemented using an API that delivers the information the user was last logged in to.

```javascript
// API that delivers the information that the user last logged in to
var lastLoginType = GP.getLastLoginType();
if (lastLoginType !== GP.ChannelType.NONE) {
  console.log('Automatic login. lastLoginType: ' + lastLoginType);
  GP.login(lastLoginType, {
    onSuccess: function (gameUserInfo) {
      console.log(
        'Auto login-complete. memberid: ' +
          gameUserInfo.memberid +
          ', userid: ' +
          gameUserInfo.userid
      );
    },

    onCancel: function () {
      console.log('Automatic login-cancel');
    },

    onFailure: function (gamepotError) {
      console.log('Automatic login-failed: ' + gamepotError.toString());
    },

    onNeedUpdate: function (status) {
      console.log('Automatic login-update required: ' + status);
    },

    onMainternance: function (status) {
      console.log('Automatic login-checking: ' + status);
    },
  });
} else {
  // The first time the game was run or logged out. Show the user a login screen to log in.
}
```

### Log out

Log out of your current member account.

```javascript
GP.logout({
  onSuccess() {
    console.log('Logout complete.');
  },
  onFailure(gamepotError) {
    console.log(
      'Failed to log out. If you are not logged in or the session has already ended: ' +
        gamepotError.toString()
    );
  },
});
```

### Change Email Password

Change the password of the currently logged-in email account.

```javascript
GP.changeEmailPassword('my_old_password', 'my_new_password', {
  onSuccess: function () {
    // Password change complete. Please expose the text about the interlocking results. (Example: Account linkage has been canceled.)
  },
  onFailure: function (error) {
    // Email password change failed. Use error.getMessage() to show the error message.
  },
});
```

### Withdrawal

Withdraw your current member account.

```javascript
GP.deleteMember({
  onSuccess: function () {
    console.log(
      'Successful membership withdrawal. Please move to the initial screen.'
    );
  },
  onFailure: function (error) {
    // Member withdrawal failed. Use error.getMessage() to show the error message.
    console.log(error.getMessage());
  },
});
```

### Verification

After completing the login, if you pass the login information from the developer server to the GAMEPOT server, the login verification will proceed.

For more information, refer to the `Authentication check` item in the `Server to server api` menu.

## 4. Account linking

It is a function to connect/disconnect multiple social accounts\(Google, Facebook, etc.) to a single game account.\(There is only one social account linked at least.\)

> Implement the interlocking screen UI in the developer.

### Social Account Integration

You can link your account with IDs such as Google and Facebook.

```javascript
// Link to Google account
// GP.ChannelType.GOOGLE
// Link to Facebook account
// GP.ChannelType.FACEBOOK
// Link to email account
// GP.ChannelType.EMAIL

GP.createLinking(GP.ChannelType.GOOGLE, {
  onSuccess: function (userInfo) {
    // Integration completed. Please expose the text of the linking result (eg, account linking was successful).
  },

  onCancel: function () {
    // User canceled
  },

  onFailure: function (error) {
    // Integration failure. Use error.getMessage() to show the error message.
  },
});
```

### Email account linkage

You can additionally link to your account linked with your social account with your email ID.

```javascript
GP.createEmailLinking('some@example.com', 'some_my_password', {
  onSuccess: function (userInfo) {
    // Integration completed. Please expose the text of the linking result (eg, account linking was successful).
  },

  onFailure: function (error) {
    // Integration failure. Use error.getMessage() to show the error message.
  },
});
```

### Linked list

You can check whether the account is linked through the corresponding API.

```javascript
// type definition
// GP.ChannelType.GOOGLE
// GP.ChannelType.FACEBOOK
// GP.ChannelType.EMAIL
// Return the interlocking result according to the type.
var isLinked = GP.isLinked(GP.ChannelType.GOOGLE);

// Return as a json object for all linked types.
// If it is linked to GOOGLE and FACEBOOK, it will be returned as below.
// [{“provider”:”google”},{“provider”:”facebook”}]
var linking = GP.getLinkedList();
```

### Unlink

Cancel an existing linked account.

```javascript
GP.deleteLinking(GP.ChannelType.GOOGLE, {
  onSuccess: function () {
    // Interlocking complete. Please expose the text about the interlocking results. (Example: Account linkage has been canceled.)
  },
  onFailure: function (error) {
    // Interlock failure. Use error.getMessage() to show the error message.
  },
});
```
