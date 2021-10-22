# Any와 AnyObject

스위프트는 불특정한 타입을 다룰 수 있는 두 가지 타입을 제공합니다.

- Any
- AnyObject

## Any

Any 타입은 다음과 같은 타입의 인스턴스를 표현할 수 있는 타입입니다.

- 스위프트 기본 타입: Int, Double, String, Bool 등
- 커스텀 타입: 클래스, 구조체, 열거형
- 함수 타입
- 옵셔널 타입

```swift
var some: Any = "Hello Swift"

(some as! String).count     // 11

some = 10
some = 3.3
some = false
```

Any 타입의 단점은 저장된 인스턴스의 타입의 메모리 구조를 알 수 없기 때문에 항상 타입캐스팅을 사용해야 한다는 점입니다. Any 타입은 범용적인 타입이므로 구체적인 타입으로 다운캐스팅 해야합니다.

```swift
class Person {
    var age = 30
    var name = "unknown"
}

class Superman {
    var name = "슈퍼맨"
    var weight = 99.9
}

var array: [Any] = [5, "안녕", 3.5, Person(), Superman(), {(name: String) in return name}]

// Any 타입은 다운캐스팅해서 사용해야 합니다
(array[1] as! String).count          // 2
(array[3] as! Person).name           // unknown
(array[4] as! Superman).weight       // 99.9
```

Any 타입의 장점은 모든 타입을 담을 수 있는 배열을 생성할 수 있다는 점입니다.

## AnyObject

AnyObject 타입은 어떤 클래스의 인스턴스도 표현할 수 있는 타입입니다. 하지만 구조체의 인스턴스를 표현하지는 못합니다.

```swift
class Person {
    var name = "이름"
    var age = 30
}

class Superman {
    var name = "슈퍼맨"
    var weight = 100
}

let objArray: [AnyObject] = [Person(), Superman(), NSString()]

(objArray[0] as! Person).age            // 30
(objArray[1] as! Superman).name         // 슈퍼맨
```

## 타입캐스팅 패턴

switch문에서 is, as 패턴을 사용해서 분기처리가 가능합니다.

```swift
var array: [Any] = [5, "안녕", 3.5, Person(), Superman(), {(name: String) in return name}]

for (index, item) in array.enumerated() {
    switch item {
    case is Int:                                    // item is Int: item에 담긴 인스턴스가 Int 타입이면
        print("Index - \(index): 정수입니다.")

    case let num as Double:                         // let num = item as Double
        print("Index - \(index): 소수 \(num)입니다.")

    case is String:                                 // item is String
        print("Index - \(index): 문자열입니다.")

    case let person as Person:                      // let person = item as Person
        print("Index - \(index): 사람입니다.")
        print("이름은 \(person.name)입니다.")
        print("나이는 \(person.age)살입니다.")

    case let superman as Superman:                  // let superman = item as Superman
        print("Index - \(index): 슈퍼맨입니다.")
        print("이름은 \(superman.name)입니다.")
        print("몸무게는 \(superman.weight)kg입니다.")

    case is (String) -> String:                     // item is (String) -> String
        print("Index - \(index): 클로저 타입입니다.")

    default:
        break
    }
}
```

- switch문에서 is 연산자를 사용해서 인스턴스의 타입을 확인할 수 있습니다.
- switch문에서 상수 바인딩과 as 연산자를 사용해서 인스턴스의 타입을 다운캐스팅할 수 있습니다.

switch문에서 상수 바인딩 시 다운캐스팅 연산자 as? 를 사용하지 않고 as를 사용하는 이유는 다운캐스팅이 성공하는 경우에만 상수 바인딩이 되기 때문입니다. 따라서 switch문에서는 as?의 ?를 생략할 수 있습니다.

## 옵셔널 값의 Any 변환

옵셔널 타입의 값을 사용하기 위해 Any 타입으로 업캐스팅하는 경우가 있습니다. 일반적으로 옵셔널 값을 언래핑하여 값을 사용하지만 옵셔널 값을 Any 타입으로 업캐스팅한다는 것은 의도적으로 옵셔널 값을 사용하겠다는 의미입니다.

```swift
let optionalNum: Int? = 3

print(optionalNum)              // 컴파일러 경고
print(optionalNum as Any)       // 컴파일러 경고 사라짐
```
