# if 조건문

if 조건문은 조건이 **true**일 때만 조건문을 실행합니다. 가장 간단한 if 조건문은 하나의 if 조건문 형식입니다.

## if 조건문의 형식

```swift
if 확인할 조건 {
    // code
}
```

조건이 참이면 조건문 내부를 실행하고 조건이 거짓이면 조건문을 실행하지 않고 넘어갑니다.

```swift
var weatherOfToday = "rainy"

if weatherOfToday == "rainy" {
    print("우산을 챙기세요.")
}

// 우산을 챙기세요.
```

조건을 판단할 때 &&, || 연산자를 사용할 수 있습니다.

```swift
var email = "a@gmail.com"
var password = "1234"

if email == "a@gmail.com" && password == "1234" {
    print("메인페이지로 이동")
}

if email != "a@gmail.com" || password != "1234" {
    print("경고메세지 띄우기")
    print("이메일주소 또는 패스워드가 올바르지 않습니다.")
}
```

## if-else 조건문

if의 조건이 **false**일 때 실행하기 위한 코드를 else 키워드를 이용하여 작성할 수 있습니다.

```swift
weatherOfToday = "sunny"

if weatherOfToday == "rainy" {
    print("우산을 챙기세요.")
} else {
    print("썬크림은 필수입니다.")
}

// 썬크림은 필수입니다.
```

## if - else if - else 조건문

추가적인 조건을 확인하기 위해 if 조건문을 else if 조건문으로 연쇄할 수 있습니다. else if 조건문은 원하는 만큼 추가할 수 있습니다.

```swift
weatherOfToday = "windy"

if weatherOfToday == "rainy" {
    print("우산을 챙기세요.")
} else if weatherOfToday == "windy" {
    print("머리가 날릴 수 있어요.")
} else {
    print("썬크림은 필수입니다.")
}

// 머리가 날릴 수 있어요.
```

## 최종 else 절의 생략

최종 else 절은 반드시 작성할 필요는 없습니다. 조건이 완전할 필요가 없다면 생략할 수 있습니다.

```swift
if weatherOfToday == "rainy" {
    print("우산을 챙기세요.")
} else if weatherOfToday == "windy" {
    print("머리가 날릴 수 있어요.")
} else if weatherOfToday == "sunny" {
    print("썬크림은 필수입니다.")
}
```
