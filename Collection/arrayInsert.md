# 배열 삽입하기

배열에 요소를 삽입할 수 있습니다.

```swift
var hanguel = ["가", "나", "라", "마", "바"]

hanguel.insert("다", at: 2)     // ["가", "나", "다", "라", "마", "바"]
hanguel.insert("사", at: hanguel.endIndex)  // ["가", "나", "다", "라", "마", "바", "사"]

hanguel.insert(contentsOf: ["아", "자", "차"], at: hanguel.endIndex)  // ["가", "나", "다", "라", "마", "바", "사", "아", "자", "차"]
```
