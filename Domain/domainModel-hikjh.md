# Domain model
## 상세 도메인 다이어 그램
```mermaid
flowchart LR
    Union(조합)
    UnionMember(조합가입자)
    UnionRegister(조합원)
    Post(우편)
    ServicePayment(서비스 요금)

    Union-->|가입 승인|UnionMember
    UnionMember-->|우편 발송|Post
    
    Post-->|우편 제작 요청|POSTPIA
    POSTPIA-->|우편 배달 접수|우체국
    우체국-->|우편 배달|UnionRegister
    POSTPIA-...->|우편 제작 상태 응답|Post
    
    Post-->|우편 배달 상태 요청|공공데이터포털
    공공데이터포털-...->|우편 베달 상태 응답|Post
    
    Union-->|요금 충전|ServicePayment
    Post-...->|비용 결제| ServicePayment
```
## 추상화 도메인 다이어그램
```mermaid
flowchart LR
%% 핵심 도메인 - 색상:초록
%% Member(회원)
%% Union(조합)
%%UnionRegister(조합원 명부)
%%Counsel(상담)
%%Meet(총회)
%%Election(선거)
%%Work(조합업무)
%%Payment(결제)

%% 서브도메인 - 색상:노랑

%% Colors %%
classDef green fill:#40c057,stroke-width:0px,color:#fff
classDef yellow fill:#ffd43b,stroke-width:0px,color:#fff

    Member:::green
    Member --- Role:::yellow
    Member --> |조합 가입| Union
    
    Union:::green
    Union --> |회원 관리| Member
    Union:::green --> |요금 충전| Payment
    Union:::green --> |명부 등록| UnionRegister
    Union:::green --> |발송/발급 업무| Work
    Union:::green --> |총회 개설| Meet
    Union:::green --> |상담| Counsel
    Union --- BizZone:::yellow
    Union --- Agreement:::yellow
    Union --- DocumentFormat:::yellow
    
    UnionRegister:::green
    UnionRegister:::green --> |총회 참석| Meet
    UnionRegister --- AddressBook:::yellow
    UnionRegister --- Agent:::yellow
    UnionRegister --- Sharer:::yellow
    
    
    Meet:::green
    Meet:::green --> |선거 관리| Election
    Meet:::green --> |비용 결제| Payment
    Meet:::green --> |상담| Counsel
    Meet --- MeetParticipant:::yellow
    Meet --- Certification:::yellow
    
    Election:::green
    Election:::green --> |투표 결과| Meet
    Election --- Vote:::yellow
    Election --- Electors:::yellow
    Election --- PromotionUser:::yellow
    
    Work:::green
    Work:::green --> |비용 결제| Payment
    Work:::green --> |문자, 우편 발송/자료 발급| UnionRegister
    Work --- Text:::yellow
    Work --- Post:::yellow
    Work --- Data:::yellow
    
    Payment:::green
    Payment --- Charge:::yellow
    Payment --- Use:::yellow

    Counsel:::green
    Counsel:::green --> |조합원 상담| UnionRegister
    Counsel:::green --> |선거인 상담| MeetParticipant
```
## 상세 도메인(우편발송) ERD
```mermaid
erDiagram
    UNION ||--|{ UNION_REGISTER : contains
    UNION ||--|{ UNION_CALLING_NUMBER : contains
    UNION ||--|{ UNION_USE : contains
    UNION ||--|{ UNION_CHARGE : contains
    UNION_CHARGE ||--|{ UNION_CHARGE_CHANGE : contains
    UNION ||--|{ UNION_CHARGE_TAX : contains

    FORM ||--|{ FORM_FILE : contains
    FORM_FILE ||--|| FILE : contains
    FILE ||--|{ POST_ORDER_FORM : contains

    POST_ORDER_MST ||--|{ POST_ORDER_DTL : contains
```
## 상세 도메인(우편발송)
```mermaid
classDiagram

    PostOrder *-- PostSender
    PostOrder *-- PostInformation
    PostOrder *-- RefundInformation
    PostOrder *-- PostOrderDetailList
    
    PostOrderDetailList *-- PostOrderDetail
    PostOrderDetail *-- PostReceiver
    PostOrderDetail *-- PostPriceInformation
    PostOrderDetail *-- PostDeliveryInformation

    PostInformation *-- PostSendMethod
    PostInformation *-- PostSendStatus
    PostInformation *-- PostSendForm
    PostInformation *-- PostSendColor

    PostDeliveryInformation *-- DeliveryStatus

    class PostOrder{
        <<AggregateRoot>>
        - Long poId
        - Long unionId
        - PostSender sender
        - PostInformation postInfo
        - RefundInformation refundInfo
        - PostOrderDtls pomList
        - LocalDateTime reqAt
        - LocalDateTime sendAt
    }

    class PostSender{
        <<ValueObject>>
        - String name
        - String postalCode
        - String address
        - String addressDetail
        - String phoneNumber
    }

    class PostInformation{
        <<ValueObject>>
        - Long fileId
        - String postpiaKey
        - PostSendMethod method
        - PostSendStatus status
        - PostSendForm form
        - PostSendColor color
        - boolean isReturn
        - boolean isUseStapler
        - int count
    }

    class RefundInformation{
        <<ValueObject>>
        - int price
        - String memo
    }

    class PostOrderDetailList{
        <<ValueObject>>
        - List<PostOrderDetail> PostOrderDetailList
    }

    class PostOrderDetail{
        <<AggregateRoot>>
        - Long podId
        - PostOrderMst pom
        - PostReceiver receiver
        - PostPriceInformation priceInformation
        - PostDeliveryInformation deliveryInformation;
    }

    class PostReceiver{
        <<ValueObject>>
        - Long urId
        - String name
        - String postalCode
        - String address
        - String addressDetail
        - String phoneNumber
    }

    class PostPriceInformation{
        <<ValueObject>>
        - int madePrice;
        - int sendPrice;
    }

    class PostDeliveryInformation{
        <<ValueObject>>
        - DeliveryStatus status;
        - String registrationNumber
        - LocalDateTime deliveryAt;
    }

    class PostSendMethod{
        <<enumeration>>
        일반우편
        일반등기
        준등기
        익일특급
    }

    class PostSendStatus{
        <<enumeration>>
        접수 대기
        제작중
        접수 완료
        접수 취소
    }

    class PostSendForm{
        <<enumeration>>
        단면
        양면
    }

    class PostSendColor{
        <<enumeration>>
        흑백
        컬러
    }
    
    class DeliveryStatus{
        <<enumeration>>
        배달전
        배달중
        배달완료
        미배달
    }
```
