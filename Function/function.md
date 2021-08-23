# 함수

함수는 특정한 기능을 수행하는 코드를 묶어 놓은 것이다. 함수를 사용하려면 함수명을 사용하면 된다.

## 함수를 사용하는 이유

1. 코드를 기능 단위로 구분할 수 있다.(기능의 모듈화)
2. 반복되는 코드를 단순화하고 이것을 재사용할 수 있다.
3. 애플이 이미 구현한 함수를 사용하면 쉽게 원하는 기능을 구현할 수 있다.

## 함수의 2단계

함수는 항상 2단계로 실행된다.

1. 먼저 원하는 기능을 구현한 함수를 정의한다.
2. 정의한 함수를 호출하여 사용한다.

```swift
// 함수 정의
func sayHello() {
    print("Hello World!")
    print("Hello Swift!")
    print("Hello Everyone!")
}

// 함수 호출
sayHello()
```

## 함수의 형태

### 1. 입력과 출력이 모두 없는 경우

```swift
// 함수의 입력과 출력이 없다.
func sayHello() {
    print("Hello World!")
    print("Hello Swift!")
    print("Hello Everyone!")
}

sayHello()
```

### 2. 입력만 있는 경우

```swift
// 함수의 입력만 있는 경우
// 함수의 파라미터에 이름과 데이터 타입을 명시적으로 선언해야 한다.
// 파라미터에 부여한 이름은 함수 내부에서 사용된다.
func greetingWithInput(name: String) {
    print("안녕하세요. \(name)님 반갑습니다.")
}

greetingWithInput(name: "스위프트") // 안녕하세요. 스위프트님 반갑습니다.
```

### 3. 출력만 있는 경우

```swift
func greetingWithOutput() -> String {
    // 함수의 출력만 있는 경우
    // 함수의 파라미터는 작성하지 않는다.
    // 함수가 반환하는 데이터 타입을 '->' 뒤에 작성한다.

    // 함수가 반환하는 값을 return 키워드 뒤에 작성한다.
    return "안녕하세요. 반갑습니다."
}

print(greetingWithOutput()) // 안녕하세요. 반갑습니다.
```

### 4. 입력과 출력이 모두 있는 경우

```swift
func greeting(name: String) -> String {
    return "안녕하세요. \(name)님 반갑습니다."
}

greeting(name: "devyoon56") // 안녕하세요. devyoon56님 반갑습니다.
```

## Void 타입

입력과 출력이 없는 함수의 경우, Void 타입을 반환할 수 있다.

```swift
// 함수의 입력이 없다면 그대로 비워두고
// 함수의 출력이 없다면 그대로 비워두워도 되고 Void 타입을 반환해도 된다.
func sayHello() -> Void {
    print("Hello World!")
    print("Hello Swift!")
    print("Hello Everyone!")
}

sayHello()
```
