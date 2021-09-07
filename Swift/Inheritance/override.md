# 재정의(Override)

오버라이딩(overriding)은 재정의를 말합니다. 재정의는 클래스의 상속 개념에서 슈퍼 클래스의 멤버를 서브 클래스에서 변형하거나 기능을 추가하는 개념입니다. 재정의는 **override** 키워드를 사용합니다.

슈퍼 클래스의 모든 멤버를 재정의할 수 있는 것은 아닙니다. 재정의할 수 있는 멤버는 다음과 같습니다.

- 속성(저장 속성에 대한 재정의는 원칙적으로 불가능)
- 메서드(메서드, 서브스크립트, 생성자)

속성과 메서드를 재정의하는 방식에는 차이가 있습니다. 이후 예시에서 알아보겠습니다.

## 재정의 간단한 예시

슈퍼 클래스의 메서드를 간단하게 재정의하는 예시입니다.

```swift
class Aclass {
    func doSomething() {
        print("do something")
    }
}

class Bclass: Aclass {
    override func doSomething() {
        print("do another thing")
        super.doSomething()             // 슈퍼 클래스의 메서드 호출 가능
    }
}

let b = Bclass()
b.doSomething()

// 출력 결과
// do another thing
// do something
```

**override** 키워드를 사용하여 슈퍼 클래스의 메서드 doSomething()을 서브 클래스에서 재정의하였습니다. 서브 클래스에서 슈퍼 클래스의 메서드를 재정의하면 기능을 추가하거나 변형할 수 있습니다. 이 때 필요에 따라 슈퍼 클래스의 메서드를 호출할 수도 있습니다. 슈퍼 클래스의 메서드를 호출하는 경우 **super** 키워드와 함께 메서드를 호출하면 됩니다.
