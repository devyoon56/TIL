# 열거형의 연관값 Associated Value

열거형의 연관값은 열거형의 케이스에 추가적으로 구체적인 정보를 함께 저장할 수 있게 해줍니다. 열거형의 케이스마다 특징이 있고, 이러한 특징들을 저장하고 활용하고자 할 때 연관값을 사용할 수 있습니다.

## 1. 연관값을 가진 열거형 정의하기

연관값을 가진 열거형을 정의하려면 열거형의 케이스에 구체적인 정보를 명시합니다. 각 케이스마다 저장하고 싶은 데이터를 모두 다르게 튜플 형식으로 정의할 수 있습니다. 함수의 파라미터를 정의하는 것과 비슷하게 케이스의 연관값을 정의하면 됩니다.

```swift
// 애플 제품 열거형 타입으로 정의
// 각 애플 제품의 연관값을 정의
enum Apple {
    case iPhone(modelName: String, isProModel: Bool, color: String)
    case mac(year: Int, isProModel: Bool, screenInch: Double)
    case iPad(year: Int, isProModel: Bool, wifiModel: Bool)
    case airpods(isProModel: Bool, generation: Int)
}

// 애플 제품 열거형 생성
var myiPhone = Apple.iPhone(modelName: "XS", isProModel: false, color: "Space Gray")
var myAirpods = Apple.airpods(isProModel: true, generation: 1)
var myMac = Apple.mac(year: 2021, isProModel: false, screenInch: 13.3)
let myOldMac = Apple.mac(year: 2015, isProModel: true, screenInch: 15.4)
```

위의 코드처럼 열거형의 하나의 케이스마다 서로 다른 연관값을 저장할 수 있습니다. 이렇게 열거형의 연관값을 사용하면 케이스의 특징을 저장할 수 있습니다. 열거형의 원시값으로는 할 수 없는 일입니다.

열거형의 연관값은 열거형을 생성할 때 저장됩니다.

## 2. 원시값과 연관값의 비교

### 2.1 사용 목적

열거형의 원시값은 열거형 타입의 케이스마다 정수 또는 문자열을 매칭시켜 열거형 타입을 생성하거나 열거형 타입을 다룰 때 편리하게 개발하기 위한 목적으로 사용합니다.

열거형의 연관값은 열거형 타입의 케이스에 추가적으로 구체적인 정보를 저장하고자 할 때 사용합니다.

### 2.2 선언 방법

원시값은 열거형 이름 옆에 데이터 타입으로 선언합니다. 원시값의 데이터 타입은 Hashable 프로토콜을 준수하는 데이터 타입 아무거나 가능하지만 주로 Int와 String 타입을 사용합니다.

연관값은 열거형의 케이스에 튜플 형식으로 자유롭게 작성하면 됩니다.

### 2.3 값의 저장

원시값은 열거형을 선언하는 시점에 각 케이스마다 값이 매칭되어 저장됩니다.

연관값은 열거형을 생성하는 시점에 저장됩니다.

### 2.4 값의 변경

원시값은 열거형을 선언하는 시점에 저장되므로 열거형을 선언한 이후로 값을 변경할 수 없습니다.

연관값은 열거형을 생성할 때 하나의 케이스에 값을 다르게 할당하여 다른 값을 저장할 수 있습니다.

### 2.5 주의점

원시값과 연관값은 하나의 열거형에서 원시값과 연관값을 동시에 사용할 수 없습니다.

## 3. 연관값의 활용

연관값을 가진 케이스를 switch 문에서 패턴 매칭할 수 있습니다.

```swift
enum Apple {
    case iPhone(modelName: String, color: String)
    case mac(year: Int, color: String, screenInch: Double)
    case iPad(year: Int, color: String, screenInch: Double)
    case airpods(generation: Int)
}

var myiPhone = Apple.iPhone(modelName: "XS", color: "Space Gray")

switch myiPhone {
case .iPhone(modelName: let model, color: let modelColor):
    print("\(modelColor) 색상의 아이폰 \(model)")
case .mac(year: let releaseYear, color: let modelColor, screenInch: let screenSize):
    print("\(releaseYear)에 출시한 \(modelColor) 색상의 \(screenSize)인치 맥")
case .iPad(year: let releaseYear, color: let modelColor, screenInch: let screenSize):
    print("\(releaseYear)에 출시한 \(modelColor) 색상의 \(screenSize)인치 아이패드")
case .airpods(generation: let gene):
    print("\(gene)세대 에어팟")
}
```
