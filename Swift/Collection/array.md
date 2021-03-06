# Array 배열

스위프트의 컬렉션 중 배열에 대해 알아봅니다. 배열은 컬렉션 중에서 딕셔너리, 집합과 다르게 데이터를 **순서대로 저장**하는 컬렉션입니다.

## 1. 배열의 문법

- 배열은 대괄호 []를 사용합니다.
- 배열의 인덱스는 0부터 시작합니다.
- 배열에는 동일한 데이터 타입만 담을 수 있습니다.
- 배열은 데이터를 순서대로 저장하므로 데이터는 중복 가능합니다.
- 배열의 각 데이터를 요소(element)라고 합니다.
- 배열의 타입을 명시하지 않으면 할당한 요소의 타입으로 타입을 추론합니다.

```swift
var numArray = [1, 2, 3, 4, 5]                  // Array<Int>, 타입 추론
var doubleArray = [1.1, 2.2, 3.3, 4.4, 5.5]     // Array<Double>
var stringArray = ["a", "b", "c", "d", "e"]     // Array<String>

var intArray = [1, 2, 2, 3, 3, 3]
print(intArray)     // [1, 2, 2, 3, 3, 3]
```

## 2. 배열의 타입 표기

배열의 타입을 표기하는 두 가지 방법이 있습니다.

```swift
var numArray: Array<Int>    // 정식 표기
var doubleArray: [Double]   // 단축 표기
```

## 3. 빈 배열 생성하기

배열을 생성할 때 다음과 같이 빈 배열을 생성할 수 있습니다.

```swift
var emptyArray1: [Int] = []
var emptyArray2: Array<Int> = []
var emptyArray3 = [Int]()
```

## 4. 배열의 요소에 접근하기

배열의 요소에 접근하는 다양한 방법이 있습니다.

```swift
// 1. 서브스크립트 문법(대괄호 사용)
var numArray = [1, 2, 3, 4, 5]

numArray[0]     // 1, 인덱스 0부터 시작
numArray[1]     // 2
numArray[2]     // 3
numArray[3]     // 4
numArray[4]     // 5

numArray[0] = 0
print(numArray)     // [0, 2, 3, 4, 5]
```

```swift
// 2. 첫 요소와 마지막 요소 반환받기
var numArray = [1, 2, 3, 4, 5]

numArray.first  // 1
numArray.last   // 5

print(numArray.first)   // Optional(1)
print(numArray.last)    // Optional(5)
```

배열이 비어있다면 first, last 프로퍼티는 nil을 반환합니다. 즉 first, last 프로퍼티는 옵셔널 타입입니다.

```swift
// 3. 시작 인덱스와 마지막 인덱스 반환받기
var numArray = [1, 2, 3, 4, 5]

numArray.startIndex     // 0
numArray.endIndex       // 5

print(numArray[numArray.startIndex])    // 1
print(numArray[numArray.endIndex - 1])  // 5
print(numArray[numArray.endIndex])      // 에러 발생, Index out of range
```

위에서 startIndex는 배열의 인덱스 0을 반환합니다. 하지만 endIndex는 배열의 인덱스 4를 반환하지 않습니다. endIndex는 배열이 차지하는 메모리 공간의 마지막 인덱스인 5를 반환합니다. 따라서 numArray의 마지막 요소에 접근하기 위해서는 endIndex - 1을 사용해야 합니다.

```swift
// 4. 요소의 인덱스 반환받기
var numArray = [1, 2, 3, 2, 5]

numArray.firstIndex(of: 2)      // 1
numArray.lastIndex(of: 2)       // 3

print(numArray.firstIndex(of: 2))   // Optional(1)
print(numArray.lastIndex(of: 2))    // Optional(3)
```

firstIndex(of: 2)은 요소 2가 배열의 앞에서부터 찾았을 때 앞에서부터 몇 번째 인덱스에 있는지를 반환합니다.

lastIndex(of: 2)은 요소 2가 배열의 뒤에서부터 찾았을 때 앞에서부터 몇 번째 인덱스에 있는지를 반환합니다.

찾고자하는 요소가 없으면 nil을 반환합니다. 따라서 firstIndex(of:)와 lastIndex(of:)가 반환하는 값을 사용하려면 옵셔널을 벗겨야 합니다.

## 5. 배열의 기본 기능

```swift
var numArray = [1, 2, 3, 2, 5]

numArray.count      // 5, 배열의 요소 개수를 반환
numArray.isEmpty    // false, 배열이 비어있는지의 여부를 반환

numArray.contains(5)    // true, 파라미터의 값이 포함되는지의 여부를 반환
numArray.contains(0)    // false

numArray.randomElement() // 배열의 요소 중 랜덤하게 하나를 뽑아서 반환

numArray.swapAt(0, 1)   // 전달한 인덱스의 요소를 서로 바꿈
print(numArray)         // [2, 1, 3, 2, 5]
```

## 6. 배열의 기타 기능

```swift
var nums = [1, 2, 3, 1, 4, 5, 2, 6, 7, 5, 0]

nums.sort()     // 배열 nums 자체를 오름차순으로 정렬
nums.sorted()   // 배열 nums를 오름차순으로 정렬한 결과를 배열로 반환
```

```swift
var nums = [1, 2, 3, 1, 4, 5, 2, 6, 7, 5, 0]

nums.reverse()      // 배열 nums 자체를 내림차순으로 정렬
nums.reversed()     // 배열 nums를 내림차순으로 정렬한 결과를 배열로 반환
```

```swift
var nums = [1, 2, 3, 1, 4, 5, 2, 6, 7, 5, 0]

nums.shuffle()      // 배열 nums 자체를 랜덤하게 섞음
nums.shuffled()     // 배열 nums를 랜덤하게 섞은 결과를 배열로 반환
```

## 7. 튜플과 enumerated()

배열의 enumerated()는 배열의 인덱스와 요소를 함께 튜플로 반환한다.

```swift
var nums = [1, 2, 3, 4, 5]

for tuple in nums.enumerated() {
    print(tuple)
}

// (offset: 0, element: 1)
// (offset: 1, element: 2)
// (offset: 2, element: 3)
// (offset: 3, element: 4)
// (offset: 4, element: 5)
```
