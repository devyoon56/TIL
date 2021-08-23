# 함수2

## 1. 함수의 파라미터와 아규먼트

파라미터 이름은 함수를 정의할 때 입력으로 사용하는 상수명입니다. 아규먼트 레이블을 사용하지 않으면 함수를 호출할 때 파라미터 이름을 그대로 사용합니다. 파라미터 이름은 함수 내부에서 사용할 수 있습니다.

아규먼트는 함수를 호출할 때 파라미터에 전달하는 실제 값을 말합니다. 파라미터의 데이터 타입과 일치해야 합니다.

```swift
func greeting(name: String) {       // 파라미터 == name: String
    print("안녕하세요. \()님 반갑습니다.")
}

greeting(name: "devyoon56")         // 아규먼트 == "devyoon56"
```

## 2. 함수의 아규먼트 레이블

함수는 함수의 파라미터 이름 뿐만 아니라 아규먼트 레이블을 가질 수 있습니다. 아규먼트 레이블은 파라미터의 이름 앞에 작성합니다.

```swift
// 두 번째 파라미터에 대한 아규먼트 레이블: from
func greet(person: String, from hometown: String) -> String {
  return "안녕하세요 \(person)님! \(hometown)에서 오신 분이군요."
}

// 함수 호출 시 아규먼트 레이블 'from' 사용
greet(person: "devyoon56", from: "서울")
```

아규먼트 레이블을 사용하면 이해하기 쉽고 의도가 명확한 함수를 제공할 수 있습니다. 함수를 사용할 때 일반적인 문장처럼 함수의 의미를 전달할 수 있다는 장점이 있습니다.

## 3. 아규먼트 레이블의 생략

아규먼트 레이블을 생략하는 와일드카드 패턴도 있습니다. 와일드카드 패턴은 언더바(\_)를 사용합니다.

```swift
// 아규먼트 레이블 생략: '_' 사용
func greet(_ person: String, _ hometown: String) -> String {
  return "안녕하세요 \(person)님! \(hometown)에서 오신 분이군요."
}

greet("devyoon56", "서울")
```

아규먼트 레이블을 생략하면 함수의 의도를 명확하게 전달하지 못할 수 있기 때문에 필요한 상황에 맞춰서 사용합니다.

## 4. 파라미터의 기본값

함수 파라미터의 데이터 타입 뒤에 파라미터의 기본값을 정의할 수 있습니다. 기본값을 정의하면 함수를 호출할 때 파라미터를 생략할 수 있습니다. 기본값을 가지는 파라미터는 기본값을 가지지 않는 파라미터 뒤에 위치합니다.

```swift
func justAddOne(num1: Int, num2: Int = 1) -> Int {
    return num1 + num2
}

var num = justAddOne(num1 = 5) // 6, 함수 호출 시 num2 파라미터 생략하면 기본값 사용
```

## 5. 가변 파라미터

가변 파라미터는 정해지지 않은 파라미터의 개수를 전달받고 싶을 때 사용합니다. 가변 파라미터는 함수마다 하나씩만 사용 가능하고 기본값을 가질 수 없습니다.

파라미터의 데이터 타입 뒤에 ... 을 붙여서 가변 파라미터로 정의합니다.

```swift
// numbers 가변 파라미터
func arithmeticMean(_ numbers: Double...) -> Double {
    var total: Double = 0

    // numbers 가변 파라미터는 배열 형태로 전달됨
    for number in numbers {
        total += number
    }

    return total / Double(numbers.count)
}

arithmeticMean(1, 2, 3, 4, 5)   // 3.0
arithmeticMean(3, 8.25, 18.75)  // 10.0
```
