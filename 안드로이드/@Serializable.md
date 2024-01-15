# @Serializable

### **Kotlinx Serialization이란?**

**[kotlinx Serialization](https://github.com/Kotlin/kotlinx.serialization)**은 JetBrains에서 만든, 말 그대로 Kotlin을 위한 JSON 라이브러리이다.

### Kotiln Serialization의 특징

1. 빠른 JSON 인코딩 & 디코딩을 지원
2. 멀티플랫폼을 지원
    
    자주 사용하는 Gson과 Moshi는 모두 자바 라이브러리이므로, 자바를 지원하는 플랫폼(ex 안드로이드, Spring FrameWork 등)에서만 사용할 수 있다. 하지만 Kotlinx Serialization 라이브러리는 자바, 자바스크립트, 네이티브 등 다양한 플랫폼을 지원하기때문에 공용 라이브러리에 구현해서 사용할 수 있다.
    
3. 코틀린을 지향
    
    Gson 라이브러리로 파싱했을때, default value는 무시하고 0이 되며, Not-Nullable 타입이 null이 되는 문제가 있다. 하지만 Kotlinx Serialization 라이브러리를 사용하면 해당 변수에 프로퍼티를 포함하고 있지 않음을 확인해서 null 대신 기본값을 대입합니다! (이 부분은 밑의 코드에서 확인하실 수 있습니다!)
    
4. 컴파일 안전을 보장
    
    다른 라이브러리와는 다르게 Kotlinx Serialization 라이브러리는 @Serializable 어노테이션이 있는 클래스만 직렬화하기때문에, 직렬화를 수행할 수 없는 경우 런타임 에러 대신 컴파일 에러가 발생하므로 버그를 사전에 방지할 수 있다.