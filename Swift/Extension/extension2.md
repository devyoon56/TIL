# 계산 속성의 확장

확장에서 타입, 인스턴스의 계산 속성을 추가할 수 있습니다.

## 타입 계산 속성의 확장

```swift
extension Double {
    static var zero: Self {
        return 0.0
    }
}

Double.zero     // 0.0
```

Double 타입을 확장하여 타입 계산 속성 zero를 추가하였습니다.

## 인스턴스 계산 속성의 확장

아래 예제는 Double 타입을 확장하여 읽기 전용 계산 속성을 추가하는 예제입니다. (소급-모델링) 단위를 입력하면 m 단위로 바꿔주는 계산 속성입니다.

```swift
extension Double {
    var km: Self { return self * 1000.0 }
    var m: Self { return self }
    var cm: Self { return self / 100.0 }
    var mm: Self { return self / 1000.0 }
    var ft: Self { return self / 3.28084 }
}

let oneInch = 25.4.mm
print("1인치는 \(oneInch) 미터")       // "1인치는 0.0254 미터"

let threeFeet = 3.ft
print("3피트는 \(threeFeet) 미터")     // "3피트는 0.914399970739201 미터"

let marathon = 42.km + 195.m
print("마라톤은 \(marathon) 미터이다.")     // "마라톤은 42195.0 미터이다."
```

Double 타입의 인스턴스에 접근 연산자를 사용하여 m 단위로 단위 변환을 할 수 있습니다.

다음 예제는 Int 타입을 확장하여 인스턴스의 제곱값을 반환하는 계산 속성을 추가하는 예제입니다.

```swift
extension Int {
    var squared: Self {
        return self * self
    }
}

func squared(num: Int) -> Int {
    return num * num
}

Int(123).squared            // 추가한 계산 속성을 사용해서 제곱값 얻기
123.squared                 // 추가한 계산 속성을 사용해서 제곱값 얻기

squared(num: 123)           // 함수를 사용해서 제곱값 얻기
```

함수를 직접 정의해서 제곱값을 얻는 것보다 계산 속성으로 구현하는 것이 훨씬 간단하고 사용하기도 쉽다는 장점이 있습니다.
