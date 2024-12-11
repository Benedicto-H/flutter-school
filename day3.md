## Day 3 
# Dart 언어

## 객체지향 프로그래밍

```dart
class Person {

  // property
  String name = '';
  int age = 0;

  // method
  void sayHello() {
    print('안녕하세요, 저는 $name입니다.');
  }
}

void main() {
  // instance 생성
  Person person1 = Person();

  // instance property에 값 할당
  person1.name = '홍길동';
  person1.age = 20;

  // instance method 호출
  person1.sayHello();
}
```

접근 지정자
- public: 어디서든 접근 가능 (default)
- private: 클래스 내부에서만 접근 가능 (클래스 이름 앞에 언더바(_)를 붙여 표기)
- protected: 클래스와 자식 클래스에서만 접근 가능

```dart
class Person {
  String _name; // private
  int age; // public

  Person(this._name, this.age);

  String get name => _name;
  set name(String newName) {
    _name = newName;
  }
}
```

생성자

```dart
class Person {
  String name;
  int age;

  // 생성자
  Person(this.name, this.age);

  void sayHello() {
    print('안녕하세요, 저는 $name입니다. 나이는 $age살입니다.');
  }
}

void main() {
  Person person = Person('홍길동', 20);
  person.sayHello();
}
```

getter와 setter
- getter: 객체의 속성 값을 읽어올 때 호출되는 메서드입니다.
- setter: 객체의 속성 값을 설정할 때 호출되는 메서드입니다.

```dart
class Person {
  String _name = ''; // private 변수

  // getter
  String get name {
    return _name;
  }

  // setter
  set name(String newName) {
    _name = '$newName 님';
  }
}

void main() {
  Person person1 = Person();
  person1.name = 'Ned';

  print('Hello ${person1.name}');
}
```

상속
- extends: 다른 클래스를 상속받아 새로운 클래스를 정의합니다.
- super: 부모 클래스의 생성자를 호출합니다.

```dart
class Person {
  String name = '';
  int age = 0;

  Person(String name, int age);
}

class Student extends Person {
  int studentId = 0;

  Student(String name, int age, this.studentId) : super(name, age);
}

void main() {
  Person person1 = Person('Ned', 13);
  Student student = Student('Tuna', 12, 20241211);
}
```

추상 클래스
- abstract: 추상 메서드를 포함하는 클래스
- `@override`: 부모 클래스의 메서드를 재정의할 때 사용

```dart
abstract class Shape {
  double get area;
}

class Circle extends Shape {
  double radius;

  Circle(this.radius);

  @override
  double get area => 3.14 * radius * radius;
}

void main() {
  Circle circle = Circle(10);
  print(circle.area);
}
```

with 믹스인
- mixin: 클래스에 추가 기능을 제공하는 방법

```dart
mixin Logger {
  void log(String message) {
    print(message);
  }
}

class Person with Logger {
  // ...
}
```

열거형
- 상수를 정의하는 특수한 형태의 클래스

```dart
enum Color { red, green, blue }

void main() {
  Color favoriteColor = Color.blue;

  switch (favoriteColor) {
    case Color.red:
      print('좋아하는 색깔은 빨간색입니다.');
      break;
    case Color.green:
      print('좋아하는 색깔은 초록색입니다.');
      break;
    case Color.blue:
      print('좋아하는 색깔은 파란색입니다.');
      break;
  }
}
```