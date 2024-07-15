# State Hoisting을 쓰는 이유

1. 컴포넌트 재사용성 증가
    - 분리된 상태 관리: 상태를 개별 컴포넌트가 아닌 상위 컴포넌트에서 관리함으로써 동일한 하위 컴포넌트를 여러 곳에서 재사용 할 수 있다.
    - 동일한 로직 사용: 상태 관리와 로직이 상위 컴포넌트에 집중되기 때문에 동일한 로직을 다양한 하위 컴포넌트에서 재사용할 수 있다.
2. 컴포넌트간 통신 용이
    - 상태 공유: 여러 하위 컴포넌트가 동일한 상태를 공유해야 할 때, 상태 호이스팅을 통해 상위 컴포넌트에서 상태를 관리하면 상태를 쉽게 전달할 수 있다.
    - 상태 일관성: 상태를 중앙에서 관리하면 여러 컴포넌트 간의 상태 일관성을 유지하기 쉽다.
3. 유지보수성 향상
    - 단일 책임 원칙: 상태를 관리하는 로직과 UI를 렌더링하는 로직을 분리함으로써 코드가 더 명확하고 유지보수하기 쉬어진다.
    - 변경 용이: 상태 관리 로직이 상위 컴포넌트에 집중되어 있기 때문에 상태 변경이 필요할 때 한 곳에서 쉽게 수정할 수 있다.
4. 테스트 용이성 증가
    - 단위 테스트: 상태를 상위 컴포넌트에서 관리함으로써 하위 컴포넌트는 단순히 입력을 받아 UI를 렌더링 하는 역할을 하게 되어 테스트가 더 쉬워진다.
    - 상태 테스트: 상태 관리 로직을 별도로 분리함으로써 상태 변화와 관련된 로직을 독립적으로 테스트할 수 있다.
5. 코드의 가독성 및 명확성 향상
    - 명시적 상태 관리: 상태가 어디에서 관리되는지 명확히 알 수 있어 코드의 가독성이 향상된다.
    - 예측 가능성: 상태변화가 예측가능하게 되어 디버깅이 용이하다.

```kotlin
@Composable
fun TextFieldExample(
    text: String,
    onTextChange: (String) -> Unit,
    onButtonClick: () -> Unit
) {
    Column(modifier = Modifier.padding(16.dp)) {
        OutlinedTextField(
            value = text,
            onValueChange = onTextChange,
            label = { Text("Enter text") },
            modifier = Modifier.padding(bottom = 8.dp)
        )
        Button(onClick = onButtonClick) {
            Text("Print Text")
        }
    }
}

@Composable
fun ParentComposable() {
    var text by remember { mutableStateOf("") }

    TextFieldExample(
        text = text,
        onTextChange = { newText -> text = newText },
        onButtonClick = { println(text) }
    )
}
```

이 예제에서 `TextFieldExample` 은 상태를 직접 관리하지 않고 상위 컴포넌트인 `ParentComposable` 에서 상태를 관리한다. 이로인해

- `TextFieldExample`  은 상태와 독립적이므로 재사용이 용이하다.
- `ParentComposable` 에서 상태를 중앙에서 관리하여 여러 컴포넌트 간의 상태 공유가 용이하다.
- 상태 관리 로직이 한 곳에 집중되어 유지보수와 테스트가 쉬워진다.

따라서 상태 호이스팅은 더 나은 구조와 관리를 가능하게 하며, 이는 특히 복잡한 UI와 대규모 애플리케이션에서 매우 중요하다.