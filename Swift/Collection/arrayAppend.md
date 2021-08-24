# 배열 추가하기

배열의 마지막에 요소를 추가할 수 있습니다.

```swift
var alphabet = ["A", "B", "C", "D", "E", "F", "G"]

alphabet += ["H"]   // ["A", "B", "C", "D", "E", "F", "G", "H"]

alphabet.append("I")    // ["A", "B", "C", "D", "E", "F", "G", "H", "I"]
alphabet.append(contentsOf: ["J", "K"])     // ["A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K"]

alphabet.append(100)        // 에러 발생, 동일한 타입의 데이터만 추가 가능
```
