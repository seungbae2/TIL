# remember와 rememberSaveable차이

### remember

**`remember`**는 컴포저블 함수의 상태를 컴포지션 동안에만 유지한다. 컴포지션이 재구성되면 (예를 들어, 구성 요소가 다시 그려질 때), **`remember`**는 해당 상태를 그대로 유지한다. 그러나 애플리케이션이 프로세스 종료나 화면 회전 등으로 인해 소멸되면 상태는 사라진다.

```kotlin
val counter = remember { mutableStateOf(0) }
```

위의 코드는 컴포지션 동안 **`counter`** 상태를 유지한다. 화면 회전이나 다른 구성 변경이 일어나면 **`remember`**는 상태를 유지하지만, 프로세스가 종료되면 상태가 사라진다.

### rememberSaveable

**`rememberSaveable`**는 **`remember`**와 유사하지만, 상태를 저장하고 복원할 수 있는 기능을 추가로 제공한다. 화면 회전이나 프로세스 종료와 같은 구성 변경이 발생해도 상태가 유지된다. 내부적으로 **`rememberSaveable`**은 **`SavedStateHandle`**을 사용하여 상태를 저장하고 복원한다.

```kotlin
val counter = rememberSaveable { mutableStateOf(0) }
```

위의 코드는 **`counter`** 상태를 저장 가능한 상태로 만들어서, 화면 회전이나 프로세스 종료 후에도 상태를 유지한다.

### **요약**

- **`remember`**: 컴포지션 동안 상태를 유지하지만, 화면 회전이나 프로세스 종료 시 상태를 잃어버린다.
- **`rememberSaveable`**: 컴포지션 동안 상태를 유지하며, 화면 회전이나 프로세스 종료 시에도 상태를 복원할 수 있다.

따라서, 애플리케이션의 상태가 구성 변경 후에도 유지되어야 한다면 **`rememberSaveable`**을 사용하는 것이 좋다. 그렇지 않으면 **`remember`**를 사용한다.