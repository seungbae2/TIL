# dart 비동기 기초

```dart
/// async / await / Future : 1회만 응답을 돌려받는 경우
Future<void> todo(int second) async {
	await Future.delayed(Duration(seconds: second));
	print('TODO Done in $second seconds');
}
todo(3);
todo(1);
todo(5);

// TODO Done in 1 seconds
// TODO Done in 3 seconds
// TODO Done in 5 seconds
```

```dart
/// async* / yield / Stream : 지속적으로 응답을 돌려받는 경우
Stream<int> todo() async* {
	int counter = 0;
	while(counter <= 10) {
	  counter++;
	  await Future.delayed(Duration(seconds: 1));
	  print('TODO is Running $counter');
	  yield counter;
	}
}

todo().listen((event) {});

// TODO is Running 1
// TODO is Running 2
// TODO is Running 3
// TODO is Running 4
// TODO is Running 5
// TODO is Running 6
// TODO is Running 7
// TODO is Running 8
// TODO is Running 9
// TODO is Running 10
// TODO is Running 11

```