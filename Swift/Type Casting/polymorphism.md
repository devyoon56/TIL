# 타입과 다형성

다형성의 의미는 다음과 같습니다.

- 하나의 인스턴스(객체)를 여러가지 타입으로 표현할 수 있다.
- 다양한 타입의 여러 인스턴스(객체)들을 하나의 타입으로 해석할 수 있다.

다형성의 구현은 클래스의 상속과 밀접한 관련이 있습니다.

## 상속 관계에서 메서드의 재정의와 인스턴스의 다형성에 대한 이해

```swift
class Person {
    var id = 0
    var name = "이름"
    var email = "abc@gmail.com"

    func walk() {                   // 새로운 메서드 정의
        print("사람이 걷는다.")
    }
}

class Student: Person {
    var studentId = 1

    override func walk() {          // walk() 메서드 재정의:  walk() - 1
        print("학생이 걷는다.")
    }

    func study() {                  // 새로운 메서드 정의
        print("학생이 공부한다.")
    }
}

class Undergraduate: Student {
    var major = "전공"

    override func walk() {          // walk() - 1 메서드 재정의: walk() - 2
        print("대학생이 걷는다.")
    }

    override func study() {         // study() 메서드 재정의: study() - 1
        print("대학생이 공부한다.")
    }

    func party() {                  // 새로운 메서드 정의
        print("대학생이 파티를 한다.")
    }
}

let person = Person()
let student: Person = Student()
let under: Person = Undergraduate()

person.walk()               // "사람이 걷는다"
student.walk()              // "학생이 걷는다"
under.walk()                // "대학생이 걷는다"
```

Person, Student, Undergraduate 타입의 인스턴스를 각각 생성하고 Student, Undergraduate 타입의 인스턴스를 가리키는 상수는 Person 타입으로 인식시킵니다. 따라서 세 개의 상수로 walk() 메서드를 실행하면 모두 "사람이 걷는다"를 출력할 것 같지만 결과는 각 타입의 walk() 메서드를 실행한 결과를 출력합니다. 그 이유는 다음과 같습니다.

- person 상수는 Person 타입의 인스턴스를 참조합니다.
  - 따라서 person.walk()는 Person 타입의 메서드 테이블을 참조하여 메서드를 실행합니다.
- student 상수는 Student 타입의 인스턴스를 참조하지만 Person 타입으로 인식됩니다.
  - 하지만 student 상수가 Student 타입의 인스턴스를 참조하는 것은 변하지 않으므로 Student 타입의 메서드 테이블을 참조하여 메서드를 실행합니다.
- under 상수는 Undergraduate 타입의 인스턴스를 참조하지만 Person 타입으로 인식됩니다.
  - 하지만 under 상수가 Undergraduate 타입의 인스턴스를 참조하는 것은 변하지 않으므로 Undergraduate 타입의 메서드 테이블을 참조하여 메서드를 실행합니다.

Person 타입으로 업캐스팅하여 메서드를 호출하여도 각 타입마다 실제 메모리에 구현된 메서드 테이블을 참조하여 재정의된 메서드를 실행합니다.

```swift
let person = Person()
let student: Person = Student()
let under: Person = Undergraduate()

student.study()     // Person 타입으로 인식되어 study() 메서드에 접근 불가능
under.study()       // Person 타입으로 인식되어 study() 메서드에 접근 불가능
under.party()       // Person 타입으로 인식되어 party() 메서드에 접근 불가능
```

student, under 상수가 각각 Student 타입의 인스턴스를, Undergraduate 타입의 인스턴스를 가리킨다면 각 타입에서 정의한 메서드에 접근할 수 있을 것 같지만 접근할 수 없습니다. 그 이유는 다음과 같습니다.

- student 상수는 Student 타입의 인스턴스를 가리키지만 Person 타입으로 인식되므로 Person 타입에서 정의한 메서드 walk() 에만 접근할 수 있습니다.
- 같은 이유로 under 상수는 Undergraduate 타입의 인스턴스를 가리키지만 Person 타입으로 인식되므로 Person 타입에서 정의한 메서드 walk() 에만 접근할 수 있습니다.

클래스 상속 관계에서 다형성은 메서드를 통해 나타납니다.

- 타입은 저장 속성과 메서드에 대한 접근 가능 범위를 나타냅니다.
- 다형성은 인스턴스가 참조하는 타입의 메모리의 실제 구현 내용에 대한 것입니다. 어떤 타입이 메서드를 재정의하고 해당 타입의 인스턴스가 메서드를 호출하면 해당 타입의 메서드 테이블을 참조하여 메서드를 실행합니다.
- 인스턴스를 참조하는 변수나 상수가 다른 타입으로 캐스팅되어도 메서드에 대한 접근 가능 범위만 바뀔뿐 인스턴스가 참조하는 타입의 메서드를 실행하는 것은 변하지 않습니다.
