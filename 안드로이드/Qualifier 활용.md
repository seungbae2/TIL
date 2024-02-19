# Qualifier 활용

Hilt는 타입으로 의존성을 구분한다

같은 타입의 객체를 중복 바인딩하는 것을 방지하기 위해 사용

커스텀 Qualifier

```kotlin
@Qualifierannotation 
class CustomQualifier

@InstallIn(SingletonComponent::class)
object AppModule {
	@CustomQualifier
	@Provides
	fun provideFoo1():Foo{
		return Foo()
	}
	@Provides
	fun provideFoo2():Foo{
		return Foo()
	}
}

@AndroidEntryPoint
class MainActivity : ComponentActivity() {
	@CustomQualifier
	@Inject
	lateinit var foo:Foo
}
```

@Named 활용하기

```kotlin
@InstallIn(SingletonComponent::class)
object AppModule {
	@Named("Foo1")
	@Provides
	fun provideFoo1():Foo{
		return Foo()
	}
}
```

요약

1. @Qualifier 어노테이션을 통해 의존성을 구분할 수 있다.
2. @Qualifier 어노테이션 여러개의 속성을 가질 수 있다.
3. @Named를 활용하여 간단하게 의존성을 구분할 수 있다.