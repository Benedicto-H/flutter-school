## Day 7 
# Flutter로 상태 관리하기

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



## InheritedWidget

Flutter에서 InheritedWidget은 **위젯 트리 내에서 데이터를 공유하는 효과적인 방법**입니다. 특정 위젯에서 설정된 데이터를 하위 위젯들이 필요할 때마다 쉽게 접근할 수 있도록 해줍니다. 이는 복잡한 위젯 트리에서 데이터 전달을 간소화하고, 상태 관리를 더욱 효율적으로 만들어줍니다.

- 위젯 트리 전반에 데이터 공유 : 위젯 트리의 깊은 곳에 있는 위젯까지도 상위 위젯에서 설정된 데이터에 쉽게 접근할 수 있습니다.
- Provider 패턴의 기반 : Flutter의 상태 관리 패턴인 Provider는 InheritedWidget을 기반으로 구축되었습니다.
- 복잡한 상태 관리 간소화 : 여러 위젯에서 공유되는 데이터를 중앙 집중식으로 관리하여 코드를 간결하게 만들 수 있습니다.

### 작성 방법
1. InheritedWidget 클래스 생성
   * `InheritedWidget` 클래스를 상속받아 새로운 클래스를 만듭니다.
   * 공유할 데이터를 클래스의 필드로 선언합니다.
   * `of` 메서드를 구현하여 하위 위젯에서 데이터에 접근할 수 있도록 합니다.
   * `updateShouldNotify` 메서드를 재정의하여 데이터가 변경될 때 위젯을 다시 렌더링할지 여부를 결정합니다.

2. 위젯 트리에 추가
   * 공유하고 싶은 데이터를 가지고 있는 위젯의 상위에 생성한 InheritedWidget을 위치시킵니다.

3. 하위 위젯에서 데이터 사용
   * `of` 메서드를 사용하여 데이터에 접근합니다.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: MyInheritedWidget(
        color: Colors.blue,
        child: Scaffold(
          appBar: AppBar(
            title: Text('InheritedWidget Example'),
          ),
          body: Center(
            child: MyTextWidget(),
          ),
        ),
      ),
    );
  }
}

class MyInheritedWidget extends InheritedWidget {
  final Color color;

  const MyInheritedWidget({
    Key? key,
    required this.color,
    required Widget child,
  }) : super(key: key, child: child);

  static MyInheritedWidget? of(BuildContext context) {
    return context.dependOnInheritedWidgetOfExactType<MyInheritedWidget>();
  }

  @override
  bool updateShouldNotify(MyInheritedWidget oldWidget) {
    return color != oldWidget.color;
  }
}

class MyTextWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final color = MyInheritedWidget.of(context)!.color;
    return Text('색상은 $color 입니다.', style: TextStyle(color: color));
  }
}
```

- Provider 패키지 : Flutter에서 Provider 패키지를 사용하면 InheritedWidget을 더욱 편리하게 사용할 수 있습니다. Provider는 InheritedWidget을 기반으로 구축된 상태 관리 패턴으로, 복잡한 상태 관리를 간소화하는 데 도움을 줍니다.
- 주의 사항 : InheritedWidget은 위젯 트리 전체에 영향을 미칠 수 있으므로, 너무 많은 데이터를 공유하면 성능 저하가 발생할 수 있습니다. 필요한 데이터만 공유하고, 불필요한 위젯의 재렌더링을 방지하기 위해 `updateShouldNotify` 메서드를 적절히 사용해야 합니다.

## ValueChanged

Flutter에서 `ValueChanged`는 특정 값이 변경될 때 호출되는 콜백 함수의 시그니처를 나타내는 타입입니다. 즉, 어떤 값이 변경되면 이에 대한 알림을 받고 원하는 동작을 수행할 수 있도록 해줍니다. 주로 사용자 입력이나 상태 변경에 따른 반응을 처리하는 데 활용됩니다.

```dart
typedef ValueChanged<T> = void Function(T value);
```

- 상태 관리 : 위젯의 상태가 변경될 때마다 자동으로 UI를 업데이트할 수 있습니다.
- 사용자 입력 처리 : 버튼 클릭, 텍스트 입력 등 사용자의 입력에 따라 특정 함수를 호출할 수 있습니다.
- 데이터 전달 : 부모 위젯에서 자식 위젯으로 데이터를 전달하고, 자식 위젯에서 데이터가 변경될 때 부모 위젯에 알릴 수 있습니다.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter 텍스트 입력 예제',
      home: Scaffold(
        appBar: AppBar(
          title: Text('텍스트 입력'),
        ),
        body: Center(
          child: MyTextField(
            onChanged: (value) {
              // 텍스트 필드 값이 변경될 때 실행되는 함수
              print('입력된 값: $value');
            },
          ),
        ),
      ),
    );
  }
}

class MyTextField extends StatefulWidget {
  final ValueChanged<String> onChanged;

  const MyTextField({Key? key, required this.onChanged}) : super(key: key);

  @override
  _MyTextFieldState createState() => _MyTextFieldState();
}

class _MyTextFieldState extends State<MyTextField> {
  final TextEditingController _controller = TextEditingController();

  @override
  void initState() {
    super.initState();
    _controller.addListener(() {
      widget.onChanged(_controller.text);
    });
  }

  @override
  Widget build(BuildContext context) {
    return TextField(
      controller: _controller,
      onChanged: (value) {
        // 여기에 값이 변경될 때 실행할 코드를 작성합니다.
      },
    );
  }
}
```

## ChangeNotifier

Flutter에서 ChangeNotifier는 상태 관리를 위한 강력한 도구입니다. 특정 값이 변경될 때마다 관찰자들에게 알림을 보내, UI를 자동으로 업데이트할 수 있도록 해줍니다. 이는 복잡한 상태 관리를 간소화하고, 앱의 반응성을 높이는 데 효과적입니다.

- `ChangeNotifierProvider` : 위젯 트리에 ChangeNotifier 인스턴스를 제공하고, 하위 위젯에서 이를 사용할 수 있도록 해줍니다.
- `Consumer` : ChangeNotifier의 상태 변화를 감지하고, UI를 업데이트하는 위젯입니다.
- `notifyListeners()` : ChangeNotifier의 상태가 변경될 때 호출하여 모든 관찰자에게 알립니다.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class CounterModel {
  int _count = 0;

  int get count => _count;

  void increment() {
    _count++;
    // DartPad에서는 notifyListeners()를 사용할 수 없으므로, 직접 상태 변경을 감지하고 UI를 업데이트해야 합니다.
  }
}

class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  CounterModel counter = CounterModel();

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('카운터 앱'),
        ),
        body: Center(
          child: Text('버튼을 ${counter.count}번 클릭했습니다.',
              style: TextStyle(fontSize: 24)),
        ),
        floatingActionButton: FloatingActionButton(
          onPressed: () {
            setState(() {
              counter.increment();
            });
          },
          child: Icon(Icons.add),
        ),
      ),
    );
  }
}
```

## ValueNotifier

ValueNotifier는 단일 값의 변경을 감지하고, 이를 수신 대상에게 알려주는 간단한 상태 관리 클래스입니다. ChangeNotifier를 상속받으며, 주로 단순한 값의 변경을 알리고 싶을 때 사용합니다.

### ValueNotifier의 장점

- 간단한 상태 관리 : 단일 값의 변경을 간단하게 관리할 수 있습니다.
- 자동 UI 업데이트 : 값이 변경될 때마다 ValueListenableBuilder를 통해 자동으로 UI가 업데이트됩니다.

### ValueNotifier의 단점

- 복잡한 상태 관리에는 부적합 : 여러 개의 값을 관리하거나 복잡한 상태 로직이 필요한 경우에는 ChangeNotifier 또는 상태 관리 라이브러리를 사용하는 것이 더 적합합니다.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class ThemeModel extends ValueNotifier<ThemeMode> {
  ThemeModel(ThemeMode initialTheme) : super(initialTheme);
}

class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  final ThemeModel themeModel = ThemeModel(ThemeMode.light);

  void toggleTheme() {
    themeModel.value = themeModel.value == ThemeMode.light ? ThemeMode.dark : ThemeMode.light;
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      themeMode: themeModel.value,
      theme: ThemeData.light(),
      darkTheme: ThemeData.dark(),
      home: Scaffold(
        appBar: AppBar(
          title: Text('테마 변경 앱'),
        ),
        body: Center(
          child: ValueListenableBuilder<ThemeMode>(
            valueListenable: themeModel,
            builder: (context, value, child) {
              return Text(value == ThemeMode.light ? '밝은 테마' : '어두운 테마');
            },
          ),
        ),
        floatingActionButton: FloatingActionButton(
          onPressed: toggleTheme,
          child: Icon(Icons.brightness_4),
        ),
      ),
    );
  }
}
```

### ValueNotifier vs ChangeNotifier

- ValueNotifier : 단일 값의 변경을 감지하고 알리는 데 특화되어 있습니다.
- ChangeNotifier : 여러 개의 값을 관리하고, 복잡한 상태 로직을 구현할 수 있습니다.

### 어떤 것을 사용해야 할까요?

- 단순한 상태 관리 : ValueNotifier
- 복잡한 상태 관리 : ChangeNotifier 또는 상태 관리 라이브러리 (Provider, Riverpod 등)
