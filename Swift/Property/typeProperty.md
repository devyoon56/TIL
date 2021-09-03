# 타입 속성(Type Property)

타입 속성은 인스턴스에 속하는 속성이 아니라 클래스나 구조체(타입) 자체에 속하는 속성을 말합니다. 주로 저장 속성을 타입 속성으로 사용하고 계산 속성도 타입 속성으로 사용할 수 있습니다.

## 타입 속성을 사용하는 경우

그렇다면 타입 속성을 언제 사용할까요? 타입 속성을 사용하는 경우는 다음과 같은 경우입니다.

- 어떤 속성이 모든 인스턴스가 동일하게 가져야 하는 보편적인 성격을 갖는 경우
- 어떤 속성이 모든 인스턴스가 공유하는 성격을 갖는 경우

메모리 구조상 타입 속성은 메모리에서 데이터 영역의 타입 정의 부분에 위치합니다. 타입 속성은 각각의 인스턴스에 속하는 것이 아니라 타입 자체에 속하기 때문에 하나의 타입으로 생성한 모든 인스턴스는 모두 동일한 타입 속성을 사용할 수 있습니다.

## 저장 타입 속성 예시

먼저 저장 타입 속성에 대해 알아봅니다. 저장 타입 속성은 일반적인 저장 속성 앞에 **static** 키워드를 붙여서 선언합니다. 이렇게 저장 타입 속성을 선언하면 해당 속성은 인스턴스에 속하지 않고 타입 자체에 속하게 됩니다.

```swift
class Circle {
    // 저장 타입 속성 선언
    static let pi: Double = 3.14159
    static var count: Int = 0

    // 저장 속성 선언
    var radius: Double

    // 계산 속성 선언
    var diameter: Double {
        get {
            return radius * 2
        }
        set {
            radius = newValue / 2
        }
    }

    // 생성자
    init(radius: Double) {
        self.radius = radius
        Circle.count += 1       // 인스턴스 생성 시 타입 속성 count에 1을 더함
    }
}

var circle = Circle(radius: 2)
print(Circle.count)        // 1, 저장 타입 속성에 접근

var circle2 = Circle(radius: 4)
print(Circle.count)        // 2, 저장 타입 속성에 접근

print(Circle.pi)           // 3.14159, 저장 타입 속성에 접근
```

저장 타입 속성에 접근하려면 **타입명.속성** 과 같은 형태를 사용해야 합니다.

## 계산 타입 속성 예시

다음은 계산 타입 속성에 대해 알아봅니다. 저장 타입 속성과 동일하게 계산 속성 앞에 **static** 키워드를 붙여서 선언합니다. 타입 속성은 주로 저장 타입 속성을 사용하기 때문에 단순히 계산 타입 속성도 선언할 수 있다는 것을 살펴보기 위한 간단한 예시를 살펴봅니다.

```swift
class Circle {
    // 저장 타입 속성 선언
    static let pi: Double = 3.14159
    static var count: Int = 0

    // 계산 타입 속성 선언
    static var multiplyPiByTwo: Double {
        return pi * 2
    }

    // 저장 속성 선언
    var radius: Double

    // 생성자
    init(radius: Double) {
        self.radius = radius
        Circle.count += 1       // 인스턴스 생성 시 타입 속성 count에 1을 더함
    }
}

let a = Circle.multiplyPiByTwo      // 6.28318, 계산 타입 속성에 접근
```

저장 타입 속성과 마찬가지로 계산 타입 속성에 접근하려면 **타입명.속성** 과 같은 형태를 사용해야 합니다.
