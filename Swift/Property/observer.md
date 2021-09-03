# 속성 감시자(Property Observer)

속성 감시자는 속성의 종류는 아니고 저장 속성이 변하는 시점을 관찰(또는 감시)하고 있는 메서드를 말합니다. 저장 속성 뒤에 속성 감시자를 추가하면 해당 저장 속성의 값이 새롭게 설정되는 시점을 관찰합니다. 저장 속성의 값이 설정되는 시점의 직전과 직후에 속성 감시자 메서드가 호출되고 메서드 내부의 코드를 실행하는 방식입니다.

## 속성 감시자 사용 이유

속성 감시자는 저장 속성 뒤에 붙어서 저장 속성이 변하는 시점을 관찰합니다. 따라서 속성이 변하는 시점에서 이 변경 내용을 반영하고 싶을 때 사용합니다. 예를 들어 프로필 상태 메세지와 프로필 사진을 업데이트하는 경우가 있습니다.

## 속성 감시자 종류

속성 감시자에는 두 가지 종류가 있습니다.

**willSet()**

- 속성의 값이 변하기 직전에 호출되는 메서드

**didSet()**

- 속성의 값이 바뀐 직후에 호출되는 메서드

두 메서드는 속성의 값을 설정하는 시점의 직전과 직후에 호출되는 메서드입니다. 아래의 예시에서 속성 감시자를 어떻게 사용하는지 알아봅니다.

## 속성 감시자 예시

```swift
class Profile {
    var name: String

    // 속성 감시자를 추가한 저장 속성
    var statusMessage: String {
        willSet(message) {          // 바뀔 값이 파라미터로 전달됨
            print("상태 메세지가 \(statusMessage)에서 \(message)으로 변경됩니다.")
        }
        didSet(message) {           // 바뀌기 전의 값이 파라미터로 전달됨
            print("상태 메세지가 \(message)에서 \(statusMessage)으로 변경되었습니다.")
        }
    }

    init(name: String, statusMessage: String) {
        self.name = name
        self.statusMessage = statusMessage
    }
}

var myProfile = Profile(name: "devyoon56", statusMessage: "기본 상태메세지")
myProfile.statusMessage = "속성 공부 중"

// 상태 메세지가 기본 상태메세지에서 속성 공부 중으로 변경됩니다.
// 상태 메세지가 기본 상태메세지에서 속성 공부 중으로 변경되었습니다.

myProfile.statusMessage = "속성 감시자 공부 중"

// 상태 메세지가 속성 공부 중에서 속성 감시자 공부 중으로 변경됩니다.
// 상태 메세지가 속성 공부 중에서 속성 감시자 공부 중으로 변경되었습니다.
```

statusMessage 저장 속성 뒤에 속성 감시자 willSet()과 didSet()을 추가해서 해당 속성을 새롭게 설정할 때마다 두 메서드를 호출하도록 코드를 작성했습니다.

> 저장 속성을 초기화할 때는 두 메서드가 호출되지 않습니다.

- myProfile.statusMessage = "속성 공부 중" 으로 속성에 값을 설정하면 두 메서드 내부의 코드가 실행되는 것을 확인할 수 있습니다.
- myProfile.statusMessage = "속성 감시자 공부 중" 으로 속성에 값을 설정하면 두 메서드의 내부 코드가 실행되는 것을 확인할 수 있습니다.

> 일반적으로 willSet 또는 didSet 중에서 하나의 메서드만 구현합니다.(didSet을 많이 사용합니다)

## 속성 감시자 파라미터의 생략

- willSet 메서드에 사용하는 파라미터를 명시하지 않은 경우 스위프트는 willSet 메서드 내부에서 사용할 수 있는 **newValue**라는 파라미터를 제공합니다.
- didSet 메서드에 사용하는 파라미터를 명시하지 않은 경우 스위프트는 didSet 메서드 내부에서 사용할 수 있는 **oldValue**라는 파라미터를 제공합니다.

이 파라미터들은 해당 메서드들의 역할을 잘 표현합니다.

- willSet은 속성이 변하기 직전에 호출되고 이 메서드에는 새로운 값이 전달되기 때문에 **newValue**라는 파라미터를 사용하는 것이 문맥적으로 맞는 표현입니다.
- didSet은 속성이 바뀐 직후에 호출되고 이 메서드에는 바뀌기 전의 값이 전달되기 때문에 **oldValue**라는 파라미터를 사용하는 것이 문맥적으로 맞는 표현입니다.

```swift
class Profile {
    var name: String

    // 속성 감시자를 추가한 저장 속성
    var statusMessage: String {
        willSet {          // 바뀔 값이 파라미터로 전달됨
            print("상태 메세지가 \(statusMessage)에서 \(newValue)으로 변경됩니다.")
        }
        didSet {           // 바뀌기 전의 값이 파라미터로 전달됨
            print("상태 메세지가 \(oldValue)에서 \(statusMessage)으로 변경되었습니다.")
        }
    }

    init(name: String, statusMessage: String) {
        self.name = name
        self.statusMessage = statusMessage
    }
}

var me = Profile(name: "devyoon56", statusMessage: "바빠")

me.statusMessage = "한가해"

// 상태 메세지가 바빠에서 한가해으로 변경됩니다.
// 상태 메세지가 바빠에서 한가해으로 변경되었습니다.
```

## 주의점

속성 감시자를 추가할 수 없는 경우

- 저장 속성이 상수인 경우
  - 상수는 값이 변하지 않기 때문에 속성의 변화를 관찰할 수 없습니다.
- 지연 저장 속성인 경우
- 계산 속성인 경우
  - 계산 속성의 경우 계산 속성의 set 블럭에서 값의 변경을 관찰하는 것이 가능하므로 계산 속성에는 속성 감시자를 추가할 수 없습니다.

속성 감시자를 추가할 수 있는 경우

- 일반적인 저장 속성
- 클래스를 상속한 저장 속성
- 클래스를 상속해서 재정의하는 계산 속성

> 일반적으로 저장 속성에 속성 감시자를 추가해서 사용한다는 사실을 알고 속성 감시자를 사용하면 됩니다.
