# 클래스와 구조체

스위프트에는 사용자 정의 타입으로 클래스, 구조체, 열거형이 있습니다.

클래스 또는 구조체는 객체지향 프로그래밍에서 말하는 객체를 생성하기 위한 어떤 틀을 의미합니다. 하나의 클래스 또는 구조체를 정의해놓으면 다양한 객체를 쉽게 생성할 수 있습니다. 여기서 말하는 객체는 클래스나 구조체로 만든 실제 데이터를 말합니다. 객체는 실제로 메모리에 할당되고 구체적인 실체를 가지기 때문에 실제 데이터라고 할 수 있는 것입니다. 객체는 인스턴스라고도 합니다.

쉽게 클래스를 이해하기 위해 붕어빵을 만든다고 가정해보겠습니다. 붕어빵을 만들기 위해 붕어빵 틀이 필요합니다. 이러한 붕어빵 틀을 클래스 또는 구조체라고 합니다. 붕어빵 틀로는 다양한 붕어빵을 만들 수 있습니다. 이렇게 붕어빵 틀을 사용하여 만든 붕어빵은 하나의 객체(인스턴스)라고 합니다. 붕어빵을 만들 때는 팥을 사용할 수도 있고 크림을 사용할 수도 있습니다. 즉 다양한 인스턴스를 생성할 수 있는 것입니다.

## 클래스와 구조체 정의와 객체 생성

먼저 클래스를 정의하고 객체를 생성하는 방법에 대해 알아봅니다.

```swift

// 스마트폰 틀(클래스) 정의
class Smartphone {
    var os = "iOS"
    var model = "iPhone 12"
    var color = "white"

    func ring() {
        print("벨이 울립니다.")
    }
}

// 스마트폰(객체) 생성
var smartphone1 = Smartphone()

// 객체 속성에 접근
print(smartphone1.os)           // iOS
print(smartphone1.model)        // iPhone 12
print(smartphone1.color)        // white

// 객체 메서드 호출
smartphone1.ring()              // 벨이 울립니다.
```

구조체를 정의하고 생성하는 방법에 대해 알아봅니다.

```swift

// 태블릿 틀(구조체) 정의
struct Tablet {
    var os = "iPadOS"
    var model = "iPad Pro 12.9-inch"
    var color = "Space Gray"

    func drawing() {
        print("펜으로 그림을 그립니다.")
    }
}

// 태블릿(객체) 생성
var tablet1 = Tablet()

// 객체 속성에 접근
print(tablet1.os)           // iPadOS
print(tablet1.model)        // iPad Pro 12.9-inch
print(tablet1.color)        // Space Gray

// 객체 메서드 호출
tablet1.drawing()           // 펜으로 그림을 그립니다.
```

클래스와 구조체의 변수와 함수를 칭하는 용어가 있습니다. 클래스와 구조체를 정의할 때 내부의 변수는 '프로퍼티(속성)'라고 합니다. 그리고 내부의 함수는 '메서드'라고 합니다.
