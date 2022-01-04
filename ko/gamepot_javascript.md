---
search:
  keyword:
    - gamepot
---

#### **네이버 클라우드 플랫폼의 상품 사용 방법을 보다 상세하게 제공하고, 다양한 API의 활용을 돕기 위해 <a href="https://guide.ncloud-docs.com/docs/ko/home" target="_blank">[설명서]</a>와 <a href="https://api.ncloud-docs.com/docs/ko/home" target="_blank">[API 참조서]</a>를 구분하여 제공하고 있습니다.**

<a href="https://api.ncloud-docs.com/docs/ko/game-gamepot" target="_blank">Gamepot API 참조서 바로가기 >></a><br />
<a href="https://guide.ncloud-docs.com/docs/game-gamepot-overview" target="_blank">Gamepot 설명서 바로가기 >></a>

# Javascript SDK

참고 URL : https://lx4fc.csb.app

소셜 로그인 관련 콘솔 내 설정 가이드 : [다운로드](https://xyuditqzezxs1008973.cdn.ntruss.com/patch/JavascriptSDK%E1%84%85%E1%85%A9%E1%84%80%E1%85%B3%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%87%E1%85%A1%E1%86%BC%E1%84%89%E1%85%B5%E1%86%A8%E1%84%89%E1%85%A1%E1%84%8B%E1%85%AD%E1%86%BC%E1%84%89%E1%85%B5%E1%84%8F%E1%85%A9%E1%86%AB%E1%84%89%E1%85%A9%E1%86%AF%E1%84%89%E1%85%A6%E1%86%BA%E1%84%90%E1%85%B5%E1%86%BC%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3.pdf)

사용 가능 로그인 : 구글 / 페이스북 / 애플 로그인

애플 로그인의 경우 게임팟 대시보드 > 프로젝트 설정 > 일반 > Apple ID Login 항목이 기입이 되어야 합니다.

로그인하는 도메인의 주소를 게임팟 대시보드 > 프로젝트 설정 > 일반 > WEB- 허용도메인에 정보가 기입되어야 합나다.


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

## 3. 로그인, 로그아웃

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
        // user.id == gamepot member_id
        // user.token == token
        // user.email == email
        user.id + ',' + user.token + ',' + user.email
    );
  }
});
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

