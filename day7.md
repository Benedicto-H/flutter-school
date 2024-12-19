## Day 7 
# Flutter로 통신하는 앱 만들기

## StatelessWidget과 StatefulWidget

### StatelessWidget

- 상태 없음: `StatelessWidget`은 내부적으로 상태를 가지지 않습니다. 즉, 위젯이 생성된 후에는 그 모습이 변하지 않습니다.
- 불변성: 위젯의 속성(properties)이 변경되더라도 위젯 자체는 다시 생성됩니다. 기존 위젯이 변경되는 것이 아닙니다.
- 단순 UI 구성: 주로 정적인 UI 요소, 즉 사용자 상호 작용에 따라 변하지 않는 UI를 구성할 때 사용됩니다. 예를 들어, 텍스트 레이블, 아이콘, 이미지 등이 있습니다.
- build 메서드: `StatelessWidget`은 build 메서드를 오버라이드하여 UI를 구성합니다. 이 build 메서드는 위젯이 처음 생성될 때 한 번 호출됩니다. 부모 위젯이 다시 빌드될 때, 또는 위젯의 속성이 변경될 때 다시 호출될 수 있습니다.

```dart
// MyStatelessWidget은 외부에서 전달받은 message를 표시하는 텍스트 위젯입니다. message가 변경되면 위젯이 새로 생성되어 텍스트가 업데이트됩니다.

class MyStatelessWidget extends StatelessWidget {
  final String message;

  MyStatelessWidget({required this.message});

  @override
  Widget build(BuildContext context) {
    return Text(message);
  }
}
```

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('StatelessWidget 예제'),
        ),
        body: Center(
          child: MyStatelessWidget(message: '안녕하세요!'), // 메시지 전달
        ),
      ),
    );
  }
}

class MyStatelessWidget extends StatelessWidget {
  final String message;

  MyStatelessWidget({required this.message});

  @override
  Widget build(BuildContext context) {
    return Text(
      message,
      style: TextStyle(fontSize: 24), // 폰트 크기 설정
    );
  }
}
```

### StatefulWidget

- 상태 있음: `StatefulWidget`은 내부적으로 상태를 가집니다. 이 상태는 위젯의 모습이나 동작을 변경할 수 있습니다.
- 가변성: 위젯의 상태가 변경되면 Flutter 프레임워크는 해당 위젯을 다시 빌드하여 화면을 업데이트합니다.
- 동적 UI 구성: 사용자 상호 작용, 데이터 변경, 타이머 등 시간에 따른 변화에 따라 UI가 변경되어야 하는 경우에 사용됩니다. 예를 들어, 버튼 클릭에 따라 숫자가 증가하는 카운터, 텍스트 입력 필드, 체크박스 등이 있습니다.
- State 객체: `StatefulWidget`은 State 객체와 함께 사용됩니다. State 객체는 위젯의 상태를 관리하고, 상태가 변경될 때 위젯을 다시 빌드하는 역할을 합니다.
- setState 메서드: State 객체 내에서 setState() 메서드를 호출하면 Flutter 프레임워크에 상태가 변경되었음을 알리고, 위젯을 다시 빌드하도록 합니다.

```dart
//  MyStatefulWidget은 버튼을 클릭할 때마다 숫자가 증가하는 카운터 위젯입니다. _counter 변수가 상태를 나타내며, setState() 메서드를 통해 상태를 변경하고 화면을 업데이트합니다.

class MyStatefulWidget extends StatefulWidget {
  @override
  _MyStatefulWidgetState createState() => _MyStatefulWidgetState();
}

class _MyStatefulWidgetState extends State<MyStatefulWidget> {
  int _counter = 0;

  void _incrementCounter() {
    setState(() {
      _counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: <Widget>[
        Text('$_counter'),
        ElevatedButton(
          onPressed: _incrementCounter,
          child: Text('증가'),
        ),
      ],
    );
  }
}
```

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('StatefulWidget 예제'),
        ),
        body: Center(
          child: MyStatefulWidget(),
        ),
      ),
    );
  }
}

class MyStatefulWidget extends StatefulWidget {
  @override
  _MyStatefulWidgetState createState() => _MyStatefulWidgetState();
}

class _MyStatefulWidgetState extends State<MyStatefulWidget> {
  int _counter = 0;

  void _incrementCounter() {
    setState(() {
      _counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.center, // Column을 중앙 정렬
      children: <Widget>[
        Text(
          '$_counter',
          style: TextStyle(fontSize: 48), // 폰트 크기 크게 설정
        ),
        SizedBox(height: 20), // 버튼과 텍스트 사이 간격 추가
        ElevatedButton(
          onPressed: _incrementCounter,
          child: Text(
            '증가',
            style: TextStyle(fontSize: 24), // 버튼 텍스트 크기 설정
          ),
        ),
      ],
    );
  }
}
```

어떤 위젯을 사용해야 할지 결정하는 기준은 위젯의 상태가 변경될 필요가 있는지 여부입니다. UI가 사용자 상호 작용이나 다른 요인에 의해 변경되어야 한다면 `StatefulWidget`을 사용해야 합니다. 그렇지 않다면 `StatelessWidget`을 사용하는 것이 좋습니다. `StatelessWidget`은 `StatefulWidget`보다 가볍고 성능상 이점이 있습니다.



| 특징           | StatelessWidget                           | StatefulWidget                               |
| -------------- | ---------------------------------------- | ------------------------------------------- |
| 상태           | 없음                                     | 있음                                        |
| 가변성         | 불변                                     | 가변                                        |
| UI             | 정적                                     | 동적                                        |
| 주요 사용 사례 | 텍스트, 아이콘, 이미지 등 변하지 않는 UI | 버튼, 입력 필드, 체크박스 등 변하는 UI |
| 핵심 메서드     | `build`                                 | `createState`, `setState`, `build`         |



(계속 준비중)

