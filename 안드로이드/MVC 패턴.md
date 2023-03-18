# MVC 패턴

## 왜 Android에서 MVC는 잘 동작하지 않는가?

- 모바일 환경의 문제
    - 복잡한 비동기 처리
    - 라이프 사이클 처리
    - UI 로직 분리의 어려움: 웹의 html에서는 뷰가 컨트롤러와 완전히 독립된 형태로 UI 로직을 구현 가능하지만, 모바일은 그렇지 못함
- 안드로이드의 문제(뷰-컨트롤러 분리가 애매하다)
    - 뷰: Android의 XML은 기본 레이아웃만을 제공. UI로직이 들어갈 여지가 없음(특히 리스트 구현)
    - 컨트롤러: Activity / Fragment가 컨트롤러 역할을 하는 것이 불가피
    - 결국 Activity / Fragment가 뷰, 컨트롤러 모두를 담당하게 됨
- 그 결과 총체적 난국(가독성, 유지보수성, 확장성)
    - Fat Activity: Activity-Fragment에 너무 많은 로직이 들어간다
    - Unit Test를 만들기가 매우 까다롭다 - 대부분의 테스트 케이스에 context가 필요

## 해결책

- 뷰의 분화
    - Android는 <include> 태스를 통해 XML 정의를 여러 개로 분리 가능
    - 나눈 View들은 Acivity / Fragment가 아닌 별도의 컨트롤러를 통해 제어
- ViewController
    - Activity / Fragment는 뷰도 컨트롤러도 아니도록 : 화면 안 요소들의 생성, 라이프 사이클 처리, 그리고 context에 밀접한 처리를 bridge 해주는 역할만 남겨야
    - 각 뷰마다 ViewController를 만들어 뷰의 동작에 관련된 로직 및 컨트롤러 로직을 여기에 구현
    - 단, ViewController는 설정변경(configuration chagne)으로 인한 라이프사이클 변화에서 살아 남도록 구현해야함
    - 예를 들면 Hilt의 @RetainedActivityScope 지정으로 실현 가능

## 여전히 남는 문제

- 사용자 이벤트와 외부 이벤트 등의 효과적인 처리가 여전히 어려움
- 또 다른 문제는 역시 Context
    - ViewController의 상당수 동작을 위해 Context가 필요
    - Fragment에 연결된 ViewController라면 설정 변경에서 살아남게 만든다는 것이 말처럼 쉽지 않음
    - 테스트의 어려움 - 여전히 대부분의 테스트 케이스에 Context가 필요하므로 테스트 작성도 까다롭고 테스트 실행 속도도 느림
- 해법: non-MVC → 뷰와 컨트롤러를 완전히 분리
    - 특히 컨트롤러는 context를 모르고도 대부분의 동작을 수행할 수 있어야함
    - 컨트롤러만으로는 부족: 기본적으로 모바일 환경의 이벤트 처리 문제