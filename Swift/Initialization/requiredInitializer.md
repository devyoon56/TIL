# 필수 생성자(Required Initializer)

필수 생성자는 서브 클래스에서 반드시 구현해야 하는 생성자입니다. 필수 생성자를 선언하려면 클래스의 생성자 앞에 **required** 키워드를 붙입니다. 이 키워드를 붙인 생성자는 필수 생성자가 됩니다. 서브 클래스에서 필수 생성자를 구현할 때 파라미터의 이름과 타입이 동일해야 합니다.

## 필수 생성자 예시

```swift
class Aclass {
    var x: Int

    // 필수 생성자
    required init(x: Int) {
        self.x = x
    }
}

class Bclass: Aclass {

    // 서브 클래스에서 필수 생성자 구현
    required init(x: Int) {
        super.init(x: x)        // 슈퍼 클래스의 필수 생성자 호출
    }
}
```

- 서브 클래스에서 필수 생성자를 구현할 때 **override** 키워드는 필요없고 **required** 키워드만 사용하면 됩니다.
- 서브 클래스에서 슈퍼 클래스의 필수 생성자를 호출하는 경우에는 required init으로 호출하지 않습니다.

## 필수 생성자 자동 상속

필수 생성자는 서브 클래스에서 다른 지정 생성자를 구현하지 않으면 서브 클래스에 자동 상속됩니다. 하지만 서브 클래스에서 다른 지정 생성자를 구현하면 슈퍼 클래스의 필수 생성자는 서브 클래스에 자동 상속되지 않으므로 서브 클래스에서 필수 생성자를 구현해야 합니다.

```swift
class Aclass {
    var x: Int

    // 필수 생성자
    required init(x: Int) {
        self.x = x
    }
}

class Bclass: Aclass {
    init() {                        // 지정 생성자
        super.init(x: 0)
    }

    required init(x: Int) {         // 필수 생성자
        super.init(x: x)
    }
}
```

## 필수 생성자 사용 예시

UIView와 UIViewController를 상속하여 지정 생성자를 구현하면 아래와 같은 필수 생성자를 반드시 구현해야 합니다. 자동 상속 조건을 만족하지 않기 때문입니다.

```swift
required init?(coder: aDecoder: NSCoder) {
    fatalError("init(coder:) has not been implemented")
}
```

```swift
class AView: UIView {
//    required init?(coder: NSCoder) {         // 자동 상속
//        fatalError("init(coder:) has not been implemented")
//    }
}


class BView: UIView {
    override init(frame: CGRect) {             // 지정 생성자
        super.init(frame: frame)
    }

    required init?(coder: NSCoder) {           // 필수 생성자
        fatalError("init(coder:) has not been implemented")
    }
}
```
