# 선택적 요구사항의 구현

프로토콜의 요구사항을 선택적으로 구현할 수 있도록 선언할 수 있습니다. 이렇게 선언하려면 어트리뷰트를 사용해야 합니다.

## 어트리뷰트

어트리뷰트는 컴파일러에게 추가적인 정보를 제공하는 특별한 신호입니다. 어트리뷰트는 두 가지 종류가 있습니다.

1. 선언에 대한 추가 정보 제공
2. 타입에 대한 추가 정보 제공

다음은 어트리뷰트의 실제 예시입니다.

```swift
// 선언에 대한 추가 정보 제공
@available(iOS 10.0, macOS 10.12, *)
class SomeClass {}      // SomeClass의 선언은 iOS 10.0, macOS 10.12 이상의 버전에서만 읽을 수 있다는 의미
```

```swift
// 타입에 대한 추가 정보 제공
func doSomething(completion: @escaping () -> ()) {}
```

## 선택적 요구사항으로 선언하기

프로토콜에서 요구사항을 선언할 때 선택적인 멤버로 구현할 수 있습니다. 이 기능은 Objective-C 에서만 지원하는 기능이기 때문에 @objc 어트리뷰트를 사용해야 합니다. @objc의 의미는 Objective-C의 코드에서 읽을 수 있다는 것입니다.

@objc 어트리뷰트와 optional 키워드를 사용하여 프로토콜의 요구사항을 선택적으로 구현할 수 있도록 선언합니다.

1. 프로토콜 선언 앞에 **@objc**를 추가한다.
2. 선택적인 멤버로 구현하려는 멤버 앞에 **@objc optional**을 추가한다.

```swift
@objc protocol Remote {

    @objc optional var isOn: Bool { get set }

    func turnOn()

    func turnOff()

    @objc optional func doNetflix()
}

class TV: Remote {

    var isOn = false        // 선택적인 멤버는 반드시 구현할 필요 없음

    func turnOn() {}

    func turnOff() {}

//    func doNeflix() {}      // 선택적인 멤버는 반드시 구현할 필요 없음

}
```

선택적인 멤버를 선언한 프로토콜을 사용할 때 주의해야할 점은 다음과 같습니다.

- 선택적인 멤버를 선언한 프로토콜은 Objective-C에 해당하는 클래스 전용 프로토콜로 선언된다.
- Objective-C는 구조체와 열거형이 프로토콜을 채택하는 것을 지원하지 않기 때문이다.
- 따라서 구조체와 열거형은 선택적인 멤버를 선언한 프로토콜을 채택할 수 없다.

```swift
let tv = TV()

tv.isOn               // false
//tv.doNetflix()      // TV 클래스에서 doNetflix() 를 구현하지 않았으므로 실행 불가능
```

```swift
let tv: Remote = TV()

tv.isOn             // Optional(false)
tv.doNetflix?()     // nil
```

선택적인 멤버를 선언한 프로토콜을 사용하여 타입으로 선언하면 선택적인 멤버로 선언한 멤버는 옵셔널 타입이 됩니다. 선택적인 멤버의 구현 여부에 따라 옵셔널 타입의 값은 다음과 같이 결정됩니다.

- 선택적인 멤버를 구현하지 않은 경우 nil을 반환
- 선택적인 멤버를 구현한 경우 옵셔널 값을 반환
