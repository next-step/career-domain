# Domain model

## 상세 도메인 다이어 그램

```mermaid
flowchart LR
        OWNER(화주)
        DRIVER(차주)
        ORDER(주문)
        DRIVING_VEHICLE(차량 운행)
        Payment(결제)
        PaymentMethod(결제수단)
        FundingSource(원결제)
        Card(카드결제)
        CreditPayment(신용결제)
        OWNER-->|주문하기|ORDER
        subgraph 주문상태
        direction TB
        ORDER-->|배차중|DIPATCHING
        ORDER-->|배차임시요청|DISPATCH_BIND
        ORDER-->|배차확정|DISPATCH_CONFIRM
        ORDER-->|배차완료|DISPATCH_COMPLETE
        ORDER-->|상차지이동중|PICKUP_MOVING
        ORDER-->|상차지도착|PICKUP_COMPLETE
        ORDER-->|하차지이동중|DROP_MOVING
        ORDER-->|운송완료|DELIEVERY_COMPLETE
        ORDER-->|결제|Payment
        end
        DRIVER-->|배차요청|ORDER
        DRIVER-->|배차요청|DRIVING_VEHICLE
        subgraph 운행상태
        direction TB
        DRIVING_VEHICLE-->|배차요청|DISPATCH_REQUEST
        DRIVING_VEHICLE-->|배차대기|DISPATCH_IN_PROGRESS
        DRIVING_VEHICLE-->|배차확정|DISPATCHED
        DRIVING_VEHICLE-->|상차지이동중|PICKUP_MOVING
        DRIVING_VEHICLE-->|상차지도착|PICKUP_COMPLETE
        DRIVING_VEHICLE-->|하차지이동중|DROP_MOVING
        DRIVING_VEHICLE-->|운송완료|DELIEVERY_COMPLETE
        DRIVING_VEHICLE-->|결제|Payment
        end
        Payment ---|결제수단|PaymentMethod
        subgraph 결제수단
        direction TB
        PaymentMethod-->|원결제|FundingSource
            subgraph 원결제
            direction TB
            Card-->|카드결제|FundingSource
            CreditPayment-->|카드결제|FundingSource
            CreditPayment(신용결제)
            end
        end
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
