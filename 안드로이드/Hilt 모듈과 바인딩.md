# Hilt 모듈과 바인딩

## 모듈

프로그램을 구성하는 구성 요소, 관련된 데이터와 함수를 하나로 묶은 단위

## 모듈이 설치되는 과정

1. 컴파일 타임, 어노테이션 처리
2. @Module 탐색
3. @InstallIn에서 설치될 컴포넌트 탐색
4. 해당컴포넌트에 설치

## @InstallIn 사용하기

```kotlin
@Module
@InstallIn(SingletonComponent::class)
object FooModule {
	@Singleton
	@Provides
	fun provideBar(app: Application): Bar {...}
}
```

## 여러 컴포넌트에 모듈 설치

예) @InstallIn(ViewComponent::class, ViewWithFragmentComponent::class)

1. 컴포넌트에 접근하여 제공되는 바인딩들은 모두 동일한 스코프에 있어야 한다.
2. 선언된 컴포넌트들의 바인딩에 접근가능하며, 프로바이드 함수에 주입할 수 있어야 한다.
3. 하위 및 상위 컴포넌트 계층간에는 동일한 모듈을 설치 할 수 없다.

## Nullable 바인딩은 지양

- Hilt는 자바코드에서 null 바인딩을 금하고 있다.
- 자바코드에서 의존성 바인딩 및 요청 시 @Nullable 어노테이션을 사용해서 우회 할 수 있다.
- 코틀린에서는 문법자체적으로 null assign을 금하고 있으나, Nullable 타입이 존재한다.
- 실제로 Hilt는 자바기반이므로 코틀린으로 작성한 nullable 바인딩이 가능하다.
- 그래도 null-safe한 코드를 위해 nullable한 의존성은 지양하자

## 요약 정리

1. Hilt 모듈은 연관된 의존성들을 한데 묶어서 제공하는 클래스
2. 컴파일 타임에 @InstallIn을 체크하여 적절한 컴포넌트에 설치된다.
3. 제약적이지만 여러 컴포넌트에 동일한 모듈을 설치하는 것이 가능하다.
4. Null은 바인딩하지도, 요청하지도 말자