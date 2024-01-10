# AndroidEntryPoint의 이해

## @AndroidEntryPoint가 지원하는 타입

- Activity
- Fragment
- View
- Service
- BroadcastReceiver (SingletonComponent 사용 only)

## @AndroidEntryPoint 주의사항

안드로이드 클래스에서 의존성 주입시, 상위 (서브)컴포넌트에도 반드시 @AndroidEntryPoint 선언

```kotlin
@AndroidEntryPoint
class MyActivity : ComponentActivity(){
// MyFragment 실행
}

@AndroidEntryPoint
class MyFragment : Fragment(){
// 의존성 주입
}
```

- Hilt는 ComponentActivity를 상속한 Activity만 지원
- Hilt는 androidx 라이브러리에 포함된 Fragment만 지원
- Android SDK에 포함된 Fragment는 Deprecated 되었으면 지원하지 않음

## 요약

1. Application은 컴포넌트, 나머지 타입은 서브 컴포넌트
2. 프레그먼트 인스턴스를 유지하려는 노력은 하지 말자
3. Fragment 범위에 바인딩 된 의존성을 View에 주입하는 경우 @WithFragmentBindings를 활용하자