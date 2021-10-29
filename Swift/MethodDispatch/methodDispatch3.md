# 프로토콜의 메서드 디스패치(Witness Table)

프로토콜은 테이블 디스패치 방식을 사용합니다. 프로토콜의 메서드 테이블을 **Witness Table**이라고 합니다. 프로토콜을 정의할 때 선언한 메서드의 실행 주소를 프로토콜의 메서드 테이블인 Witness Table에 저장합니다. 이러한 Witness Table을 생성하는 것은 해당 프로토콜을 채택하는 타입입니다.

```swift
protocol MyProtocol {
    func method1()    // Witness Table
    func method2()    // Witness Table
}

extension MyProtocol {
    // 확장에서 프로토콜 요구사항의 기본 구현 제공
    func method1() { print("Protocol - Witness Table method1") }
    func method2() { print("Protocol - Witness Table method1") }

    // 프로토콜 요구사항이 아니면 Direct Dispatch 사용
    func anotherMethod() { print("Protocol Extension - Direct method") }
}

class FirstClass: MyProtocol {
    func method1() { print("Class - Virtual Table method1") }
    func method2() { print("Class - Virtual Table method2") }
    func anotherMethod() { print("Class - Virtual Table method3") }
}

/**==============================================================
[Class Virtual Table]
- func method1() { print("Class - Virtual Table method1") }
- func method2() { print("Class - Virtual Table method2") }
- func anotherMethod() { print("Class - Virtual Table method3") }
=================================================================**/

/**==============================================================
[Protocol Witness Table]
- func method1() { print("Class - Virtual Table method1") }   // 요구사항 - 우선순위 반영⭐️
- func method2() { print("Class - Virtual Table method2") }   // 요구사항 - 우선순위 반영⭐️
=================================================================**/
```

- 클래스는 클래스의 메서드 테이블을 생성한다.
- 클래스는 채택한 프로토콜의 메서드 테이블 또한 생성한다.
- 프로토콜의 메서드 테이블을 생성할 때 **메서드 우선순위**에 따라 메서드 실행 주소가 달라질 수 있다.

```swift
let first = FirstClass()
first.method1()                   // Virtual Table - method1
first.method2()                   // Virtual Table - method2
first.anotherMethod()             // Virtual Table - anotherMethod

let myProtocol: MyProtocol = FirstClass()
myProtocol.method1()              // Witness Table - method1
myProtocol.method2()              // Witness Table - method2
myProtocol.anotherMethod()        // Protocol Extension - Direct Dispatch
```

- 클래스의 인스턴스를 프로토콜로 인식시키면 클래스의 메서드 테이블을 참조하지 않고 프로토콜의 메서드 테이블을 참조한다.
- anotherMethod()는 프로토콜의 필수 요구사항이 아니므로 메서드 실행 결과는 인스턴스를 인식하는 타입에 따라 달라질 수 있다.
- 프로토콜 필수 요구사항이 아닌 메서드의 경우 Witness Table에 해당 메서드 실행 주소가 저장되지 않고 Direct Dispatch 방식을 사용해서 컴파일 시점에 메서드의 실행 주소를 직접 삽입한다.
