# 프로토콜의 확장과 메서드 우선순위

프로토콜의 확장에서 메서드의 기본 구현을 제공하더라도 프로토콜을 채택한 타입은 프로토콜의 요구사항 메서드를 직접 구현하고 사용할 수 있습니다.

```swift
protocol Remote {
    func turnOn()
    func turnOff()
}

extension Remote {
    func turnOn() { print("리모컨 켜기") }
    func turnOff() { print("리모컨 끄기") }

    // 프로토콜 요구사항이 아닌 메서드
    func doAnotherAction() { print("리모컨 다른 동작") }
}

class TV1: Remote {

    func turnOn() { print("TV 켜기") }

    // 프로토콜 요구사항이 아닌 메서드
    func doAnotherAction() { print("TV 또 다른 동작") }

}

struct Aircon1: Remote {

    func turnOn() { print("에어컨 켜기") }
    func turnOff() { print("에어컨 끄기") }

    // 프로토콜 요구사항이 아닌 메서드
    func doAnotherAction() { print("에어컨 방향 조절하기") }

}
```

타입에서 직접 구현한 메서드와 프로토콜의 확장에서 제공하는 기본 메서드 중 어떤 메서드를 실행하는지는 메서드의 우선순위에 따라 달라집니다. 메서드를 실행하는 우선순위는 다음과 같습니다.

1. 프로토콜을 채택한 타입에서 직접 구현한 메서드
2. 프로토콜의 확장에서 제공하는 기본 메서드

즉 프로토콜의 정의에서 선언한 메서드를 타입에서 직접 구현한 경우 프로토콜의 확장에서 제공하는 기본 메서드가 있더라도 타입에서 직접 구현한 메서드가 실행됩니다.

```swift
let tv = TV()
tv.turnOn()                 // "TV 켜기", 직접 구현한 메서드 실행
tv.turnOff()                // "리모컨 끄기", 기본 메서드 실행
tv.doAnotherAction()        // "TV 또 다른 동작", 직접 구현한 메서드 실행

let airCon = AirCon()
airCon.turnOn()             // "에어컨 켜기", 직접 구현한 메서드 실행
airCon.turnOff()            // "에어컨 끄기", 직접 구현한 메서드 실행
airCon.doAnotherAction()    // "에어컨 방향 조절하기", 직접 구현한 메서드 실행
```
