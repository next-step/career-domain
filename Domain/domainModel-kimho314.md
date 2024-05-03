# Domain model

## 상세 도메인 다이어 그램

```mermaid
flowchart LR
        OWNER(화주)
        DRIVER(차주)
        ORDER(주문)
        DRIVING_VEHICLE(운행)
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
        OWNER(화주 웹)
        DRIVER(차주 앱)
        Sattlement(정산)
        Order(주문)
        Pricing(요금)
        ADMIN(어드민 웹)
        DRIVING_VEHICLE(운행)
        Pay(결제)
        OWNER-->|주문 생성|ORDER
        ORDER-->|요금정보|Pricing
        DRIVER-->|배차요청|ORDER
        DRIVING_VEHILCE-->|상/하차 일시 및 장소|ORDER
        ADMIN-->|운행 추적|DRIVING_VEHICLE
        ADMIN-->|주문 내역|ORDER
        ADMIN-->|주문 취소|Order
        ADMIN-->|결제 내역 확인|Pay
        ORDER-->|결제요청|Pay
        Sattlement-->|주문 및 요금 정보|Order
        Sattlement-->|운행 상태|DRIVING_VEHICLE
```
