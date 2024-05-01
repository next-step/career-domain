# Domain model
## 상세 도메인 다이어 그램
```mermaid
flowchart LR
    Meet(총회)
%%    MeetMethod(총회방식)
%%    Electronic(전자투표)
%%    Onsite(현장투표)
%%    ElectronicOnsite(전자/현장투표)
    MeetInfo(총회정보)
    MeetParticipant(선거인명부)
    Payment(결제)
    ElectronicVote(전자투표)
    VoteStatus(투표상태)
    VoteSuccess(투표성공)
    VoteFail(투표실패)
    Resend(재발송)
    VoteResult(투표결과)
    
    Meet-->|개설하기|MeetInfo
%%        subgraph 투표방식
%%            direction TB
%%            MeetMethod-->|전자투표|Electronic-->|전자투표 정보|MeetInfo
%%            MeetMethod-->|현장투표|Onsite-->|현장투표 정보|MeetInfo
%%            MeetMethod-->|전자/현장투표|ElectronicOnsite-->|전자/현장투표 정보|MeetInfo
%%        end
    MeetInfo-->|선거인선택하기|MeetParticipant
    MeetParticipant-->|비용결제|Payment
    Payment-->|모바일등기|ElectronicVote
    ElectronicVote-->|투표|VoteStatus
        subgraph 투표발송결과
            direction TB
            VoteStatus-->|성공|VoteSuccess
            VoteStatus-->|실패|VoteFail-->|재발송|Resend
        end
    Resend-->|비용결제|Payment
    VoteSuccess-->|자동집계|VoteResult

```
## 추상화 도메인 다이어그램
```mermaid
flowchart LR
        
```
