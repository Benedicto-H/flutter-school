## Day 4 
# Dart 언어

## Tips

## Dart에서 final과 const 키워드의 차이점

### final
- 런타임 시에 한 번만 값을 할당할 수 있습니다. 즉, 변수가 선언될 때 값이 정해지지 않아도 됩니다.
- 변수의 값이 한 번만 할당되면 변경되지 않도록 보장하고 싶을 때 사용합니다.
- 클래스의 멤버 변수를 초기화하거나, 함수의 매개변수를 상수로 만들고 싶을 때 사용합니다.
- 변수의 값이 한 번만 설정되면 되고, 컴파일 시에 값을 알 수 없는 경우에 사용합니다. (예: 사용자 입력 값, API 호출 결과 등)

### const
- 컴파일 시에 값이 결정됩니다. 즉, 변수가 선언될 때 값이 반드시 상수 표현식으로 초기화되어야 합니다.
- 컴파일 시에 값이 결정되는 상수를 만들고 싶을 때 사용합니다.
- 불변 객체를 만들거나, 리터럴 값을 대체하여 코드를 더 명확하게 만들고 싶을 때 사용합니다.
- 값이 절대 변하지 않는 상수를 만들고 싶을 때 사용합니다.
- 예: 수학 상수(pi), 색상 코드, enum 값 등

### 3. 예시

```dart
// final 예시
final name = '홍길동'; // 런타임에 값이 할당됨
final age = 30;

// const 예시
const pi = 3.14159; // 컴파일 시에 값이 결정됨
const colors = ['red', 'green', 'blue'];

// 클래스에서 사용
class Person {
  final String name;
  final int age;

  Person(this.name, this.age);
}
```

| 구분 | final | const |
|---|---|---|
| 초기화 시점 | 런타임 | 컴파일 |
| 사용 용도 | 변수 값 한 번 할당, 불변성 보장 | 상수 생성, 불변 객체 생성 |
| 특징 | 런타임에 값이 결정될 수 있음 | 컴파일 시에 값이 결정되어야 함 |

## Private property
- 클래스 내부에서만 접근 가능한 속성
- private property를 선언하려면 변수 이름 앞에 언더스코어(_)를 붙입니다.

```dart
class Person {
  String _name; // private property
  int _age; // private property

  // 생성자
  Person(this._name, this._age);
}
```

- private property에 직접 외부에서 접근할 수는 없지만, getter와 setter를 통해 간접적으로 값을 읽고 변경할 수 있습니다.

```dart
class Person {
  String _name;
  int _age;

  Person(this._name, this._age);

  String get name => _name; // getter
  int get age => _age;
}
```

```dart
class Person {
  String _name;
  int _age;

  Person(this._name, this._age);

  set name(String newName) {
    _name = newName;
  }

  set age(int newAge) {
    if (newAge >= 0) {
      _age = newAge;
    } else {
      print('나이는 0 이상이어야 합니다.');
    }
  }
}
```

```dart
void main() {
  var person = Person('홍길동', 30);

  // getter를 사용하여 값 읽기
  print(person.name); // 홍길동
  print(person.age); // 30

  // setter를 사용하여 값 변경
  person.name = '김철수';
  person.age = 25;

  print(person.name); // 김철수
  print(person.age); // 25
}
```


## 컬렉션

List (리스트)
- 순서가 있는 데이터의 집합입니다. 같은 타입의 데이터를 여러 개 저장할 수 있습니다.

List의 메서드
- add: 리스트에 요소 추가
- remove: 리스트에서 요소 제거
- contains: 리스트에 특정 요소가 있는지 확인
- sort: 리스트 정렬

```dart
void main() {
  List<int> numbers = [1, 2, 3];
  List<String> names = ['홍길동', '김철수'];

  print(numbers[0]); // 1 출력
}
```

Map (맵)
- 키와 값의 쌍으로 이루어진 데이터 집합입니다. 각 키는 유일해야 합니다.

Map의 메서드
- keys: 모든 키 반환
- values: 모든 값 반환
- containsKey: 특정 키가 있는지 확인


```dart
void main() {
  Map<String, int> ages = {'홍길동': 20, '김철수': 30};
  print(ages['홍길동']); // 20 출력
}
```

Set (셋)
- 순서가 없고 중복된 값을 허용하지 않는 데이터의 집합입니다.

Set의 메서드
- add: 셋에 요소 추가
- remove: 셋에서 요소 제거
- contains: 셋에 특정 요소가 있는지 확인

```dart
void main() {
  Set<String> fruits = {'사과', '바나나', '딸기'};
  print(fruits.contains('사과'));
}
```


- 순서가 중요하고 중복을 허용해야 할 때: List
- 키-값 쌍으로 데이터를 관리해야 할 때: Map
- 중복을 허용하지 않고 집합 연산이 필요할 때: Set

```dart
class Student {
  String name;
  int age;

  Student(this.name, this.age);
}

void main() {
  // 학생 정보를 담을 List 생성
  List<Student> students = [
    Student('홍길동', 20),
    Student('김철수', 25),
    Student('박영희', 30)
  ];

  // 학생 이름을 key, 나이를 value로 하는 Map 생성
  Map<String, int> studentAges = {
    '홍길동': 20,
    '김철수': 25,
    '박영희': 30
  };

  // 좋아하는 과일을 저장하는 Set 생성
  Set<String> favoriteFruits = {'사과', '바나나', '딸기'};

  // 학생 정보 출력
  for (var student in students) {
    print('${student.name}: ${student.age}세');
  }

  // 특정 학생의 나이 출력
  print('홍길동의 나이: ${studentAges['홍길동']}세');

  // 좋아하는 과일 목록 출력
  for (var fruit in favoriteFruits) {
    print(fruit);
  }
}
```

Dart에서 스프레드 연산자(Spread Operator)는 ...으로 표현되며, 컬렉션(List, Set, Map)의 요소들을 개별 요소로 펼쳐서 전달하는 데 사용됩니다.

```dart
void main() {
  List<int> numbers = [1, 2, 3];
  List<int> moreNumbers = [...numbers, 4, 5]; // numbers 복사 후 4, 5 추가
  print(moreNumbers);
}
```
