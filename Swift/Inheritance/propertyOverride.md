# 속성 재정의

속성을 재정의하는 방법에 대해 알아보겠습니다. 속성을 아래와 같이 재정의 할 수 있습니다.

> 타입 속성, 인스턴스 속성을 구분해야 하지만 타입 속성을 재정의하는 것은 매우 드문 일이므로 타입 속성의 재정의는 배제합니다.

인스턴스 속성의 재정의 원칙

1. 저장 속성 재정의는 원칙적으로 불가능합니다. 그러나 메서드 형태로 재정의할 수 있습니다.
2. 계산 속성의 유지 및 확장은 가능합니다. 그러나 기능 축소는 불가능합니다.
3. 속성 감시자를 추가하는 재정의는 가능합니다. 그러나 읽기 전용 계산 속성 값의 변화를 관찰하는 것은 논리에 맞지 않습니다.

## 저장 속성의 재정의

저장 속성을 재정의하는 것은 원칙적으로 불가능합니다. 그 이유는 다음과 같습니다.

- 저장 속성은 메모리의 클래스 정의 부분에서 고유의 메모리 공간을 갖습니다.
- 서브 클래스에서 저장 속성의 고유 메모리 공간을 바꾸는 방식으로 저장 속성을 재정의할 수 없습니다.

따라서 서브 클래스에서 저장 속성을 재정의하려면 메서드로 변형하는 방식을 사용해야 합니다. 그렇게 하기 위해서는 저장 속성을 계산 속성으로 재정의해야 합니다.

- 읽기와 쓰기 모두 가능한 계산 속성으로 재정의할 수 있습니다. 계산 속성은 형태는 속성이지만 실질적으로 메서드이기 때문입니다.
  - 그렇지만 읽기만 가능한 계산 속성으로 재정의할 수 없습니다.
  - 왜냐하면 기본적으로 저장 속성은 쓰기와 읽기 모두 가능한데 읽기만 가능하도록 기능을 축소하는 재정의는 불가능하기 때문입니다.

또한 저장 속성에 속성 감시자를 추가하는 방식으로 재정의할 수 있습니다.

- 속성 감시자 또한 속성의 변화 시점을 관찰하는 메서드이기 때문입니다.

다음 예시는 저장 속성을 계산 속성으로, 속성 감시자를 추가하여 재정의하는 예시입니다.

```swift
class Vehicle {
    var currentSpeed = 0.0                      // 저장 속성
}

class Bicycle1: Vehicle {
    override var currentSpeed: Double {         // 계산 속성으로 재정의
        get {
            return super.currentSpeed
        }
        set {
            super.currentSpeed = newValue
        }
    }
}

let bicycle1 = Bicycle()
bicycle1.currentSpeed               // 0.0
bicycle1.currentSpeed = 5.0
bicycle1.currentSpeed               // 5.0

class Bicycle2: Vehicle {
    override var currentSpeed: Double {         // 속성 감시자를 추가하여 재정의
        willSet {
            print("\(currentSpeed)에서 \(newValue)로 속도가 변경됩니다.")
        }
        didSet {
            print("\(oldValue)에서 \(currentSpeed)로 속도가 변경되었습니다.")
        }
    }
}

let bicycle2 = Bicycle2()
bicycle2.currentSpeed               // 0.0
bicycle2.currentSpeed = 5.0

// 출력 결과
// 0.0에서 5.0로 속도가 변경됩니다.
// 0.0에서 5.0로 속도가 변경되었습니다.
```

## 계산 속성의 재정의

계산 속성은 속성의 형태를 가진 메서드이므로 메서드 형태로만 재정의 가능합니다. 다만 메서드 기능을 축소하는 형태로 재정의하는 것은 불가능합니다.

슈퍼 클래스의 읽기 전용 계산 속성의 경우

- 서브 클래스에서 읽기와 쓰기 가능한 계산 속성으로 재정의 가능합니다.
- 속성 감시자를 추가하는 재정의는 불가능합니다.
  - 슈퍼 클래스의 계산 속성이 읽기 전용이므로 속성 감시자를 추가하는 것은 논리에 맞지 않습니다.

슈퍼 클래스의 읽기와 쓰기 가능한 계산 속성의 경우

- 서브 클래스에서 읽기만 가능한 계산 속성으로 재정의하는 것은 불가능합니다.
  - 메서드의 기능을 축소하는 형태로 재정의할 수 없습니다.
- 속성 감시자를 추가하는 재정의는 가능합니다.
  - 속성의 변화 시점을 관찰하는 메서드를 추가하는 것입니다.

다음 예시는 슈퍼 클래스의 읽기 전용 계산 속성을 서브 클래스에서 재정의하는 예시입니다.

```swift
class Vehicle {
    var currentSpeed = 1.0

    var halfSpeed: Double {                         // 읽기 전용 계산 속성
        return currentSpeed / 2
    }
}

class Bicycle1: Vehicle {
    override var halfSpeed: Double {                // 읽기 쓰기 계산 속성으로 재정의
        get {
            return super.currentSpeed / 2
        }
        set {
            super.currentSpeed = newValue * 2
        }
    }
}

let bicycle1 = Bicycle1()
bicycle1.currentSpeed           // 1.0
bicycle1.halfSpeed              // 0.5
bicycle1.halfSpeed = 2.0
bicycle1.currentSpeed           // 4.0
```

다음 예시는 슈퍼 클래스의 읽기 쓰기 계산 속성을 서브 클래스에서 재정의하는 예시입니다.

```swift
class Vehicle {
    var currentSpeed = 1.0

    var halfSpeed: Double {                     // 읽기 쓰기 계산 속성
        get {
            return currentSpeed / 2
        }
        set {
            currentSpeed = newValue * 2
        }
    }
}

class Bicycle2: Vehicle {
    override var halfSpeed: Double {            // 속성 감시자를 추가하여 재정의
        willSet {
            print("\(halfSpeed)에서 \(newValue)로 속도가 변경됩니다.")
        }
        didSet {
            print("\(oldValue)에서 \(halfSpeed)로 속도가 변경되었습니다.")
        }
    }
}

let bicycle2 = Bicycle2()
bicycle2.currentSpeed           // 1.0
bicycle2.halfSpeed              // 0.5
bicycle2.halfSpeed = 2.0

// 0.5에서 2.0으로 속도가 변경됩니다.
// 0.5에서 2.0으로 속도가 변경되었습니다.

bicycle2.currentSpeed           // 4.0
```
