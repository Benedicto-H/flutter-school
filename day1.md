## Day 1 
# Dart 언어

Dart 프로그래밍 언어를 공부하려면 꼭 공식 웹사이트의 내용부터 살펴보세요.

- [공식 웹사이트](https://dart.dev/)
- [언어 소개](https://dart.dev/language)

Dart 언어와 Flutter의 간단한 예제를 학습하는 방법 중엔, DartPad를 이용해 웹브라우저에서 바로 코드를 작성하고 실행하는 방법이 있습니다. 처음엔 이 도구를 사용해 공부해보시길 권장드립니다.

- [DartPad](https://dartpad.dev/)

## main 함수와 주석
- Dart 코드는 main 함수의 내용부터 부터 실행합니다. 
- 함수 밖에서 직접 다른 함수 호출 같은 실행문을 적을 경우 오류가 발생합니다. 
- 각 명령문은 세미콜론(;)으로 끝나야 합니다.
- 들여쓰기는 보통 스페이스 두칸씩으로 처리합니다.

```dart
void main() {
  // Hello World 라고 출력합니다
  print("Hello World");
  
  /*
  여기도
  주석문을
  만들어봅시다
  */
  print("Hi my friend");
  
  /// 문서 주석입니다
  /// 문서 주석은 여기에서 더 자세한 내용이 나옵니다
  /// https://dart.dev/tools/dartdoc
  print("Good morning");
}
```

## 변수

```dart
void main() {
  /*
   변수를 알아봅시다
   
   int : 정수 (소숫점 이하 없음)
   double : 실수 (수숫점 이하 있음)
   String : 문자열
   bool : 참/거짓
   */
  
  // Swift와 비교해봅시다
  // var name: String = "Ned"
  String name = 'Ned';
  print(name);
  
  int age = 12;
  print(age);
  
  double pi = 3.142;
  print(pi);
  
  bool isTrue = true;
  print(isTrue);
  
  // 나름 Dart 언어도 적절한 타입값만을 할당하도록 따진다.
  // String length = 123;
  
  // 적절한 원시값 변환도 해줍니다.
  double width = 123;
  width = 56.78;
  print(width);
}
```

## 상수
```dart
void main() {
  /*
   상수를 알아봅시다
   
   final
   const
   */

  final String name = "Ned";
  // 에러 발생
  // name = "Tuna"; 
  print(name);
  
  const int age = 13;
  // 에러 발생
  // age = 14;
  print(age);
}
```

## 산술 연산자
```dart
void main() {
  /*
   산술 연산자를 알아봅시다.
   
   + - * / % ~/
   */
  
  int add = 2 + 3;
  print(add);
  
  int minus =  15 - 4;
  print(minus);
  
  int multiply = 4 * 3;
  print(multiply);
  
  // 나눗셈은 double 타입에만 담을 수 있다
  double divide = 4.5 / 2.1;
  print(divide);
  
  int remainder = 10 % 3;
  print(remainder);
  
  // ~/ : 몫
  int something = 10 ~/ 3;
  print(something);
}
```

## 비교 연산자
```dart
void main() {
  /*
   비교 연산자를 알아봅시다.
   
   == 같다
   != 다르다
   > 더 크다
   < 더 작다
   >= 크거나 같다
   <= 작거나 같다
   */
  
  bool isTrue = (3 == 3);
  print(isTrue);
  
  isTrue = (3 != 3);
  print(isTrue);
  
  isTrue = (3 > 4);
  print(isTrue);
  
  isTrue = (3 < 4);
  print(isTrue);
  
  
  isTrue = (6 >= 8);
  print(isTrue);
  
  isTrue = (5 <= 5);
  print(isTrue);
}
```    

## 논리 연산자
```dart
void main() {
  /*
   논리 연산자를 알아봅시다.
   
   && 그리고
   || 또는
   == 같다
   ! 부정(NOT)
   != 다르다
   */

  bool isTrue = (true && false);
  print(isTrue);
  
  isTrue = (true || false);
  print(isTrue);
}
```

## 타입 검사
```dart
void main() {
  /*
   타입검사를 알아봅시다.
   
   is : 같은 타입인가?
   is! : 다른 타입인가?
   */
  
  int age = 12;
  
  bool isTrue = (age is int);
  print(isTrue);
  
  isTrue = (age is! double);
  print(isTrue);
}
```

## 형 변환
```dart
void main() {
  /*
   형 변환(type-casting)을 알아봅시다.
   
   as
   */

  int age = 12;
  double detailAge = age as double;
  print(detailAge);
}
```

