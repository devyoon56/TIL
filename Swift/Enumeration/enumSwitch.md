# 열거형과 스위치문1

열거형은 한정된 케이스로 만든 타입입니다. 그리고 스위치문은 표현식에 대한 분기처리에 최적화되어 있습니다. 따라서 열거형의 분기처리에 스위치문을 활용하는 것은 적합합니다.

## 일반적인 열거형 분기처리 예제

열거형의 분기처리는 스위치문을 사용하면 편리합니다.

```swift
// 원시값 정수형 타입 설정은 랜덤하게 열거형을 생성할 때 편함
enum LoginProvider: Int {
    case apple
    case google
    case facebook
    case naver
}

// 원시값을 랜덤으로 설정하여 열거형 생성
var userLogin: LoginProvider = LoginProvider(rawValue: Int.random(in: 0...3))!

switch userLogin {
case .apple:
    print("애플 계정으로 로그인합니다.")    // 출력
case .google:
    print("구글 계정으로 로그인합니다.")
case .facebook:
    print("페이스북 계정으로 로그인합니다.")
case .naver:
    print("네이버 계정으로 로그인합니다.")
}

```
