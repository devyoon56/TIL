# 연관값이 있는 열거형과 스위치문

연관값이 있는 열거형을 분기처리하는 경우, 열거형 case 패턴을 사용합니다. 열거형 case 패턴은 연관값을 변수나 상수에 바인딩하는 패턴을 말합니다.

## 연관값이 있는 열거형 case 패턴 예제

```swift
// 연관값이 있는 열거형 정의
enum Apple {
    case iPhone(modelName: String, modelColor: String)
    case mac(year: Int, screenInch: Double)
    case airpods(isProModel: Bool, generation: Int)
}

// 연관값이 있는 열거형 생성
var myAppleDevice: Apple = .iPhone(modelName: "아이폰 XS", modelColor: "스페이스 그레이")

// 연관값이 있는 열거형의 분기처리
// 바인딩 패턴 사용
switch myAppleDevice {
case .iPhone(let model, let color):
    print("\(color) 색상의 \(model) 모델입니다.")
case .mac(let year, let screenSize):
    print("\(year)년에 출시한 \(screenSize)인치 모델입니다.")
case .airpods(isProModel: true, generation: 1):
    print("에어팟 프로 모델입니다.")
case .airpods(isProModel: false, let generation):
    print("에어팟 \(generation)세대 모델입니다.")
}
default:
    print("아이폰, 맥, 에어팟 모델만 출력합니다.")

// "스페이스 그레이 색상의 아이폰 XS 모델입니다." 출력
```

연관값의 특정 케이스만 분기처리하기 위해 if문이나 for문을 사용할 수도 있습니다.

```swift
enum Apple {
    case iPhone(modelName: String, modelColor: String)
    case mac(year: Int, screenInch: Double)
    case airpods(isProModel: Bool, generation: Int)
}

myAppleDevice = .mac(year: 2021, screenInch: 13.3)

if case Apple.mac(year: let releaseYear, screenInch: let screenSize) = myAppleDevice, releaseYear == 2021 {
    print("2021년에 출시한 \(screenSize)인치 맥북 모델입니다.")
}
// "2021년에 출시한 13.3인치 맥북 모델입니다." 출력
```

```swift
enum Apple {
    case iPhone(modelName: String, modelColor: String)
    case mac(year: Int, screenInch: Double)
    case airpods(isProModel: Bool, generation: Int)
}

// 열거형 리스트 생성
var appleDevices: [Apple] = [
    .iPhone(modelName: "아이폰 XS", modelColor: "스페이스 그레이"),
    .iPhone(modelName: "아이폰 12", modelColor: "화이트"),
    .iPhone(modelName: "아이폰 12 미니", modelColor: "레드"),
    .mac(year: 2021, screenInch: 13.3),
    .mac(year: 2019, screenInch: 16),
    .mac(year: 2015, screenInch: 15.4),
    .airpods(isProModel: true, generation: 1),
    .airpods(isProModel: false, generation: 2)
]

// 모든 케이스 출력
for device in appleDevices {
    print("나의 애플 기기: \(device)")
}

// 열거형 배열의 특정 케이스 출력
for case let .iPhone(modelName: model, modelColor: color) in appleDevices {
    print("\(color) 색상의 \(model) 모델입니다.")
}

for case let .mac(year: releaseYear, screenInch: screenSize) in appleDevices {
    print("\(releaseYear)에 출시한 \(screenSize)인치 맥북 모델입니다.")
}

for case let .airpods(isProModel: isProModel, generation: generation) in appleDevices {
    if isProModel {
        print("에어팟 프로 모델입니다.")
    } else {
        print("에어팟 \(generation)세대 모델입니다.")
    }
}
```
