## Day 6 
# Flutter와 위젯과 레이아웃

## 주요위젯

### Text
텍스트를 표시
```dart
Text('안녕하세요, Flutter!');
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
          title: Text('텍스트 예제'),
        ),
        body: Center(
          child: Text(
            '안녕하세요, Flutter!',
            style: TextStyle( // 스타일을 추가하여 가독성을 높임
              fontSize: 24.0,
              fontWeight: FontWeight.bold,
              color: Colors.blue,
            ),
          ),
        ),
      ),
    );
  }
}
```

### Image
이미지를 표시
```dart
Image.asset('assets/my_image.png'); // assets 폴더에 있는 이미지 사용
```

### Icon
아이콘을 표시
```dart
Icon(Icons.home);
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
          title: Text('아이콘 예제'),
        ),
        body: Center( // 아이콘을 화면 중앙에 배치
          child: Column( // 아이콘과 텍스트를 함께 보여주기 위해 Column 사용
            mainAxisAlignment: MainAxisAlignment.center, // Column 내 요소 중앙 정렬
            children: [
              Icon(
                Icons.home, // 홈 아이콘
                size: 50.0, // 아이콘 크기 설정
                color: Colors.blue, // 아이콘 색상 설정
              ),
              SizedBox(height: 10), // 아이콘과 텍스트 사이 간격 추가
              Text("홈 아이콘"), // 아이콘 설명 텍스트
            ],
          ),
        ),
      ),
    );
  }
}
```


### Container
다른 위젯을 감싸고 스타일을 적용하는 위젯
```dart
Container(
  padding: EdgeInsets.all(16.0),
  decoration: BoxDecoration(
    color: Colors.blue,
  ),
  child: Text('컨테이너 예제'),
);
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
          title: Text('컨테이너 예제'),
        ),
        body: Center( // 컨테이너를 화면 중앙에 배치
          child: Container(
            padding: EdgeInsets.all(16.0), // 모든 방향으로 16픽셀의 패딩
            decoration: BoxDecoration(
              color: Colors.blue, // 배경색을 파란색으로 설정
              borderRadius: BorderRadius.circular(10.0), // 모서리를 둥글게 설정
              boxShadow: [ // 그림자 효과 추가
                BoxShadow(
                  color: Colors.grey.withOpacity(0.5),
                  spreadRadius: 5,
                  blurRadius: 7,
                  offset: Offset(0, 3), // 그림자 위치 조정
                ),
              ],
            ),
            child: Text(
              '컨테이너 예제',
              style: TextStyle(
                color: Colors.white, // 텍스트 색상을 흰색으로 설정
                fontSize: 20.0,
                fontWeight: FontWeight.bold,
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```

### Row
위젯을 가로로 배치하는 위젯
```dart
Row(
  children: [
    Icon(Icons.star),
    Text('별'),
  ],
);
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
          title: Text('Row 예제'),
        ),
        body: Center( // Row를 화면 중앙에 배치
          child: Container( // Row 주변에 여백을 주기 위한 Container
            padding: EdgeInsets.all(20),
            decoration: BoxDecoration(
              border: Border.all(color: Colors.black), //테두리 추가
            ),
            child: Row(
              mainAxisAlignment: MainAxisAlignment.spaceAround, // 주축 정렬 방식 설정
              crossAxisAlignment: CrossAxisAlignment.center, // 교차축 정렬 방식 설정
              mainAxisSize: MainAxisSize.min, // Row의 크기를 내용물에 맞게 조절
              children: [
                Icon(
                  Icons.star,
                  size: 40,
                  color: Colors.amber,
                ),
                SizedBox(width: 10), // 아이콘과 텍스트 사이 간격 추가
                Text(
                  '별',
                  style: TextStyle(fontSize: 24),
                ),
                SizedBox(width: 10),
                ElevatedButton(onPressed: (){}, child: Text("버튼"))
              ],
            ),
          ),
        ),
      ),
    );
  }
}
```

### Column
위젯을 세로로 배치하는 위젯
```dart
Column(
  children: [
    Text('위'),
    Text('아래'),
  ],
);
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
          title: Text('Column 예제'),
        ),
        body: Center( // Column을 화면 중앙에 배치
          child: Container( // Column 주변에 여백을 주기 위한 Container
            padding: EdgeInsets.all(20),
            decoration: BoxDecoration(
              border: Border.all(color: Colors.black),
            ),
            child: Column(
              mainAxisAlignment: MainAxisAlignment.spaceAround, // 주축 정렬 방식 설정
              crossAxisAlignment: CrossAxisAlignment.center, // 교차축 정렬 방식 설정
              mainAxisSize: MainAxisSize.min, // Column의 크기를 내용물에 맞게 조절
              children: [
                Text(
                  '위',
                  style: TextStyle(fontSize: 24),
                ),
                SizedBox(height: 10), // 텍스트 사이 간격 추가
                Text(
                  '아래',
                  style: TextStyle(fontSize: 24),
                ),
                SizedBox(height: 10),
                ElevatedButton(onPressed: (){}, child: Text("버튼"))
              ],
            ),
          ),
        ),
      ),
    );
  }
}
```

## 레이아웃

### Center
위젯을 가운데 정렬
```dart
Center(
  child: Text('가운데'),
);
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
          title: Text('Center 예제'),
        ),
        body: Center(
          child: Container( // Center된 영역을 시각적으로 확인하기 위한 Container
            padding: EdgeInsets.all(20),
            decoration: BoxDecoration(
              border: Border.all(color: Colors.black),
            ),
            child: Text(
              '가운데',
              style: TextStyle(fontSize: 24),
            ),
          ),
        ),
      ),
    );
  }
}
```

### Padding
위젯의 여백을 설정
```dart
Padding(
  padding: EdgeInsets.all(20.0),
  child: Text('여백'),
);
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
          title: Text('Padding 예제'),
        ),
        body: Center( // Padding된 영역을 확인하기 쉽게 Center로 감쌈
          child: Container( // Padding 영역을 시각적으로 확인하기 위한 Container
            decoration: BoxDecoration(
              border: Border.all(color: Colors.black), // 테두리 추가
            ),
            child: Padding(
              padding: EdgeInsets.all(20.0),
              child: Text(
                '여백',
                style: TextStyle(fontSize: 24),
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```

### Expanded
부모 위젯의 남은 공간을 채우도록 위젯을 확장
```dart
Row(
  children: [
    Expanded(
      child: Container(color: Colors.red),
    ),
    Expanded(
      flex: 2, // 다른 Expanded 위젯보다 2배의 공간 차지
      child: Container(color: Colors.blue),
    ),
  ],
);
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
          title: Text('Expanded 예제'),
        ),
        body: Column( // Expanded를 포함하는 Row를 Column으로 감싸서 화면 전체를 채우도록 함
          children: [
            Expanded( // Column의 남은 공간을 모두 채우도록 Expanded 적용
              child: Row(
                children: [
                  Expanded(
                    child: Container(
                      color: Colors.red,
                      child: Center(child: Text('1', style: TextStyle(color: Colors.white))), // 내용 추가
                    ),
                  ),
                  Expanded(
                    flex: 2,
                    child: Container(
                      color: Colors.blue,
                      child: Center(child: Text('2', style: TextStyle(color: Colors.white))),// 내용 추가
                    ),
                  ),
                ],
              ),
            ),
            Expanded(child: Container(color: Colors.green, child: Center(child: Text('아래', style: TextStyle(color: Colors.white))))),
          ],
        ),
      ),
    );
  }
}
```

### ListView
스크롤 가능한 목록을 생성
```dart
ListView(
  children: [
    ListTile(title: Text('항목 1')),
    ListTile(title: Text('항목 2')),
    ListTile(title: Text('항목 3')),
  ],
);
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
          title: Text('ListView 예제'),
        ),
        body: ListView(
          padding: const EdgeInsets.all(8), // ListView 주변에 여백 추가
          children: <Widget>[
            ListTile(
              leading: Icon(Icons.star), // leading 아이콘 추가
              title: Text('항목 1'),
              trailing: Icon(Icons.arrow_forward_ios), // trailing 아이콘 추가
              onTap: () { // 탭 이벤트 처리
                print('항목 1 탭!');
              },
            ),
            Divider(height: 1, thickness: 1,), // 항목 사이에 구분선 추가
            ListTile(
              leading: Icon(Icons.android),
              title: Text('항목 2'),
              subtitle: Text('부제목'), // 부제목 추가
              onLongPress: (){ // 길게 누르기 이벤트 처리
                print("항목 2 롱프레스!");
              },
            ),
            Divider(height: 1, thickness: 1,),
            ListTile(
              title: Text('항목 3'),
              dense: true, // ListTile의 높이를 줄임
              tileColor: Colors.grey[200], // ListTile 배경색 설정
            ),
          ],
        ),
      ),
    );
  }
}
```

## 네비게이션

### Navigator.push
새로운 화면으로 이동
```dart
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => SecondScreen()),
);
```

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(home: FirstScreen()));
}

class FirstScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('첫 번째 화면')),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            Navigator.push(
              context,
              MaterialPageRoute(builder: (context) => SecondScreen()),
            );
          },
          child: Text('두 번째 화면으로 이동'),
        ),
      ),
    );
  }
}

class SecondScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('두 번째 화면')),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            Navigator.pop(context);
          },
          child: Text('첫 번째 화면으로 돌아가기'),
        ),
      ),
    );
  }
}
```

## 예제코드 1

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(CalculatorApp());
}

class CalculatorApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: CalculatorScreen(),
    );
  }
}

class CalculatorScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('계산기'),
      ),
      body: Padding(
        padding: const EdgeInsets.all(8.0), // 화면 여백 추가
        child: Column( // 버튼들을 세로로 배치하기 위해 Column 사용
          children: [
            Row( // 숫자 버튼들을 가로로 배치
              mainAxisAlignment: MainAxisAlignment.spaceEvenly,
              children: [
                buildNumberButton('1'),
                buildNumberButton('2'),
                buildNumberButton('3'),
                buildNumberButton('4'),
              ],
            ),
            SizedBox(height: 8), // 버튼 사이 간격 추가
            Row(
              mainAxisAlignment: MainAxisAlignment.spaceEvenly,
              children: [
                buildNumberButton('5'),
                buildNumberButton('6'),
                buildNumberButton('7'),
                buildNumberButton('8'),
              ],
            ),
            SizedBox(height: 8),
            Row(
              mainAxisAlignment: MainAxisAlignment.spaceEvenly,
              children: [
                buildNumberButton('9'),
                buildNumberButton('0'),
              ],
            ),
          ],
        ),
      ),
    );
  }

  // 숫자 버튼 생성 함수
  Widget buildNumberButton(String number) {
    return Expanded( // 버튼이 Row 내에서 균등하게 공간을 차지하도록 함
      child: Padding( // 버튼 주변에 여백 추가
        padding: const EdgeInsets.all(4.0),
        child: ElevatedButton(
          onPressed: () {
            // 버튼 클릭 시 동작 (추후 계산 로직 추가)
            print('$number 버튼 클릭!');
          },
          child: Text(
            number,
            style: TextStyle(fontSize: 24), // 텍스트 크기 조정
          ),
        ),
      ),
    );
  }
}
```

## 예제코드 2

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(CalculatorApp());
}

class CalculatorApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: CalculatorScreen(),
    );
  }
}

class CalculatorScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('계산기'),
      ),
      body: Padding(
        padding: const EdgeInsets.all(8.0),
        child: Column(
          children: [
            buildNumberRow(['1', '2', '3', '4'], context), // 수정된 부분
            SizedBox(height: 8),
            buildNumberRow(['5', '6', '7', '8'], context), // 수정된 부분
            SizedBox(height: 8),
            buildNumberRow(['9', '0'], context), // 수정된 부분
          ],
        ),
      ),
    );
  }

  // 숫자 버튼 행 생성 함수 (수정됨)
  Widget buildNumberRow(List<String> numbers, BuildContext context) {
    return Row(
      mainAxisAlignment: MainAxisAlignment.spaceEvenly,
      children: numbers.map((number) {
        return Expanded(
          child: Padding(
            padding: const EdgeInsets.all(4.0),
            child: ElevatedButton(
              onPressed: () {
                // 네비게이션 코드 추가
                Navigator.push(
                  context,
                  MaterialPageRoute(
                    builder: (context) => ResultScreen(selectedNumber: number),
                  ),
                );
              },
              child: Text(
                number,
                style: TextStyle(fontSize: 24),
              ),
            ),
          ),
        );
      }).toList(),
    );
  }
}

// 결과를 보여주는 새로운 화면
class ResultScreen extends StatelessWidget {
  final String selectedNumber;

  const ResultScreen({required this.selectedNumber});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('선택된 숫자'),
      ),
      body: Center(
        child: Text(
          '선택된 숫자: $selectedNumber',
          style: TextStyle(fontSize: 32),
        ),
      ),
    );
  }
}
```

### 예제코드 3

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(CalculatorApp());
}

class CalculatorApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: CalculatorScreen(),
    );
  }
}

class CalculatorScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    List<String> numbers = List.generate(10, (index) => index.toString());

    return Scaffold(
      appBar: AppBar(
        title: Text('숫자 선택'),
      ),
      body: Center( // Center 위젯으로 중앙 정렬
        child: Padding(
          padding: const EdgeInsets.all(16.0),
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center, // Column 내부 중앙 정렬
            children: numbers.map((number) => buildNumberButton(number, context)).toList(),
          ),
        ),
      ),
    );
  }

  Widget buildNumberButton(String number, BuildContext context) {
    return Padding( // 버튼 사이에 간격 추가
      padding: const EdgeInsets.symmetric(vertical: 8.0),
      child: SizedBox( // 버튼 크기 고정
        width: double.infinity, // 부모의 가로 폭에 맞춤
        child: ElevatedButton(
          onPressed: () {
            Navigator.push(
              context,
              MaterialPageRoute(
                builder: (context) => ResultScreen(selectedNumber: number),
              ),
            );
          },
          child: Text(
            number,
            style: TextStyle(fontSize: 24),
          ),
        ),
      ),
    );
  }
}

class ResultScreen extends StatelessWidget {
  final String selectedNumber;

  const ResultScreen({required this.selectedNumber});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('선택된 숫자'),
      ),
      body: Center(
        child: Text(
          '선택된 숫자: $selectedNumber',
          style: TextStyle(fontSize: 32),
        ),
      ),
    );
  }
}
```