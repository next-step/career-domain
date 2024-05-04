# Domain model

## 상세 도메인 다이어 그램

```mermaid
flowchart LR
        OWNER(화주)
        DRIVER(차주)
        ORDER(주문)
        OWNER_STATUS(주문상태)
        DRIVING_VEHICLE(운행)
        DRIVING_VEHICLE_STATUS(운행상태)
        Payment(결제)
        PaymentMethod(결제수단)
        FundingSource(원결제)
        Card(카드결제)
        CreditPayment(신용결제)
        ROUTING(라우팅)
        PRICING(요금)
        OWNER-->|주문하기|ORDER
        ROUTING-->|예상경로및운행거리|ORDER
        PRICING-->|요금산출|ORDER
        subgraph 주문상태
        direction TB
        ORDER-->|배차중|OWNER_STATUS
        ORDER-->|배차임시요청|OWNER_STATUS
        ORDER-->|배차확정|OWNER_STATUS
        ORDER-->|배차완료|OWNER_STATUS
        ORDER-->|상차지이동중|OWNER_STATUS
        ORDER-->|상차지도착|OWNER_STATUS
        ORDER-->|하차지이동중|OWNER_STATUS
        ORDER-->|운송완료|OWNER_STATUS
        ORDER-->|결제|Payment
        end
        DRIVER-->|배차요청|ORDER
        DRIVER-->|배차요청|DRIVING_VEHICLE
        subgraph 운행상태
        direction TB
        DRIVING_VEHICLE-->|배차요청|DRIVING_VEHICLE_STATUS
        DRIVING_VEHICLE-->|배차대기|DRIVING_VEHICLE_STATUS
        DRIVING_VEHICLE-->|배차확정|DRIVING_VEHICLE_STATUS
        DRIVING_VEHICLE-->|상차지이동중|DRIVING_VEHICLE_STATUS
        DRIVING_VEHICLE-->|상차지도착|DRIVING_VEHICLE_STATUS
        DRIVING_VEHICLE-->|하차지이동중|DRIVING_VEHICLE_STATUS
        DRIVING_VEHICLE-->|운송완료|DRIVING_VEHICLE_STATUS
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
        Owner(화주)
        Driver(차주)
        MDM(MDM)
        Sattlement(정산)
        Order(주문)
        Pricing(요금)
        DrivingVehicle(운행)
        Pay(결제)
        Routing(라우팅)
        Owner-->|회원승인요청|MDM
        MDM-.승인완료.->Owner
        Driver-->|회원승인요청|MDM
        MDM-.승인완료.->Driver
        Owner-->|주문 생성|Order
        Order-->|예상 운행 경로 및 소요 시간 조회|Routing
        Order-->|요금정보|Pricing
        Driver-->|배차요청|Order
        Driver-->|운행시작|DrivingVehicle
        DrivingVehicle-->|상/하차 일시 및 장소|Order
        Order-->|결제요청|Pay
        Sattlement-->|주문 및 요금 정보|Order
        Sattlement-->|운행 상태|DrivingVehicle
        Pay-->|전표발행|Sattlement
```
