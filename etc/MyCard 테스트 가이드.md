# MyCard 테스트

마이카드 와 연동하기 위한 FacServiceID /  KEY  값은 마이카드 측을 통해 확인 후 대시보드에 설정 해주세요.

 

1. 대시보드 >> 결제 >> IAP의 Google 항목의 상품에 아래와 같이 가격이 추가 되어 있는지 확인 합니다. 

   ![MyCard001](/Users/jyj1127/Desktop/git_source/gamepot-docs/etc/image/MyCard001.png)

2. 대시보드 >> 프로젝트 설정 >> 외부결제 항목에 MyCard를 추가하고 해당 FacService ID / Sign Key 가 정상적으로 입력되어 있는지 확인해주세요.

3. 대시보드 >> 프로젝트 설정 >> 화이트 유저 에 테스트 하려는 Device의 IP를 개발과 결제/쿠폰 항목으로 2개 등록 해주세요.

4. 테스트 하려는 Device에서 결제를 시도 하시면 아래와 같은 화면이 노출 됩니다. 해당 부분에서 표기한 Phone Billing을 선택해주세요.

5. 결제는 SDK의 아래 코드를 호출 합니다. 

   Unity : GamePot.purchase(string productId);

   Android : GamePot.getInstance().purchase("product id");

   iOS : [[GamePot getInstance] purchase:productid];

   * MyCard 사용 중 결제 아이템 호출 형태는 기존 GamePot.getPurchaseItems(); 호출 시 에러발생 됩니다. 
     이를 대체하여 GamePot.getPurchaseThirdPaymentsItems();을 호출 해주세요.

![MyCard002](/Users/jyj1127/Desktop/git_source/gamepot-docs/etc/image/MyCard002.png)

5. 아래 부분에 전화번호 입력하고 체크박스 활성화 후 다음을 선택합니다. 

   ![MyCard003](/Users/jyj1127/Desktop/git_source/gamepot-docs/etc/image/MyCard003.png)

   ![MyCard004](/Users/jyj1127/Desktop/git_source/gamepot-docs/etc/image/MyCard004.png)

6. 아래와 같은 화면에서 sw로 시작하는 값을 복사하여 붙여넣기 후 버튼을 누릅니다. 

   ![MyCard005](/Users/jyj1127/Desktop/git_source/gamepot-docs/etc/image/MyCard005.png)

7. 결제 완료

   ![MyCard006](/Users/jyj1127/Desktop/git_source/gamepot-docs/etc/image/MyCard006.png)



- SDK 설정 [참고]

  - /Assets/Plugins/Android/libs 폴더 내에 gamepot-billing-mycard.aar 이 포함 되어 있는지 확인 합니다. 

  - /Assets/Plugins/Android/AndroidManifest.xml 파일에 <application> 레벨에 name을 제거 합니다.

    ![MyCard007](/Users/jyj1127/Desktop/git_source/gamepot-docs/etc/image/MyCard007.png)

    Mycard 외에 다른 버전 빌드 시엔 위 항목이 있어야 합니다.

  - /Assets/Plugins/Android/mainTemplate.gradle 파일에 아래와 같이 설정 합니다.
  
  ``` java
  resValue "string", "gamepot_store", "google"
  resValue "string", "gamepot_payment", "mycard" // 스토어가 google인 경우만 동작합니다.
  ```
  
  

