# 계산 속성(Computed Property)

계산 속성은 일반적인 저장 속성의 값을 사용해서 계산한 값을 가지는 속성을 말합니다. 사실 계산 속성은 속성의 형태를 가지고 있는 메서드입니다. 다른 저장 속성들의 값을 사용해서 계산한 결과를 사용하는 메서드를 속성의 형태로 만든 것이 바로 계산 속성입니다.

## 계산 속성이 아닌 예시

먼저 체질량 지수(BMI)를 구하는 메서드를 구현해봅니다. 여기서는 계산 속성을 구현하지 않습니다.

```swift
class Person {
    var name: String = "익명의 사람"
    var height: Double
    var weight: Double

    init(height: Double, weight: Double) {
        self.height = height
        self.weight = weight
    }

    func calculateBMI() -> Double {
        return weight / (height * height) * 10000       // height는 m 단위로 계산해야 합니다
    }
}

var person = Person(height: 165.0, weight: 65.0)
person.calculateBMI()           // 23.875
```

BMI를 계산하는 메서드는 파라미터가 없고 인스턴스의 저장 속성을 사용합니다. 생성자로 초기화한 저장 속성의 값을 사용해서 BMI를 계산해서 결과값을 리턴합니다. 이런 메서드는 속성의 형태로 구현할 수 있습니다.

## 계산 속성 예시

BMI를 구하는 위 예시의 메서드를 계산 속성으로 바꾸어서 구현해봅니다.

```swift
class Person {
    var name: String = "익명의 사람"
    var height: Double
    var weight: Double

    // 계산 속성 선언
    var bmi: Double {
        get {       // 값을 얻는다(읽는다)
            return weight / (height * height) * 10000
        }
    }

    init(height: Double, weight: Double) {
        self.height = height
        self.weight = weight
    }
}

var person = Person(height: 165.0, weight: 65.0)

print(person.bmi)       // 23.875, 값을 읽는다
```

bmi는 항상 다른 저장 속성(weight, height)의 값을 사용해서 계산한 결과값이 됩니다. 이런 방식의 메서드를 아예 속성의 형태로 구현하는 것이 바로 계산 속성입니다. 따라서 계산 속성을 보면 메서드와 형태가 유사합니다. 리턴 타입이 있고 return 키워드를 사용해서 값을 리턴합니다.

위 코드에서 사용한 **get** 키워드는 값을 얻는다 또는 값을 읽는다는 의미의 키워드입니다. 계산 속성에 접근해서 계산 속성의 값을 읽는 경우에 get 블럭 내부의 코드를 실행합니다. 위 코드에서 **person.bmi**가 계산 속성의 값을 읽는 것이고 bmi 계산 속성의 get 블럭 내부의 코드를 실행해서 값을 읽습니다.

위 코드는 get 블럭만 구현했기 때문에 속성 값을 읽어오는 것만 가능합니다. 속성 값을 읽어오는 것만 가능한 속성을 _get-only property_ 또는 _read-only property_ 라고 합니다.

## 읽기와 쓰기가 가능한 계산 속성 예시

위의 예시를 읽기와 쓰기 모두 가능한 계산 속성으로 변경할 수 있습니다.

```swift
class Person {
    var name: String = "익명의 사람"
    var height: Double
    var weight: Double

    // 계산 속성 선언
    var bmi: Double {
        get {            // getter, 값을 얻는다(읽는다)
            return weight / (height * height) * 10000
        }
        set(bmi) {       // setter, 값을 설정한다(넣는다)
            weight = bmi * height * height / 10000
        }
    }

    init(height: Double, weight: Double) {
        self.height = height
        self.weight = weight
    }
}

var person = Person(height: 165.0, weight: 65.0)

print(person.bmi)       // 23.875, 값을 읽는다

person.bmi = 25         // 값을 넣는다
print(person.weight)    // 68.062, weight 저장 속성 변경
```

**set** 키워드는 값을 설정한다 또는 값을 넣는다(쓴다)는 의미의 키워드입니다. 계산 속성에 값을 넣어서 set 블럭 내부의 코드를 실행할 수 있습니다.

> get을 표현할 때 getter, set을 표현할 때 setter라고 합니다.

위 코드에서 bmi 계산 속성에 값을 넣었더니 weight 저장 속성이 변경되었습니다. 이것은 bmi 속성의 set 블럭 내부의 코드가 실행되었기 때문입니다. 이렇게 계산 속성에 값을 넣어서 그 값으로 저장 속성을 변경하는 등의 코드를 실행할 수 있습니다.

## get 블록 생략

get-only property 또는 read-only property는 편의상 get 블록을 생략할 수 있습니다. set 블록이 있다면 get 블록은 생략할 수 없습니다.

```swift
class Person {
    var name: String = "익명의 사람"
    var height: Double
    var weight: Double

    // read-only 계산 속성의 get 블록 생략
    var bmi: Double {
        return weight / (height * height) * 10000
    }

    init(height: Double, weight: Double) {
        self.height = height
        self.weight = weight
    }
}
```

## set 블록의 파라미터 생략

set 블록에는 특별하게 사용하는 파라미터 **newValue**가 있습니다. set 블록에 파라미터를 설정하지 않으면 스위프트가 먼저 지정해놓은 파라미터 **newValue**를 사용하면 됩니다. 이것은 문법적인 약속이기 때문에 단순하게 **newValue**를 사용하면 됩니다.

```swift
class Person {
    var name: String = "익명의 사람"
    var height: Double
    var weight: Double

    // 계산 속성 선언
    var bmi: Double {
        get {            // getter, 값을 얻는다(읽는다)
            return weight / (height * height) * 10000
        }
        set {            // setter, 값을 설정한다(넣는다)
            weight = newValue * height * height / 10000     // 파라미터 newValue 사용
        }
    }

    init(height: Double, weight: Double) {
        self.height = height
        self.weight = weight
    }
}
```

이전에는 set 블록에 bmi라는 파라미터를 설정해서 사용했지만 이 파라미터를 생략하면 newValue라는 파라미터를 사용할 수 있습니다. bmi 계산 속성에 값을 넣으면 이 값이 newValue 파라미터의 값이 되는 것입니다.
