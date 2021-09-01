# 클래스와 구조체의 let과 var 키워드

클래스와 구조체의 가장 큰 차이점은 인스턴스를 메모리에 저장하는 방식입니다. 메모리에 인스턴스를 저장하는 방식 때문에 클래스와 구조체의 인스턴스를 상수에 할당하는 것은 의미가 다릅니다.

## 클래스의 let 키워드

```swift
class Person {
    var name = "사람"
    var age = 1
}

let classPerson = Person()

classPerson.name = "사람2"      // 에러 없음
classPerson.age = 2             // 에러 없음


let classPerson2 = Person()
classPerson = classPerson2      // 에러 발생
```

Person 클래스의 인스턴스를 생성하고 classPerson 상수에 할당합니다. classPerson가 상수임에도 name, age 속성을 변경할 수 있습니다. 이것은 클래스 인스턴스의 메모리 저장 방식 때문입니다.

인스턴스 자체는 힙 영역에 저장되고 인스턴스를 가리키는 메모리 주소를 상수 classPerson이 갖고 있습니다. 즉 상수 classPerson에는 메모리 주소값이 저장되어 있고 이 메모리 주소값이 바뀔 수 없는 것입니다. 따라서 가리키고 있는 인스턴스의 속성은 변경할 수 있습니다.

메모리 주소값이 바뀌지 않는다는 것은 위에서 에러가 발생하는 부분에서 확인할 수 있습니다. 또다른 인스턴스를 가리키는 주소값을 저장하고 있는 상수 classPerson2를 복사해서 classPerson에 전달하면 에러가 발생합니다. classPerson은 상수이므로 다른 인스턴스를 가리킬 수 없기 때문입니다.

## 구조체의 let 키워드

```swift
struct Animal {
    var name = "동물"
    var age = 1
}

let structAnimal = Animal()

structAnimal.name = "동물2"     // 에러 발생
```

상수 structAnimal에 스택 영역에 저장된 구조체 인스턴스를 할당합니다. 인스턴스 자체가 상수가 되기 때문에 인스턴스의 속성을 변경할 수 없는 것입니다.
