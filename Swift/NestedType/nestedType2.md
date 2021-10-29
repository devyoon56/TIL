# 중첩 타입의 활용

애플의 공식 문서의 예시를 보면서 중첩 타입을 사용하는 방법에 대해 알아봅니다.

## 중첩 타입의 활용 예시

```swift
struct BlackjackCard {

    // 중첩 타입 선언: 카드의 세트를 표현하는 열거형
    enum Suit: Character {
        case spades = "♠", hearts = "♡", diamonds = "♢", clubs = "♣"
    }

    // 중첩 타입 선언: 카드의 숫자를 표현하는 열거형
    enum Rank: Int {
        case two=2, three, four, five, six, seven, eight, nine, ten
        case jack, queen, king, ace     // 원시값을 사용하지 않는 케이스

        // 중첩 타입 선언: Rank 열거형의 원시값을 사용하지 않는 케이스를 표현하는 구조체
        struct Values {
            let first: Int
            let second: Int?
        }

        // Values 타입의 계산 속성
        var values: Values {
            switch self {                                               // self: Rank 열거형의 인스턴스
            case .ace:
                return Values(first: 1, second: 11)                     // ace: 1 또는 11 으로 사용
            case .jack, .queen, .king:
                return Values(first: 10, second: nil)                   // jack, queen, king: 10 으로 사용
            default:
                return Values(first: self.rawValues, second: nil)       // 나머지: 원시값으로 사용
            }
        }
    }

    // 카드 한 장: 세트 + 숫자
    let suit: Suit
    let rank: Rank

    // 카드를 표현하는 계산 속성
    var description: String {
        var output = "\(suit.rawValue) 세트,"
        output += "숫자 \(rank.values.first)"

        if let second = rank.values.second { output += "또는 \(second)" }

        return output
    }
}
```

BlackjackCard 구조체를 선언하면 다음과 같이 인스턴스를 생성할 수 있습니다.

```swift
// 카드: 스페이드 - 10
let card1 = BlackjackCard(suit: .spades, rank: .ten)

// 카드: 하트 - 에이스
let card2 = BlackjackCard(suit: .hearts, rank: .ace)

// 카드: 다이아몬드 - 2
let card3 = BlackjackCard(suit: .diamonds, rank: .two)
```

BlackjackCard 내부에 열거형 Suit, Rank를 선언하여 BlackjackCard 타입의 인스턴스를 생성할 때 편리하게 사용할 수 있습니다. 한 장의 카드는 Suit(세트), Rank(숫자)로 표현할 수 있으므로 포함 관계도 명확합니다.

## 중첩 타입을 활용하는 API

실제 많은 API들은 중첩 타입을 활용하여 설계되었습니다. 대표적으로 DateFormatter 클래스가 있습니다.

```swift
let formatter = DateFormatter()

formatter.dateStyle = DateFormatter.Style.long
formatter.dateStyle = .full

/**==========================================================
 - var dateStyle: Style { get set }                 (타입확인)
 - var dateStyle: DateFormatter.Style { get set }   (내부정의)
============================================================**/
```

만약 DateFormatter 내부에 선언된 Style 타입이 DateFormatter 외부에서 선언된다면 Style 타입이 어떤 타입에 대해 어떤 역할을 하는지 명확하지 않았을 것입니다. 포함 관계가 불분명해지고 역할을 명확하게 알 수 없습니다.

따라서 DateFormatter 내부에 Style 타입이 선언되어 있습니다. 이렇게 내부에 중첩된 Style 타입이 DateFormatter 타입에 포함되어 다양한 형식을 나타내는 역할을 한다는 것이 명확해지는 것입니다.
