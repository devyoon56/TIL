# repeat-while 반복문

repeat-while 반복문은 while 반복문의 변화 버전으로 반복문 조건을 확인하지 않고 일단 반복문을 한 번 실행합니다. 반복문을 한 번 실행한 후에 조건을 확인하고 조건이 **true**이면 반복문을 계속 실행합니다. 조건이 **false**이면 반복문을 실행하지 않습니다.

> 스위프트의 repeat-while 반복문은 다른 언어의 do-while 반복문과 유사합니다.

## repeat-while 반복문의 형식

조건을 확인하지 않고 일단 반복문을 실행한 뒤에 조건에 따라 반복문 실행 여부를 결정합니다.

```swift
repeat {
    // code
} while 확인할 조건
```

## repeat-while 반복문 사용 시 주의할 점

while 반복문과 마찬가지로 repeat-while 반복문도 _무한루프_ 상태에 빠질 수 있습니다. 따라서 _무한루프_ 상태에서 빠져나오기 위해 조건을 변화시키는 코드가 필요합니다.

```swift
var i = 1

repeat {
    print("\(3) * \(i) = \(3 * i)")
    i += 1
} while i <= 9
```
