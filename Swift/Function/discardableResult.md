# discardableResult

## @어트리뷰트 키워드

_@_ 키워드는 컴파일러에게 추가적인 정보를 알려주는 역할을 합니다.

1. 선언에 추가적인 정보를 제공하는 경우

```swift
@available(iOS 10.0)
class MyClass{
    // class definition
}
```

2. 타입에 추가적인 정보를 제공하는 경우

```swift
func doSomething(completion: @escaping() -> ()) {
    // code
}
```

## @discardableResult

함수의 리턴값을 활용하지 않는 경우 함수 정의 앞에 **@discardableResult**를 붙이면 됩니다.

```swift
// 일반적인 함수 선언
func sayHello() -> String {
    return "안녕하세요. devyoon56 입니다."
}

sayHello()      // 경고 발생, 반환값을 사용하지 않음

_ = sayHello()  // 반환값의 사용을 생략하기 위해 와일드카드 패턴 사용
```

```swift
// @discardableResult 어트리뷰트 사용
@discardableResult
func sayHello() -> String {
    return "안녕하세요. devyoon56 입니다."
}

sayHello()      // 결과값을 사용하지 않는다는 경고가 사라짐
```

**@discardableResult**를 사용하는 것은 컴파일러에게 함수의 반환값을 사용하지 않는다는 정보를 알려주는 것이기 때문에 반환값을 사용하지 않는다는 경고가 사라집니다.

## 내 생각

**@discardableResult**를 사용하기 전에 함수의 정의에서 반환값이 필요없는지 먼저 로직에 이상이 없는지 확인하는 것이 필요하다고 생각한다.
