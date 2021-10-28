# 프로토콜 확장의 제한

특정 프로토콜을 채택한 타입만 프로토콜의 확장이 적용되도록 제한할 수 있습니다.

아래 예시는 Bluetooth 프로토콜의 확장을 Remote 프로토콜을 채택한 타입에만 적용하는 예시입니다.

```swift
protocol Remote {
    func turnOn()
    func turnOff()
}

extension Remote {
    func turnOn() { print("리모컨 켜기") }
    func turnOff() { print("리모컨 끄기") }
}

protocol Bluetooth {
    func blueOn()
    func blueOff()
}

extension Bluetooth where Self: Remote {
    func blueOn() { print("블루투스 켜기") }
    func blueOff() { print("블루투스 끄기") }
}
```

프로토콜의 확장에서 where 절을 사용해 프로토콜 확장의 적용을 제한할 수 있습니다.

```swift
class Smartphone: Remote, Bluetooth {}

let smartphone = Smartphone()
smartphone.turnOn()
smartphone.turnOff()
smartphone.blueOn()
smartphone.blueOff()
```

Remote, Bluetooth 프로토콜을 모두 채택한다면 Remote, Bluetooth 프로토콜의 확장에서 제공하는 기본 메서드를 사용할 수 있습니다.

```swift
class Ipad: Bluetooth {
    func blueOn() { print("블루투스 켜기") }
    func blueOff() { print("블루투스 끄기") }
}

let ipad = Ipad()
ipad.blueOn()
ipad.blueOff()
```

Bluetooth 프로토콜만 채택한다면 Bluetooth 프로토콜의 확장이 적용되지 않기 때문에 Bluetooth 프로토콜의 정의에서 선언한 메서드를 직접 구현해야 합니다.
