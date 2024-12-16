## Day 5 
# Dart 언어

## 함수형 프로그래밍

일급 객체 (First-class Citizens)
- 함수를 변수에 할당, 함수의 인자로 전달, 함수의 반환값으로 사용할 수 있다는 의미입니다.

```dart
void main() {
  void greet(String name) {
    print('Hello, $name!');
  }

  Function greeter = greet;
  greeter('Alice');

  void applyTo(String name, Function func) {
    func(name);
  }

  applyTo('Bob', greet);
}
```

for문 vs. forEach() 함수
- for문: 일반적인 반복문으로, 리스트의 요소를 순서대로 접근합니다.
- forEach(): 리스트의 각 요소에 대해 특정 함수를 실행합니다.

```dart
void main() {
  List<int> numbers = [1, 2, 3, 4, 5];

  // for문
  for (int number in numbers) {
    print(number);
  }

  // forEach()
  numbers.forEach((number) => print(number));
}
```

where
- List에서 특정 조건을 만족하는 요소만 추출하여 새로운 List를 반환합니다.

```dart
void main() {
  List<int> numbers = [1, 2, 3, 4, 5];
  List<int> evenNumbers = numbers.where((number) => number % 2 == 0).toList();
  print(evenNumbers); // [2, 4] 출력
}
```

map
- List의 각 요소에 함수를 적용하여 새로운 List를 생성합니다.

```dart
void main() {
  List<int> numbers = [1, 2, 3, 4, 5];
  List<int> doubledNumbers = numbers.map((number) => number * 2).toList();
  print(doubledNumbers); // [2, 4, 6, 8, 10] 출력
}
```

toList, toSet
- Iterable을 List 또는 Set으로 변환합니다.

```dart
void main() {
  List<int> numbers = [1, 2, 3, 2, 1];
  Set<int> uniqueNumbers = numbers.toSet();
  print(uniqueNumbers); // {1, 2, 3} 출력
}
```

any
- List의 요소 중 하나라도 주어진 조건을 만족하는지 확인합니다.

```dart
void main() {
  List<int> numbers = [1, 2, 3, 4, 5];
  bool hasEvenNumber = numbers.any((number) => number % 2 == 0);
  print(hasEvenNumber); // true 출력
}
```

reduce
- List의 요소들을 누적하여 하나의 값으로 축소합니다.

```dart
void main() {
  List<int> numbers = [1, 2, 3, 4, 5];
  int sum = numbers.reduce((value, element) => value + element);
  print(sum); // 15 출력
}
```

함수형 프로그래밍의 장점
- 코드 가독성 향상: 간결하고 명확한 코드 작성 가능
- 재사용성 증가: 함수를 조합하여 다양한 기능 구현 가능
- 병렬 처리 용이: 각 요소를 독립적으로 처리하기 때문에 병렬 처리에 적합
- 테스트 용이: 순수 함수를 사용하여 테스트 케이스 작성이 용이

## 그밖의 문법들

### Dart의 계단식 표기법 (Cascade Notation)
- Dart의 계단식 표기법은 동일한 객체에 대한 연속적인 메서드 호출을 간결하게 표현하는 방법입니다. 마치 계단처럼 메서드 호출을 이어나갈 수 있다는 의미에서 '계단식'이라는 표현을 사용합니다. 주로 객체를 생성하고 초기화하거나 여러 속성을 연속적으로 설정할 때 유용하게 사용됩니다.

```
객체 .. 메서드1() .. 메서드2() .. 메서드3();
```

- 객체: 계단식 표기법을 적용할 객체를 지정합니다.
- ..: 연속적인 메서드 호출을 연결하는 연산자입니다.
- 메서드1(), 메서드2(), 메서드3(): 객체에 호출할 메서드들입니다.


```dart
class Product {
  String name;
  double price;
  int stock;

  Product({required this.name, required this.price, required this.stock});

  void setName(String newName) {
    name = newName;
  }

  void setPrice(double newPrice) {
    price = newPrice;
  }

  void setStock(int newStock) {
    stock = newStock;
  }

  @override
  String toString() {
    return 'Product(name: $name, price: $price, stock: $stock)';
  }
}

void main() {
  var product = Product(name: 'Laptop', price: 999.99, stock: 10)
    ..setName('Gaming Laptop')
    ..setPrice(1299.99)
    ..setStock(5);

  print(product); // Product(name: Gaming Laptop, price: 1299.99, stock: 5)
}
```

### 컬렉션 if 문법

Dart 언어의 컬렉션 if 문법은 조건에 따라 컬렉션의 요소를 동적으로 포함시킬 수 있는 유용한 기능입니다. 이 기능을 사용하면 리스트, 맵 또는 셋과 같은 컬렉션에서 조건에 따라 값을 추가하거나 생략할 수 있습니다. 이를 통해 더 간결하고 가독성 높은 코드를 작성할 수 있습니다.

```dart
void main() {
  bool includeExtraItem = true;

  var items = [
    'Item 1',
    'Item 2',
    if (includeExtraItem) 'Extra Item',
  ];

  print(items); // ['Item 1', 'Item 2', 'Extra Item']
}
```

```dart
void main() {
  bool isAdmin = false;

  var menuItems = [
    'Home',
    'Profile',
    'Settings',
    if (isAdmin) 'Admin Panel',
  ];

  print(menuItems); // ['Home', 'Profile', 'Settings']
}
```

```dart
void main() {
  bool hasDiscount = true;

  var productInfo = {
    'name': 'Laptop',
    'price': 999.99,
    if (hasDiscount) 'discount': 100.00,
  };

  print(productInfo); // {'name': 'Laptop', 'price': 999.99, 'discount': 100.00}
}
```

```dart
void main() {
  var numbers = [1, 2, 3, 4, 5];

  // 컬렉션 for 문법과 결합
  var evenNumbers = [
    for (var number in numbers)
      if (number.isEven) number
  ];

  print(evenNumbers); // [2, 4]
}

```

### Null 안전성 (Null Safety)

- Dart 2.12부터 Null Safety가 도입되어 변수에 null 값을 할당할 수 있는지 여부를 명시적으로 지정할 수 있습니다. 기본적으로 모든 변수는 null이 될 수 없습니다. 
- 여기서 int?는 null이 될 수 있는 정수를 나타냅니다. 반면 int는 null이 될 수 없는 정수를 나타냅니다.

```dart
// Null이 될 수 없는 변수
int nonNullableInt = 42;

// Null이 될 수 있는 변수
int? nullableInt;
nullableInt = null;
```

### Null 병합 연산자 (??)

- null 병합 연산자는 왼쪽 피연산자가 null인지 확인하고, null이면 오른쪽 피연산자를 반환합니다. 이는 기본값을 제공할 때 유용합니다.

```dart
int? nullableInt;
int value = nullableInt ?? 0; // nullableInt가 null이면 0을 사용

```

### Null 접근 연산자 (?.)

- null 접근 연산자는 객체가 null인 경우에도 안전하게 해당 객체의 속성이나 메서드에 접근할 수 있도록 합니다. 객체가 null이면 null을 반환합니다.

```dart
class Person {
  String? name;
}

Person? person;
String? name = person?.name; // person이 null이면 name은 null
```

### 강제 null 확인 연산자 (!)

- 강제 null 확인 연산자는 변수나 표현식이 null이 아님을 보장할 때 사용됩니다. 이 연산자는 변수에 null 값이 있으면 예외를 발생시킵니다.

```dart
int? nullableInt;
nullableInt = 42;
int nonNullableInt = nullableInt!; // nullableInt가 null이 아님을 보장
```

### null-aware 할당 연산자 (??=)

- null-aware 할당 연산자는 변수가 null일 때만 값을 할당합니다.

```dart
int? nullableInt;
nullableInt ??= 0; // nullableInt가 null이면 0을 할당
```

```dart
void main() {
  int? a;
  int b = 5;

  // Null 병합 연산자
  int c = a ?? b; // a가 null이면 b를 사용
  print(c); // 5

  // Null 접근 연산자
  String? name;
  String? upperName = name?.toUpperCase();
  print(upperName); // null

  // 강제 null 확인 연산자
  int? nullableInt = 10;
  int nonNullableInt = nullableInt!;
  print(nonNullableInt); // 10

  // null-aware 할당 연산자
  int? nullableValue;
  nullableValue ??= 7;
  print(nullableValue); // 7
}
```
