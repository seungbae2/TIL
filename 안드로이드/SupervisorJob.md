# SupervisorJob

### SupervisorJob의 특징 및 역할

1. **독립적인 에러 처리**:
    - 일반적인 `Job`은 하나의 하위 코루틴이 실패하면 그 실패가 상위 코루틴과 모든 다른 하위 코루틴에 전파된다. 반면, `SupervisorJob`을 사용하면 하위 코루틴의 실패가 상위 코루틴이나 다른 하위 코루틴에 영향을 미치지 않는다.
    - 예를 들어, 여러 개의 하위 작업을 병렬로 수행할 때, 하나의 작업이 실패해도 다른 작업들은 계속 진행되도록 하고 싶을 때 유용하다.
2. **상위 코루틴의 책임**:
    - 상위 코루틴은 하위 코루틴의 실패를 명시적으로 처리해야 한다. 상위 코루틴이 명시적으로 실패를 처리하지 않으면, 하위 코루틴의 실패는 무시된다.

### SupervisorJob 사용 예시

```kotlin
kotlin코드 복사
import kotlinx.coroutines.*

fun main() = runBlocking {
    // SupervisorJob을 사용한 CoroutineScope 생성
    val scope = CoroutineScope(SupervisorJob() + Dispatchers.Default)

    // 하위 코루틴 1: 지연 후 예외 발생
    val job1 = scope.launch {
        delay(1000)
        println("Job 1 started")
        throw RuntimeException("Job 1 failed")
    }

    // 하위 코루틴 2: 지연 후 정상 종료
    val job2 = scope.launch {
        delay(2000)
        println("Job 2 completed")
    }

    // 모든 작업이 완료될 때까지 대기
    joinAll(job1, job2)
    println("Scope completed")
}

```

위 예시에서 `job1`은 예외를 던지지만 `SupervisorJob` 덕분에 `job2`는 영향을 받지 않고 정상적으로 완료된다. 이렇게 하면 하나의 하위 작업이 실패해도 나머지 작업들이 독립적으로 진행될 수 있다.

### 정리

`SupervisorJob`은 여러 코루틴을 동시에 실행할 때, 하나의 실패가 다른 코루틴에 영향을 미치지 않도록 하기 위한 도구이다. 이를 통해 코루틴 계층 구조에서 더 유연하고 독립적인 에러 처리가 가능해진다. `SupervisorJob`은 특히 애플리케이션 전역에서 다양한 작업을 병렬로 실행해야 할 때 유용하다.