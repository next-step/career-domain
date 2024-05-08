# Domain model
## 상세 도메인 모델
```mermaid
flowchart LR
    Meet(총회)
    Info(총회정보)
    Agenda(안건)
    UnionRegister(조합원)
    Elector(선거인)
    Agent(대리인)
    Payment(결제)
    VoteStatus(투표현황)
    Resend(재발송)
    VoteResult(투표결과)
    Calculate(집계결과)
    Certificate(증명서)
    Distribution(유통증명서)
    Online(전자문서증명서)
    OriginDoc(투표원본문서)
    VoteDoc(투표내역문서)
    VoteTotal(총투표결과)
    
    Meet-->|생성|Info
    Info-->|투표안건|Agenda
    Agenda-->|선거인 선택|UnionRegister
    UnionRegister-->|선거인 확정|Elector
    UnionRegister-->|대리인 확인|Agent
    Agent-->|선거인 확정|Elector
    Elector-->|총회비용|Payment
    Payment-->|발송|VoteStatus
        subgraph 전자투표 결과
            VoteStatus-->|재발송|Resend
            VoteStatus-->|투표완료|VoteResult
            Resend-->|발송비용|Payment
            VoteResult-->|자동집계|Calculate
        end
    Calculate-->|총회종료|Certificate
        subgraph 증명서 발급
            Certificate-->|외부 요청|Distribution
            Certificate-->|외부 요청|Online
            Certificate-->|내부 발급|OriginDoc
            Certificate-->|내부 발급|VoteDoc
            Certificate-->|내부 발급|VoteTotal
        end

```
## 추상 도메인 모델

```mermaid
flowchart LR
    Admin([관리자])
    User([사용자])
    BizZone(정비구역)
    Union(조합)
    Contract(계약)
    Member(일반가입자)
    UnionMember(조합가입자)
    Board(조합게시판)
    UnionRegister(조합원)
    Address(주소록)
    Meet(총회)
    Elector(선거인)
    Vote(투표결과)
    Certificate(증명서)
    Promotion(홍보)
    Post(우편)
    Document(자료)
    Sms(문자)
    Counsel(상담)
    Agreement(동의서)
    Payment(결제)
    CS(고객센터)

    Union-->|가입승인|UnionMember
    Admin-.->|고객센터 관리|CS
    Admin-.->|정비구역 등록|BizZone
    Admin-.->|비용설정|Contract
    Admin-.->|조합관리|Union
    
    BizZone-->|조합개설|Union
    subgraph 일반회원
        User-.->|회원가입|Member
        UnionMember
    end
    UnionMember-->|게시글|Board
    UnionMember-->|조합원명부 등록|UnionRegister
    subgraph 조합원
        UnionRegister
        UnionRegister-->|대리인 등록|UnionRegister
        Elector
    end
    Member-->|조합가입|Union
    Union-->|서비스 계약|Contract
    Contract-->|월이용료|Payment
    Union-->|서비스사용|Payment
    Payment-->|환불처리|Payment
    UnionRegister-->|총회개설|Meet-->|선거인 확정|Elector-->|투표|Vote-->|투표결과 증빙|Certificate
    Elector-->|담당자 지정|Promotion
    UnionRegister-->|주소록관리|Address-->|우편발송|Post
    Address-->|자료발급|Document
    Address-->|문자발송|Sms
    UnionRegister-->|상담관리|Counsel
    UnionRegister-->|동의서관리|Agreement
```
