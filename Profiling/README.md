# 요구사항
- [ ] 자신의 서비스 시스템의 Profiling을 해본다.
    - [ ] Profiling 을 하면서 본인의 서비스에서 부하가 큰 class나 code를 확인해보고 그 이유를 생각 해본다.
    - [ ] Profiling을 통해서 특정 기능에 대한 sequence diagram을 작성한다.
- [ ] SpringData의 @Transactional annotation에 대하여 Profiling 해 본다.
    - [ ] Transactional annotation에 대한 동작기제(메커니즘)을 이해한다.
    - [ ] Transactional annotation에 대한 sequcne diagram을 작성한다.



## 🚀미션(해야할 일)
1. 본인의 시스템에서 본인이 모르는 기능이나 특정 부분에 대하여 Profiling을 진행한다.
    - Profiling은 Local환경에서 진행 한다. 
        - local 컴퓨터에서 profiling할 때는 본인 컴퓨터의 리소스 (cpu, memory...)에 영향을 많이 받기 때문에 정확한 profiling데이터를 확보 할 수 없는 것을 이해하고 있어야한다. (코드상의 병목현상을 찾거나 프로그램의 흐름을 이해하는 목적이다.)
    - 참고자료 ![lowlevelProfiling.gif](https://nextstep-storage.s3.ap-northeast-2.amazonaws.com/81d4177ead1740ae80a85878e04e6a4f)
1. 특정 기능을 실행해보고 Profiling된 Call Tree를 확인해 본다. 
    - 그 외에도 부하가 되는 지점을 찾거나 메모리, CPU, Thread의 상태 등도 확인 해볼 수 있다.
    - Call Tree 확인 : [intelliJ CallTree](https://www.jetbrains.com/help/idea/read-the-profiling-report.html#profiler-call-tree)
1. Call Tree를 통해 비지니스 객체들의 흐름을 확인 해보고 해당 기능의 전체적인 flow를 이해한다.
    - Mothod List를 확인시에는 해당 package로 filter를 걸면 원하는 package범위만 확인 할 수 있다. 
    - 소스코드에서는 쉽게 찾지 못한 AOP class들도 확인 될 수 있다.
1. Profiling한 내용으로 sequnce diagram을 작성해 본다.
    - 예시 : ![sequencediagram.png](https://nextstep-storage.s3.ap-northeast-2.amazonaws.com/e924aa7f146b45da9c4c7076916b4094)
1. 추상화된 sequence flow를 작성해본다.
    - 특정 기능에서 profiling한 부분을 확장하여 하나의 use case 정도를 sequence flow로 작성 한다.
    - 앞서 진행한 도메인 분석의 이해를 바탕으로 확장된 flow를 작성 해본다.
    - 예시 : ![sequnceFlow.png](https://nextstep-storage.s3.ap-northeast-2.amazonaws.com/6445f88ad50b4fd5b2a1c17a4c77f220)
1. 작성된 Sequence flow 문서를 [GitHub](https://github.com/next-step/career-domain/)의 Profiling 폴더에 올리고 review를 진행한다.
    - 작성된 파일은 png, gif, jpg 등의 이미지 파일형식이나 pdf 방식으로 올려도 되고 [Mermaid](https://mermaid.js.org/#/) 을 활용한 마크다운 문서로 올려도 된다. 
    - 파일명은 sequenceFlow-{gitID}.png 같은 형식으로 upload해주세요.
    - Git review는 [링크](https://github.com/next-step/nextstep-docs/tree/master/codereview)를 참고해서 진행 한다.
1. SpringData @Transactional annotation에 대한 Profiling을 진행 한다.
    - 꼭 Profiling을 통해서 진행 하지 않아도 되며 직접 소스를 보거나 Debugg 모드를 활용 할 해도 상관 없다.
1. 분석(profiling, debugging, sourcecode)된 내용을 가지고 @Transactional annotation에 대한 동작방식을 이해한다. 
1. @Transactional annotation에 대한 sequence digram을 작성한다.
    - 작성된 Sequence flow 문서를 [GitHub](https://github.com/next-step/career-domain/)의 Profiling 폴더에 올리고 review를 진행한다.
    - 작성된 파일은 png, gif, jpg 등의 이미지 파일형식이나 pdf 방식으로 올려도 되고 [Mermaid](https://mermaid.js.org/#/) 을 활용한 마크다운 문서로 올려도 된다. 
    - 파일명은 sequenceFlow-{gitID}.png 같은 형식으로 upload해주세요.
    - Git review는 [링크](https://github.com/next-step/nextstep-docs/tree/master/codereview)를 참고해서 진행 한다.



## 참고자료
1. Java Profiling 툴 소개: [Bealdung](https://www.baeldung.com/java-profilers)
2. Intellij Profiling : [Intellij Profiling](https://blog.jetbrains.com/idea/2020/03/profiling-tools-and-intellij-idea-ultimate/)
