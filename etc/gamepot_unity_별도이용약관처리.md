## 이메일 인증 처리 / 확인 / 게임팟에 인증 이메일 정보 기입 

네이버 클라우드 Cloud Outbound Mailer 서비스 신청이 진행이 되어 있어야 하며 

고객지원 > 설정 > GDPR > 이메일 인증 항목에 인증 메일을 보낼때의 내용이 기입되어 있어야 합니다.

### 인증 이메일 발송

인증 이메일을 발송합니다.


- Case 1

Request:

```csharp
GamePot.sendAgreeEmail("수신자 이메일 주소");
```

Response:

```csharp
// 인증 이메일 발송 성동
public void onSendAgreeEmailSuccess(NAgreeSendEmailInfo resultInfo)
{
    // resultInfo.key  발송한 인증 이메일의 고유 키 - 인증 확인시 사용
}

public void onSendAgreeEmailFailure(NError error)
{
    // error : 오류 코드 및 메시지 정보
    //error.message 오류 메시지 정보를 표기 해주세요. 
}
```

- Case 2

Request:

```csharp
GamePot.sendAgreeEmail("수신자 이메일 주소", GamePotCallbackDelegate.CB_SendAgreeEmail);
```

```csharp
GamePot.sendAgreeEmail("수신자 이메일 주소", (success, sendEmailInfo ,error) => {

    string result = "result : ";

    if (success)
    {
        // 인증 메일 발신 성공
        //sendEmailInfo.key : 이메일 인증 키 

    }

    if (error != null)
    {
        // 인증 메일 발신 살패
        // error.ToJson();
    }

});
```

### 이메일 인증 승인 여부 확인

이메일 인증 발송 다시 발급된 키와 메일 정보를 이용하여 승인여부 확인

- Case 1

Request:

```csharp
GamePot.checkAgreeEmail("수신자 이메일 주소","이메일 인증 키");
```

Response:

```csharp
/// 이메일 인증 완료 성공
public void onCheckAgreeEmailSuccess(NAgreeCheckEmailInfo resultInfo)
{
    // 이메일 인증이 완료된 상태로 판단
}
/// 이메일 인증 미 완료 상태
public void onCheckAgreeEmailFailure(NError error)
{
    // error : 오류 코드 및 메시지 정보
    //error.message 오류 메시지 정보를 표기 해주세요.
}
```

- Case 2

Request:

```csharp
GamePot.checkAgreeEmail("수신자 이메일 주소","이메일 인증 키", GamePotCallbackDelegate.CB_CheckAgreeEmail);
```

```csharp
GamePot.checkAgreeEmail("수신자 이메일 주소","이메일 인증 키", (success,  checkEmailInfo, error) => {
   

    if (success)
    {
        // 이메일 인증이 완료된 상태로 판단
    }

    if (error != null)
    {
        // 이메일 미 인증 상태
        // error : 오류 코드 및 메시지 정보
        //error.message 오류 메시지 정보를 표기 해주세요.
    }


});
```

### 이메일 인증을 진행한 이메일 정보 셋팅

이메일 인증을 진행한 이메일 정보, GDPR 약관 설정 항목만 설정 가능.

( 푸시 설정은 기존의 약관 UI처럼 방식 처럼 로그인 성공 이후 별도의 방식으로 푸시 상태 설정 필요 )

- Case 1

Request:

```csharp
NAgreeResultInfo info = new NAgreeResultInfo();
info.emailVerified = "이메일인증 계정"; // 인증을 진행한 이메일 정보


info.agreeGDPRStatus = 4; // 3: 나이가 XX 이상 / 4: 나이가 XX 미만 
List<string> agreeGDPRlist = new List<string>() {"gdpr_term","gdpr_privacy","gdpr_push_normal"};
string sAgreeGDPRlist = String.Join(", ", agreeGDPRlist.ToArray());
info.agreeGDPR = sAgreeGDPRlist;

GamePot.setAgreeInfo(info);
```

Response:

```csharp
// 설정 성공
public void onSetAgreeInfoSuccess()
{
    // 설정 성공
}

//설정 실패
public void onSetAgreeInfoFailure(NError error)
{
    // error : 오류 코드 및 메시지 정보
    //error.message 오류 메시지 정보를 표기 해주세요.
}
```

- Case 2

Request:

```csharp
GamePot.setAgreeInfo(info,GamePotCallbackDelegate.CB_SetAgreeInfo);
```

```csharp
GamePot.setAgreeInfo(info, (success, error) => {

    string result = "result : ";

    if (success)
    {
        //설정 성공
    }

    if (error != null)
    {
        // 설정 실패
        // error : 오류 코드 및 메시지 정보
        //error.message 오류 메시지 정보를 표기 해주세요.
    }

});
```