# 중첩 타입의 확장

클래스, 구조체, 열거형을 확장하여 새로운 중첩 타입을 추가할 수 있습니다.

## 중첩 타입의 확장 예시

Int 타입을 확장하여 새로운 중첩 열거형 Kind를 추가하는 예제입니다. 중첩 열거형 Kind는 인스턴스 계산 속성의 반환 타입으로 사용되고 해당 인스턴스 계산 속성 kind는 인스턴스가 0보다 큰지, 0보다 작은지, 0인지를 알려주는데 사용할 수 있습니다.

```swift
extension Int {

    enum Kind {
        case negative
        case zero
        case positive
    }

    var kind: Kind {
        switch self {
        case 0:
            return Kind.zero
        case let num where num > 0:
            return Kind.positive
        default:
            return Kind.negative
        }
    }
}

let num1 = 10
let num2 = 0
let num3 = -10

num1.kind       // positive
num2.kind       // zero
num3.kind       // negative
```

```swift
func printIntegerKinds(_ numbers: [Int]) {

    for number in numbers {         // number: Int 인스턴스
        switch number.kind {        // number.kind: Int 인스턴스의 계산 속성 kind (중첩 열거형 타입)
        case .negative:
            print("- ", terminator: "")
        case .zero:
            print("0 ", terminator: "")
        case .positive:
            print("+ ", terminator: "")
        }
    }

    print("")
}

printIntegerKinds([3, 19, -27, 0, -6, 0, 7])    // + + - 0 - 0 + 출력
```
