# Hilt

Dagger2를 기반으로 안드로이드를 위한 표준화된 의존성 방법 제공

보일러플레이트감소

Jetpack과의 통합

테스트 도구 제공

마이그레이션 API 제공

## 표준 컴포넌트 제공

- 정해진 방법대로 의존성 주입

보일러플레이트 감소 with Hilt

- Hilt가 제공하는 ViewModel.Factory
- Hilt가 제공하는 테스트용 컴포넌트
- 표준 컴포넌트 사용으로 별도 컴포넌트 정의 불필요
- 적은 Dagger 모듈 생성과 중복되는 바인딩 정의 축소
- 바이트 코드 변조

Jetpack 라이브러리와의 통합

- ViewModel
- Navigation
- WorkManager

Hilt 테스트 어노테이션

1. @HiltAndroidTest
2. @UninstallModules
3. @BindValue
4. @CustomTestApplication

Hilt 마이그레이션

- 손쉬운 마이그레이션 방법 제공
- Hilt는 dagger2및 dagger2.android와 함께 동작 가능
- 마이그레이션을 위한 다양한 API 제공

요약

- Hilt는 Dagger2가 갖고 있던 어려움을 개선하기 위해 등장했다
- 다른 솔루션들과 비교해서 Hilt는 많은 장점들을 갖고 있다
- 손쉬운 사용과 보일러플레이트를 감소시킨다
- Jetpack 라이브러리와 함께 사용하기 좋다
- 테스트 및 마이그레이션 편의를 위해 다양한 API를 제공한다