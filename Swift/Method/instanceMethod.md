# 인스턴스 메서드(Instance Method)

인스턴스 메서드는 클래스나 구조체의 인스턴스에 속하는 메서드를 말합니다. 클래스와 구조체 인스턴스의 일반적인 메서드입니다.

## 인스턴스 메서드의 특징

1. 메서드이므로 인스턴스에 메모리 공간이 할당되지 않습니다.
   - 클래스와 구조체의 정의가 위치한 데이터 영역에 메서드 실행 주소가 저장되어 있습니다.
2. 인스턴스에 속하는 메서드이므로 메서드 접근은 인스턴스 이름을 사용해야 합니다.
   - 인스턴스명.메서드(파라미터)
3. 인스턴스 메서드를 실행하면 스택에 스택프레임을 만들고 인스턴스의 데이터를 사용합니다.
   - 메서드가 종료되면 스택프레임은 해제됩니다.
4. 값 타입(구조체, 열거형)의 인스턴스 메서드는 원칙적으로 인스턴스의 속성을 수정할 수 없습니다.
   - 인스턴스의 속성을 수정하려면 명시적으로 메서드에 **mutating** 키워드를 붙여야 합니다.
5. 일반적인 함수와 동일하게 함수 오버로딩을 지원합니다.

## 클래스 인스턴스 메서드 예제

```swift
class Person {
    var name: String
    var age: Int

    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }

    func introduce() {
        print("저는 \(self.name)이고 \(self.age)살입니다.")
    }

    func learnSwift() {
        print("\(self.name)이 스위프트를 공부중입니다.")
    }

    func changeName(newName name: String) {
        self.name = name                // 클래스 인스턴스 메서드는 저장 속성 변경 가능
    }
}

var me = Person(name: "devyoon56", age: 29)

me.introduce()             // 저는 devyoon56이고 29살입니다.
me.learnSwift()            // devyoon56이 스위프트를 공부중입니다.

me.changeName(newName: "devyoon67")     // 인스턴스 메서드는 인스턴스 이름으로 호출
print(me.name)             // devyoon67
```

## 구조체 인스턴스 메서드 예제

```swift
struct Person {
    var name: String

    func learnSwift() {
        print("\(self.name)이 스위프트를 공부중입니다.")
    }

    mutating func changeName(newName name: String) {        // mutating으로 속성 변경 가능
        self.name = name
    }
}

var me = Person(name: "devyoon56")

me.learnSwift()             // devyoon56이 스위프트를 공부중입니다.
me.changeName(newName: "devyoon67")
me.learnSwift()             // devyoon67이 스위프트를 공부중입니다.
```

값 타입(구조체, 열거형)의 인스턴스 메서드는 원칙적으로 속성을 수정할 수 없습니다. 그러나 인스턴스 메서드에 **mutating** 키워드를 붙이면 속성을 변경할 수 있습니다.

> 이 점이 클래스와 구조체의 차이점 중 하나입니다.
