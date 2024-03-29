# UseCase

## UseCase를 사용하는 이유

1. **비즈니스 로직의 분리:**
UseCase는 주로 비즈니스 로직을 캡슐화하고 분리하는 역할을 한다. 이는 애플리케이션의 핵심 로직이 독립적으로 존재하고, 다른 레이어와 분리되어 있음을 의미한다. 이것은 코드의 응집성을 높이고 변경에 대한 영향을 최소화한다.
2. **테스트 용이성:**
UseCase를 사용하면 비즈니스 로직을 테스트하기가 쉬워진다. UseCase는 단일 책임 원칙에 따라 하나의 구체적인 작업을 수행하므로, 이를 단위 테스트하기가 더 편리하다.
3. **의존성 역전(Dependency Inversion):**
UseCase는 안드로이드 프레임워크나 외부 라이브러리에 대한 직접적인 의존성을 낮춘다. 이는 의존성 역전 원칙을 따르며, 안드로이드 프레임워크에 대한 의존성을 낮추면 테스트 용이성이 향상되고, 코드의 재사용성이 높아진다.
4. **비동기 작업 관리:**
UseCase는 비동기 작업을 처리하거나 백그라운드 스레드에서 실행되어야 하는 작업들을 효과적으로 관리할 수 있다. 이로써 UI 스레드에서의 블로킹을 최소화하고, 앱의 반응성을 유지할 수 있다.
5. **클린 아키텍처 적용:**
UseCase는 클린 아키텍처의 핵심 구성 요소 중 하나로 간주된다. 이 아키텍처 패턴은 소프트웨어를 레이어로 나누어 관리하며, 비즈니스 논리를 외부 요소와 분리하여 더욱 모듈화된 코드를 작성할 수 있도록 돕는다.

## UseCase를 만들 때 고려할 수 있는 기준

1. **단일 책임 원칙(Single Responsibility Principle):**
각 UseCase는 하나의 구체적인 작업에 책임을 가져야 한다. UseCase는 특정 비즈니스 로직이나 사용 사례를 처리해야 하며, 여러 역할을 수행하지 않아야 한다.
2. **사용 사례의 정의:**
UseCase는 사용자의 요구나 특정한 비즈니스 시나리오를 나타내야 한다. 즉, 애플리케이션에서 특정한 작업 또는 기능을 수행하는 단위여야 한다.
3. **의존성의 최소화:**
UseCase는 안드로이드 프레임워크나 외부 라이브러리에 대한 직접적인 의존성을 최소화해야 한다. 의존성 주입(Dependency Injection)을 통해 외부 의존성을 주입받을 수 있도록 설계하는 것이 좋다.
4. **테스트 용이성:**
UseCase는 테스트하기 쉬워야 한다. 비즈니스 로직을 포함하므로 단위 테스트를 쉽게 작성하고 실행할 수 있도록 설계되어야 한다.
5. **애플리케이션 레이어 간의 경계:**
UseCase는 도메인 레이어에 속하며, Presentation 레이어나 Data 레이어와 직접적으로 소통해야 한다. 이를 통해 각 레이어 간의 역할과 책임이 명확하게 나뉘어지며, 각 레이어는 독립적으로 테스트 가능하게 된다.
6. **유연성과 확장성:**
UseCase는 앱의 요구사항이 변경되거나 확장될 수 있는 유연성을 가지고 있어야 한다. 새로운 기능이나 변경사항이 생겼을 때 기존의 UseCase를 수정하지 않고 새로운 UseCase를 추가할 수 있도록 구조를 설계해야 한다.