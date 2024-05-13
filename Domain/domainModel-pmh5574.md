```mermaid
flowchart LR
    Member(회원)
    Admin(관리자)
    Board(게시판)
    Client(고객사)
    Contract(계약)
    Excel(엑셀)

    Member-->|문의|Board
    Admin-->|답변|Board
    Member-->|재문의|Board
    Admin-->|재답변|Board
    Admin-->|월별 문의 내용|Excel-->|문의 내용|게시판
    Admin-->|회원 생성|Member
    Admin-->|고객사 생성|Client
    Admin-->|계약 생성|Contract
    Member---|고객사 종류|Client
    Contract---|고객사 종류|Client
```