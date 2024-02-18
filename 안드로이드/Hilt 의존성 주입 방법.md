# Hilt 의존성 주입 방법

## @Inject

생성자 주입

```kotlin
class Foo **@Inject** construct(bar: Bar){
 // ... 
}
```

필드 주입

```kotlin
@AndroidEntryPoint
class AndroidClass : ... {
	@Injectlateinit var bar:Bar
}
```

매서드 주입

```kotlin
@AndroidEntryPoint
class AndroidClass: ... {
	@Injectfun setBar(bar: Bar){
		// ...
	}
}
```