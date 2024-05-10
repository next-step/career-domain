```mermaid
flowchart LR
    subgraph 조합 관리
        Union_Regi(조합원 명부)
        Union(조합)
        Admin(운영진)
        Certificate(증명서)
        Union_Member_Regi(가입자 명부)
        Union_Leader(조합장)
        Zone(구역)
        Point(포인트)
        Promotion_Leader(홍보 팀장)
        Promotion_Manager(홍보 담당자)
    end
    subgraph 총회
        Meeting(총회)
        Meet_Participant(선거인 명부)
        Electronic_Voting(전자 투표)
        Onsite_Voting(현장 투표)
        Statistics(통계)
        Revocation_Management(철회 관리)
        Written_Management(서면 관리)
        Dup_Voting_Management(중복 투표 관리)
        Early_Voting(사전 투표)
        Revocation_Voting(서면 투표)
    end
    subgraph 커뮤니티
        Guest(게스트)
        Member(일반 회원)
        Board(게시판)
    end
    subgraph Third_Party
        Sms(문자 발송)
        Materials(자료 발급)
        Address(우편 발송) 
    end

    Guest --> |구역 정보| Zone
    Guest --> |조합 정보| Union
    Guest --> |회원 가입| Member
    Guest --> |게시판| Board
    Guest --> |가입 요청| Union
    Member --> |구역 정보| Zone
    Member --> |조합 생성 요청| Admin
    Admin --> |생성| Union
    Admin --> |조합장 등급 변경| Union_Leader 
    Admin --> |포인트 충전| Point 
    Union --> |개설| Meeting
    Union --> |명부 목록| Union_Regi
    Union --> |구역 정보| Zone
    Union --> |가입 승인| Union_Member_Regi
    Promotion_Leader --> |총회 정보| Meeting
    Promotion_Manager --> |총회 정보| Meeting
    Promotion_Leader --> |계정 생성 문자 발송| Promotion_Manager
    Promotion_Leader --> |선거인 명부| Meet_Participant
    Union_Leader --> |증명서 발급| Certificate
    Union_Leader --> |총회 정보| Meeting
    Union_Leader --> |조합 정보| Union
    Union_Leader --> |Excel 업로드 명부 생성| Union_Regi
    Union_Leader --> |계정 생성 문자 발송| Promotion_Leader
    Union_Regi --> |문자 발송| Sms
    Union_Regi --> |자료 발급| Materials
    Union_Regi --> |우편 발송| Address
    Union_Regi --> |가입자 목록| Union_Member_Regi
    Meeting --> |참석 관리 및 투표지 배부| Onsite_Voting
    Meeting --> |생성 시 문자 발송| Electronic_Voting
    Meeting --> |선거인 명부 생성| Meet_Participant
    Meeting --> |통계| Statistics
    Meeting --> |현장 투표 철회| Revocation_Management
    Meeting --> |서면 투표| Written_Management
    Meeting --> |중복 투표 관리| Dup_Voting_Management
    Meet_Participant --> |투표| Electronic_Voting
    Revocation_Management --> |현장 투표 정보| Onsite_Voting
    Early_Voting --> Electronic_Voting
    Early_Voting --> Revocation_Voting
    Dup_Voting_Management --> Onsite_Voting
    Dup_Voting_Management --> Electronic_Voting
```
### 리팩토링1 포인트
- 도메인은 명사로 생각해보고, 행위는 Line에 표현해보자.
- 테이블에 명확히 표현되는 데이터를 기준으로 도메인을 뽑아보자.
- 추상화가 많이 되어도 신경쓰지 말아보자.
- 단기간에 잘할 수 없다는 것을 인정하고 그리자.
- 현재 이정도 그릴 수 있는 것만해도 전체 시스템을 대략 알고 있는 것으로 업무에는 큰 도움이 된다.
- 아무래도 처음와서 상세하게 코드를 까봐서 이미 지식이 있기 때문에 더욱 상세하게 그려지는 것 같다.
- 리팩토링2에서 한 번 더 리팩토링을 할건데 해당 차트에서 빨간색이 최종본에서 리팩토링될 포인트이다. 
```mermaid
flowchart LR
%% Colors %%
    classDef blue fill:#2374f7,stroke-width:0px,color:#fff
    classDef green fill:#137433,stroke-width:0px,color:#fff
    classDef red fill:#FF3399,stroke-width:0px,color:#fff
    classDef orange fill:#FFB226,stroke-width:0px,color:#fff
    classDef yellow fill:#CCCC00,stroke-width:0px,color:#fff
    classDef violet fill:#6600CC,stroke-width:0px,color:#fff
    
    subgraph 조합
        Union_Regi(조합원 명부)
        Union_Member(조합 가입자)
        Union(조합)        
        Sms(문자):::red
        Materials(자료):::red
        Post(우편):::red
        Consultation(상담):::red
        Agreement(동의서)
    end
    
    subgraph 구역 
        Zone(구역)
    end
    subgraph 회원 
        Member(일반 회원)
    end
    subgraph CMS 
        CMS(운영 관리)
    end
    
    subgraph 총회
        Certificate(증명서)
        Meet(총회)
        Meet_Participant(선거인 명부)
    end
    subgraph 투표 
        Vote(투표):::red
    end
    subgraph 홍보요원
        Promotion_Team(홍보 요원)
        Promotion_Leader((홍보 팀장))
        Promotion_Manager((홍보 담당자))
        Promotion_Leader --> |선거인 배정| Promotion_Manager
    end
    
    Member --> |조합 가입요청| Union
    Member --> |조합 생성 요청| CMS
    CMS --> |조합 생성| Union
    Union --> |조합 가입 승인| Union_Member
    Union --> |구역 정보| Zone
    Union --> |명부 생성 - Excel| Union_Regi
    Union --> |홍보 팀장 계정 발송| Sms
    Union_Regi --> |우편 발송| Post
    Union_Regi --> |문자 발송| Sms
    Union_Regi --> |자료 발급| Materials
    Union_Regi --> |동의서 관리| Agreement
    Union_Regi --> |상담 관리| Consultation
    Union_Regi --> |총회 개설| Meet
    Meet --> |선거인 명부 생성| Meet_Participant
    Meet --> |증명서 발급| Certificate
    Meet --> |투표| 투표
    Meet --> |상담 관리| Consultation
    Vote --> |선거인 명부 정보| Meet_Participant
    Certificate --> |투표 정보| 투표
    Certificate --> |선거인 정보| Meet_Participant
    Promotion_Team -.- Promotion_Leader
    Promotion_Team -.- Promotion_Manager
    홍보요원 --> |팀장이 홍보 담당자 계정 발송| Sms
    홍보요원 --> |총회 정보| Meet
    홍보요원 --> |선거인 정보| Meet_Participant
```
### 리팩토링 2 포인트
- 상담을 조합과 총회가 별도로 데이터를 갖도록 테이블 자체를 분리하는 컨셉
- 조합과 총회를 아예 분리. 실제 프로세스는 조합원 명부를 기반으로 체크박스로 선택해서 선거인명부를 복사해서 총회에 선거인명부를 생성하는데 도메인 상으로는 크게 연관이 없는 것 같아 분리.
  조합원 명부도 엑셀로 업로드하는데 선거인 명부도 그런 개념으로 생각해서 하면 분리가 된다고 생각
- 문자, 자료, 우편을 별도의 제네릭한 느낌의 도메인으로 도출
- 투표도 별도의 테이블이 있기 때문에 도출
```mermaid
flowchart LR
%% Colors %%
    classDef blue fill:#2374f7,stroke-width:0px,color:#fff
    classDef green fill:#137433,stroke-width:0px,color:#fff
    classDef red fill:#FF3399,stroke-width:0px,color:#fff
    classDef orange fill:#FFB226,stroke-width:0px,color:#fff
    classDef yellow fill:#CCCC00,stroke-width:0px,color:#fff
    classDef violet fill:#6600CC,stroke-width:0px,color:#fff
    
    subgraph 조합
        Union_Regi(조합원 명부)
        Union_Member(조합 가입자)
        Union(조합)
        Union_Consultation(상담):::red
        Agreement(동의서)
        Zone(구역)
    end
    subgraph 조합업무
        Sms(문자):::red
        Materials(자료):::red
        Post(우편):::red
    end
    
    subgraph 회원 
        Member(일반 회원)
    end
    subgraph CMS 
        CMS(운영 관리)
    end
    
    subgraph 총회
        Meet(총회)
        Meet_Participant(선거인 명부)
        Meet_Consultation(상담):::red
    end
    subgraph 투표
        Vote(투표):::red
        Onsite_Vote((현장 투표)):::red
        Elector_Vote((전자 투표)):::red
        Vote -.- Onsite_Vote
        Vote -.- Elector_Vote
    end
    subgraph 홍보요원
        Promotion_Team(홍보 요원)
        Promotion_Leader((홍보 팀장))
        Promotion_Manager((홍보 담당자))
        Promotion_Leader --> |선거인 배정| Promotion_Manager
    end
    subgraph 증명서
        Certificate(증명서):::red
    end
    subgraph 결제 
        Payment(결제):::red
    end
    
    Member --> |조합 가입요청| Union
    Member --> |조합 생성 요청| CMS
    CMS --> |조합 생성| Union
    Union --> |조합 가입 승인| Union_Member
    Union --> |구역 정보| Zone
    Union --> |명부 생성 - Excel| Union_Regi
    Union --> |홍보 팀장 계정 발송| Generic:::red
    Union --> |증명서 발급| 증명서
    Union_Regi --> |우편 발송| 조합업무
    Union_Regi --> |문자 발송| 조합업무
    Union_Regi --> |자료 발급| 조합업무
    Union_Regi --> |동의서 관리| Agreement
    Union_Regi --> |상담 관리| Union_Consultation
    Union_Regi --> |총회 개설| Meet
    Meet --> |선거인 명부 생성| Meet_Participant
    Meet --> |증명서 발급| 조합업무
    Meet_Participant --> |현장 투표| 투표
    Meet_Participant --> |전자 투표| 투표
    Meet --> |상담 관리| Meet_Consultation
    Meet_Participant --> |증명서 생성| 증명서
    Promotion_Team -.- Promotion_Leader
    Promotion_Team -.- Promotion_Manager
    홍보요원 --> |팀장이 홍보 담당자 계정 발송| Generic:::red
    홍보요원 --> |총회 정보| Meet
    홍보요원 --> |선거인 정보| Meet_Participant
    Union_Regi --> |총회 개설 비용 차감| Payment
    조합업무 --> |비용 차감| Payment
    CMS --> |충전| Payment

%%    linkStyle 14,15,16,19,20,21,23,25 stroke-width:4px, stroke:red
```