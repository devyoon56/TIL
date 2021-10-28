# 프로토콜 확장의 기본 개념

프로토콜의 확장에 대해 알아봅니다.

프로토콜도 타입으로 취급할 수 있으므로 프로토콜을 확장할 수 있습니다. 프로토콜을 확장하는 이유는 코드의 중복 구현을 줄이기 위함입니다. 코드의 중복 구현이란 프로토콜을 채택한 타입에서 실제로 메서드를 구현해야하는데 프로토콜을 채택하는 모든 타입마다 동일한 메서드를 구현한다면 코드가 중복될 수 있다는 의미입니다. 프로토콜을 확장하는 이유를 다음과 같이 정리할 수 있습니다.

- 코드의 중복을 없앤다.
- 프로토콜 요구사항 메서드의 기본 구현을 제공한다.

프로토콜의 확장에서 메서드의 기본 구현을 제공하지 않는 경우 코드가 중복될 수 있습니다.

```swift
protocol Remote {

    func turnOn()

    func turnOff()

}

class TV: Remote {
    let name = "애플티비"

    func turnOn() { print("리모컨 켜기") }          // 코드 중복

    func turnOff() { print("리모컨 끄기") }         // 코드 중복

}

struct AirCon: Remote {
    let name = "삼성에어컨"

    func turnOn() { print("리모컨 켜기") }          // 코드 중복

    func turnOff() { print("리모컨 끄기") }         // 코드 중복
}
```

프로토콜의 확장에서 기본 구현을 제공한다면 프로토콜을 채택한 타입은 프로토콜의 요구사항을 직접 구현하지 않고도 프로토콜이 제공하는 메서드의 기본 구현을 사용할 수 있습니다. 또한 프로토콜의 정의에서 선언하지 않은 메서드를 확장에서 제공하는 경우 해당 메서드 또한 사용할 수 있습니다.

```swift
protocol Remote {

	func turnOn()

	func turnOff()

}

extension Remote {

	func turnOn() { print("리모컨 켜기") }

	func turnOff() { print("리모컨 끄기") }

	func doAnotherAction() { print("리모컨 다른 동작") }        // 프로토콜 요구사항이 아닌 메서드

}

class TV: Remote {}
struct AirCon: Remote {}

let tv = TV()
tv.turnOn()                     // "리모컨 켜기"
tv.turnOff()                    // "리모컨 끄기"
tv.doAnotherAction()            // "리모컨 다른 동작"

let airCon = AirCon()
airCon.turnOn()                 // "리모컨 켜기"
airCon.turnOff()                // "리모컨 끄기"
airCon.doAnotherAction()        // "리모컨 다른 동작"
```

TV 클래스와 AirCon 구조체 모두 Remote 프로토콜을 채택했지만 어떤 프로토콜 요구사항 메서드도 구현하지 않았습니다. 그럼에도 프로토콜 확장에서 제공하는 모든 메서드를 사용할 수 있습니다.
