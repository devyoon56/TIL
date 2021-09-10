# 지정 생성자(Designated Initializer)

지정 생성자는 **init()** 의 형태를 가지는 생성자입니다. 구조체, 클래스 또는 열거형은 모두 지정 생성자를 구현할 수 있습니다. 지정 생성자의 특징에 대해 알아보겠습니다.

## 지정 생성자

- **init()** 의 형태를 갖는 생성자를 말합니다.
- 지정 생성자는 인스턴스 생성 시 모든 저장 속성을 초기화해야 합니다.
  - 저장 속성 선언 시 값을 할당하거나 저장 속성을 옵셔널로 선언할 수도 있습니다.
- 오버로딩이 가능하므로 다양한 지정 생성자를 구현할 수 있습니다.
- 지정 생성자를 구현하지 않고 모든 저장 속성이 초기화되는 경우 기본 생성자 init()이 자동 제공됩니다.
- 하지만 지정 생성자를 1개 이상 구현하면 기본 생성자를 제공하지 않습니다.

## 구조체 지정 생성자

먼저 구조체의 여러개의 지정 생성자를 구현해봅니다.

```swift
struct Color {
    let red: Double
    let green: Double
    let blue: Double

    // 기본 생성자: 기본값을 설정하면 자동으로 제공
    init() {
        red = 0.0
        green = 0.0
        blue = 0.0
    }

    // 지정 생성자
    init(white: Double) {
        red = white
        gree = white
        blue = white
    }

    // 지정 생성자
    init(red: Double, green: Double, blue: Double) {
        self.red = red
        self.green = green
        self.blue = blue
    }
}
```

위와 같이 구조체의 지정 생성자를 구현할 수 있습니다. 하지만 이런 방식으로 지정 생성자를 구현하는 것은 올바른 구현 방식이 아닙니다. 왜냐하면 지정 생성자의 코드가 중복된다고 볼 수 있기 때문입니다.

일반적으로 지정 생성자를 구현하는 방법은 다음과 같습니다.

```swift
struct Color {
    let red, green, blue: Double

    init() {
        self.init(red: 0.0, green: 0.0, blue: 0.0)              // 다른 지정 생성자 호출
    }

    init(white: Double) {
        self.init(red: white, green: white, blue: white)        // 다른 지정 생성자 호출
    }

    init(red: Double, green: Double, blue: Double) {
        self.red = red
        self.green = green
        self.blue = blue
    }
}
```

일반적으로 위와 같이 생성자를 구현할 수 있습니다. 생성자에서 다른 생성자를 호출하는 방식입니다. 생성자 내부에서 self.init()을 사용하면 다른 생성자를 호출할 수 있습니다.

코드를 보면 모든 저장 속성을 초기화하는 지정 생성자를 구현하고 이 지정 생성자를 호출하는 방식을 사용하고 있습니다. 여기서 모든 저장 속성을 초기화하는 지정 생성자는 init(red:green:blue:) 입니다.

클래스의 지정 생성자는 다음 글에서 알아보겠습니다.
