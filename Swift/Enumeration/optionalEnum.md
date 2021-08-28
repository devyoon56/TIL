# 옵셔널의 내부

옵셔널 타입은 비어있는 메모리 공간에 접근했을 때 발생하는 에러를 방지하도록 메모리 공간에 임시적인 타입을 담아두는 개념이라고 볼 수 있습니다. 임시적인 타입은 값이 있느냐와 없느냐에 따라 Optional(값) 또는 nil이 됩니다. 이 임시적인 타입의 값 사용하려면 옵셔널 포장을 먼저 벗겨야 합니다.

옵셔널의 임시적인 타입 개념은 내부적으로 열거형으로 구현되어 있습니다. 옵셔널 타입은 값이 있는 경우와 없는 경우로 나뉘기 때문에 열거형으로 정의하기에 적합합니다. 옵셔널은 값이 있는 경우 some 케이스에 연관값을 저장하고 값이 없는 경우 none 케이스에 해당됩니다. none 케이스는 값이 없음을 표현하는 nil 키워드와 동일합니다.

```swift
enum Optional<Wrapped> {    // 제너릭
    case some(Wrapped)
    case none
}
```

옵셔널은 열거형이므로 switch 문으로 분기처리를 할 수 있습니다.

```swift
var optionalNum: Int? = 7

switch optionalNum {
case .some(let num):    // 열거형 case 패턴, let num = 7
    print(num)          // 7을 출력
case .none:             // .none: 명시적인 열거형 표현
    print("nil입니다.")
}
```
