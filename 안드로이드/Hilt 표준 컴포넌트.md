# Hilt 표준 컴포넌트

안드로이드 컴포넌트에 대응 되는 Hilt 컴포넌트

| Component | Injector for |
| --- | --- |
| SingletonComponent | Application |
| ViewModelComponent | ViewModel |
| ActivityComponent | Activity |
| FragmentComponent | Fragment |
| ViewComponent | View |
| ViewWithFragmentComponent | View with @WithFragmentBindings |
| ServiceComponent | Service |

컴포넌트의 생명주기

| Component | Scope | Created at | Destroyed at |
| --- | --- | --- | --- |
| SingletonComponent | @SingletonComponent | Application#onCreate() | Application process is destroyed |
| ActivityRetainedComponent | @ActivityRetainedScoped | Activity#onCreate() | Activity#onDestroy() |
| ViewModelComponent | @ViewModelScope | ViewModel created | Viewodel destroyed |
| ActivityComponent | @ActivityScope | Activity#onCreate() | Activity#onDestroy() |
| FragmentComponent | @FragmentScope | Fragment#onAttach() | Fragment#onDestroy() |
| ViewComponent | @ViewScope | View#super() | View destroyed |
| ViewWithFragmentComponent | @ViewScope | View#super() | View destroyed |
| ServiceComponent | @ServiceScope | Servie#onCreate() | Servie#onDestroy() |

Scope vs Unscope

```kotlin
// 이 바인딩은 매 요청시 새로운 인스턴스를 생성합니다.
class UnscopedBinding @Inject constructor() {
}

// 이 바인딩은 스코프 애노테이션이 있으므로,
// 해당 Hilt 컴포넌트의 수명동안은 매 요청에 동일 인스턴스 반환을 보장합니다
@FragmentScoped
class ScopedBinding @Inject constructor() {
}
```

모듈에서 Scope 지정하기

```kotlin
@Module
@InstallIn(FragmentComponent::class)
object FooModule {
// 스코프 없음
@Provides
fun provideUnscopedBinding() = UnscopedBinding()

// 스코프 있음
@Provides
@FragmentScoped
fun provideScopedBinding() = ScopedBinding()
}
```

Scope Annotation 언제 써야할까?

- 어떤 의존성을 인스턴스화하는 비용이 클 때
- 동일한 인스턴스를 반환을 원할 때
- 특정 인스턴스를 공유하고 싶을때

기본으로 제공되는 바인딩

| Component | Default Bindings |
| --- | --- |
| SingletonComponent | Application |
| ActivityRetainedComponent | Application |
| ViewModelComponent | SavedStateHandle, ViewModelLifeCycle |
| ActivityComponent | Application, Activity |
| FragmentComponent | Application, Activity, Fragment |
| ViewComponent | Application, Activity, View |
| ViewWithFragmentComponent | Application, Activity, Fragment, View |
| ServiceComponent | Application, Service |