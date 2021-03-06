# 프로토콜의 문법

프로토콜의 기본 문법에 대해 알아보겠습니다.

## 프로토콜의 기본 문법

1. 우선 프로토콜을 정의해야 합니다. 이 때 프로토콜의 요구사항을 나열합니다.

```swift
// 프로토콜 정의
protocol MyProtocol {
    // 최소한의 요구사항 나열
}
```

2. 정의된 프로토콜을 채택하고 프로토콜의 요구사항을 구현합니다.

```swift
class SuperClass {}

// 클래스를 상속하는 경우 먼저 슈퍼 클래스를 선언하고 프로토콜을 채택합니다.
class SubClass: SuperClass, MyProtocol {

    // 프로토콜 정의에 명시된 요구사항의 구체적인 구현

}

// 프로토콜 채택
struct SomeStruct: MyProtocol {

    // 프로토콜 정의에 명시된 요구사항의 구체적인 구현

}

// 프로토콜 채택
enum SomeEnum: MyProtocol {

    // 프로토콜의 정의에 명시된 요구사항의 구체적인 구현

}
```
