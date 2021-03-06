# 지연 저장 속성(Lazy Stored Property)

클래스와 구조체의 지연 저장 속성은 동일합니다. 지연 저장 속성은 인스턴스를 초기화할 때 반드시 속성을 초기화할 필요가 없는 경우 사용하는 속성입니다. 지연 저장 속성은 저장 속성의 초기화를 지연시키는 것으로 이해하면 됩니다. 지연 저장 속성은 **lazy** 키워드를 사용해서 선언합니다.

## 지연 저장 속성 선언

```swift
class Person {
    var name: String
    var age: Int
    lazy var weight: Double = 80.5      // 지연 저장 속성 선언

    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }

    func learnSwift() {
        print("스위프트를 공부하고 있습니다.")
    }
}

var me = Person(name: "devyoon56", age: 29)     // 지연 저장 속성은 초기화되지 않음

print(me.weight)        // 80.5, 지연 저장 속성에 접근하면 속성이 초기화됨
```

지연 저장 속성은 다음과 같은 특징이 있습니다.

- 생성자를 사용해서 인스턴스를 초기화할 때 속성이 초기화되지 않습니다.(메모리 공간과 값을 가지지 않습니다)
- 지연 저장 속성에 접근했을 때 해당 속성이 개별적으로 초기화됩니다.(해당 속성은 메모리 공간과 값을 가집니다)
- 생성자에서 지연 저장 속성을 초기화하지 않기 때문에 지연 저장 속성을 선언하는 시점에 기본값을 저장해야 합니다.

## 지연 저장 속성이 기본값을 저장해야 하는 이유

위에서 weight 지연 저장 속성은 인스턴스를 초기화하는 시점에 초기화되지 않습니다. 인스턴스가 생성된 이후, weight 속성에 접근했을 때 속성이 초기화됩니다. 따라서 해당 속성에 접근했을 때 아무 값이 없다면 속성을 초기화할 수 없기 때문에 반드시 지연 저장 속성은 기본값을 가지고 있어야 합니다.

지연 저장 속성의 기본값은 어떤 값이나 모든 형태의 표현식이 될 수 있습니다. 따라서 함수 호출, 계산, 클로저 코드 등이 지연 저장 속성의 기본값이 될 수 있습니다. 표현식의 결과의 타입이 속성의 타입과 일치하기만 하면 됩니다.

## 지연 저장 속성을 사용하는 이유

1. 메모리 공간을 많이 차지하는 데이터(이미지 등)를 속성에 저장할 때입니다.

   데이터를 반드시 메모리에 올려놓을 필요가 없기 때문에 메모리 공간을 낭비하는 것을 막기위해 지연 저장 속성을 사용합니다.

2. 다른 속성들을 사용할 때입니다.

   인스턴스를 초기화할 때 모든 저장 속성들을 생성자를 사용하여 초기화합니다. 저장 속성들은 지연 저장 속성들 보다 먼저 초기화됩니다. 먼저 초기화된 저장 속성들을 사용해서 속성을 초기화하고 싶은 경우, 속성을 지연 저장 속성으로 선언하고 저장 속성에 저장된 값을 사용해서 지연 저장 속성을 초기화합니다.

```swift
class Person {
    var name: String
    var height: Double
    var weight: Double

    lazy var facePic = UIImageView()        // 1. 메모리를 많이 차지하는 경우
    lazy var bmi: Double = {                // 2. 다른 속성을 사용하는 경우
        return weight / (height * height)
    }()

    init(name: String, height: Double, weight: Double) {
        self.name = name
        self.height = height
        self.weight = weight
    }
}

var person = Person(name: "unknown", height: 1.75, weight: 75)

// height, weight 속성을 사용해서 bmi 지연 저장 속성을 초기화
print(person.bmi)       // 24.5
```

이런 지연 저장 속성의 특징 때문에 지연 저장 속성은 상수로 선언할 수 없고 오직 변수로만 선언할 수 있습니다.
