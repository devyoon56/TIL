# 열거형의 원시값 Raw Value

열거형의 **원시값**은 매칭되는 기본값을 정해서 열거형을 조금 더 쉽게 사용하게 해줍니다. 원시값은 다양한 타입(Hashable한 데이터 타입 Int, String, Character, Double 등)으로 정의할 수 있습니다. 주로 사용하는 원시값의 타입은 Int, String 입니다.

## 1. 원시값 정의하고 사용하기

Int타입으로 열거형의 원시값을 정의합니다. 원시값이 Int 타입일 때 열거형의 케이스에 원시값을 입력하지 않으면 자동으로 0부터 원시값을 할당합니다.

원시값을 사용하면 열거형의 인스턴스를 쉽게 생성할 수 있습니다. 원시값으로 인스턴스 생성 시 주의할 점은 옵셔널 열거형 타입을 반환한다는 것입니다. 이것은 원시값에 해당하는 케이스가 없을 수도 있기 때문입니다.

```swift
// 원시값이 Int 타입일 때
// 케이스에 원시값을 입력하지 않으면
// 자동으로 0부터 할당
enum Directions: Int {
    case forward             // rawValue: 0
    case backward           // rawValue: 1
    case left           // rawValue: 2
    case right          // rawValue: 3
}

// 원시값으로 인스턴스 생성
var carDirection = Directions(rawValue: 0)      // Directions?

// 접근 연산자로 원시값 접근 가능
var forwardRawValue: Int = Directions.forward.rawValue  // 0
var leftRawValue: Int = Directions.left.rawValue        // 2
```

다음은 String 타입으로 원시값을 정의합니다. 원시값이 String 타입일 때 열거형의 케이스에 원시값을 입력하지 않으면 자동으로 케이스 자체를 문자열로 할당합니다.

Int 타입과 마찬가지로 원시값으로 인스턴스 생성 시 옵셔널 열거형 타입을 반환하는 것에 주의해야 합니다.

```swift
enum Weekday: String {
    case monday         // rawValue = "monday"
    case tuesday        // rawValue = "tuesday"
    case wednesday
    case thursday
    case friday
    case saturday
    case sunday
}

// 원시값으로 인스턴스 생성
var today = Weekday(rawValue: "friday")     // Weekday?

// 접근 연산자로 원시값 접근 가능
Weekday.monday.rawValue         // monday
```
