# 클래스의 상속(Inheritance)

상속은 성격이 비슷한 타입을 새로 만들어서 데이터(저장 속성)를 추가하거나 기능(메서드)를 변형시켜서 사용하는 개념입니다. 클래스가 어떤 클래스를 상속하면 상속하는 클래스를 _자식 클래스_, _서브 클래스_ 또는 _하위 클래스_ 라고 합니다. 그리고 상속되는 클래스는 _부모 클래스_, _슈퍼 클래스_ 또는 _상위 클래스_ 라고 합니다. 이것은 상대적인 개념으로 어떤 클래스는 _부모 클래스_ 이면서 동시에 _자식 클래스_ 가 될 수 있습니다.

기본적으로 서브 클래스는 슈퍼 클래스의 모든 멤버를 상속합니다. 여기서 말하는 멤버는 속성과 메서드를 의미합니다.

> 기존 클래스를 상속하여 새로운 클래스를 만드는 것을 '서브클래싱'한다라고 표현합니다.

> 상속은 오직 클래스에서만 지원하는 기능으로 구조체는 상속이 불가능합니다.

## 클래스 상속 예시

먼저 간단하게 데이터(저장 속성)을 추가하는 개념의 상속을 알아봅니다.

```swift
class Person {
    var name: String = "이름"
    var weight: Double = 0.0
    var height: Double = 0.0
}

class Student: Person {             // Person 클래스 상속
    var studentId: Int = 012345
}

class Undergraduate: Student {      // Student 클래스 상속
    var major = "전자공학"
}
```

- 클래스 Person은 기본 클래스입니다. 아무 클래스도 상속하지 않는 클래스를 기본 클래스라고 합니다.
- 클래스를 상속하려면 클래스 이름 뒤에 콜론을 붙이고 상속하려는 클래스를 적습니다.
- 클래스 Student는 클래스 Person을 상속하고 있습니다.
  - 클래스 Person은 클래스 Student의 슈퍼 클래스입니다.
- 클래스 Undergraduate는 클래스 Student를 상속하고 있습니다.
  - 클래스 Student는 클래스 Undergraduate의 슈퍼 클래스입니다.

```swift
var someUndergraduate = Undergraduate()
someUndergraduate.name          // 이름
someUndergraduate.weight        // 0.0
someUndergraduate.height        // 0.0
someUndergraduate.studentId     // 012345
someUndergraduate.major         // 전자공학
```

클래스 Undergraduate는 클래스 Student를 상속하고, 클래스 Student는 클래스 Person을 상속하므로 클래스 Undergraduate는 클래스 Student, Person의 모든 멤버를 상속합니다. 따라서 Undergraduate의 인스턴스는 두 클래스의 멤버에도 접근할 수 있습니다.

> 주의할 점: 다중 상속(여러 개의 클래스를 한번에 상속하는 것)은 불가능합니다.
