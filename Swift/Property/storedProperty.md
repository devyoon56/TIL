# 저장 속성(Stored Properties)

클래스와 구조체의 여러가지 속성 중 하나인 저장 속성은 일반적으로 값을 저장하는 속성을 말합니다. 클래스와 구조체의 저장 속성은 동일합니다. 저장 속성은 일반적인 변수와 상수처럼 값을 저장할 수 있는 속성입니다.

```swift
class Person {
    var name: String        // 저장 속성
    var age: Int            // 저장 속성
    var weight: Double?     // 옵셔널 타입 저장 속성

    init(name: String, age: Int) {          // 저장 속성에 기본값이 없다면 생성자를 통해 반드시 초기화합니다
        self.name = name
        self.age = age
    }

    func learnSwift() {
        print("스위프트를 공부합니다.")
    }
}

var me = Person(name: "devyoon56", age: 29)

print(me.name)      // devyoon56
print(me.age)       // 29
print(me.weight)    // nil
me.learnSwift()     // 스위프트를 공부합니다.
```

저장 속성은 다음과 같은 특징이 있습니다.

- var(변수) 또는 let(상수)로 선언할 수 있습니다.
- 생성자로 인스턴스를 초기화하면 저장 속성은 자신만의 메모리 공간을 가집니다.
- 인스턴스에서 저장 속성은 데이터 저장 공간이 되는 것입니다.
- 인스턴스를 초기화할 때 저장 속성은 기본값을 가지거나 기본값이 없다면 생성자를 사용하여 반드시 값을 초기화해야 합니다.
- 저장 속성이 옵셔널 타입인 경우, 생성자를 사용하여 반드시 값을 초기화하지 않아도 됩니다.
- 옵셔널 타입에 값을 초기화하지 않으면 nil로 초기화되기 때문입니다.
