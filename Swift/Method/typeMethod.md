# 타입 메서드(Type Method)

타입 메서드는 인스턴스에 속하지 않고 타입 자체에 속한 메서드를 말합니다. 클래스와 구조체 자체에 속하는 메서드인 것입니다. 타입 속성과 비슷하게 타입 자체에 속하는 보편적인 동작을 정의할 때 타입 메서드를 사용합니다.

## 타입 메서드의 특징

1. 메서드이므로 타입에 메모리 공간이 할당되지 않습니다.
   - 클래스와 구조체의 정의가 위치한 데이터 영역에 메서드 실행 주소가 저장되어 있습니다.
2. 타입 자체에 속한 메서드이므로 메서드에 접근하려면 타입 이름을 사용해야 합니다.
   - 타입명.메서드(파라미터)
3. 타입 메서드를 실행하면 스택에 스택프레임을 만들고 타입 데이터를 사용합니다.
   - 메서드가 종료되면 스택프레임은 해제됩니다.
4. 타입 메서드를 선언하려면 메서드 앞에 **static** 또는 **class** 키워드를 추가합니다.
   - **static** 타입 메서드는 클래스 상속 시 재정의가 불가능합니다.
   - **class** 타입 메서드는 클래스 상속 시 재정의가 가능합니다.

## 타입 메서드 예제

```swift
class Person {
    static var species = "인간"

    var name: String
    var age: Int

    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }

    func learnSwift() {
        print("\(self.name)은 스위프트를 배우는 중입니다.")
    }

    // 타입 메서드 정의
    static func introduce() {
        print("저는 \(species)입니다.")      // 타입 메서드에서 타입 속성에 접근하는 경우 타입명 생략 가능
    }
}

var me = Person(name: "devyoon56", age: 29)
me.learnSwift()                 // devyoon56은 스위프트를 배우는 중입니다.
Person.introduce()              // 저는 인간입니다.     타입 메서드 호출
```

## 실제 타입 메서드 예제

자주 사용하는 메서드인 random(in:) 메서드도 타입 메서드입니다. Int와 Double은 구조체입니다.

```swift
Int.random(in: 1...10)       // 5        타입 메서드 호출
Double.random(in: 0...1)     // 0.4520045245         타입 메서드 호출
```

## 타입 메서드 상속

클래스의 타입 메서드를 클래스 상속 시 재정의 가능하도록 하려면 타입 메서드를 선언할 때 **static** 키워드가 아니라 **class** 키워드를 사용해야 합니다.

```swift
class SomeClass {
    // 재정의 가능한 타입 메서드
    class func someTypeMethod() {
        print("타입 메서드입니다.")
    }
}

SomeClass.someTypeMethod()      // 타입 메서드 호출
```

클래스를 상속하려면 상속하고자 하는 클래스를 콜론 우측에 적습니다. 타입 메서드를 재정의하려면 타입 메서드 앞에 override 키워드를 사용합니다.

```swift
// 부모 클래스: SomeClass, 자식 클래스: SomeThingClass
class SomeThingClass: SomeClass {
    // 타입 메서드 재정의
    override class func someTypeMethod() {
        print("타입 메서드를 재정의합니다.")
    }
}

SomeThingClass.someTypeMethod()     // 타입 메서드 호출
```
