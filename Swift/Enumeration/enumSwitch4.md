# 옵셔널 타입의 열거형 케이스 패턴

옵셔널 타입을 열거형 케이스 패턴으로 분기처리할 수 있지만 열거형 케이스 패턴을 간소화하는 방법도 있습니다. 열거형 케이스 패턴을 간소화한 것을 옵셔널 패턴이라고 합니다.

## 옵셔널 타입의 열거형 케이스 패턴 예제

```swift
let a: Int? = 1

// 옵셔널 타입의 열거형 케이스 패턴
// 상수 바인딩 패턴 사용
switch a {
case .some(let num):
    print(num)
case .none:
    print("아무 값도 없습니다.")
}
```

옵셔널 타입의 some 케이스 분기처리를 간소화하는 방법은 다음과 같습니다.

```swift
// 열거형 케이스 패턴 간소화(옵셔널 패턴)
// some 케이스를 쓰지 않고 상수 바인딩 패턴 사용 시 상수명 뒤에 "?"를 붙임
switch a {
case let num?:
    print(num)
case nil:
    print("아무 값도 없습니다.")
}
```

특정 케이스를 다루는 if문에서도 옵셔널 패턴을 사용할 수 있습니다.

```swift
let b: Int? = 5

// 열거형 케이스 패턴
if case .some(let num) = b, num == 5 {
    print("정수 5가 있습니다.")
}

// 옵셔널 패턴
if case let num? = b, num == 5{
    print("정수 5가 있습니다.")
}
```

특정 케이스를 다루는 for문에서도 옵셔널 패턴을 사용할 수 있습니다. 옵셔널 타입을 포함하는 배열에서 for 반복문 사용 시, 옵셔널 패턴을 사용하면 편리합니다.

```swift
let numArray: [Int?] = [nil, 2, 3, nil, 5, 6, nil]

// 열거형 케이스 패턴
for case .some(let num) in numArray {
    print("\(num)을 찾았습니다.")
}

// 옵셔널 패턴
for case let num? in numArray {
    print("\(num)을 찾았습니다.")
}

```
