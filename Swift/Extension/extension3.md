# 메서드의 확장

타입의 확장에서 타입, 인스턴스 메서드를 추가할 수 있습니다.

## 타입 메서드의 확장

Int 타입을 확장하여 1~5까지 출력하는 타입 메서드를 추가하는 예제입니다.

```swift
extension Int {
    static func printOneToFive() {
        for i in 1...5 { print(i) }
    }
}

Int.printOneToFive()        // 1부터 5까지 출력

// 애플이 제공하는 타입 메서드 예시
Int.random(in: 1...10)      // 1부터 10까지의 랜덤 정수 반환
```

## 인스턴스 메서드의 확장

String 타입을 확장하여 인사말을 반복해서 출력하는 인스턴스 메서드를 추가하는 예제입니다.

```swift
extension String {
    func printHelloSeveralTimes(of times: Int) {
        for _ in 1...times { print("Hello \(self)!") }
    }
}

"Swift".printHelloSeveralTimes(of: 5)       // "Hello Swift!" 5번 출력
```

## mutating 인스턴스 메서드의 확장

구조체 또는 열거형의 저장 속성을 변경하는 메서드의 경우 mutating 키워드가 필요합니다. 구조체 또는 열거형의 경우 인스턴스 자체를 변경하는 경우에도 mutating 키워드를 사용합니다.

Int 타입(구조체)을 확장하여 인스턴스의 값을 제곱한 결과를 인스턴스에 다시 할당하는 인스턴스 메서드를 추가하는 예제입니다.

```swift
extension Int {
    mutating func square() {
        self = self * self
    }
}

var num = 10
num.square()
num             // 100
```
