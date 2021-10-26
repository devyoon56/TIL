# 타입으로써의 프로토콜

스위프트에서 프로토콜은 **일급객체(First Class Citizen)** 이므로 타입으로 사용할 수 있습니다. 프로토콜을 타입으로 사용한다는 의미는 다음과 같습니다.

1. 프로토콜을 변수에 할당할 수 있다.
2. 함수 호출 시 프로토콜을 파라미터로 전달할 수 있다.
3. 함수에서 프로토콜을 리턴할 수 있다.

다음은 타입으로써 프로토콜 예제입니다.

```swift
protocol Remote {

    func turnOn()

    func turnOff()

}

class TV: Remote {

    func turnOn() { print("TV 켜기") }

    func turnOff() { print("TV 끄기") }

}

struct SetTopBox: Remote {

    func turnOn() { print("셋톱박스 켜기") }

    func turnOff() { print("셋톱박스 끄기") }

    func doNetflix() { print("넷플릭스 보기") }       // 프로토콜 요구사항이 아닌 메서드

}

let tv = TV()
tv.turnOn()         // TV 켜기
tv.turnOff()        // TV 끄기

// 구조체 인스턴스를 생성하고 프로토콜 타입으로 선언 (SetTopBox 타입이 Remote 프로토콜을 채택하므로)
let sbox: Remote = SetTopBox()
sbox.turnOn()       // 셋톱박스 켜기
sbox.turnOff()      // 셋톱박스 끄기

//sbox.doNetflix()    // Remote 타입으로 선언되어 있어서 접근 불가능
```

## 프로토콜을 타입으로 취급하는 것의 장점

첫 번째 장점은 인스턴스를 프로토콜 타입으로 저장 가능하다는 것입니다. 두 번째 장점은 프로토콜을 파라미터로 전달 가능하다는 것입니다.

```swift
let tv = TV()
let sbox: Remote = SetTopBox()
let electronics: [Remote] = [tv, sbox]      // 인스턴스를 프로토콜 타입으로 저장

for item in electronics {
    item.turnOn()
    item.turnOff()
}

func turnOnSomeElectronics(item: Remote) {  // 프로토콜을 파라미터로 전달 가능
    item.turnOn()
}

turnOnSomeElectronics(item: tv)
turnOnSomeElectronics(item: sbox)
```

## 프로토콜 준수성 검사

is 연산자를 사용하면 인스턴스의 타입이 프로토콜을 채택하는지 확인할 수 있습니다.

```swift
let tv = TV()
let sbox: Remote = SetTopBox()

tv is Remote    // true
sbox is Remote  // true
```

tv가 참조하는 인스턴스는 TV 타입이고 TV 타입은 Remote 프로토콜을 채택하므로 true를, sbox는 Remote 타입으로 선언되어 있으므로 true를 반환합니다.

또는 is 연산자를 사용하여 프로토콜 타입으로 선언된 인스턴스의 구체적인 타입을 확인할 수 있습니다.

```swift
let tv = TV()
let sbox: Remote = SetTopBox()
let electronics: [Remote] = [tv, sbox]

electronics[0] is TV            // true
electronics[0] is SetTopBox     // false

electronics[1] is TV            // false
electronics[1] is SetTopBox     // true
```

## 프로토콜과 타입 캐스팅

프로토콜은 클래스, 구조체보다 범용적인 타입이므로 as 연산자를 사용하여 클래스, 구조체를 프로토콜로 업캐스팅할 수 있습니다.

```swift
protocol Remote {

    func turnOn()

    func turnOff()

}

struct SetTopBox: Remote {

    func turnOn() { print("셋톱박스 켜기") }

    func turnOff() { print("셋톱박스 끄기") }

    func doNetflix() { print("넷플릭스 보기") }       // 프로토콜 요구사항이 아닌 메서드

}

let newSbox = SetTopBox()
let newSbox2 = newSbox as Remote        // SetTopBox -> Remote

newSbox2.turnOn()           // 셋톱박스 켜기
newSbox2.turnOff()          // 셋톱박스 끄기
//newSbox2.doNetflix()      // Remote 타입으로 업캐스팅되어 접근 불가능
```

as?, as! 연산자를 사용하여 프로토콜을 클래스, 구조체로 다운캐스팅할 수 있습니다.

```swift
let sbox: Remote = SetTopBox()
let sbox2 = sbox as? SetTopBox          // Remote -> SetTopBox?

sbox2?.turnOn()
sbox2?.turnOff()
sbox2?.doNetflix()          // SetTopBox? 타입으로 다운캐스팅되어 접근 가능
```
