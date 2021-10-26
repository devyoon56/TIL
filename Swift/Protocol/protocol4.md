# 프로토콜 요구사항의 종류2

프로토콜을 정의할 때 나열하는 요구사항에는 크게 두 가지 종류가 있습니다.

1. 속성 요구사항
2. 메서드 요구사항
   - 메서드
   - 생성자
   - 서브스크립트

## 메서드의 요구사항을 정의하고 구현하는 방법

이제 메서드의 요구사항을 정의하고 구현하는 방법에 대해 알아봅니다. 먼저 메서드의 요구사항을 정의하는 방법에 대해 알아봅니다.

- 메서드의 경우 헤드부분(입력과 출력)만 정의한다.
- 타입 메서드로 정의하려면 static 키워드를 사용한다.
  - 타입 메서드 구현 시 static, class 키워드를 선택한다.
- 메서드의 요구사항 정의 시 mutating 키워드 사용은 다음을 의미한다.
  - 저장 속성을 변경하는 메서드인 경우 구조체도 프로토콜을 채택할 수 있다는 의미이다.
  - 구조체만 프로토콜을 사용하도록 제한한다는 의미는 아니다.

다음은 메서드의 요구사항을 정의하고 해당 메서드를 구현하는 예제입니다.

```swift
protocol RandomNumber {

    static func reset()

    func random() -> Int

}

class Number: RandomNumber {

    static func reset() { print("다시 세팅") }

    func random() -> Int { return Int.random(in: 1...100) }

}
```

다음은 mutating 키워드를 사용하여 요구사항의 메서드를 정의하고 해당 메서드를 구현하는 예제입니다.

```swift
protocol Togglable {
    mutating func toggle()
}

enum OnOffSwift: Togglable {
    case on
    case off

    mutating func toggle() {
        switch self {
        case .on:
            self = .off
        case .off:
            self = .on
        }
    }
}

class ClassSwitch: Togglable {
    var isOn = false

    func toggle() {
        isOn = isOn ? false : true
    }
}
```

## 생성자의 요구사항을 정의하고 구현하는 방법

다음은 생성자의 요구사항을 정의하고 구현하는 방법을 알아봅니다.

- 클래스의 경우 상속 관계를 고려하여 요구사항으로 지정한 생성자 앞에 required 키워드를 붙인다.
  - 서브 클래스에서 해당 생성자 구현을 강제하는 것
  - 구조체의 경우 상속이 없으므로 required 키워드가 필요없음
- final 키워드를 사용하여 클래스의 상속을 제한하면 required 키워드를 생략할 수 있다.
- 클래스의 경우 반드시 지정 생성자로 구현할 필요는 없고 편의 생성자로 구현할 수 있다.

아래는 생성자의 요구사항을 정의하고 구현하는 예제입니다.

```swift
protocol SomeProtocol {
    init(num: Int)      // 생성자를 프로토콜 요구사항으로 정의
}

class SomeClass: SomeProtocol {

    // 프로토콜 요구사항으로 지정된 생성자 앞에 required 키워드 필요
    required init(num: Int) {}

}

class SomeSubClass: SomeClass {
    // 서브 클래스에서 다른 생성자를 구현하지 않으면 필수 생성자 자동 상속
}

final class SomeFinalClass: SomeProtocol {
    init(num: Int) {}
}
```

```swift
protocol AnotherProtocol {
    init()
}

class SomeSuperClass {
    init()
}

class SomeSubClass: SomeSuperClass, AnotherProtocol {

    // AnotherProtocol 을 채택하므로 생성자 구현 시 required 키워드 필요
    // SomeSuperClass 를 상속하므로 생성자 구현 시 override 키워드 필요
    required override init() {}
}
```

실패불가능, 실패가능 생성자의 요구사항을 정의하고 구현하는 방법은 다음과 같습니다.

- 실패가능 생성자를 요구사항으로 정의한 경우
  - 실패불가능 생성자로 구현 가능: init()
  - 실패가능 생성자로 구현 가능: init?(), init!()
- 실패불가능 생성자를 요구사항으로 정의한 경우
  - 실패불가능 생성자로만 구현 가능: init()
  - 실패가능 생성자로 구현 할 수 없음

다음은 실패가능 생성자를 요구사항으로 정의하고 구현하는 예제입니다.

```swift
protocol SomeProtocol {
    init?(num: Int)     // 실패가능 생성자를 요구사항으로 정의
}

struct SomeStruct: SomeProtocol {

    // 실패불가능 생성자 또는 실패가능 생성자로 구현 가능
    init(num: Int) {}
    //init?(num: Int) {}
    //init!(num: Int) {}

}
```

```swift
class SomeClass: SomeProtocol {

    // 실패불가능 생성자 또는 실패가능 생성자로 구현 가능
    required init(num: Int) {}
    //required init?(num: Int) {}
    //required init!(num: Int) {}

}
```

## 서브스크립트의 요구사항을 정의하고 구현하는 방법

다음은 서브스크립트 요구사항을 정의하고 구현하는 방법을 알아봅니다.

- 최소한의 요구사항을 지정한다.
- get, set 키워드를 사용하여 읽기와 쓰기 여부를 결정한다.
- get 키워드로 정의 시
  - 읽기 전용 서브스크립트로 구현 가능
  - 읽기/쓰기 서브스크립트로 구현 가능
- get, set 키워드로 정의 시
  - 반드시 읽기/쓰기 서브스크립트로만 구현 가능

```swift
protocol DataList {
    subscript(index: Int) -> Int { get }
}

struct DataStruct: DatList {
    // 읽기 전용 서브스크립트로 구현하는 경우
    subscript(index: Int) -> Int { return 0 }

    // 읽기/쓰기 서브스크립트로 구현하는 경우
    //subscript(index: Int) -> Int {
    //    get { return 0 }
    //    set {
    //        // 쓰기 구현
    //   }
    //}
}
```
