# 옵셔널(Optionals)

> [옵셔널(optionals)은 값이 없을 수도 있는 상황에서 사용합니다. 옵셔널은: 값이 있고 (is), 해당 값의 접근을 위해 옵셔널의 포장을 풀 수 있거나, 아니면 값이 전혀 없다 (isn’t) 는 두 가지 가능성을 표현합니다.](http://xho95.github.io/swift/language/grammar/basics/2016/04/24/The-Basics.html)

## 1. 스위프트에서 옵셔널 타입을 사용하는 이유

변수나 상수를 선언하고 값을 초기화하지 않은 상황에서(변수나 상수의 메모리 공간을 할당한 상황) 해당 변수나 상수에 접근하면(메모리 공간에 접근하면) 에러가 발생합니다.

```swift
let myName: String  // String 타입 상수 선언

print(myName)       // 에러 발생
```

메모리 공간에 값이 저장되지 않은 상황에서도 메모리 공간에 접근했을 때 에러가 발생하지 않기 위해 스위프트는 옵셔널이라는 개념을 사용합니다.

## 2. 옵셔널 타입

옵셔널 타입과 일반적인 데이터 타입은 같지 않습니다. 서로 다른 타입인 것입니다. 왜냐하면 일반적인 데이터 타입은 반드시 해당 타입의 값을 가져야 하지만 옵셔널 타입은 값이 없다는 가능성을 가지고 있기 때문입니다. 옵셔널 타입은 값이 없다는 것을 표현하기 위해 **nil**을 사용합니다.

스위프트에서 **nil**은 값이 없음을 표현하는 키워드입니다. 옵셔널 타입을 선언할 때 **nil**을 할당할 수 있고 아무 값도 할당하지 않으면 컴파일러는 자동으로 **nil**을 할당합니다.

옵셔널 타입은 일반적인 데이터 타입 뒤에 **?**를 붙여서 사용합니다.

```swift
var num: Int? = 10
var age: Int? = nil
var grade: Double?      // nil
var name: String? = "devyoon56"
```

옵셔널 타입은 반드시 명시적으로 작성해야 합니다. **nil**을 할당하면서 옵셔널 타입을 생략할 수 없는 이유는 컴파일러가 어떤 옵셔널 타입을 사용할 것인지 추론할 수 없기 때문입니다.

```swift
var tempVar = nil // 에러 발생
```

따라서 변수를 **nil**로 초기화하려면 반드시 타입을 명시해야 합니다.

## 3. 옵셔널 타입의 정식 표현

옵셔널 타입을 표현하는 두 가지 방법이 있습니다.

```swift
let num1: Int?              // 간편 표기
let num2: Optional<Int>     // 정식 표현
```

## 4. 옵셔널 타입 사용하기

```swift
var num: Int? = 10
var age: Int? = nil
var grade: Double?      // nil
var name: String? = "devyoon56"

print(num)      // Optional(10)
print(age)      // nil
print(grade)    // nil
print(name)     // Optional("devyoon56")
```

옵셔널 타입의 변수에 값이 없는 상황에서도 변수에 접근하면 에러가 발생하지 않고 nil을 출력합니다. 그리고 값이 있는 상황에서 변수에 접근하면 Optional()과 함께 값을 알려줍니다.

```swift
var age: Int? = 29
var currentAge = age

print(currentAge)       // Optional(29)
```

변수에 옵셔널 타입의 데이터를 할당하면 옵셔널 타입이 됩니다.

```swift
var myNickName = "devyoon56"
var myName: String? = myNickName

print(myName)   // Optional("devyoon56")
```

옵셔널 타입에 일반적인 데이터 타입의 변수를 할당하면 변수의 값이 옵셔널 타입으로 바뀌어 할당됩니다.

```swift
var a: Int? = 1
var b: Int? = 2

a + b   // 에러 발생
```

옵셔널 타입에 바로 연산자를 적용하면 연산이 불가능합니다. 옵셔널 타입을 일반적인 타입으로 사용하기 위해서는 옵셔널의 포장을 우선 _벗겨야 합니다.(unwrapping)_
