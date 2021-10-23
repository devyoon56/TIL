# 확장

확장과 상속을 비교해보면

## 상속과 확장의 비교

상속

- 수직적 개념(수직 확장)
- 성격이 비슷한 타입을 새롭게 만들어서 저장 속성을 추가하고 메서드를 변형시켜 사용하려는 것

확장

- 수평적 개념(수평 확장)
- 타입에 메서드를 추가하여 사용하려는 것

확장은 본질적으로 기존 메서드 테이블 이외에 별도의 메서드를 추가하는 것입니다. (Direct Dispatch로 동작함)

## 확장 가능한 타입이란?

확장 가능한 타입은 다음과 같은 타입을 말합니다.

- 클래스
- 구조체
- 열거형
- 프로토콜

위와 같은 타입을 확장할 수 있습니다. 프로토콜도 타입으로 취급할 수 있으므로 확장이 가능합니다.

## 확장 문법

```swift
// SomeType 클래스 정의
class SomeType {}

// SomeType 클래스 확장
extension SomeType {
    func doSomething() {
        // 새로운 메서드 구현
    }
}
```

- extension 키워드를 사용하여 정의된 타입을 확장할 수 있습니다.
- 확장을 구현하기 전에 생성한 인스턴스도 새롭게 확장한 기능을 사용할 수 있습니다.

## 확장 가능한 멤버의 종류

확장 가능한 멤버의 종류는 다음과 같습니다.

- (타입, 인스턴스) 계산 속성
- (타입, 인스턴스) 메서드
- 새로운 생성자
  - 클래스의 경우 편의 생성자만 추가 가능
  - 지정 생성자 및 소멸자는 반드시 본체에 구현
  - 확장에 추가한 편의 생성자는 반드시 본체의 지정 생성자를 호출해야함
- 서브스크립트
- 새로운 중첩 타입
- 프로토콜의 채택 및 프로토콜 요구사항 구현
- 프로토콜

클래스의 지정 생성자는 인스턴스를 생성하는 역할을 담당하기 때문에 확장에서 구현할 수 없습니다.

확장에서 저장 속성은 추가할 수 없습니다. 저장 속성에 대한 메모리 공간이 추가적으로 필요하기 때문입니다. 또한 속성 감시자는 저장 속성의 변화를 관찰하는 메서드이므로 추가할 수 없습니다.

## 확장 예시

```swift
class Person {
    var id = 0
    var name = "이름"
    var email = "1234@gmail.com"

    func walk() {
        print("사람이 걷는다.")
    }
}

class Student: Person {
    var studentId = 1

    override func walk() {
        print("학생이 걷는다.")
    }

    func study() {
        print("학생이 공부한다.")
    }
}


extension Student {
//    override func study() {}           // 확장에서 기존 타입에 구현된 메서드 재정의 불가 ⭐️

    @objc func play() {
        print("학생이 논다.")
    }
}
```

Person 클래스를 상속하는 Student 클래스와 확장에 대한 예시입니다.

- 확장에서 기존 타입에 구현된 메서드를 재정의할 수 없습니다.⭐️
- 확장에서 @objc 키워드를 사용하여 메서드를 추가하면 서브 클래스에서 해당 메서드를 재정의할 수 있습니다.

```swift
class Undergraduate: Student {
    var major = "전공"

    override func walk() {
        print("대학생이 걷는다.")
    }

    override func study() {
        print("대학생이 공부한다.")
    }

    func party() {
        print("대학생이 파티한다.")
    }

    // func play()

    override func play() {
        print("대학생이 논다.")
    }
}

extension Undergraduate {
//    override func play() {
//        print("대학생이 논다.")
//    }

//    override func party() {}       // 확장에서 기존 타입에 구현된 메서드 재정의 불가 ⭐️
}
```

Student 클래스를 상속하는 Undergraduate 클래스와 확장에 대한 예시입니다.

- 슈퍼 클래스의 확장에서 추가한 메서드도 서브 클래스가 상속합니다.
- Undergraduate 서브 클래스가 상속한 play() 메서드는 슈퍼 클래스의 확장에서 @objc 키워드로 구현되어 있기 때문에 서브 클래스의 본체 또는 확장에서도 재정의할 수 있습니다.
- 확장에서 기존 타입에 정의된 메서드는 재정의할 수 없다는 것은 변하지 않습니다.⭐️

## 확장의 장점

애플의 원본 소스 코드에 대한 액세스 권한은 없지만 확장을 사용하여 타입에 기능을 추가할 수 있습니다. 즉 애플이 구현해놓은 Int, Double, String 등의 타입을 확장할 수 있다는 것입니다. 이것을 소급-모델링(retroactive-modeling)이라고 합니다.

```swift
extension Int {
    var squared: Self {
        return self * self
    }
}

10.squared      // 100
5.squared       // 25
```
