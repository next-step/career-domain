# Domain model
## 상세 도메인 다이어 그램
```mermaid
flowchart LR
        Cart(장바구니)
        OrderSheet(주문서)
        Order(주문)
        DeliveryAddress(배송지)
        OrderDetail(주문상세)
        Payment(결제)
        PaymentMethod(결제수단)
        FundingSource(원결제)
        Card(카드결제)
        Bank(계좌이체)
        VitualAccount(가상계좌)
        Phone(휴대폰결제)
        EasyPay(간편결제)
        Point(포인트)
        Coupon(쿠폰)
        Cancel(취소)
        Refund(환불)
        Propotentional(안분)
        Cart-->|주문하기|OrderSheet
        OrderSheet---|주문상태|Order
        Order---|주문상세|OrderDetail
        OrderSheet---|배송지|DeliveryAddress
        subgraph 주문상태
        direction TB
        Order-->|결제|Payment
        Order-->|취소|Cancel
        Order-->|환불|Refund
        end
        Payment-->|환불|Refund
        Payment ---|결제수단|PaymentMethod
        subgraph 결제수단
        direction TB
        PaymentMethod-->|원결제|FundingSource
        PaymentMethod-->|쿠폰|Coupon
        PaymentMethod-->|포인트|Point
            subgraph 원결제
            direction TB
            Card-->|카드결제|FundingSource
            Bank-->|계좌이체|FundingSource
            VitualAccount-->|가상계좌|FundingSource
            Phone-->|휴대폰결제|FundingSource
            EasyPay-->|간편결제|FundingSource
            end
        end
        Refund-->|안분로직|Propotentional
        Propotentional---FundingSource
        Propotentional---Point
        Propotentional---Coupon
```
## 추상화 도메인 다이어그램
```mermaid
flowchart LR
        PDP(상품 Page)
        Sattlement(정산)
        Product(상품)
        Order(주문)
        CRM(고객센터-MyPage)
        Delivery(배송)
        User(회원)
        Pay(결제)
        PDP-->Product
        Sattlement-->|상품종류|Product
        Sattlement-->|주문/취소상태|Order
        Sattlement-->|배송상태|Delivery
        CRM-->|주문내역|Order
        CRM-->|배송추적|Delivery
        CRM-->|결제수단확인|Pay
        Product-->|판매수량|Order
        Order-->|상품정보|Product
        Order-->|회원정보|User
        Order-->|결제요청|Pay
        Delivery-->|배송지정보|Order
        Delivery-->|상품정보|Product
```
