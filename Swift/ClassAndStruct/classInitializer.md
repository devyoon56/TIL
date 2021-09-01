# 클래스의 초기화(Initialization)

클래스의 모든 속성과 메서드를 사용하기 위해서는 반드시 초기화 과정이 필요합니다. 이 초기화 과정은 클래스의 특별한 메서드인 생성자(initializer) **init()** 을 사용합니다. 인스턴스 생성 과정은 클래스의 저장 속성에 대한 초기값을 설정해서 속성이 사용가능한 상태가 되는 것입니다. 생성자의 실행이 종료되는 시점에는 모든 속성에 초기값이 저장되어 있어야 합니다. 그렇지 않으면 에러가 발생합니다.

결국 생성자 init()을 사용하는 이유는 모든 저장 속성을 초기화하며 인스턴스를 생성하기 위함입니다. 생성자는 인스턴스를 생성할 때 사용하는 특별한 메서드라고 이해할 수 있습니다.

## 클래스 생성자 정의

```swift
class Dog {
    var name: String
    var weight: Double
    var age: Int

    // 생성자 정의
    init(name: String, weight: Double, age: Int) {
        self.name = name
        self.weight = weight
        self.age = age
    }

    func shakeTail() {
        print("\(self.name)가 꼬리를 흔듭니다.")
    }

    func sit() {
        print("\(self.name)가 앉아서 기다립니다.")
    }
}

// 생성자로 인스턴스 생성
var dog1 = Dog(name: "흰둥이", weight: 7.2, age: 5)
var dog2 = Dog(name: "흑구", weight: 13.3, age: 4)
var dog3 = Dog(name: "황구", weight: 16.7, age: 6)
```

클래스를 정의하는 곳에서 생성자를 정의합니다. 생성자를 정의하는 것은 함수를 정의하는 것과 동일하게 파라미터와 파라미터의 타입을 명시합니다. 생성자 정의 내부에서 파라미터를 이용해서 모든 저장 속성에 파라미터의 값을 할당합니다.

인스턴스를 생성할 때 생성자를 사용합니다. 생성자의 파라미터에 값을 전달하면 생성자를 정의한 대로 모든 저장 속성에 값을 초기화합니다. 생성자를 사용해서 인스턴스를 생성하면 메모리에 정상적으로 인스턴스가 저장됩니다.

## self 키워드

클래스 생성자 정의 내부와 메서드에서 **self** 키워드를 볼 수 있습니다. **self** 키워드는 클래스나 구조체의 인스턴스(자기자신)을 가리킵니다. 생성자를 정의할 때 보통 속성과 동일한 파라미터 이름을 사용하게 되는데 이 때 인스턴스 내부에서 속성과 파라미터를 명확하게 구분하기 위해 속성에 **self** 키워드를 사용합니다.

즉 'self.속성'은 인스턴스의 속성을 의미하는 것입니다.

## 속성이 옵셔널 타입인 경우

```swift
class Dog {
    var name: String?       // 속성 타입: 옵셔널 String
    var age: Int

    // 생성자 정의
    init(age: Int) {
        self.age = age
    }

    func shakeTail() {
        print("\(self.name)가 꼬리를 흔듭니다.")
    }

    func sit() {
        print("\(self.name)가 앉아서 기다립니다.")
    }
}

var dog = Dog(age: 10)

print(dog.name)     // nil
print(dog.age)      // 10

dog.shakeTail()     // nil가 꼬리를 흔듭니다.
```

옵셔널 타입을 가진 속성의 경우, 생성자를 사용하여 반드시 초기화를 하지 않아도 됩니다. 옵셔널 타입의 경우 아무 값도 초기화하지 않으면 nil로 초기화되기 때문입니다.
