# @unknown 키워드

열거형을 스위치문으로 분기처리하는 경우, 열거형 최초 정의 후에 케이스를 추가하면 스위치문으로 모든 열거형의 케이스에 대해 분기처리하지 않는 상황이 발생할 수 있습니다. 다루지 않은 케이스에 대해 default문으로 분기처리하여 에러가 발생하지 않을 수 있지만 이러한 분기처리 방식은 로직에 대한 안정성을 보장하지 않습니다.

## @unknown 키워드 예제

```swift
enum LoginProviders: String {
    case apple
    case google
    case facebook
    case naver
    case kakaotalk      // 열거형 최초 정의 후 추가된 케이스
}

var userLogin: LoginProviders = .apple

switch userLogin {
case .apple:
    print("애플 계정으로 로그인합니다.")
case .google:
    print("구글 계정으로 로그인합니다.")
case .facebook:
    print("페이스북 계정으로 로그인합니다.")
case .naver:
    print("네이버 계정으로 로그인합니다.")
default:
    print("그외 다른 방법으로 로그인합니다.")
}

// "그외 다른 방법으로 로그인합니다." 출력
// 에러가 발생하지 않기 때문에 모든 로직이 처리됬다고 착각할 수 있음
```

이런 경우 default 앞에 **@unknown** 키워드를 사용하면 스위치문에서 모든 열거형의 케이스에 대해 분기처리를 하지 않았다고 컴파일러가 경고로 알려줍니다. 이 경고 메세지를 확인하고 실수를 방지하고 모든 열거형의 케이스에 대해 분기처리할 수 있습니다.

```swift
enum LoginProviders: String {
    case apple
    case google
    case facebook
    case naver
    case kakaotalk      // 열거형 최초 정의 후 추가된 케이스
}

var userLogin2: LoginProviders = .apple

switch userLogin2 {                             // 경고 메세지: "Switch must be exhaustive"
case .apple:
    print("애플 계정으로 로그인합니다.")
case .google:
    print("구글 계정으로 로그인합니다.")
case .facebook:
    print("페이스북 계정으로 로그인합니다.")
case .naver:
    print("네이버 계정으로 로그인합니다.")
@unknown default:
    print("그외 다른 방법으로 로그인합니다.")
}
```
