# 프로토콜의 개념

프로토콜은 무엇이고 왜 프로토콜이 필요한지에 대해 알아봅니다.

## 프로토콜이란

프로토콜은 규약, 협약 등의 사전적 의미를 가집니다. 이러한 추상적인 의미를 "자격증"이라는 개념으로 조금 더 자세하게 표현할 수 있습니다. 여기에서 프로토콜이 자격증이라는 개념은 어떤 자격을 갖추기 위한 능력을 명시해놓은 것입니다. 아래 예제에서 피아니스트라는 프로토콜을 정의합니다.

```swift
// 프로토콜 정의
protocol Pianist {
    func playPiano()
}
```

Pianist라는 자격증을 얻기 위해서는 Pianist 자격증을 정의할 때 명시한 playPiano() 라는 능력을 반드시 가져야 합니다. 이렇게 하려면 먼저 Pianist 프로토콜을 채택하고 프로토콜에서 명시한 playPiano() 메서드를 구현해야 합니다.

```swift
// 프로토콜 채택
struct SomeStruct: Pianist {

    // 요구사항 구현
    func playPiano() { print("피아노를 칠 수 있습니다.") }

}
```

## 상속의 단점과 프로토콜의 필요성

스위프트의 상속에는 다음과 같은 단점이 있습니다.

- 하나의 클래스만 상속 가능하다. 즉 다중 상속이 불가능하다.
- 기본적으로 슈퍼 클래스의 메모리 구조를 따른다. 즉 필요하지 않은 속성, 메서드도 상속한다.
- 클래스(참조 타입)만 상속 가능하다. 즉 값 타입은 상속이 불가능하다.

```swift
class Bird {
    var isFemale = false

    func layEgg() {
        if isFemale { print("새가 알을 낳는다.") }
    }

    func fly() { print("새가 하늘로 날아간다.") }
}

class Eagle: Bird {
    func soar() { print("공중으로 치솟아 날아간다.") }
}

class Penguin: Bird {
    func swim() { print("헤엄친다.") }
}

class Airplane: Bird {
    override func fly() { print("비행기가 날고있다.") }
}
```

Eagle 클래스는 Bird 클래스를 상속하므로 Bird 클래스의 속성과 메서드를 상속합니다.

```swift
let eagle = Eagle()
eagle.layEgg()
eagle.fly()
eagle.soar()
```

Penguin 클래스도 Bird 클래스를 상속하므로 Bird 클래스의 속성과 메서드를 상속합니다. 하지만 Penguin은 하늘을 날 수 없습니다. 그렇지만 Bird 클래스를 상속하므로 fly() 메서드까지 상속합니다. 즉 필요없는 메서드까지 상속한 것입니다.

```swift
let penguin = Penguin()
penguin.layEgg()
penguin.fly()
penguin.swim()
```

Airplane 클래스도 Bird 클래스를 상속하므로 Bird 클래스의 속성과 메서드를 상속합니다. 하지만 Airplane은 알을 낳을 수 없습니다. 그렇지만 Bird 클래스를 상속하므로 isFemale 속성과 layEgg() 메서드까지 상속합니다. 즉 필요없는 속성과 메서드를 상속한 것입니다.

```swift
let airplane = Airplane()
airplane.layEgg()
airplane.fly()
```

위와 같은 클래스의 단점을 프로토콜이 해결해줍니다.

- Bird 클래스에서 fly() 메서드를 따로 분리해서 fly() 메서드를 사용 가능하게 해준다.
- 구조체도 fly() 메서드를 사용할 수 있다.

```swift
// CanFly 프로토콜 정의
protocol CanFly {
    func fly()      // 프로토콜 요구사항 명시
}

class Bird {
    var isFemale = false

    func layEgg() {
        if isFemale { print("새가 알을 낳는다.") }
    }
}

// Bird 클래스 상속, CanFly 프로토콜 채택
class Eagle: Bird, CanFly {
    func soar() { print("공중으로 치솟아 날아간다.") }

    // fly() 메서드 구현
    func fly() { print("독수리가 하늘을 날아간다.") }
}

class Penguin: Bird {
    func swim() { print("펭귄이 헤엄친다.") }
}

// CanFly 프로토콜 채택
struct Airplane: CanFly {

    // fly() 메서드 구현
    func fly() { print("비행기가 하늘을 날아간다.") }

}
```

CanFly 프로토콜을 채택한 클래스와 구조체는 fly() 메서드를 사용할 수 있습니다. 이 때 CanFly 프로토콜을 채택한 타입마다 fly() 메서드를 원하는 대로 정의해서 사용합니다.

```swift
let eagle = Eagle()
eagle.fly()

let penguin = Penguin()
penguin.fly()       // 해당 메서드가 없으므로 접근 실패

let airplane = Airplane()
airplane.fly()
airplane.isFemale   // 해당 속성이 없으므로 접근 실패
airplane.layEgg()   // 해당 메서드가 없으므로 접근 실패
```
