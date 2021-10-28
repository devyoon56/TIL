# 메서드 우선순위와 메서드 디스패치

메서드 우선순위와 메서드 디스패치의 관계에 대해 알아봅니다.

## 메서드 우선순위

타입에서 직접 구현한 메서드와 프로토콜의 확장에서 제공하는 기본 메서드 중 어떤 메서드를 실행하는지는 메서드의 우선순위에 따라 달라집니다. 메서드를 실행하는 우선순위는 다음과 같습니다.

1. 프로토콜을 채택한 타입에서 직접 구현한 메서드
2. 프로토콜의 확장에서 제공하는 기본 메서드

## 메서드 우선순위와 메서드 디스패치

메서드 디스패치는 간단하게 스위프트에서 메서드를 실행하는 방법을 말합니다. 사실 앞서 언급한 메서드 우선순위는 메서드 디스패치에 적용됩니다. 다양한 타입의 메서드 디스패치는 다음과 같이 결정됩니다.

1. 클래스

클래스는 채택한 프로토콜이 확장에서 기본적으로 제공하는 메서드와 프로토콜의 요구사항을 직접 구현한 메서드의 우선순위를 고려해서 클래스만의 메서드 테이블(Virtual Table)을 생성하고 테이블에 메서드의 실행 주소를 저장합니다.

- 타입 내부에 직접 구현한 메서드가 1순위가 됨
- 타입 내부에 직접 구현한 메서드가 없고 프로토콜의 확장에서 제공하는 기본 메서드가 있다면 해당 메서드가 2순위가 됨

프로토콜을 정의할 때 선언하지 않았지만 확장에서 제공하는 메서드는 Direct Dispatch로 동작합니다.

```swift
protocol Remote {
    func turnOn()
    func turnOff()
}

extension Remote {
    func turnOn() { print("리모컨 켜기") }
    func turnOff() { print("리모컨 끄기") }

    // 프로토콜 요구사항이 아닌 메서드
    func doAnotherAction() { print("리모컨 또 다른 동작") }
}

class TV: Remote {
    func turnOn() { print("TV 켜기") }
}

/*
[Class Virtual Table]
 - func turnOn()  { print("TV 켜기") }     실행 주소
 - func turnOff() { print("리모콘 끄기") } 실행 주소
*/

let tv = TV()
tv.turnOn()             // "TV 켜기"             (Virtual Table)
tv.turnOff()            // "리모컨 끄기"         (Virtual Table)
tv.doAnotherAction()    // "리모컨 또 다른 동작" (Direct Dispatch)
```

2. 구조체

구조체는 메서드 테이블을 생성하지 않고 다이렉트 디스패치라는 방법을 사용합니다. 구조체가 프로토콜을 채택했을 때 위에서 언급한 우선순위를 따라 다이렉트 디스패치를 사용합니다.

- 타입 내부에 직접 구현한 메서드가 1순위가 됨
- 타입 내부에 직접 구현한 메서드가 없고 프로토콜의 확장에서 제공하는 기본 메서드가 있다면 해당 메서드가 2순위가 됨

프로토콜을 정의할 때 선언하지 않았지만 확장에서 제공하는 메서드는 Direct Dispatch로 동작합니다.

```swift
protocol Remote {
    func turnOn()
    func turnOff()
}

extension Remote {
    func turnOn() { print("리모컨 켜기") }
    func turnOff() { print("리모컨 끄기") }

    // 프로토콜 요구사항이 아닌 메서드
    func doAnotherAction() { print("리모컨 또 다른 동작") }
}

struct AirCon: Remote {
    func turnOn() { print("에어컨 켜기") }
    func turnOff() { print("에어컨 끄기") }
}

let airCon = AirCon()
airCon.turnOn()                 // "에어컨 켜기"          (Direct Dispatch)
airCon.turnOff()                // "에어컨 끄기"          (Direct Dispatch)
airCon.doAnotherAction()        // "리모컨 또 다른 동작"  (Direct Dispatch)
```

3. 프로토콜

프로토콜을 채택하는 타입은 프로토콜을 정의할 때 선언한 메서드에 대해서만 위에서 언급한 우선순위를 따라 메서드 테이블(Witness Table)을 생성하고 메서드의 실행 주소를 저장합니다. 프로토콜을 정의할 때 선언하지 않았지만 확장에서 제공하는 메서드는 메서드 테이블에 추가되지 않습니다.

- 타입 내부에 직접 구현한 메서드가 1순위가 됨
- 타입 내부에 직접 구현한 메서드가 없고 프로토콜의 확장에서 제공하는 기본 메서드가 있다면 해당 메서드가 2순위가 됨

프로토콜을 정의할 때 선언하지 않았지만 확장에서 제공하는 메서드는 Direct Dispatch로 동작합니다.

```swift
protocol Remote {
    func turnOn()
    func turnOff()
}

extension Remote {
    func turnOn() { print("리모컨 켜기") }
    func turnOff() { print("리모컨 끄기") }

    // 프로토콜 요구사항이 아닌 메서드
    func doAnotherAction() { print("리모컨 또 다른 동작") }
}

class Ipad: Remote {
    func turnOn() { print("아이패드 켜기") }
    func doAnotherAction() { print("아이패드 다른 동작") }
}

/*
[Protocol Witness 테이블] - 요구사항 메서드 테이블(우선순위에 맞게 생성)
 - func turnOn()  { print("아이패드 켜기") } 실행 주소
 - func turnOff() { print("리모컨 끄기") }   실행 주소
*/

let ipad: Remote = Ipad()
ipad.turnOn()               // "아이패드 켜기"    (Witness Table)
ipad.turnOff()              // "리모컨 끄기"      (Witness Table)
ipad.doAnotherAction()      // "리모컨 다른 동작" (Direct Dispatch)
```

Ipad 클래스의 인스턴스를 생성하고 Remote 타입으로 인식시키는 경우 Ipad 클래스의 인스턴스는 Remote 프로토콜의 Witness Table을 참조하여 메서드를 실행합니다.
