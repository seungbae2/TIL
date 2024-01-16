# Dispatchers

Dispatcher를 사용하여 코루틴 실행에 사용되는 스레드를 지정할 수 있다. 기본적으로 제공하는 Dispatcher는 다음과 같다.

- Default: CPU 코어 수에 비례하는 스레드 풀에서 수행한다. CPU 집약적인 작업에 적합하다.
- IO: 일반적으로 IO 작업은 CPU에 영향을 미치지 않으므로, CPU 코어 수보다 훨씬 많은 스레드를 가지는 스레드 풀에서 수행한다(최대 64개). Default dispatcher와 스레드를 공유하기 때문에 Context switching으로 인한 오버헤드가 없다.
- Unconfined: 해당 코루틴을 호출한 부모의 쓰레드에서 실행 또는 재게된다.
- newSingleThreadContext: 새로운 쓰레드를 생성한다.