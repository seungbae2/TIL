# Entry Point

Hilt 의존성 주입이 어려운 코드에서 바인딩 된 의존성을 참조하는 방법

EntryPoint는 interface로 선언해야 한다.

EntryPoint는 언제 사용할까?

- Hilt를 사용하지 않는 라이브러리에서 의존성 주입이 어려울 때
- Hilt가 지원하지 않는 안드로이드 컴포넌트에 의존성 주입이 어려울 때
- Dynamic Feature Module에 의존성 주입이 필요한 경우

EntryPoint 인터페이스에 접근할 때는 EntryPointAccessors메소드를 이용한다.

EntryPointAccessors 메서드

- fromApplication
- fromActivity
- fromFragment
- fromView