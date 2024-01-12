# CoroutineContext

- CoroutineContext는 맵이나 집합과 같은 컬렉션이랑 개념적으로 비슷하다.
- CoroutineContext는 Element 인터페이스의 인덱싱된 집합이며, Element 또한 CoroutineContext이다.
- CoroutineContext 안의 모든 원소는 식별할 때 사용되는 유일한 Key를 가지고 있다.
- CoroutineContext는 코루틴에 관련된 정보를 객체로 그룹화 하고 전달하는 보편적인 방법이다.
- CoroutineContext는 코루틴에 저장되며, CoroutineContext를 사용해 코루틴의 상태가 어떤지 확인하고, 어떤 스레드를 선택할지 등 코루틴의 작동방식을 정할 수 있다.