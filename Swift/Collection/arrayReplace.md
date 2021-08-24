# 배열 교체하기

배열의 요소를 교체할 수 있습니다.

```swift
var alphabet = ["A", "B", "C", "D", "E", "F", "G"]

// 요소 교체하기
alphabet[0] = "a"   // ["a", "B", "C", "D", "E", "F", "G"]

// 범위 연산자로 교체하기
alphabet[1...3] = ["b", "c", "d"]   // ["a", "b", "c", "d", "E", "F", "G"]

// 원하는 범위 삭제하기
alphabet[4...alphabet.endIndex - 1] = []    // ["a", "b", "c", "d"]

alphabet.replaceSubrange(0...3, with: ["A", "B", "C", "D"])     // ["A", "B", "C", "D"]
```
