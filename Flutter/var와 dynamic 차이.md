# var와 dynamic 차이

Dart에는 변수 선언시 다양한 자료형을 지원한다.

var와 dynamic는 일반적인자료형이 아니라 입력된 정보를 통해 타입을 추론해서 데이터 형식을 저장한다.

## var

추론된 타입이 한번 입력되고 나면 다른 타입을 저장할 수 없다.

```dart
var name = 'var test';
print(name); // 출력 var test;
name = 123; // error
```

## dynamic

var와의 차이점은 어떤 형식이라도 항상 입력이 가능하다.

```dart
dynamic name = 'var test';
print(name); // 출력 var test
name = 123;
print(name); // 123 error 발생하지 않는다
```