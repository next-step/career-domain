# Domain model
## 상세 도메인 다이어 그램
```mermaid
flowchart LR
    MobileGame(모바일 게임앱)
    Account(회원)
    Facebook(페이스북)
    Google(구글)
    GameCenter(게임센터)
    Guest(게스트)
    Payment(결제)
    Store(스토어)
    InAppPayment(인앱결제)
    Product(상품)
    Consumable(소모성제품)
    NonConsumable(비소모성제품)
    AutoRenewableSubscription(자동 갱신 구독)
    NonRenewableSubscription(비갱신형 구독)
    Receipt(영수증)
    Effectuate(정상 지급)
    Refund(환불 취소)
    CustomerServiceCenter(고객센터)
    Inquiry(문의)
    InquiryType(문의 종류)
    GameInquiry(게임 관련 문의)
    PaymentInquiry(결제 관련 문의)
    Push(푸시)
    Send(발송)
    ReservedSend(예약발송)
    NowSend(즉시발송)
    PushType(푸시 종류)
    Topic(구독)
    Token(토큰)
    Target(타겟)
    Direct(다이렉트)
    MobileGame--->|회원가입하기|Account
    subgraph 회원종류
        Account-->Facebook
        Account-->Google
        Account-->GameCenter
        Account-->Guest
    end
    
    Account --->|회원이 게임관련 문의|CustomerServiceCenter
    CustomerServiceCenter --->Inquiry
    Inquiry--->InquiryType
    InquiryType--->GameInquiry
    InquiryType--->PaymentInquiry
    PaymentInquiry --->Payment
    
    Account --->Payment
    Account(사용자) --> |구매 요청| MobileGame
    MobileGame --> |결제 정보 전달| Store(스토어)
    Store --> |결제 인증 및 처리| MobileGame
    MobileGame --> |구매 완료 메시지 표시| Account
    Store --> |영수증 발행| Receipt(영수증)
    Receipt --> |영수증 검증 완료| GameServer(게임 서버)
    GameServer --> |아이템 제공| Account
    Account --> |환불 요청| MobileGame
    MobileGame --> |환불 요청 전달| Store
    Store --> |환불 승인 및 처리| MobileGame
    MobileGame --> |환불 완료 알림| Account

    Payment --> Store
    subgraph 스토어 종류
    Apple(애플)
    google(구글)
    oneStore(원스토어)
    Store --->Apple
    Store --->google
    Store --->oneStore
    end
    Store --> InAppPayment
    InAppPayment --> Product
    subgraph 인앱결제 상품 종류
    Product --> Consumable
    Product --> NonConsumable
    Product --> AutoRenewableSubscription
    Product --> NonRenewableSubscription
    end
    InAppPayment --> Receipt
    Receipt --> Effectuate
    Receipt --> Refund
    
    MobileGame--->Push
    Push --->|발송종류|Send
    Send --->ReservedSend
    Send --->NowSend
    Push --->|푸시 종류|PushType
    PushType --->Topic
    PushType --->Token
    Token --->|타겟 신규회원,휴면회원 등 으로 푸시 전송|Target
    Token --->|직접 푸시 전송|Direct

```
## 추상화 도메인 다이어그램
```mermaid
    flowchart LR
    MobileGame(모바일 게임앱)
    Account(회원)
    Payment(결제)
    Refund(환불 취소)
    Store(스토어)
    Product(상품)
    Receipt(영수증)
    CustomerServiceCenter(고객센터)
    Push(푸시)
    GameServer(게임서버)

    MobileGame --> Account
    Account -->|결제요청| Payment
    Account -->|환불 요청| Refund
    Payment --> |인앱결제|Store
    Refund --> |환불 요청|Store
    Store --> Product
    Store --> |영수증 발급|Receipt
    Store --> |영수증 취소|Receipt
    Receipt --> |영수증 검증완료|GameServer
    GameServer --->|아이템지급|Account
    GameServer --->|아이템철회|Account
    Account --> |게임관련 문의|CustomerServiceCenter
    MobileGame --> |푸시 전송|Push
```
