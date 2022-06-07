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


JavaScript SDK를 사용하기 위한 기본 설정 방법은 다음과 같습니다. 
1. [gamepot-sdk-javascript-lastest.min.js](https://gamepot.gcdn.ntruss.com/gamepot-sdk-javascript-lastest.min.js)을 다운로드해 주십시오. 
2. 다운받은 파일을 gamepot-sdk-javascript-lastest.min.js를 head와 head 사이에 추가해 주십시오. 
    ```javascript
    <head><script src="gamepot-sdk-javascript-lastest.min.js"></script></head>
    // 혹은 CDN 링크를 바로 사용하셔도 됩니다. (추천)    
     <head><script src="https://gamepot.gcdn.ntruss.com/gamepot-sdk-javascript-lastest.min.js"></script></head>
    ```

GamePot  Javascript SDK 는 npm 패키지로 제공되며 yarn 을 통해서도 사용할 수 있습니다.
```javascript
# using npm
npm install gamepot

# using yarn
yarn add gamepot
```


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
<script src="https://cdn.gamepot.io/release/gamepot-sdk-javascript-lastest.min.js"></script>
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
          // 공통
          api_url: "https://gpapps.gamepot.ntruss.com",
          api_key: "XXXXXXXXXXXXX",
          // Google 로그인을 사용하는 경우 아래와 같이 Google API 클라이언트 ID를 입력합니다.
          google_signin_client_id:"XXXXXXXXXX-XXXXXXXXXXX.apps.googleusercontent.com",
          // 페이스북 로그인을 사용하는 경우 아래와 같이 Facebook 앱 ID를 입력합니다.
          facebook_app_id: "XXXXXXXXXX",
          // 애플 로그인을 사용하는 경우 아래와 같이 애플 콘솔의 Services ID 및 로그인을 시도하는 도메인 주소를 입력합니다.(미사용시 빈값으로 설정)
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
| project_id              | 게임팟 대시보드 프로젝트 아이디 |
| api_url                 | 게임팟 대시보드에 연관된 URL (기본적으로 https://gpapps.gamepot.ntruss.com 이나  매니지드 상품 고객의 경우 해당 주소가 다르기 때문에 게임팟에 문의 필요 ) |
| api_key | GamePot에서 발급하는 인증 키( 대시보드 > 프로젝트 설정 > API Key) |
| google_signin_client_id | 구글 콘솔 내 웹 애플리케이션 아이디 |
| facebook_app_id         | 페이스북 앱 아이디 |
| apple_client_id         | 애플 콘솔에 생성한 Services ID |
| apple_redirect_uri      | 로그인 시도하는 도메인 주소 |

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


// 페이스북 로그인 버튼을 눌렀을 때 호출
GP.login(GP.ChannelType.FACEBOOK, function (user, error) {
  if (error) {
    alert(error); // 오류 메세지
    return;
  }
    // 로그인 완료
    alert(user);
});
```

USER Data Class 
| ID         | type   | desc               |
| :--------- | :----- | :----------------- |
| id | string | 회원 아이디      |
| token    | string | 로그인 토큰(JWT)  |
| nickname | string | 닉네임 |
| provider | string | 소셜 로그인 종류 |
| providerId | string | 소셜 로그인 ID |
| verify | string | 인증여부 |
| agree | string | 약관 동의 여부 |

### 로그아웃

현재 회원 계정을 로그아웃합니다.

```javascript
GP.logout(function (result, error) {
  if (error) {
    // 로그아웃 실패
    alert(error); // 오류 메세지
  } else {
    // 로그아웃 아웃 완료
  }
});
```
### 소셜 계정으로 회원 여부 확인
로그인을 한 후에 해당 소셜 계정으로 게임팟내 회원 중에 연동되어 있는지를 확인 합니다. 
```javascript
GP.linkingByUser(channeltype, function( user, error) {
    if(error) {
        alert(`${error.code}-${error.message}`); // 오류 메세지
        return false;
    }
    if(user == null)
        alert('계정 미존재')
   else if(user.member_id.id)
        alert(user.member_id.id);       // 아이디 리턴
});
```

USER Data Class 
| ID         | type   | desc               |
| :--------- | :----- | :----------------- |
| member_id.id    | string | 게임팟 회원 아이디  |
| username | string | 소셜 아이디 |

## 4. 플러그인
게임팟 기본 기능 이외에 다양한 외부 모듈고의 연동 기능 등을 지원합니다.
지원 가능 모듈 
- 본인 인증(다날)
- 해외 PG(엑솔라)
- 국내 PG(다날)
- 블록체인(준비 중)


### 본인 확인
휴대폰 본인인증 서비스란 본인 명의로 휴대폰을 이용하여 인증 절차를 거쳐 본인 여부와 확인하는 기능입니다. (한국만 가능)
```javascript
 GP.Identity('[본인 확인 코드]',{},function(resp) {
  if(resp.success) {
    alert(resp.orderId); 
  } else {
    alert(resp.error);
  }
});
```
### 외부 결제
엑솔라 혹은 다날과 같은 외부PG 를 사용할때 결제창을 보여주는 함수입니다.

```javascript
function Payment(key) {
    GP.Payment(key,
      {
        userId: "[USERID]",
        productId : "[ITEMID]",
        name: "[ITEMNAME]",
        buyer_name: "[구매자명]",
        buyer_email: "[구매자EMAIL]",
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
| userId              | 게임팟 회원 아이디 |
| productId                 |  상품 코드 |
| name | 아이템명 |
| buyer_name | 구매자명 (option) |
| buyer_email         | 구매자 이메일 (option) |
| playerId  | 플레이어 ID (option) |
| serverId         | 서버 ID (option) |
| userdata      | 사용자 데이터 (option) |

