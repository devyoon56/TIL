# 배열의 요소 삭제하기

배열의 요소를 삭제할 수 있습니다.

```swift
var alphabet = ["A", "B", "C", "D", "E", "F", "G"]

alphabet[0...2] = []  // ["D", "E", "F", "G"]
alphabet.remove(at: 3)  // ["D", "E", "F"], 인덱스의 요소를 삭제하고 삭제된 요소 반환

alphabet.remove(at: 3)  // 에러 발생, 인덱스가 없음 Index out of range

alphabet.removeSubrange(0...2)   // []
```

```swift
var alphabet = ["A", "B", "C", "D", "E", "F", "G"]

alphabet.removeFirst()   // 맨 앞에 요소 삭제하고 삭제된 요소 반환 ("A")
alphabet.removeFirst(2)   // 맨 앞의 두 개 요소 삭제, ["D", "E", "F", "G"]

alphabet.removeLast()   // 맨 뒤에 요소 삭제하고 삭제된 요소 반환 ("G")
alphabet.removeLast(2)  // 맨 뒤의 두 개 요소 삭제, ["D"]
```

```swift
var alphabet = ["A", "B", "C", "D", "E", "F", "G"]

alphabet.removeAll()    // 배열의 요소 모두 삭제
alphabet.removeAll(keepingCapacity: true)   // 배열의 메모리 공간은 유지하고 요소만 모두 삭제
```
