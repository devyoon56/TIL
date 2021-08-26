# 딕셔너리 Dictionary

딕셔너리는 데이터를 키와 값의 쌍으로 관리하는 컬렉션입니다. 배열과 다르게 딕셔너리의 데이터에는 순서가 없습니다.

## 1. 딕셔너리의 문법

- 배열처럼 대괄호 []를 사용합니다.
- 키와 값의 쌍은 콜론 : 으로 구분합니다.
- 딕셔너리의 키는 데이터를 구분하기 때문에 중복 불가능합니다.
- 딕셔너리의 값은 중복 가능합니다.
- 하나의 딕셔너리에는 동일한 자료형의 키와 값 쌍의 데이터만 담을 수 있습니다.
- 키 값은 **Hashable**해야 합니다.

```swift
// [키:값, 키:값, ...]
var dic1 = ["A": "Apple", "B": "Banana", "C": "City"]
let dic2 = [1: "Apple", 2: "Banana", 3: "City"]

print(dic1)
print(dic2)

/*
    출력결과: 데이터의 순서가 없음
    ["B": "Banana", "C": "City", "A": "Apple"]
    [2: "Banana", 3: "City", 1: "Apple"]
*/
```

## 2. 딕셔너리 타입 표기

딕셔너리의 타입을 표기하는 두 가지 방법이 있습니다.

```swift
// 단축 표기
var englishDict: [String: String]

// 정식 표기
var koreanDict: Dictionary<String, String>
```

## 3. 빈 딕셔너리 생성하기

단축 표기와 정식 표기를 사용하여 빈 딕셔너리를 생성할 수 있습니다.

```swift
var emptyDict1: Dictionary<String, String> = [:]
var emptyDict2 = Dictionary<String, String>()
var emptyDict3 = [Int: String]()

var emptyDict4 = [:]    // 에러 발생, 딕셔너리 타입을 알 수 없음
```

## 4. 딕셔너리 기본 기능

```swift
var dic = ["A": "Apple", "B": "Banana", "C": "City"]

dic.count   // 3

dic.isEmpty // false

print(dic.randomElement())
// named tuple 형태 반환
// 옵셔널 튜플 반환
// Optional((key: "C", value: "City"))
```

## 5. 딕셔너리 요소에 접근하기

딕셔너리 요소에 접근하는 방법은 주로 키와 함께 서브스크립트 문법을 사용합니다. 딕셔너리 요소를 가져오면 옵셔널 값을 가져오는 것에 주의해야 합니다. 옵셔널 값을 가져오는 이유는 딕셔너리에 없는 키를 사용하는 경우 값을 가져올 수 없기 때문에 **nil**을 반환하기 때문입니다.

```swift
var dic = ["A": "Apple", "B": "Banana", "C": "City"]

print(dic["A"]) // Optional("Apple")
print(dic["q"]) // nil
```

딕셔너리의 키를 사용하여 요소에 접근할 때 기본값을 제공할 수 있습니다.

```swift
var dic = ["A": "Apple", "B": "Banana", "C": "City"]

// [] 안에 default: 로 기본값 제공
print(dic["A", default: "app"])     // Apple
print(dic["q", default: "Quit"])    // Quit
```

기본값을 제공하면 옵셔널의 가능성을 없앨 수 있습니다. 이것은 딕셔너리의 키에 해당하는 값이 있다면 해당 값을 가져오고 값이 없다면 기본값을 사용하기 때문입니다. 이 방법은 옵셔널을 추출하는 _nil coalescing_ 방법과 유사합니다.

```swift
var dic = ["A": "Apple", "B": "Banana", "C": "City"]

// 키와 값 얻기
print(dic.keys)    // ["C", "A", "B"]
print(dic.values)  // ["City", "Apple", "Banana"]

// 키와 값을 오름차순으로 정렬해서 얻기
print(dic.keys.sorted())   // ["A", "B", "C"]
print(dic.values.sorted())  // ["Apple", "Banana", "City"]
```

**reversed()** 메서드를 사용하면 내림차순으로 정렬할 수 있습니다.

## 6. 딕셔너리 업데이트하기(삽입, 교체, 추가)

```swift
// 업데이트하기
var words: [String: String] = [:]

words["A"] = "Apple"    // 키가 없으면 키와 함께 값 추가
words                   // ["A": "Apple"]

words["B"] = "Banana"

words["B"] = "Boat"     // 키가 있으면 기존 값을 덮어씀
words                   // ["A": "Apple", "B": "Boat"]

words.updateValue("Cocoa", forKey: "C")
words                   // ["A": "Apple", "C": "Cocoa", "B": "Boat"]

words.updateValue("Coconut", forKey: "C")       // "Cocoa", 키에 해당하는 기존 값 반환
words                   // ["C": "Coconut", "A": "Apple", "B": "Boat"]

words = [:]             // 빈 딕셔너리로 만들기
words                   // [:]
```

딕셔너리에는 배열과 다르게 **append()** 함수가 없습니다. 딕셔너리는 순서가 없는 컬렉션이기 때문에 컬렉션 순서 마지막에 데이터를 추가하는 **append**는 사용할 수 없습니다.

```swift
// 삭제하기
var dic = ["A": "Apple", "B": "Banana", "C": "City"]

dic["B"] = nil      // 해당 요소 삭제
dic                 // ["A": "Apple", "C": "City"]

dic.removeValue(forKey: "A")    // Apple, 삭제한 값 반환

dic.removeAll()     // 전체 요소 삭제
dic.removeAll(keepingCapacity: true)    // 전체 요소 삭제, 컬렉션 메모리 공간 유지
```

## 7. 딕셔너리 활용하기

딕셔너리의 값은 배열이 될 수 있습니다.

```swift
var dic = [String: [String]]()

dic["array1"] = ["a", "b", "c"]
dic["array2"] = ["A", "B", "C"]
dic             // ["array2": ["A", "B", "C"], "array1": ["a", "b", "c"]]
```

딕셔너리의 값은 딕셔너리가 될 수도 있습니다.

```swift
var dic = [String: [String: Double]]()

dic["dic1"] = ["weight": 80.0, "height": 178.2]
dic["dic2"] = ["weight": 50.0, "height": 156.5]

dic     // ["dic1": ["height": 178.2, "weight": 80.0], "dic2": ["weight": 50.0, "height": 156.5]]
```

딕셔너리를 for문으로 반복하면 named 튜플 형태로 데이터를 하나씩 반환합니다. 딕셔너리에 순서가 없기 때문에 실행마다 결과는 다릅니다.

```swift
var dic = ["A": "Apple", "B": "Banana", "C": "City"]

for (key, value) in dic {
    print("\(key): \(value)")
}

// B: Banana
// A: Apple
// C: City
```
