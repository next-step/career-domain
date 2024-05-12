# Domain model
```mermaid
flowchart TB
    User(일반 가입자) -->|회원가입| PhunaniSite(펴나니 사이트)
    SalesRep(영업 사원) -->|서면 가입| PeonaniStaff(펴나니 직원)
    FacilityManager(요양 시설 관리자) -->|초대 링크 발송| FacilityStaff(요양 시설 직원)
    FacilityStaff -->|회원가입 및 등록| Facility(요양 시설)
    FacilityManager -->|초대 링크 발송| Caregiver(수급자의 보호자)
    Caregiver -->|회원가입 및 등록| Facility
    PeonaniStaff -->|백오피스 등록| FacilityManager

    subgraph 회원 종류
        direction LR
        User
        Caregiver
        FacilityManager
        FacilityStaff
        PeonaniStaff
    end
```