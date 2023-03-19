# Non-MVC 의 설계 전략

- Non-MVC에서 Activity는 무엇인가?
    - Activity는 아주 제한적인 컨트롤러
- MVP의 궁극적 접근법
    - Activity에서 뷰와 컨트롤러의 역할을 최대한 빼앗아 뷰와 프리젠터로 넘김
    - Activity는 객체 생성 및 순수 흐름 관리 역할 위주
- MVVM / MVI 등의 접근법
    - 단방향 데이터 흐름(Uni-directional Data Flow): 컨트롤러 → 뷰 방향의 데이터 흐름을 이벤트를 수신하는 형태로 구현
    - 마찬가지로 Acivity는 최대한 일부 context 의존 기능만 하도록
    - 뷰 logic은 최대한 data binding으로 구혐