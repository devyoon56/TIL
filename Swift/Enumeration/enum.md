# 열거형 Enumeration

열거형은 스위프트에 내장된 기본 타입과 다르게 개발자가 직접 만들어서 사용할 수 있는 *사용자 정의 타입*입니다. 사용자 정의 타입에는 **Enum, Class, Struct**가 있습니다.

## 1. 열거형 기본 개념

열거형(Enumeration)은 **한정된 사례 안에서 정의**할 수 있는 타입입니다. 서로 연관된 케이스들을 하나의 이름으로 묶은 타입이라고 생각하면 됩니다. 열거체의 장점은 열거체는 한정된 케이스들을 정의한 타입이므로 정의한 케이스들만 사용할 수 있기 때문에 코드의 가독성과 코드 사용의 안정성이 올라갑니다.

한정된 케이스로 정의할 수 있는 대표적인 사례로는 월화수목금토일의 주7일, 나침판 방향의 동서남북, 1월부터 12월까지의 12달 등이 있습니다.

열거형을 사용하려면 먼저 열거형을 정의해야 합니다. 열거체는 **enum** 키워드로 정의합니다. 열거체의 이름은 대문자로 시작하고 각 케이스는 소문자로 시작합니다.

```swift
// 열거형 구문
enum SomeEnumeration {
    // 열거형 케이스 정의
}

// 주7일, 열거형 정의
enum Weekday {
    case monday
    case tuesday
    case wednesday
    case thursday
    case friday
    case saturday
    case sunday
}

// 나침판 방향, 열거형 정의
enum CompassPoint {
    case east
    case west
    case south
    case north
}

// 12달, 열거형 정의
enum Month {
    case january
    case February
    case march
    case april
    case may
    case june
    case july
    case august
    case september
    case october
    case november
    case december
}
```

## 2. 열거형 사용하기

열거형를 사용하는 것은 일반적인 스위프트 타입 사용과 동일하게 사용합니다. 열거형은 타입이므로 변수나 상수의 데이터 타입을 열거형으로 명시하고 명시한 열거형의 케이스를 할당하면 됩니다.

```swift
// 주7일, 열거형 정의
enum Weekday {
    case monday
    case tuesday
    case wednesday
    case thursday
    case friday
    case saturday
    case sunday
}

var today: Weekday = Weekday.friday // 열거형 타입의 값은 리터럴
var tomorrow: Weekday = .saturday   // 데이터 타입을 명시하면 타입 생략 가능
```

## 3. 열거형 분기처리

열거형의 분기처리는 **switch**문으로 처리하는 것이 가장 명확합니다. 특이한 점은 열거형 타입의 모든 케이스들을 분기처리하면 default 문을 작성하지 않아도 에러가 발생하지 않습니다.

```swift
var today: Weekday = .friday

switch today {
case .monday:
    print("오늘은 월요일입니다.")
case .tuesday:
    print("오늘은 화요일입니다.")
case .wednesday:
    print("오늘은 수요일입니다.")
case .thursday:
    print("오늘은 목요일입니다.")
case .friday:
    print("오늘은 금요일입니다.")   // 출력
case .saturday:
    print("오늘은 토요일입니다.")
case .sunday:
    print("오늘은 일요일입니다.")
}
```
