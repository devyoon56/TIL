# inout

스위프트에서 기본적으로 함수의 파라미터는 상수이고 값 타입(복사되어 전달됨)입니다. 따라서 함수의 파라미터를 직접 변경할 수 없습니다.

다음 함수는 에러가 발생합니다.

```swift
var a = 1
var b = 10

func swapTwoNumbers(num1: Int, num2: Int) {
    var temp = num1
    num1 = num2         // 파라미터는 상수이므로 값 변경 불가능
    num2 = temp         // 파라미터는 상수이므로 값 변경 불가능
}

swapTwoNumbers(num1: a, num2: b)
```

전달하는 파라미터의 값을 바꾸기 위해 함수 내부에서 별도의 지역변수를 선언합니다. 하지만 바뀐 값은 그 함수가 종료되면 함께 사라집니다.(메모리 구조)

```swift
var a = 10

func increment(_ num: Int) {
    var num = num
    num += 1
}

increment(a)
print(a) // 10
```

**inout** 키워드를 파라미터에 사용하면 함수 내부에서 직접 값을 수정할 수 있습니다. **inout** 키워드를 사용하면 파라미터를 값 타입으로 전달하지 않고 _참조로 전달합니다_. 참조로 전달한다는 것은 메모리 주소를 전달하는 것과 같습니다.

**inout** 파라미터는 변수를 직접 넣었다가 뺀다고 생각하면 쉽습니다.

```swift
var a = 1
var b = 10

// 파라미터의 데이터 타입 앞에 inout 키워드 사용
func swapTwoNumbers(num1: inout Int, num2: inout Int) {
    var temp = num1
    num1 = num2
    num2 = temp
}

// inout 파라미터에 값을 넘길 때 & 표시 필수
swapTwoNumbers(num1: &a, num2: &b)

print(a)    // 10
print(b)    // 1
```

**inout** 키워드는 값을 직접 바꾸겠다는 선언으로 볼 수 있습니다. 따라서 상수나 리터럴을 inout 파라미터로 넘길 수 없습니다.

또한 파라미터의 기본값을 사용할 수 없고 가변 파라미터로 선언할 수 없습니다.

## inout의 원리 copy-in copy-out

inout 파라미터는 다음의 과정을 거칩니다.

- 함수가 호출되면 파라미터로 넘겨진 변수가 복사됩니다.
- 함수 내부의 코드로 복사한 변수의 값을 바꿉니다.
- 함수가 종료될 때 바뀐 값을 아규먼트로 전달된 원본 변수에 다시 할당합니다.

위와 같은 과정을 **copy-in copy-out**이라고 합니다. 실제로 inout은 **copy-in copy-out**의 줄임말로, 안으로 복사되고 바깥으로 복사된다는 뜻입니다.
