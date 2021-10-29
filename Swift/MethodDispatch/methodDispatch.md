# 메서드 디스패치(Method Dispatch)의 개념

클래스와 프로토콜의 메서드가 실행되는 방식에 대해 알아봅니다.

## 메서드 디스패치의 개념 이해하기

메서드 디스패치는 스위프트가 함수를 실행하는 방식을 말합니다. 세 가지 방법이 있으며 세 가지 방법을 모두 사용합니다.

1. Direct Dispatch(직접, static)

- 컴파일 시점에 코드 자체에 함수의 메모리 주소를 삽입하거나 함수의 명령 코드를 해당 함수 위치에 코드를 심는 방식(in-line)
- 가장 빠르게 동작하는 방식(0~2.13ns)
- 밸류 타입(구조체, 열거형)에서 사용되는 방식
- **상속과 다형성**의 장점을 사용할 수 없음

2. Table Dispatch(동적, dynamic)

- 함수의 포인터를 배열 형태로 보관 후 함수 실행 시 포인터를 참조하여 실행하는 방식
- Direct Dispatch 방식보다 느리게 동작하는 방식(3.23ns)
- **클래스와 프로토콜**에서 사용되는 방식
  - 클래스 테이블: Virtual Table
  - 프로토콜 테이블: Witness Table

3. Message Dispatch(메세지)

- 상속 구조를 모두 훑은 다음에 실행할 메서드를 결정하는 방식
- 가장 느리게 동작하는 방식(5.82ns)
- 주로 **Objective-C 클래스**에서 사용되는 방식
- Objective-C 런타임에 의존하는 방식

## 메세지 디스패치의 구분

1. Value Type(Struct)

   - Initial Declaration: Direct Dispatch
   - Extension: Direct Dispatch

2. Protocol

   - Initial Declaration: Table Dispatch(Witness Table)
   - Extension: Direct Dispatch
   - 비고
     - 프로토콜 정의 시 선언한 요구사항의 메서드의 실행 주소를 Witness Table에 저장한다.
     - 프로토콜을 채택하는 타입은 Witness Table을 생성한다.

3. Class

   - Initial Declaration: Table Dispatch(Virtual Table)
   - Extension: Direct Dispatch(클래스 상속 시 재정의 불가능 원칙)
   - 비고
     - final 키워드를 사용한 클래스의 메서드는 Direct Dispatch 방식으로 동작한다.
     - @objc dynamic 키워드를 사용한 클래스의 메서드는 Message Dispatch 방식으로 동작한다. 그리고 extension 내의 메서드를 재정의할 수 있다.

4. @objc dynamic
   - Initial Declaration: Message Dispatch
   - Extension: Message Dispatch
