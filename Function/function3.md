# 함수3

## 함수 사용 시 주의할 점

### 1. 함수 파라미터 이해

파라미터는 변수가 아닌 **상수(let)**이기 때문에 값을 변경할 수 없습니다.

```swift
func addOne(num: Int) -> Int {  // let num: Int
    num += 1    // 에러 발생

    return num
}
```

### 2. 범위

함수 내에서 선언한 변수는 함수 밖에서 사용할 수 없습니다. 함수 안에서만 사용할 수 있도록 제한됩니다. 함수 밖에서 선언한 변수나 상수는 함수 내에서 사용할 수 있습니다.

```swift
func greeting(person: String) -> String {
    var greeting = "\(person)님 안녕하세요. 저는 스위프트입니다."

    return greeting
}

print(greeting) // 에러 발생
```

### 3. return 키워드

return 타입이 있는 함수와 없는 함수에서 return 키워드는 다른 의미를 가집니다.

```swift
// 리턴 타입이 없는 함수
func isThisNumberOverFive(num: Int) {
    if num >= 5 {
        print("숫자가 5 이상입니다.")

        return      // 리턴 타입이 없는 함수에서 return 키워드는 함수를 중료하고 함수를 벗어납니다.
    }

    print("숫자가 5 미만입니다.")
}
```

```swift
// 리턴 타입이 있는 함수
func greeting(person: String) -> String {
    var greeting = "\(person)님 안녕하세요. 저는 스위프트입니다."

    return greeting  // 리턴 타입이 있는 함수에서 return 키워드는 뒤의 표현식을 함수를 호출한 곳에 리턴하고 함수를 벗어납니다.
}
```

### 4. 함수의 실행문

리턴 타입을 가지고 있는 함수의 실행문은 자체로 표현식이 됩니다. 표현식은 함수가 반환하는 값입니다.

```swift
func greeting(person: String) -> String {
    var greeting = "\(person)님 안녕하세요. 저는 스위프트입니다."

    return greeting
}

var hello = greeting(person: "devyoon56")
print(hello)        // devyoon56님 안녕하세요. 저는 스위프트입니다.
```

### 5. 함수의 중첩

함수 안에 함수를 정의할 수 있습니다. 함수 안에 정의한 함수는 외부에서 사용할 수 없습니다.

```swift
func sayGoodbyeOrHello(hello: Bool) -> String {

    func sayGoodbye() -> String {
        return "잘가"
    }

    func sayHello() -> String {
        return "안녕"
    }

    if hello {
        return sayHello()
    } else {
        return sayGoodbye()
    }

}

sayGoodbyeOrHello(hello: true)  // 안녕
sayGoodbyeOrHello(hello: false) // 잘가

sayHello()  // 에러 발생
```
