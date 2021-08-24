# 함수 표기법, 함수의 타입 표기, 함수 오버로딩

## 1. 함수 표기법

함수 표기법은 함수를 지칭하는 법을 말합니다. 함수를 실행하는 것과 다릅니다. 함수 표기법은 다음과 같은 상황에서 사용됩니다.

- 애플의 개발자 문서를 읽을 때
- 함수를 변수에 담거나 함수를 지칭할 때

함수를 표기하는 방법은 아래와 같습니다.

```swift
// 파라미터가 없는 경우
doSomething

// 아규먼트 레이블이 있는 경우
doSomething(with:)

// 파라미터가 여러개인 경우
// 파라미터 사이의 ',' 생략
doSomething(with:and:)

// 아규먼트 레이블이 생략된 와일드 패턴의 경우
// 언더바(_) 사용
doSomething(with:_:)
```

## 2. 함수의 타입 표기

함수의 타입 표기는 함수의 자료형을 표현하는 법을 말합니다.

```swift
func greeting(person: String) -> String {
    var greeting = "\(person)님 안녕하세요. 저는 스위프트입니다."

    return greeting
}

// greeting(person:) 함수의 자료형을 표현하는 방법: (String) -> String
var greetingFunction: (String) -> String = greeting(person:)   // 변수에 함수를 담을 때 함수 표기법 사용
```

## 3. 함수 오버로딩

스위프트는 함수 오버로딩을 지원합니다. 함수 오버로딩은 함수를 정의할 때 동일한 함수 이름을 사용하고 파라미터는 다르게 정의하는 것입니다. 하나의 함수 이름에 여러 기능의 함수를 대응하는 것으로 볼 수 있습니다. 즉 함수의 이름을 재사용한다고 쉽게 이해할 수 있습니다.

실제로 애플은 함수 오버로딩을 사용하여 다양한 함수를 구현하였습니다. 대표적으로 **print()** 함수가 있습니다.

```swift
print(items: Any...)
print(items: Any..., to: &TextOutputStream)
print(Any..., separator: String, terminator: String)
print(Any..., separator: String, terminator: String, to: &TextOutputStream)
```

같은 이름의 함수라도 전달하는 파라미터에 따라 다른 기능을 수행할 수 있습니다.
