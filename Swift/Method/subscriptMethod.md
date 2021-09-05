# 서브스크립트(Subscripts)

서브스크립트는 대괄호([])를 사용하는 문법입니다. 서브스크립트를 사용하는 것은 사실 익숙합니다. 왜냐하면 배열과 딕셔너리에서 서브스크립트(대괄호)를 사용해서 배열의 원소와 딕셔너리의 값에 접근할 수 있기 때문입니다. 그 이유는 무엇일까요?

```swift
var array = ["Hello", "Swift"]

array[0]        // Hello, 서브스크립트 사용
array[1]        // Swift, 서브스크립트 사용
```

이 대괄호는 사실 특별한 형태의 메서드를 호출하는 것입니다. 배열과 딕셔너리에는 이미 대괄호 형태의 메서드가 구현되어 있으므로 이 메서드를 사용할 수 있는 것입니다. 구조체인 배열과 딕셔너리에 이와 같은 서브스크립트 메서드가 구현되어 있는 것처럼 자신만의 클래스와 구조체를 정의할 때 서브스크립트 메서드를 구현할 수 있습니다.

## 서브스크립트 특징

1. 메서드 이름은 생성자 메서드(init)처럼 특별한 키워드인 **subscript**를 사용합니다.
2. 인스턴스 뿐만 아니라 타입 메서드로도 구현할 수 있습니다.
   - 타입 서브스크립트는 **static** 또는 **class**를 **subscript** 앞에 붙여 정의합니다.
   - **static**을 사용하면 클래스 상속 시 재정의가 불가능하고
   - **class**를 사용하면 클래스 상속 시 재정의가 가능합니다.
3. 메서드이므로 메모리 공간을 할당받지 않습니다.
   - 인스턴스 메서드, 타입 메서드가 메모리 공간을 할당받지 않는 것과 같습니다.
   - 타입 정의에 메서드 실행 주소가 저장되어 있습니다.
4. 메서드를 호출하려면 인스턴스 이름, 타입 이름과 대괄호를 사용합니다.(서브스크립트 문법)
   - 인스턴스명[파라미터]
   - 타입명[파라미터]
5. 파라미터 두 개 이상도 구현할 수 있습니다.
6. 아규먼트 레이블은 사용하지 않습니다.

## 인스턴스 서브스크립트 예제

```swift
class SomeData {
    var data = ["apple", "iOS", "Swift", "Subscript"]

    // 인스턴스 서브스크립트
    subscript(index: Int) -> String {
        get {
            return data[index]
        }
        set {
            data[index] = newValue
        }
    }
}

var data = SomeData()
data[0]                 // apple, 서브스크립트 메서드로 읽기
data[0] = "Apple"       // 서브스크립트 메서드로 쓰기
```

서브스크립트 메서드에는 계산 속성처럼 getter, setter를 구현할 수 있습니다.

- 서브스크립트로 읽는 경우, get 블럭 내부의 코드를 실행합니다.
- 서브스크립트로 쓰는 경우, set 블럭 내부의 코드를 실행합니다.
- 계산 속성처럼 set 블럭 내부에서 newValue라는 파라미터를 사용할 수 있습니다.
- getter는 필수적이고 setter는 선택적입니다.

```swift
struct TimesTable {
    let multiplier = 3

    subscript(index: Int) -> Int {
        return multiplier * index
    }
}

let threeTimesTable = TimesTable()
print("6에 3배를 하면 \(threeTimesTable[6])이(가) 나옵니다.)
// 6에 3배를 하면 18이(가) 나옵니다.
```

2개의 파라미터를 받는 서브스크립트를 구현할 수 있습니다.

```swift
struct Matrix {
    var data = [["1", "2", "3"],
                ["4", "5", "6"],
                ["7", "8", "9"]]

    // 2개의 파라미터를 받는 서브스크립트 구현
    subscript(row: Int, column: Int) -> String? {
        if row >= 3 || column >= 3 {
            return nil
        }
        return data[row][column]
    }
}

var mat = Matrix()
mat[0, 1]           // Optional("2")
```

## 타입 서브스크립트 예제

```swift
enum Planet: Int {
    case mercury = 1, venus, earth, mars, jupiter, saturn, uranus, neptune

    // 타입 서브스크립트
    static subscript(n: Int) -> Planet {
        return Planet(rawValue: n)!     // 원시값으로 열거형 생성 시 옵셔널 열거형 생성
    }
}

let mars = Planet[4]
print(mars)         // mars
```

타입 메서드처럼 static과 class 키워드로 타입 서브스크립트를 구현할 수 있습니다. class 키워드를 사용하면 클래스 상속 시 재정의가 가능한 타입 서브스크립트를 구현할 수 있습니다.

> static 키워드를 사용한 타입 메서드 또는 타입 서브스크립트도 클래스 상속은 가능합니다. 하지만 클래스 상속 시 재정의가 불가능합니다.
