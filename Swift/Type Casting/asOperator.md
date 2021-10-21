# as 연산자 (type casting operator)

as 연산자는 클래스의 상속 관계에서 타입을 변환하는 연산자입니다. as 연산자는 인스턴스의 메모리 구조에 대한 힌트를 변경하는 연산자라고 이해할 수 있습니다.

## 메모리 구조에 대한 힌트 변경

메모리 구조에 대한 힌트를 변경한다는 의미에 대해 아래 코드를 통해 알아보겠습니다.

```swift
class Person {
    var name = "unknown"
    var id = 0122333
    var email = "abc123@gmail.com"
}

class Student: Person {
    var studentId = 12345
}

class Undergraduate: Student {
    var major = "CS"
}

let person: Person = Undergraduate()

person.name                // unknown
person.id                  // 0122333
person.email               // abc123@gmail.com

person.studentId           // 접근 불가능
person.major               // 접근 불가능

person is Person           // true
person is Student          // true
person is Undergraduate    // true
```

Undergraduate 타입의 인스턴스를 생성했지만 studentId, major 저장 속성에 접근할 수 없습니다. 그 이유는 다음과 같습니다.

- person 상수는 Undergraduate 타입의 인스턴스를 가리키지만 Person 타입으로 선언되어 있습니다.
- person 상수는 Person 타입의 인스턴스를 가리키는 것으로 인식합니다. 즉 메모리 구조에 대한 힌트를 변경한 것입니다. 하지만 메모리 구조에 대한 힌트만 변경한 것일뿐 Undergraduate 타입의 인스턴스를 가리킨다는 사실은 변하지 않습니다.
- 따라서 person 상수를 사용해서 Undergraduate 인스턴스가 갖고 있는 Person 타입의 속성에만 접근할 수 있습니다.
- Person 타입의 속성뿐만 아니라 Student, Undergraduate 타입의 속성에도 접근하고 싶다면 타입캐스팅을 통해 타입을 변환해야 합니다.

또한 person 상수가 Person, Student, Undergraduate 타입이 모두 맞다는 것은 person 상수가 Undergraduate 타입의 인스턴스를 가리키기 때문입니다.

## 타입 캐스팅의 의미

타입 캐스팅은 인스턴스를 사용할 때 어떤 타입으로 사용할 것인지 메모리 구조에 대한 힌트를 변경하는 것입니다. 위에서 메모리 구조에 대한 힌트를 변경한다는 의미를 살펴봤듯이 Undergraduate 타입의 인스턴스를 생성했어도 Person 타입으로 인식해서 사용할 수 있습니다.

또한 타입 캐스팅은 Undergraduate 타입으로 생성한 인스턴스의 메모리 값 자체를 변경하지 않는 것처럼 메모리의 값 자체를 변경하는 것이 아니고 단순하게 다른 타입의 인스턴스인 것처럼 취급하려는 목적으로 사용합니다.

## 다운캐스팅

다운캐스팅은 범용적인 타입에서 좀 더 구체적인 타입으로 타입을 변환하는 것을 말합니다. 위 클래스의 상속 관계에서 Person 클래스는 Undergraduate 클래스보다 상위에 위치하므로 Person 타입을 Undergraduate 타입으로 변환하는 것은 다운캐스팅입니다.

```swift
let person: Person = Undergraduate()

// 다운캐스팅
let person2 = person as? Undergraduate

person2?.major      // Undergraduate 타입의 속성에 접근 가능 -> CS
```

- person 상수는 Undergraduate 타입의 인스턴스를 가리키지만 Person 타입으로 인식됩니다.
- Person 타입의 person 상수를 person2 상수에 할당하는데 이 때 다운캐스팅 as? 연산자를 사용하여 Undergraduate 타입으로 인식시킵니다.
- 즉 person2 상수는 person 상수와 동일한 인스턴스를 가리키고 person 상수가 Person 타입으로 인식되는 반면에 person2 상수는 Undergraduate 타입으로 인식됩니다.
- 따라서 person2 상수를 사용해서 Undergraduate 타입의 속성에 접근할 수 있습니다.
  - 타입의 포함 관계를 고려했을 때 다운캐스팅은 실패 가능성을 가지고 있습니다.
  - as? 연산자를 사용하여 다운캐스팅이 성공하면 옵셔널 타입이 됩니다.
  - 다운캐스팅이 실패할 경우 nil을 리턴해야 하므로 옵셔널 타입을 리턴하는 것입니다.

```swift
let person: Person = Undergraduate()

if let newPerson = person as? Undergraduate() {
    newPerson.major = "Computer Science"
    print(newPerson.major)                  // Computer Science
}
```

- as? 연산자를 사용한 다운캐스팅은 옵셔널 타입을 리턴하므로 if let 바인딩을 사용해서 옵셔널을 언래핑할 수 있습니다.

```swift
let person: Person = Undergraduate()

let person2 = person as! Undergraduate()

person2.major       // Undergraduate 타입의 속성에 접근 가능 -> CS
```

- as! 연산자를 사용하여 다운캐스팅을 할 수 있습니다.
- as! 연산자를 사용한 다운캐스팅이 성공한다면 옵셔널을 강제로 언래핑한 타입이 됩니다.
- 하지만 as! 연산자를 사용한 다운캐스팅이 실패한다면 런타임 오류가 발생하므로 주의해야 합니다.

## 업캐스팅

업캐스팅은 구체적인 타입에서 범용적인 타입으로 타입을 변환하는 것을 말합니다. 위 클래스의 상속 관계에서 Person 클래스는 Undergraduate 클래스보다 상위에 위치하므로 Undergraduate 타입을 Person 타입으로 변환하는 것은 업캐스팅입니다.

```swift
let under = Undergraduate()
let person = under as Person

person.id           // Person 타입의 속성에 접근 가능
person.name         // Person 타입의 속성에 접근 가능
person.email        // Person 타입의 속성에 접근 가능

person.studentId    // Student 타입의 속성에 접근 불가능
person.major        // Undergraduate 타입의 속성에 접근 불가능
```

- person 상수는 under 상수가 가리키는 Undergraduate 타입의 인스턴스를 동일하게 가리킵니다.
- 하지만 as 연산자를 사용하여 Person 타입으로 업캐스팅했기 때문에 Student, Undergraduate 타입의 속성에 접근할 수 없고 오직 Person 타입의 속성에만 접근 가능합니다.

업캐스팅은 실패할 가능성이 없기 때문에 항상 성공적으로 타입을 변환할 수 있습니다.

## as 연산자의 활용

스위프트의 타입과 Objective-C의 타입은 완전히 상호 변환이 가능하도록 설계되었습니다.(브릿징) 따라서 as 연산자를 사용하면 스위프트의 타입과 Objective-C의 타입을 쉽게 변환할 수 있습니다.

```swift
let str: String = "Hello Objective-C"
let otherStr = str as NSString      // NSString: Objective-C의 String 타입
```
