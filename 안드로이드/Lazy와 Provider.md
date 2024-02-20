# Lazy와 Provider

## Lazy주입 예제코드

```kotlin
@AndroidEntryPoint
class MainActivity : ComponentActivity() {
	@Inject
	lateinit var fooLazy:Lazy<Foo>
	
	override fun onCreate(savedInstanceState: Bundle?) {
		super.onCreate(savedInstanceState)
		
		// get() 호출 시 인스턴스화
		val foo1 = fooLazy.get()
	}
}
```

## Lazy 주입 특징

- Lazy<T>의 get() 호출이후 다시 get()을 호출하면 캐시 된 (동일한) T 인스턴스를 얻는다
- Lazy<T>의 get() 메서드를 호출할 때 T를 반환한다. get() 호출 시점에 T가 인스턴스화 된다.
- T 바인딩에 Scope가 지정되어 있다면, 각 Lazy<T> 요청에 대한 동일한 Lazy<T> 인스턴스가 주입된다.
- 특정시점에 바인딩 인스턴스화 할 때 사용하면 좋다
- 인스턴스 생성에 비용이 큰 경우 사용하면 좋다

## Provider 주입 예제 코드

```kotlin
@AndroidEntryPoint
class MainActivity : ComponentActivity() {
	@Inject
	lateinit var fooProvider:Provider<Foo>

	override fun onCreate(savedInstanceState: Bundle?) {
		super.onCreate(savedInstanceState)

		// 매 get() 호출마다 새로운 인스턴스 생성
		val foo = fooProvider.get()
	}
}
```

## Provider 주입 특징

- T 바인딩에 Scope가 지정되어 있다면, Provider<T>의 get() 메서드를 호출할 때 동일한 인스턴스 T를 반환한다.
- Provider<T>의 get() 메서드를 호출할 때마다 새로운 인스턴스 T를 반환한다.
- T 바인딩에 Scope가 지정되어 있다면, 각 Provider<T> 요청에 대한 동일한 Provider<T> 인스턴스가 주입된다.
- 하나의 Provider<T>로 여러 T 인스턴스를 생성하기 원할 때 사용할 수 있다. (Builder, Factory 패턴과 유사)