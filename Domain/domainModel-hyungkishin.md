# Domain model
## 결제

## 추상화 도메인 다이어 그램
```mermaid
    flowchart LR
    PRODUCT(상품)
    CART(장바구니)
    ORDER(주문)
    PAY(결제)
    ORDER_API_IN(외부상품)
    RESERVATION(예약)
    SETTLEMENT(정산)
    PRODUCT --> CART
    CART --> ORDER -->|주문요청| ORDER_API_IN
    ORDER_API_IN --> PAY
    ORDER -->|주문요청| PAY --> RESERVATION
    RESERVATION --> SETTLEMENT
```
---
## 상세 도메인 다이어그램
```mermaid
    flowchart LR
    Product(상품)
    ProductDetail(상품상세)
    Cart(장바구니)
    Order(주문)
    OrderDetail(주문상세)
    Payment(결제)
    Card(카드결제)
    EasyPay(간편결제)
    Mileage(마일리지)
    VitualAccount(가상계좌)
    MainAccount(주 결제수단)
    Refund(환불)
    Coupon(쿠폰)
    EGiftCard(전자상품권)
    PGiftCard(지류상품권)
    Reservation(예약)
    Settlement(정산)
    MyPage(마이페이지)
    Product --> ProductDetail -->|옵션 선택| Cart
    Cart -->|주문 요청| Order
    Order --> Payment
    subgraph 결제 수단
        direction TB
        Payment --> MainAccount -->|카드결제| Card
        MainAccount -->|간편 결제| EasyPay
        MainAccount -->|계좌 이체| VitualAccount
    end
    subgraph 할인
        direction TB
        Payment --> DisCount(할인 수단) --> Coupon
    end
    subgraph 보조 결제수단
        direction TB
        Payment --> SubAccount(보조 결제수단) --> Mileage
        SubAccount(보조 결제수단) --> EGiftCard
        SubAccount(보조 결제수단) --> PGiftCard
    end
    Payment -->|예약 요청| Reservation -->|정산 승인요청| Settlement -->|예약확인| MyPage
    MyPage --> OrderDetail -->|환불 요청| Refund
```
