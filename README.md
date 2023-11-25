# career-domain

```font-jua
```

```innerHtml
<style>
.tui-editor-contents p {
    line-height: 1.5 !important;
}

.tui-editor-contents ul {
    padding-left: 25px !important;
}

.tui-editor-contents .task-list-item {
    margin-bottom: 5px;
}

.tui-editor-contents .task-list-item ul {
    margin-top: 5px !important;
}

.tui-editor-contents .google-form-container {
    padding-bottom: 75% !important;
}
</style>
```
# 요구사항
- [ ] 자신의 서비스 시스템의 Domain Model을 작성한다.
    - [ ] Local 환경(혹은 Test환경)에서 Reverse Engineering을 이용하여 DB ERD문서를 생성한다.
    - [ ] 생성된 ERD를 가지고 본인의 서비스에 대한 도메인 모델을 작성한다.



# 도메인 모델
<center><img src="https://nextstep-storage.s3.ap-northeast-2.amazonaws.com/da6a4df544314a15941a08f560fbee72" width="30%"></center>

```alert-primary
* 좋은 개발자, 역량있는 개발자는 결국 소프트웨어의 본질이라 할 수 있는 도메인의 이해가 중요하다.<br>
* 소프트웨어 개발자로서 성공적으로 일하고 성장 및 성과를 얻기 위해, 먼저 일에 대한 도메인을 이해하기 위한 접근 방법을 탐구하고 체득하기 위한 실습을 진행합니다.
```

## ERD
- 최근 개발 트랜드는 ORM을 활용하여 물리적인 Persistant layer와는 분리하여 개발하는 것이 주류 방식이다. 
- 개발 관점에서는 당연히 의존성을 분리하고 개발하는 것이 적절한 방식이나 실제 서비스에서는 데이터가 사용되고 있는데 이런 데이터에 대한 계층구조나 관계의 이해는 서비스 개발에서 로직 구현을 위해서 반드시 필요하다.
- 하지만 대부분의 ERD문서는 한번 만들어지면 최신화가 어렵다.
    - 가급적 새로운 사람이 와서 서비스 분석을 할 때 최신 문서로 update하는 문화를 만들어 보면 좋다.
    - 기존에 문서가 없다면 DB 리버스 엔지니어링을 통해서 만들어 놓는다.

## Domain model
```alert-primary
도메인 모델을 그릴 수 있다는 것은 소프트웨어를 개발하는 대상역역에 대한 이해가 있어야 한다.<br>
그렇기 때문에 본인이 개발하는 문제 영역을 도식화로 표현할 수 있어야 결국 본인의 지식이 될 수 있고 그 내용이 머리속에 잘 정리되어 있을 때 다른 사람에게도 잘 이야기 할 수 있게 된다.
```
> 도메인 모델을 단순히 DB로만 볼 수 없지만 아직 익숙하지 않은 시점(입사나 부서 이동으로 새로운 서비스를 개발하게 되었을 때) DB를 활용한 도메인 모델을 그려보는 것은 좋은 접근법이 될 수 있다.
> 

- 지금 하고 있는 업무가 많이 익숙하고 이미 잘 알고 있더라도 완전히 모른다고 생각 하고 도메인 모델을 그려보자
    - 이직이나 부서이동 같은상황에서 빠르게 서비스를 분석 하기위한 방법으로 데이터와 그 흐름을 이해하는 것이 적절하다.
    - 소스 코드 부터 보는 경우가 있는데 도메인에 대한 이해를 하고 그 흐름에서 소스코드가 어떻게 구현되어 있는지를 이해한다면 전체를 이해하기 용이 하다.
- 도메인 모델은 추상화를 하여서도 작성할 수 있고 사실적 표현으로도 작성할 수 있으나 아래 기준으로 작성해보자
    - 핵심 Entity는 작성한다.
    - Entity의 attribute는 최소화 해서 작성한다.
    - Relation과 의존 관계는작성한다.
    - 아래의 예시와 같은 형태의 문서를 작성한다.
<center><img src="https://nextstep-storage.s3.ap-northeast-2.amazonaws.com/46250f7159ab42fd8ffaef7dac3f5f04" width="60%"></center>

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


## 🚀미션(해야할 일)

1. 자신의 서비스 시스템의 DB를 리버스 엔지니어링으로 ERD를 만들어 본다. (이미 생성된 문서가 있다면 최신화하여 활용)
    - MySQL workbench를 기준으로 실습해본다.
    - local환경의 data를 이용한다. (절대 real DB를 하지 않도록 한다.)
    - 자료는 보안이 중요하기 때문에 본인만 사용하고 회사내에만 공유 하도록 한다.
    - 참고자료 
        -  [Reverse Engineering](https://dev.mysql.com/doc/workbench/en/wb-reverse-engineer-live.html)
2. 생성된 ERD를 보고 데이터의 관계나 의존성을 확인하고 서비스에 대한 이해를 높인다.
    - relation은 정확히 그려 볼 수 있도록 한다.
    - 특히 추가되거나 flag 같은 속성은 분기를 하는 속성일 가능성이 높으므로 눈여겨 보는것이 좋다.
    - 참고자료
        -  [UML](https://www.ictdemy.com/software-design/uml/uml-domain-model)
    - Tip 
        - 속도 관점에서 물리적인 relation은 가급적 stage환경이나 dev환경에서만 적용하면 좋다.
3. 이러한 이해를 가지고 추상화된 Domain modeling을 진행 한다. 
    - 보안 적인 이슈가 되지 않도록 추상화된 modeling을 진행한다.
4. 작성된 Domain model 문서를 git(<span style="color:red">링크필요</span>)에 올리고 review를 진행 한다. 
    - Git review는 [링크](https://github.com/next-step/nextstep-docs/tree/master/codereview)를 참고해서 진행 한다.
    
    
    
# 참고자료
1. DB Reverse engineering을 위한 Mysql 공식 문서 : [Reverse Engineering](https://dev.mysql.com/doc/workbench/en/wb-reverse-engineer-live.html)
2. 도메인 모델 작성을 위한 UML 문법 (UML도 언어입니다.) : [UML](https://www.ictdemy.com/software-design/uml/uml-domain-model)
3. 도메인 모델 작성 방법 Tip 
 ```innerHtml
<iframe src="https://nextstep-storage.s3.ap-northeast-2.amazonaws.com/82ca334e15da46a5a6999d4ecb90e201" style="width:70%; height:500px;"></iframe>
```


