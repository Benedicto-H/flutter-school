## Day 1 
# Dart 언어

## 함수

함수는 반환할 타입을 앞에 두고 함수 이름 순서로 작성합니다. void는 반환할 내용이 없다는 뜻입니다. void은 생략 가능합니다.

```dart
void sayHello() {
  print('Hello World');
}

sayHi() {
  print('Hi World');
}

void main() {
  sayHello();
  sayHi();
}
```

매개변수는 함수 이름에 이어지는 괄호 안에 타입과 이름 순서로 작성합니다. 반환할 내용은 return문으로 처리합니다.

```dart
String sayHello(String name) {
  return 'Hello $name';
}

void main() {
  String greeting = sayHello('Ned');
  print(greeting);
}
```

```dart
String sayHello(String greeting, String name) {
  return '$greeting $name';
}

void main() {
  String message = sayHello('Hello', 'Ned');
  print(message);
}
```

print문은 대표적인 함수입니다. $를 활용해 문자열보간법 구현이 가능합니다.

```dart
void main() {
  int age = 13;
  String name = 'Ned';
  
  print('$name is $age years old.');
}
```

클래스 밖에서 존재하고 호출되는 함수는 최상위 함수라고 부릅니다. 클래스 안에 존재하는 함수는 메서드로 부릅니다.

```dart
void sayHello(int age, String name) {
  print('$name is $age years old.');
}

void main() {
  int age = 13;
  String name = 'Ned';

  sayHello(age, name);
}
```

익명 함수((anonymous function)은 이름이 없는 함수를 말합니다. 익명 함수란 이름이 없는 함수로, 다른 함수의 인자로 전달하거나 변수에 할당하여 사용할 수 있는 함수를 의미합니다. 일반적인 함수처럼 매개변수와 반환값을 가질 수 있으며, 함수의 본체에는 실행될 코드가 들어갑니다.

익명 함수는 변수에 할당, 다른 함수의 인자로 전달, 콜백 함수로 사용합니다. 익명 함수는 함수 본체가 복잡할 때 유용합니다. 중괄호를 사용하여 함수 본체를 감싸는 것이 특징입니다.

```
(매개변수) {
  // 함수 본체
}
```

```dart
void main() {
  var greet = (String name) {
    print('Hello, $name!');
  };
  greet('Alice');
}
```

화살표 함수(Fat Arrow Function) 또는 람다식(Lambda Expression)이라 부르는 함수도 있습니다. 람다식은 익명 함수의 간결한 표현 방식입니다. => 기호 뒤에 반환할 값을 직접 작성할 수 있습니다. 람다식은 익명 함수와 동일하게 사용됩니다. 간단한 연산이나 값을 반환할 때 매우 효율적입니다.

```
(매개변수) => 표현식;
```

```dart
void main() {
  // 람다 표현식
  var greet = (String name) => print('Hello, $name!');
  greet('Bob');

  // 람다 표현식을 이용한 리스트 처리
  var numbers = [1, 2, 3, 4, 5];
  numbers.forEach((number) => print(number * 2));

  // 람다 표현식을 이용한 조건문
  var isEven = (int number) => number % 2 == 0;
  print(isEven(4)); // 출력: true
}
```

함수 정의에서 {}로 감싼 매개변수는 선택사항이 됩니다. 호출할 때 매개변수명을 값 앞에 써서 사용하기 때문에 명명된 매개변수(named parameter)라고 부릅니다. 매개변수의 이름으로 직접 값을 전달하기 때문에 순서를 신경쓰지 않아도 됩니다. 대신 함수 선언에 기본값을 정해줄 필요가 있습니다.

```dart
void printPersonInfo({String name = 'Ned', int age = 13, String city = '수원'}) {
  print('이름: $name, 나이: $age, 도시: $city');
}

void main() {
  printPersonInfo(name: '홍길동', age: 30, city: '서울'); // 모든 매개변수 전달
  printPersonInfo(name: '김철수', city: '부산'); // 일부 매개변수만 전달
}
```


## 분기와 반복
if-else문의 조건은 반드시 ()를 사용해야합니다.

```dart
void main() {
  int age = 20;

  if (age >= 18) {
    print('성인입니다.');
  } else {
    print('미성년입니다.');
  }
}
```

```dart
void main() {
  int score = 85;

  if (score >= 90) {
    print('A등급');
  } else if (score >= 80) {
    print('B등급');
  } else if (score >= 70) {
    print('C등급');
  } else {
    print('F등급');
  }
}
```

```dart
void main() {
  int x = 10, y = 5;

  if (x > y) {
    if (x % 2 == 0) {
      print('x는 y보다 크고 짝수입니다.');
    } else {
      print('x는 y보다 크고 홀수입니다.');
    }
  } else {
    print('x는 y보다 작거나 같습니다.');
  }
}
````

삼항연산자로 if-else문을 한 줄로 줄일 수 있습니다.
```dart
String result = (age >= 18) ? '성인' : '미성년';
print(result);
```

열거형(enum)과 switch문의 조합도 많이 활용되는 분기 문법입니다.
```dart
enum Operator {
  add,
  subtract,
  multiply,
  divide
}

void main() {
  double num1 = 10.0;
  double num2 = 5.0;
  Operator op = Operator.divide;

  switch (op) {
    case Operator.add:
      print('$num1 + $num2 = ${num1 + num2}');
      break;
    case Operator.subtract:
      print('$num1 - $num2 = ${num1 - num2}');
      break;
    case Operator.multiply:
      print('$num1 * $num2 = ${num1 * num2}');
      break;
    case Operator.divide:
      if (num2 == 0) {
        print('0으로 나눌 수 없습니다.');
      } else {
        print('$num1 / $num2 = ${num1 / num2}');
      }
      break;
  }
}
```

for 반복문은 배열의 내용을 탐색할 때 많이 활용합니다.

```dart
void main() {
  // 정수형 배열 생성
  List<int> numbers = [1, 2, 3, 4, 5];

  // 일반적인 for문 사용
  for (int i = 0; i < numbers.length; i++) {
    print(numbers[i]);
  }

  // 향상된 for문 (for in) 사용
  for (int number in numbers) {
    print(number);
  }
}
```

## 객체지향 프로그래밍

Class에는 프로퍼티와 메서드를 포함 할 수 있습니다. dot(.)연산자로 인스턴스의 프로퍼티 값에 접근할 수 있습니다.

```dart
class Student {
  String name;
  int age;

  Student(this.name, this.age);

  void printInfo() {
    print('이름: $name, 나이: $age');
  }
}

void main() {
  Student student1 = Student('홍길동', 20);
  Student student2 = Student('김철수', 25);

  student1.printInfo();
  student2.printInfo();

  print(student1.name);
  print('${student2.age}살');
}

```

접근 지정자부터는 다음 시간에...


