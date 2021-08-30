# 옵셔널 열거형과 스위치문

열거형이 옵셔널인 경우, 옵셔널 자체는 열거형이므로 옵셔널 열거형은 열거형을 감싸는 열거형의 형태가 됩니다. 옵셔널 열거형의 분기처리도 스위치문을 사용하면 편리하게 처리할 수 있습니다.

## 옵셔널 열거형 case 패턴 예제

옵셔널 열거형을 스위치문으로 분기처리할 때 원칙적인 방법이 있습니다. 또한 스위치문은 옵셔널을 쉽게 사용할 수 있도록 편의적인 기능도 제공합니다. 스위치문에서 옵셔널 열거형을 사용할 때 옵셔널 포장을 벗기지 않아도 열거형 내부값에 접근할 수 있습니다.

```swift
enum LeftOrRight {
    case left
    case right
}

// 옵셔널 열거형 생성
let rightDirection: LeftOrRight? = .right

// 옵셔널 열거형 분기처리(원칙)
switch rightDirection {
case .some(let direction):  // Optional.some(let direction) = Optional.some(LeftOrRight.right)
    switch direction {
    case .left:
        print("왼쪽으로 가기")
    case .right:
        print("오른쪽으로 가기")
    }
case .none:
    print("가만히 있기")
}

// 옵셔널 열거형 분기처리(편의적 기능)
switch rightDirection {
case .left:
    print("왼쪽으로 가기")
case .right:
    print("오른쪽으로 가기")
case .none:
    print("가만히 있기")
}
```
