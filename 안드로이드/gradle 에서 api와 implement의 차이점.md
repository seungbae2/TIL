# gradle 에서 api와 implement의 차이점

Gradle에서 `api`와 `implementation`은 프로젝트 의존성 관리에 사용되는 키워드입니다. 이 두 키워드의 주된 차이점은 해당 라이브러리 또는 모듈을 어디까지 노출시키는지에 있습니다.

1. **`api` 키워드:**
    - `api` 키워드를 사용하여 선언한 종속성은 해당 모듈을 사용하는 다른 모듈들에게 노출됩니다.
    - 다른 모듈이 이 모듈의 의존성을 사용할 수 있고, 컴파일 시에 해당 라이브러리가 클래스패스에 포함됩니다.
    - 예를 들어, `api 'com.google.guava:guava:30.1-android'`와 같이 사용될 수 있습니다.

```
// Module A의 build.gradle
dependencies {
    api 'com.google.guava:guava:30.1-android'
}
```

```
// Module B의 build.gradle
dependencies {
    implementation project(':moduleA')
}
```

1. **`implementation` 키워드:**
    - `implementation` 키워드를 사용하여 선언한 종속성은 해당 모듈 내부에서만 사용 가능합니다.
    - 다른 모듈에서는 이 종속성을 참조할 수 없습니다. 따라서 해당 라이브러리가 컴파일되는 동안 클래스패스에 노출되지 않습니다.
    - 이를 통해 모듈 간에 의존성을 좀 더 캡슐화하고, 변경이 생겼을 때 다른 모듈들에게 영향을 미치지 않도록 할 수 있습니다.

```
// Module A의 build.gradle
dependencies {
    implementation 'com.google.guava:guava:30.1-android'
}
```

```
// Module B의 build.gradle
dependencies {
    implementation project(':moduleA')
}
```

일반적으로, 외부 라이브러리나 모듈을 사용할 때는 `api`를 사용하여 다른 모듈들에게 노출시키고, 내부 모듈이나 유틸리티와 같이 다른 모듈에서 사용하지 않아야 하는 경우에는 `implementation`을 사용합니다. 이를 통해 모듈 간 의존성을 관리하고 불필요한 라이브러리 노출을 방지할 수 있습니다.