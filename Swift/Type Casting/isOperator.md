# is 연산자

is 연산자에 대해 알아보기 전에 먼저 상속과 타입의 포함 관계에 대해 알아보겠습니다.

## 클래스의 상속과 타입의 포함 관계

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
```

- Student 클래스는 Person 클래스를 상속하고 Undergraduate 클래스는 Student 클래스를 상속합니다.
- 이런 상속 관계에서 타입의 포함 관계를 살펴보겠습니다.
  - Person 타입은 Student 타입을 포함하지 않지만 Student 타입은 Person 타입을 포함합니다.
  - Person 타입은 Undergraduate 타입을 포함하지 않지만 Undergraduate 타입은 Person 타입을 포함합니다.
  - Student 타입은 Undergraduate 타입을 포함하지 않지만 Undergraduate 타입은 Student 타입을 포함합니다.

정리하자면

- Undergraduate 타입은 Student, Person 타입을 포함합니다.
- Student 타입은 Person 타입을 포함합니다.

## is 연산자

is 연산자는 인스턴스의 타입을 검사하는 연산자입니다. is 연산자를 사용해서 인스턴스가 어떤 타입인지 확인할 수 있습니다.

is 연산자는 이항 연산자로 '인스턴스 is 타입'의 형태를 가집니다.

- 인스턴스가 제시한 타입이 맞다면 true를 반환합니다.
- 인스턴스가 제시한 타입이 아니면 false를 반환합니다.

위 상속 관계와 타입의 포함 관계에서 is 연산자를 사용하여 인스턴스의 타입을 확인해보겠습니다.

```swift
let person = Person()
let student = Student()
let under = Undergraduate()

person is Person            // true
person is Student           // false
person is Undergraduate     // false

student is Person           // true
student is Student          // true
student is Undergraduate    // false

under is Person             // true
under is Student            // true
under is Undergraduate      // true
```

- Person 타입의 인스턴스의 경우
  - 당연히 Person 타입입니다.
  - Student 타입이 아닙니다.
  - Undergraduate 타입이 아닙니다.
- Student 타입의 인스턴스의 경우
  - Person 타입입니다.
  - 당연히 Student 타입입니다.
  - Undergraduate 타입이 아닙니다.
- Undergraduate 타입의 인스턴스의 경우
  - Person 타입입니다.
  - Student 타입입니다.
  - 당연히 Undergraduate 타입입니다.

타입의 포함 관계를 생각하면 인스턴스가 어떤 타입일 수 있는지를 쉽게 이해할 수 있습니다.

- Person 타입의 인스턴스는 Student, Undergraduate 타입이 아닙니다. 왜냐하면 Person 타입이 Student, Undergraduate 타입에 포함되기 때문입니다.
- Student 타입의 인스턴스는 Undergraduate 타입이 아닙니다. 왜냐하면 Student 타입이 Undergraduate 타입에 포함되기 때문입니다.
  - 하지만 Student 타입이 Person 타입을 포함하므로 Person 타입이기도 합니다.
- Undergraduate 타입의 인스턴스는 Person, Student 타입이기도 합니다. 왜냐하면 Undergraduate 타입이 Person, Student 타입을 포함하기 때문입니다.

```swift
let person1 = Person()
let person2 = Person()
let student1 = Student()
let student2 = Student()
let under1 = Undergraduate()
let under2 = Undergraduate()

let people = [person1, person2, student1, student2, under1, under2]
var numberOfStudents = 0

for person in people {
    if person is Student {
        numberOfStudents += 1
    }
}

print(numberOfStudents)     // 4
```

for 문에서 people 배열의 요소가 Student 타입인지 확인하고 numberOfStudents 변수를 1씩 증가시키는 코드입니다.

4가 출력되는 이유

- person1, person2는 Person 타입의 인스턴스이므로 Student 타입이 아닙니다.
- student1, student2는 Student 타입의 인스턴스이므로 Student 타입입니다.
- under1, under2는 Undergraduate 타입이지만 Student 타입이기도 합니다.
- 따라서 numberOfStudents는 4가 됩니다.
