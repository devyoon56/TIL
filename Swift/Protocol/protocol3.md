# 프로토콜 요구사항의 종류1

프로토콜을 정의할 때 나열하는 요구사항에는 크게 두 가지 종류가 있습니다.

1. 속성 요구사항
2. 메서드 요구사항

## 속성의 요구사항 정의하는 방법

먼저 속성의 요구사항을 정의하는 방법에 대해 알아봅니다.

- var 를 사용하여 선언해야 한다.
- get, set 키워드를 사용하여 읽기와 쓰기 여부를 결정한다.
- 최소한의 요구사항을 지정한다.

```swift
protocol RemoteMouse {

    var id: String { get }

    var name: String { get set }

    static var type: String { get set }

}
```

var id: String { get } 의 경우

- 최소한의 요구사항: get(읽기) 속성
- 저장 속성, 계산 속성 모두 구현 가능하다. (프로토콜의 요구사항만으로 두 종류의 속성 구별 불가능)
- 저장 속성으로 구현 가능 -> let, var 사용하여 구현 가능
- 계산 속성으로 구현 가능 -> 읽기 전용, 읽기/쓰기 모두 구현 가능

var name: String { get set } 의 경우

- 최소한의 요구사항: 읽기, 쓰기 속성
- 저장 속성, 계산 속성 모두 구현 가능하다. (프로토콜의 요구사항만으로 두 종류의 속성 구별 불가능)
- 저장 속성으로 구현 가능 -> var 사용하여 구현 가능
- 계산 속성으로 구현 가능 -> 읽기/쓰기로 구현 가능

static var type: String { get set } 의 경우

- 최소한의 요구사항: 읽기, 쓰기 타입 속성
- 저장 속성, 계산 속성 모두 구현 가능하다. (프로토콜의 요구사항만으로 두 종류의 속성 구별 불가능)
- 타입 저장 속성으로 구현 가능 -> static var로 구현 가능
- 타입 계산 속성으로 구현 가능 -> static 또는 class로 구현 가능
  - 클래스에서 채택 시 타입 계산 속성을 static으로 구현하면 재정의 불가능
  - 클래스에서 채택 시 타입 계산 속성을 class로 구현하면 재정의 가능
  - 클래스가 아닌 타입은 static으로 구현해야함 -> class로 구현 불가능

```swift
struct TV: RemoteMouse {

    var id: String = "456"
    // var 저장 속성: 읽기, 쓰기 모두 가능(최소 요구사항: 읽기)

    var name: String = "Samsung TV"
    // var 저장 속성: 읽기, 쓰기 모두 가능(최소 요구사항: 읽기, 쓰기)

    static var type: String = "리모컨"
    // var 타입 저장 속성: 읽기, 쓰기 모두 가능(최소 요구사항: 읽기, 쓰기)

}
```

클래스에서 static 키워드를 사용하여 타입 저장 속성으로 구현하는 경우

```swift
class SmartPhone: RemoteMouse {

    var id: String { return "123" }
    // 읽기 전용 계산 속성(최소 요구사항: 읽기)

    var name: String {
        get { return "아이폰" }
        set {}
    }
    // 읽기, 쓰기 계산 속성(최소 요구사항: 읽기, 쓰기)

    static var type: String = "리모컨"
    // 타입 저장 속성의 재정의 원칙적 불가능
}
```

클래스에서 class 키워드를 사용하여 타입 계산 속성으로 구현하는 경우

```swift
class Ipad: RemoteMouse {

    var id: String = "777"
    // var 저장 속성: 읽기, 쓰기 모두 가능(최소 요구사항: 읽기)

    var name: String = "아이패드"
    // var 저장 속성: 읽기, 쓰기 모두 가능(최소 요구사항: 읽기, 쓰기)

    class var type: String {
        get { "리모콘" }
        set {}
    }
    // 타입 계산 속성 재정의 가능 (class 키워드 사용)

}

class IpadAir: Ipad {

    override class var type: String {
        get { return "리모콘" }
        set {}
    }
    // 타입 계산 속성 재정의 가능 (class 키워드 사용)

}
```
