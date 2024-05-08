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
    User(고객)
    Seller(판매자)
    Product(상품)
    Notify(알림)
    ApiProduct(외부 상품)
    ProductDetail(상품상세)
    Cart(장바구니)
    Order(주문)
    OrderDetail(주문상세)
    Payment(결제)
    Card(카드결제)
    EasyPay(간편결제)
    Mileage(마일리지)
    VirtualAccount(가상계좌)
    MainAccount(주 결제수단)
    Coupon(쿠폰)
    Reservation(예약)
    PackagePlatForm(패키지 플랫폼)
    ReservationDetail(예약상세)
    Settlement(정산)
    subgraph 통신 판매업 중개 서비스 'FND'
        direction TB
        User --> ApiProduct
        User --> Product
        ApiProduct -->|상품 조회| ProductDetail
        Product -->|상품조회| ProductDetail -->|옵션 선택| Cart
        Cart -->|주문 요청| Order
        Order -->|주문 요청| OrderDetail
        Reservation
        ReservationDetail
        Seller
        Notify
    end
    OrderDetail -->|결제 요청| Payment
    subgraph 결제
        direction TB
        Payment --> MainAccount -->|카드결제| Card
        MainAccount -->|간편 결제| EasyPay
        MainAccount -->|계좌 이체| VirtualAccount
        Payment --> DisCount(할인 수단) --> Coupon
        Payment --> SubAccount(보조 결제수단) --> Mileage
    end
    subgraph 플랫폼
        direction TB
        Payment -->|예약생성 요청| PackagePlatForm
    end
    subgraph 정산
        direction TB
        Payment -->|정산 승인요청| Settlement
    end
    Payment -->|예약 요청| Reservation
    Reservation -->|예약 조회| ReservationDetail
    ReservationDetail -->|주문 취소 요청| Seller
    Seller -->|취소 승인| Notify
    Notify
```
