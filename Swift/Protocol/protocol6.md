# 프로토콜 관련 기타 문법

프로토콜에 대한 여러가지 기타 문법에 대해 알아봅니다.

## 프로토콜의 상속

1. 프로토콜은 프로토콜을 상속할 수 있다.
2. 프로토콜은 여러개의 프로토콜을 상속할 수 있다.

```swift
protocol Remote {
    func turnOn()
    func turnOff()
}

protocol AirConRemote {
    func Up()
    func Down()
}

// 프로토콜 사이에 상속 구조를 만드는 것이 가능 ⭐️
// 프로토콜은 다중 상속 가능
protocol SuperRemoteProtocol: Remote, AirConRemote {

    // 프로토콜 상속 시 상속한 프로토콜의 요구사항을 자동 상속함
    // 프로토콜 Remote의 요구사항 자동 상속
    // func turnOn()
    // func turnOff()

    // 프로토콜 AirConRemote의 요구사항 자동 상속
    // func Up()
    // func Down()

    func doSomething()             // SuperRemoteProtocol의 요구사항 정의
}
```

- 프로토콜 사이에 상속 구조를 만들 수 있다.
- 프로토콜 상속 시 상속한 프로토콜의 요구사항을 자동 상속한다.
- 여러개의 프로토콜을 상속한 프로토콜을 채택하면 자동 상속한 요구사항까지 구현해야 한다.

```swift
class HomePot: SuperRemoteProtocol {

    func turnOn() { }
    func turnOff() { }

    func Up() { }
    func Down() { }

    func doSomething() { }

}
```

## 클래스 전용 프로토콜 AnyObject

AnyObject는 어떤 클래스의 타입도 표현할 수 있는 타입으로, 사실 AnyObject는 클래스 전용 프로토콜입니다. AnyObject가 클래스 전용 프로토콜이기 때문에 AnyObject를 범용적인 타입으로 사용하여 구체적인 타입(클래스)로 다운캐스팅하여 사용할 수 있는 것입니다.

AnyObject를 상속하는 프로토콜을 선언하면 해당 프로토콜을 클래스만 채택할 수 있는 프로토콜로 선언할 수 있습니다. 따라서 구조체는 AnyObject를 상속한 프로토콜을 채택할 수 없습니다.

```swift
protocol SomeProtocol: AnyObject {
    func doSomething()
}

class SomeClass: SomeProtocol {
    func doSomething() { print("do something...") }
}

```

## 프로토콜의 합성

& 연산자를 사용하여 프로토콜을 합성하고 임시적인 타입으로 사용할 수 있습니다.

```swift
protocol Named {
    var name: String { get }
}

protocol Aged {
    var age: Int { get }
}

// 동시에 여러개의 프로토콜 채택 가능
struct Person: Named, Aged {

    // Named 프로토콜 요구사항 구현
    var name: String

    // Aged 프로토콜 요구사항 구현
    var age: Int

}
```

```swift
// Named & Aged: 두 개의 프로토콜을 모두 채택한 타입
func wishHappyBirthday(to celebrator: Named & Aged) {
    print("생일 축하해, \(celebrator.name), 넌 이제 \(celebrator.age)살이 되었구나!")
}

let gildong = Person(name: "홍길동", age: 20)

// Person 구조체는 Named, Aged 프로토콜을 채택하므로 Person 인스턴스를 파라미터로 전달 가능
wishHappyBirthday(to: gildong)

// 임시적인 타입으로 저장 가능 (두 개의 프로토콜을 모두 채택한 타입만 저장 가능)
let whoIsThis: Named & Aged = gildong
```
