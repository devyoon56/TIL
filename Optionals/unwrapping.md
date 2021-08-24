# 옵셔널 타입 사용하기

옵셔널 타입은 값이 없을 수도, 값이 있을 수도 있는 두 가지 가능성을 표현합니다. 값이 있는 경우 옵셔널 타입의 형태는 **Optional\(값\)**이고 값이 없는 경우 옵셔널 타입의 형태는 **nil**입니다.

값이 있는 경우 옵셔널 타입을 사용하기 위해 먼저 **Optional**이라는 _포장을 벗겨내야 합니다.(unwrapping)_ 하지만 값이 없는 경우 옵셔널 타입을 사용하기 위해 포장을 벗기면 에러가 발생합니다.

옵셔널 포장을 벗기기 위한 방법은 크게 네 가지가 있습니다.

## 1. 강제 추출하기(Forced Unwrapping)

강제 추출하기는 강제 추출연산자 '!'를 옵셔널 표현식 뒤에 붙여서 사용할 수 있습니다.

```swift
var myName: String? = "devyoon56"
var myAge: Int? // nil

print(myName!)  // devyoon56
print(myAge!)   // 에러 발생
```

강제 추출하기는 옵셔널 타입에 반드시 값이 있다는 것이 확실할 때만 사용해야 합니다. 왜냐하면 옵셔널 타입에 값이 없는 상황에서 강제 추출하기를 사용하면 에러가 발생합니다. 따라서 강제 추출하기는 옵셔널 포장을 벗길 때 사용하는 방법으로 자주 사용되지 않습니다.

## 2. nil이 아닌지 확인하고 강제 추출하기

if문으로 nil이 아닌지 먼저 확인하고 옵셔널의 값을 강제 추출하는 방법입니다.

```swift
var myAge: Int?

if myAge != nil {
    print(myAge!)   // 아무것도 출력하지 않음
}
```

옵셔널 타입의 값이 없는 상황을 if문으로 확인하기 때문에 강제 추출하기 방법보다 안전한 방법입니다.

## 3. 옵셔널 바인딩(if let / guard let 바인딩)

옵셔널 타입에 값이 있어서 바인딩(상수나 변수에 값을 대입)이 가능한 경우 바인딩된 값을 사용할 수 있습니다.

```swift
// if let 바인딩
var myName: String? = "devyoon56"

if let name = myName {        // 옵셔널 타입인 myName에 값이 있어서 name에 값이 담긴다면 실행
    print("안녕하세요. 저는 \(name) 입니다.")     // 안녕하세요. 저는 devyoon56 입니다.
}
```

```swift
// guard let 바인딩
func greeting(name: String?) {
    guard let n = name else { return }

    print("안녕하세요. 저는 \(n) 입니다.")
}

var myName: String? = "devyoon56"
greeting(name: myName)      // 안녕하세요. 저는 devyoon56 입니다.
```

일반적인 상황에서 옵셔널 바인딩 방법을 가장 많이 사용합니다. **guard let** 바인딩은 같은 코드 블록에서 상수를 사용할 수 있으므로 편리합니다.

## 4. Nil-Coalescing 연산자

Nil-Coalescing 연산자 '??'을 사용하면 기본값을 제공하여 옵셔널의 가능성을 없앨 수 있습니다. 옵셔널에 값이 있다면 그 값을 사용하고, 값이 없다면 제공한 기본값을 사용하여 옵셔널의 가능성이 없어지는 것입니다.

```swift
var myName: String? = "devyoon56"
var userName = myName ?? "unknown user"

print("안녕하세요. \(userName)님")  // 안녕하세요. devyoon56님

myName = nil
userName = myName ?? "unknown user"

print("안녕하세요. \(userName)님")  // 안녕하세요. unknown user님
```
