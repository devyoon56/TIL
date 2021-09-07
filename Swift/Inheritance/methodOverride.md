# 메서드 재정의

속성을 재정의하는 것에 비해 메서드를 재정의하는 것은 비교적 자유로운 편입니다.

- 슈퍼 클래스의 인스턴스, 타입 메서드 상관없이 기능을 추가할 수 있습니다.
  - 기능을 추가할 때 슈퍼 클래스의 메서드를 호출할 수 있습니다.
  - 슈퍼 클래스의 메서드 호출은 필요에 따라 선택합니다.
- 상위 클래스 메서드의 기능을 무시하고 새롭게 메서드를 구현하는 것도 가능합니다.

> 생성자의 재정의는 특이한 케이스로 뒤에서 알아보겠습니다.

## 메서드 재정의 예시

```swift
class Vehicle {
    func makeNoise() {
        print("....")
    }
}

class Train: Vehicle {
    override func makeNoise() {
        super.makeNoise()
        print("칙칙폭폭")
        super.makeNoise()       // 원하는 곳에서 슈퍼 클래스 메서드 호출 가능
    }
}

class Bicycle: Vehicle {
    override func makeNoise() {
        print("띠링 띠링")      // 슈퍼 클래스 메서드 구현 무시 가능
    }
}

let train = Train()
train.makeNoise()

// 출력 결과
// ....
// 칙칙폭폭
// ....

let bicycle = Bicycle()
bicycle.makeNoise

// 출력 결과
// 띠링 띠링
```

```swift
class ArrayString {
    var datas = ["1", "2", "3", "4", "5"]

    subscript(index: Int) -> String {
        get {
            if index > 4 {
                return "0"
            }
            return datas[index]
        }
        set {
            datas[index] = newValue
        }
    }
}

class ArrayString2: ArrayString {
    override subscript(index: Int) -> String {          // 서브스크립트 재정의 가능
        get {
            if index > 4 {
                return "없는 인덱스입니다."
            }
            return super[index]
        }
        set {
            super[index] = newValue
        }
    }
}

let arrayString = ArrayString2()
arrayString[5]                  // 없는 인덱스입니다.
arrayString[3]                  // "4"
arrayString[0] = "0"
arrayString[0]                  // "0"
```
