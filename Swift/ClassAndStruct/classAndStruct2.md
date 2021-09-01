# 클래스와 구조체의 메모리 저장 방식

클래스와 구조체의 정의는 공통적으로 메모리의 데이터 영역에 저장됩니다. 메모리의 데이터 영역은 타입 속성이 저장되는 영역으로 어디서든 접근 가능한 데이터를 저장하는 공간입니다.

클래스와 구조체의 차이점은 여러가지가 있지만 가장 큰 차이점은 인스턴스를 생성해서 메모리에 저장하는 방식입니다.

## 구조체의 메모리 저장 방식

- 구조체는 값 형식(value type)입니다.
- 구조체의 인스턴스를 생성하면 메모리의 스택 영역에 인스턴스를 저장합니다.
- 구조체의 인스턴스를 복사해서 전달하면 인스턴스의 복사본을 새롭게 생성하여 값을 전달합니다. 즉 스택 영역에 또다른 인스턴스를 생성하는 것입니다.
- 구조체 인스턴스는 스택 영역에 생성되므로 구조체 인스턴스를 생성한 스택 프레임이 종료되면 스택 영역에서 사라집니다.

```swift
// 구조체 정의
struct Person {
    var name = "사람"
}

// 인스턴스 생성
var person = Person()

print(person.name)      // 사람

var person2 = person    // 인스턴스 person 복사
person2.name = "사람2"  // name 속성 변경

print(person.name)      // 사람
print(person2.name)     // 사람2
```

인스턴스 person을 복사하여 person2에 전달하면 새로운 인스턴스를 생성하여 전달합니다. 인스턴스 person과 인스턴스 person2는 스택 영역의 각각의 공간에 저장되는 것입니다. 그래서 person과 person2는 각각의 인스턴스가 되기 때문에 person2의 name 속성을 변경해도 person의 name 속성은 변경되지 않습니다.

## 클래스의 메모리 저장 방식

- 클래스는 참조 타입(reference type)입니다.
- 클래스의 인스턴스를 생성하면 메모리의 힙 영역에 인스턴스를 저장합니다.
- 인스턴스를 할당한 변수나 상수는 스택 영역에 저장됩니다. 이런 변수나 상수는 힙 영역에 저장된 인스턴스의 주소값을 가지고 있습니다. 즉 변수나 상수에 저장된 주소값이 힙 영역의 인스턴스를 가리키는 것입니다.
- 클래스의 인스턴스를 복사하면 값을 전달하는 것이 아니라 저장된 주소값을 전달합니다.

```swift
class Person {
    var name = "사람"
}

var classPerson = Person()
print(classPerson.name)           // 사람

var classPerson2 = classPerson    // 인스턴스 classPerson 복사, classPerson과 동일한 인스턴스를 가리킴
print(classPerson2.name)          // 사람

classPerson.name = "사람2"
print(classPerson.name)           // 사람2
print(classPerson2.name)          // 사람2

classPerson2.name = "사람3"
print(classPerson.name)           // 사람3
print(classPerson2.name)          // 사람3
```

클래스의 인스턴스를 복사해서 전달하면 값을 전달하는 것이 아니라 저장된 주소값을 전달합니다. 즉 인스턴스 자체를 전달하는 것이 아니라 같은 인스턴스를 가리키는 주소값을 전달한다는 의미입니다. classPerson을 복사해서 classPerson2에 전달하면 결국 두 변수는 같은 인스턴스를 가리키게 됩니다.

따라서 classPerson의 name 속성을 변경해도 classPerson2의 name 속성이 변경됩니다. 마찬가지로 classPerson2의 name 속성을 변경해도 classPerson의 name 속성이 변경됩니다. 두 변수가 동일한 인스턴스를 가리키고 있기 때문입니다.
