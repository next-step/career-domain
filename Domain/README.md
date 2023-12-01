# career-domain
> 작성한 Domain model은 png, gif, jpg, pdf 파일 형식으로 파일명은 domainModel-{gitID}.pdf 형식으로 upload 해주세요
# 요구사항
- [x] 자신의 서비스 시스템의 Domain Model을 작성한다.
    - [x] Local 환경(혹은 Test환경)에서 Reverse Engineering을 이용하여 DB ERD문서를 생성한다.
    - [x] 생성된 ERD를 가지고 본인의 서비스에 대한 도메인 모델을 작성한다.


## 🚀미션(해야할 일)
```alert-error-border
민감한 정보가 포함된 ERD는 본인 학습용으로만 사용하고 외부에 노출 되지 않도록 주의 하세요!
```

### 도메인 모델 작성(거시적인 접근)
1. 자신의 서비스 시스템의 DB를 리버스 엔지니어링으로 ERD를 만들어 본다. (이미 생성된 문서가 있다면 최신화하여 활용)
    - MySQL workbench를 기준으로 실습해본다.
    - local환경의 data를 이용한다. (절대 real DB를 하지 않도록 한다.)
    - 자료는 보안이 중요하기 때문에 본인만 사용하고 회사내에만 공유 하도록 한다.
    - 참고자료 
        -  [Reverse Engineering](https://dev.mysql.com/doc/workbench/en/wb-reverse-engineer-live.html) : MySQL 공식 Reverse Engineering 가이드 문서
        -  예시: ![OrderERD.png](https://nextstep-storage.s3.ap-northeast-2.amazonaws.com/b889ca18a4384db0a5656145dde55839)
2. 생성된 ERD를 보고 데이터의 관계나 의존성을 확인하고 서비스에 대한 이해를 높인다.
    - relation은 정확히 그려 볼 수 있도록 한다.
    - 특히 추가되거나 flag 같은 속성은 분기를 하는 속성일 가능성이 높으므로 눈여겨 보는것이 좋다.
        - 이런 속성의 경우 개발을 할때 분기 조건이 나거나 특정 validation을 하는 속성일 가능성이 높아 이런 내용을 놓쳤을 때 bug가 발생할 가능성이 높다.
    - 참고자료
        -  [UML](https://www.ictdemy.com/software-design/uml/uml-domain-model) : domain modeling uml 가이드
    - Tip 
        - 속도 관점에서 물리적인 relation은 가급적 stage환경이나 dev환경에서만 적용하면 좋다.
        - 도메인 모델은 가급적 거시적인 관점에서 볼 수 있도록 최대한 확장해서 그릴 수 있도록 한다. (경력이 쌓이면서 더 넓게 그릴 수 있어야 되며 종국에는 회사전체 시스템의 도메인 모델을 작성 할 수 있어야 한다.)
3. 이러한 이해를 가지고 추상화된 Domain modeling을 진행 한다. 
    - 보안 적인 이슈가 되지 않도록 추상화된 modeling을 진행한다.
    - UML 툴은 본인이 편한 것을 사용하여 최종 이미지 파일 형식으로 출력 할 수 있도록 한다.
    - 형식에 너무 집착하지 말고 처음 보는 사람이 봤을 때 이해 할수 있도록 그려보자.
        - 핵심 도메인 위주로 작성 한다.
        - 주문하기, 결제하기 같은 relation이나 flow가 있다면 같이 표현해 보도록 한다.
    - 예시1 : ![OrderDomain.png](https://nextstep-storage.s3.ap-northeast-2.amazonaws.com/0c24abd56e5a41429d2f6c52cb0fe0a9) 
4. 작성된 Domain model 문서를 [GitHub](https://github.com/next-step/career-domain)의 Domain 폴더에 올리고 review를 진행 한다. 
    - 작성한 Domain model은 png, gif, jpg등 이미지 파일 형식이나 pdf 파일 형식으로 올린다.
    - <b>파일명은 domainModel-{gitID}.png 형식으로 upload 해주세요</b>
    - Git review는 [링크](https://github.com/next-step/nextstep-docs/tree/master/codereview)를 참고해서 진행 한다.


### ERD를 활용한 도메인 모델 작성 가이드라인
#### 1. 도메인 이해:
- 비즈니스나 조직의 도메인에 대한 깊은 이해를 얻기 위해 도메인 전문가와 소통합니다.
- 핵심 개념과 그들 간의 관계를 파악합니다.
#### 2. ERD 작성:
- 주요 엔터티(개체)를 식별하고, 각 엔터티 간의 관계를 ERD로 표현합니다.
- 속성(Attribute)을 정의하고, 각 엔터티의 주요 속성을 명시합니다.
- 기본 키와 외래 키를 정의하여 엔터티 간의 관계를 명확히 합니다.
#### 3. 도메인 모델 작성:
- ERD를 기반으로 도메인 모델을 작성합니다.
- 엔터티를 클래스로 변환하고, 클래스 간의 관계를 명시합니다.
- 클래스의 속성을 정의하고, 각 클래스가 수행하는 메서드 등을 추가합니다.
#### 4. 클래스 다이어그램 작성:
- ERD에서 얻은 정보를 바탕으로 UML(Unified Modeling Language)의 클래스 다이어그램을 작성합니다.
- 클래스 간의 연관 관계, 집합 관계, 일반화 관계 등을 표현합니다.
#### 5. 도메인 규칙 포함:
- 도메인 내에서 적용되는 규칙을 클래스 다이어그램에 포함시킵니다.
- 각 클래스의 책임과 행위에 대한 도메인 규칙을 정확하게 표현합니다.
#### 6. 시험 및 수정:
- 작성한 도메인 모델을 도메인 전문가나 팀원들과 검토합니다.
- 피드백을 받아 모델을 수정하고 개선합니다.
#### 7. 문서화:
- 작성한 도메인 모델을 문서화하여 팀원들과 공유합니다.
- 도메인 모델에 대한 설명과 주요 개념들을 명시적으로 기술합니다.
#### 참고사항:
- ERD와 도메인 모델은 프로젝트의 특정 요구사항과 팀의 선호도에 따라 다양하게 변형될 수 있습니다.
- 지속적인 소통과 수정을 통해 모델을 개선하고 정확성을 확보하세요.

    
# 참고자료
1. DB Reverse engineering을 위한 Mysql 공식 문서 : [Reverse Engineering](https://dev.mysql.com/doc/workbench/en/wb-reverse-engineer-live.html)
2. 도메인 모델 작성을 위한 UML 문법 (UML도 언어입니다.) : [UML](https://www.ictdemy.com/software-design/uml/uml-domain-model)
3. 도메인 모델 작성 방법 Tip 


