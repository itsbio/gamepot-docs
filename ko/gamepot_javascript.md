---
search:
  keyword:
    - gamepot
---

#### **네이버 클라우드 플랫폼의 상품 사용 방법을 보다 상세하게 제공하고, 다양한 API의 활용을 돕기 위해 <a href="https://guide.ncloud-docs.com/docs/ko/home" target="_blank">[설명서]</a>와 <a href="https://api.ncloud-docs.com/docs/ko/home" target="_blank">[API 참조서]</a>를 구분하여 제공하고 있습니다.**

<a href="https://api.ncloud-docs.com/docs/game-gamepot-index" target="_blank">Gamepot API 참조서 바로가기 >></a><br />
<a href="https://guide.ncloud-docs.com/docs/game-gamepotconsole" target="_blank">Gamepot 설명서 바로가기 >></a>

# Javascript SDK

## 1. 시작하기

### 개발 환경 구성

브라우저에서 GAMEPOT을 사용하기 위한 시스템 환경은 다음과 같습니다.

\[ 시스템 환경 \]

- 최소사항: `크롬 4`, `IE 8`, `Firefox 3.5`, `Safari 4`, `Opera 10.50` 등

#### 자바스크립트 추가

다운로드한 Javascript SDK 파일을 `<header>`블록 또는 `<body>` 블록 내에 추가합니다.

> `GP` global variable을 통해 기능을 사용할 수 있습니다\
> 게임팟 스크립트 로드 후 동일한 변수명으로 재 선언되지 않도록 주의해주세요.

```html
<script src="https://cdn.gamepot.io/v1/release/gamepot-sdk.min.js"></script>
```

## 2. 초기화

웹페이지 로딩이 완료될 때 실행할 수 있도록 `window.onload = function() {...}` 또는 jQuery를 사용하는 경우 `$(ducement).ready(function() {...})` 블록 내에서 초기화합니다.

```html
<html>
  <head>
    <title>Gamepot Javscript</title>
  </head>
  <body>
    <!-- YOUR WEB HTML CODES -->
    <script>
      window.onload = function () {
        // 프로젝트 ID는 게임팟 대시보드에서 확인할 수 있습니다.
        var project_id = 'xxxxxxx-xxxx-xxxx-xxxx-xxxxxx';
        var gamepotConfig = {
          // 옵션
        };
        GP.initialize(project_id, gamepotConfig);
      };
    </script>
    <!-- YOUR WEB HTML CODES -->
  </body>
</html>
```

### 오류 처리

오류처리 방법은 모두 동일하며, function (user, error) { } 과 같이 error 가 있을 경우에는 메시지를 보여주고 에러가 없을 경우에는 성공으로 리턴한다.

```html
GP.login(GP.ChannelType.EMAIL, function (user, error) { if(error) { // 로그인
실패 alert(error); // 실패 메시지 } else { // 로그인 성공 alert(user); } });
```

## 3. 로그인, 로그아웃, 회원 탈퇴

구글, 페이스북, 네이버, 애플ID, 라인, 트위터, 이메일 등 다양한 로그인 SDK를 통합하여 사용할 수 있습니다. 대시보드 환경설정에서 설정해 주시기 바랍니다.

### 로그인

로그인 UI는 개발사에서 구현하고, 로그인 버튼 클릭 시에 연동합니다.

#### 소셜 플랫폼 로그인

```javascript
// 로그인 타입 정의
// GP.ChannelType.GOOGLE: 구글
// GP.ChannelType.FACEBOOK: 페이스북
// GP.ChannelType.APPLE: 애플ID
// GP.ChannelType.NAVER: 네이버

// 페이스북 로그인 버튼을 눌렀을 때 호출
GP.login(GP.ChannelType.FACEBOOK, function (user, error) {
  if (error) {
    alert(error); // 오류 메세지
  } else {
    // 정상 로그인 완료
    console.log(
      user.getMemberId() + ',' + user.getToken() + ',' + user.getEmail()
    );
  }
});
```

#### 이메일 로그인

```javascript
// <input>태그 등에서 사용자로 부터 입력
var email_id = $('#input-email-id').val();
var email_password = $('#input-email-password').val();

$('#email-result-status').html('');

GP.signin(
  GP.ChannelType.EMAIL,
  email_id,
  email_password,
  function (user, error) {
    if (error) {
      alert(error); // 오류 메세지
    } else {
      // 정상 로그인 완료
      console.log(
        user.getMemberId() + ',' + user.getToken() + ',' + user.getEmail()
      );
    }
  }
);
```

#### 이메일 가입

```javascript
// <input>태그 등에서 사용자로 부터 입력
var new_email_id = $('#input-email-new-id').val();
var new_email_password = $('#input-email-new-password').val();

GP.signup(
  GP.ChannelType.EMAIL,
  new_email_id,
  new_email_password,
  function (user, error) {
    if (error) {
      alert(error); // 오류 메세지
    } else {
      // 정상 가입 완료
      console.log(
        user.getMemberId() + ',' + user.getToken() + ',' + user.getEmail()
      );
    }
  }
);
```

#### 회원 정보 가져오기

```javascript
const user = GP.getUser();
console.log(user.getMemberId());
```

### 로그아웃

현재 회원 계정을 로그아웃합니다.

```javascript
GP.logout(function (user, error) {
  if (error) {
    // 로그아웃 실패
    alert(error); // 오류 메세지
  } else {
    // 로그아웃 아웃 완료
  }
});
```

### 이메일 비밀번호 변경

현재 입력된 이메일로 비밀번호로 변경 안내 메일이 발송 됩니다.

```javascript
GP.forgot('email', function (error) {
  if (error) {
    // 이메일 찾기 실패
    alert(error); // 오류 메세지
  } else {
    // 이메일 찾기 성공
    alert('메일 찾기 성공');
  }
});
```

### 회원 탈퇴

현재 회원 계정을 탈퇴시킵니다.

```javascript
GP.unsignup({
  onSuccess: function () {
    console.log('회원탈퇴 성공. 초기화면으로 이동해주세요.');
  },
  onFailure: function (error) {
    // 회원탈퇴 실패. error.getMessage()를 이용해서 오류 메시지를 보여주세요.
    console.log(error.getMessage());
  },
});
```

## 4. 계정 연동

하나의 게임 계정에 복수 개의 소셜 계정\(구글, 페이스북 등\)을 연결/해제할 수 있는 기능입니다.\(최소 연동 소셜 계정은 1가지입니다.\)

> 연동화면 UI는 개발사에서 구현해주세요.

### 소셜 계정 연동

Google, Facebook 등의 아이디로 계정을 연동할 수 있습니다.

```javascript
// 구글 계정에 연동
// GP.ChannelType.GOOGLE
// 페이스북 계정에 연동
// GP.ChannelType.FACEBOOK
// 이메일 계정에 연동
// GP.ChannelType.EMAIL

GP.createLinking(GP.ChannelType.GOOGLE, {
  onSuccess: function (userInfo) {
    // 연동 완료. 연동 결과에 대한 문구를 노출시켜 주세요.(예: 계정 연동에 성공했습니다.)
  },

  onCancel: function () {
    // 사용자가 취소한 경우
  },

  onFailure: function (error) {
    // 연동 실패. error.getMessage()를 이용해서 오류 메시지를 보여주세요.
  },
});
```

### 이메일 계정 연동

소셜계정으로 연동된 계정에 이메일 아이디로 추가 연동할 수 있습니다.

```javascript
GP.createEmailLinking('some@example.com', 'some_my_password', {
  onSuccess: function (userInfo) {
    // 연동 완료. 연동 결과에 대한 문구를 노출시켜 주세요.(예: 계정 연동에 성공했습니다.)
  },

  onFailure: function (error) {
    // 연동 실패. error.getMessage()를 이용해서 오류 메시지를 보여주세요.
  },
});
```

### 연동된 리스트

해당 API를 통해 계정에 대해 연동 여부를 확인하실 수 있습니다.

```javascript
// 타입 정의
// GP.ChannelType.GOOGLE
// GP.ChannelType.FACEBOOK
// GP.ChannelType.EMAIL
// 타입에 따른 연동 결과를 반환합니다.
var isLinked = GP.isLinked(GP.ChannelType.GOOGLE);

// 연동되어 있는 모든 타입에 대해 json object로 반환합니다.
// 만약 GOOGLE과 FACEBOOK에 연동된 경우 아래와 같이 반환됩니다.
// [{“provider”:”google”},{“provider”:”facebook”}]
var linking = GP.getLinkedList();
```

### 연동 해제

기존에 연동되어 있는 계정을 해제합니다.

```javascript
GP.deleteLinking(GP.ChannelType.GOOGLE, {
  onSuccess: function () {
    // 연동 해제 완료. 연동 결과에 대한 문구를 노출시켜 주세요. (예: 계정 연동을 해지했습니다.)
  },
  onFailure: function (error) {
    // 연동 해제 실패. error.getMessage()를 이용해서 오류 메시지를 보여주세요.
  },
});
```
