# 5 UseCase mistakes

1. 1개의 UseCase에 2개 이상의 public 함수가 있으면 안된다. 한개의 public 함수만 있어야 한다. Single Responsibility principle 위배
2. UseCase는 비지니스 로직을 의미해야 한다. 도메인 계층에 있다는 것은 비지니스 로직을 가져야 한다는 것을 의미한다.  예를 들어 데이터 formatting 같은 것은 presentation layer에 있어야 한다. FormatSocialStateUseCase 
3. UseCase에서는 안드로이드 SDK 참조를 하지 말아야 한다. 도메인 계층은 다른 모듈이나 안드로이드 SDK에 독립하여 실행되어야 한다. Keep isolate
4. UseCase에서 추상화는 가급적 피하라
5. UseCase에서 UI에서 쓸 Result에 대한 성공 실패 등 여부를 결정해줄 필요는 없다. 그것은 presentation layer의 역할이다