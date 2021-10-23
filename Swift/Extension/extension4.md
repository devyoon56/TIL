# 생성자의 확장

먼저 클래스 생성자의 확장에 대해 알아보겠습니다.

## 클래스 생성자의 확장

클래스의 확장에서 생성자를 추가하는 경우

- 클래스의 확장에서 지정 생성자는 추가할 수 없고 편의 생성자만 추가할 수 있습니다.
- 편의 생성자를 추가할 때 편의 생성자는 이미 정의된 지정 생성자를 호출해야 합니다.
  - 결국 클래스의 지정 생성자가 인스턴스를 생성하는 역할을 하기 때문입니다.

## 클래스 생성자의 확장 예시

UIColor 타입을 확장하여 편의 생성자를 구현하는 예제입니다.

```swift
// UIColor 클래스의 지정 생성자로 인스턴스 생성
var color = UIColor(red: 0.3, green: 0.5, blue: 0.4, alpha: 1)

extension UIColor {
    convenience init(color: CGFloat) {
        // 편의 생성자는 반드시 지정 생성자를 호출해야 합니다.
        self.init(red: color/255, green: color/255, blue: color/255, alpha: 1)
    }
}

// UIColor 클래스의 확장에서 추가한 편의 생성자로 인스턴스 생성
var color2 = UIColor(color: 1.0)
```

확장에서 추가한 편의 생성자로 편리하게 인스턴스를 생성할 수 있습니다.

## 값타입의 확장

값타입(구조체, 열거형)을 확장하여 생성자를 추가하는 경우

1. 값타입이 자동으로 기본 생성자와 멤버와이즈 생성자를 제공하는 경우

   - 모든 저장 속성에 기본값을 할당하고 어떤 생성자도 정의하지 않았다면 값타입은 자동으로 기본 생성자와 멤버와이즈 생성자를 제공합니다.
   - 값타입을 확장하여 생성자를 추가할 때 해당 생성자 내부에서 기본 생성자와 멤버와이즈 생성자를 호출할 수 있습니다.
   - 기본 생성자와 멤버와이즈 생성자를 호출하지 않고 자유롭게 구현할 수도 있습니다.

2. 값타입이 자동으로 기본 생성자와 멤버와이즈 생성자를 제공하지 않는 경우

   - 만약 값타입을 정의할 때 생성자를 구현했다면 값타입은 자동으로 기본 생성자와 멤버와이즈 생성자를 제공하지 않습니다.
   - 값타입을 정의할 때 생성자를 구현했다면 값타입의 확장에서 생성자를 추가할 때 정의된 생성자를 호출할 수 있습니다.
   - 정의된 생성자를 호출하지 않고 자유롭게 구현할 수도 있습니다.

## 구조체 생성자의 확장 예시

직사각형을 나타내는 Rect 구조체를 정의하는 예제입니다. 또한 모든 저장 속성에 기본값을 할당하고 있는 Size, Point 구조체를 정의하여 Rect 구조체 내부에서 사용합니다.

```swift
struct Size {
    var width = 0.0, height = 0.0
}

struct Point {
    var x = 0.0, y = 0.0
}

struct Rect {
    var origin = Point()
    var size = Size()
}
```

Rect 구조체 또한 모든 저장 속성에 기본값을 할당하고 있기 때문에 기본 생성자와 멤버와이즈 생성자를 제공받습니다.

```swift
// 기본 생성자를 사용하여 인스턴스 생성
let defaultRect = Rect()

// 멤버와이즈 생성자를 사용하여 인스턴스 생성 (origin, size 속성의 경우 멤버와이즈 생성자 사용하여 인스턴스 생성)
let memberwiseRect = Rect(origin: Point(x: 2.0, y: 2.0), size: Size(width: 5.0, height: 5.0))

// 멤버와이즈 생성자를 사용하여 인스턴스 생성 (origin, size 속성의 경우 기본 생성자 사용하여 인스턴스 생성)
let memberwiseRect = Rect(origin: Point(), size: Size())
```

Rect 구조체를 확장하여 추가적인 생성자를 구현할 수 있습니다. 생성자를 구현할 때 멤버와이즈 생성자를 호출할 수 있습니다.

```swift
extension Rect {
    init(center: Point, size: Size) {
        let originX = center.x - (size.width / 2)
        let originY = center.y - (size.height / 2)

        // 멤버와이즈 생성자 호출
        self.init(origin: Point(x: originX, y: originY), size: size)
    }
}

// 추가한 생성자를 사용하여 인스턴스 생성
let centerRect = Rect(center: Point(x: 4.0, y: 4.0), size: Size(width: 3.0, height: 3.0))
centerRect.origin.x     // 2.5
centerRect.origin.y     // 2.5
centerRect.size.width   // 3.0
centerRect.size.height  // 3.0
```
